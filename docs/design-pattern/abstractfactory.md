---
layout: default
title: AbstractFactory Pattern
parent: Creational Patterns
grand_parent: Design Patterns
permalink: /docs/design-pattern/structural-pattern/abstractfactory/
nav_order: 4
---

# AbstractFactory Pattern
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

### Overall Diagram

![abstractFactory Diagram](../../resource/abstractFactory_diagram.png){:height="400px" width="600px" .centered-image}

### Sample source code

<div class="code-example" markdown="1">
<span class="fs-3">
[WidgetFactory -> AbstractFactory  ](){: .btn }
</span>
</div>
```markdown
public interface WidgetFactory {
    Button createButton();
    TextBox createTextBox();
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[Widget, TextBox, Button: interface of families of related objects, defined in abstract factory  ](){: .btn } 
</span>
</div>
```markdown
public interface Widget {
    void render();
}
```
```markdown
public interface Button extends Widget{
}
```
```markdown
public interface TextBox extends Widget {
}
```

<div class="code-example" markdown="1">
<span class="fs-3">
[AntFactory -> ConcreteFactory  ](){: .btn }
</span>
</div>
```markdown
public class AntFactory implements WidgetFactory {
    @Override
    public Button createButton() {
        return new AntButton();
    }

    @Override
    public TextBox createTextBox() {
        return new AntTextBox();
    }
}
```

<div class="code-example" markdown="1">
<span class="fs-3">
[AntButton,AntTextBox: Concrete objects for concrete factory  ](){: .btn }
</span>
</div>
```markdown
public class AntButton implements Button {
    @Override
    public void render() {
        System.out.println("Rendering ant button");
    }
}
```
```markdown
public class AntTextBox implements TextBox {
    @Override
    public void render() {
        System.out.println("Rendering Ant Textbox...");
    }
}
```

<div class="code-example" markdown="1">
<span class="fs-3">
[ContactForm: rendering by calling interface  ](){: .btn }
</span>
</div>
```markdown
public class ContactForm {
    public void render(WidgetFactory factory){
        factory.createButton().render();
        factory.createTextBox().render();
    }
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[Main: declare concrete factory when use  ](){: .btn }
</span>
</div>
```markdown
ContactForm form = new ContactForm();
        form.render(new AntFactory());
        form.render(new MaterialFactory());
```


### Comment
1. This abstractFactory pattern is widely used in framework, framework designer create abstract factory and user(developer) implement and create families of related objects.
2. The difference between factory pattern and abstract factory pattern is, factory provide method while abstract factory provide interface.  