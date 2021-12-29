---
layout: default
title: Adapter Pattern
parent: Structural Patterns
grand_parent: Design Patterns
permalink: /docs/design-pattern/structural-pattern/adapter/
nav_order: 2
---

# Adapter Pattern
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

### Overall Diagram

![Adaptr Diagram](../../resource/adapter_diagram.png){:height="400px" width="600px" .centered-image}

### Sample source code

<div class="code-example" markdown="1">
<span class="fs-3">
[Filter -> Target  ](){: .btn }
</span>
</div>
```markdown
public interface Filter {
    void filter(Image image);
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[CaramelFilter -> Adapter  ](){: .btn }
</span>
</div>
```markdown
public class CaramelFilter implements Filter{
    private Caramel caramel;

    public CaramelFilter(Caramel caramel) {
        this.caramel = caramel;
    }

    @Override
    public void filter(Image image) {
        caramel.init();
        caramel.render(image);
    }
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[Caramel -> Adaptee  ](){: .btn }
</span>
</div>
```markdown
public class Caramel {
    public void init(){
        System.out.println("Initiate...");
    }

    public void render(Image image){
        System.out.println("Rendering caramel...");
    }
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[ImageView -> Client  ](){: .btn }
</span>
</div>
```markdown
public class ImageView {
    private Image image;

    public ImageView(Image image) {
        this.image = image;
    }

    public void apply(Filter filter){
        filter.filter(image);
    }
}
```

<div class="code-example" markdown="1">
<span class="fs-3">
[VividFilter: a normal operation without adapter  ](){: .btn }
</span>
</div>
```markdown
public class VividFilter implements Filter{
    @Override
    public void filter(Image image) {
        System.out.println("Apply vivid filter....");
    }
}
```

<div class="code-example" markdown="1">
<span class="fs-3">
[Main Class:   ](){: .btn }
</span>
</div>
```markdown
    ImageView imageView = new ImageView(new Image());
    imageView.apply(new VividFilter());
    imageView.apply(new CaramelFilter(new Caramel()));
```

### Comment
1. Caramel option does different modification: init and render, with the VividFilter, by using adapter, caramel is capped by filter, became CaramelFilter, this transform makes client more convenient to use filter. (Polymorphism)
2. 


