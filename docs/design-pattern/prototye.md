---
layout: default
title: Prototype Pattern
parent: Creational Patterns
grand_parent: Design Patterns
permalink: /docs/design-pattern/structural-pattern/prototype/
nav_order: 1
---

# Prototype Pattern
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

### Overall Diagram

![Prototype Diagram](../../resource/prototype_diagram.png){:height="400px" width="600px" .centered-image}

### Sample source code

<div class="code-example" markdown="1">
<span class="fs-3">
[Component-> Prototype ](){: .btn }
</span>
</div>
```markdown
public interface Component {
    void render();
    Component clone();

}
```

<div class="code-example" markdown="1">
<span class="fs-3">
[Circle-> ConcretePrototype ](){: .btn }
</span>
</div>
```markdown
public class Circle implements Component{
    private int radius;

    public int getRadius() {
        return radius;
    }

    public void setRadius(int radius) {
        this.radius = radius;
    }

    @Override
    public void render() {
        System.out.println("Rendering circle...");
    }

    @Override
    public Component clone() {
        Circle newCircle = new Circle();
        newCircle.setRadius(radius);
        System.out.println("New circle...");
        //render();
        return newCircle;
    }
}
```

<div class="code-example" markdown="1">
<span class="fs-3">
[ContextMenu-> Client ](){: .btn }
</span>
</div>
```markdown
public class ContextMenu {
    public void duplicate(Component component){
        Component newComponent = component.clone();
    }
}
```


### Comment
1. This design pattern is used for clone and create new components. 