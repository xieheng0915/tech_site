---
layout: default
title: Composite Pattern
parent: Structural Patterns
grand_parent: Design Patterns
permalink: /docs/design-pattern/structural-pattern/composite/
nav_order: 1
---

# Composite Pattern
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

### Overall Diagram

![Composite Diagram](../../resource/composite_diagram.png){:height="400px" width="600px" .centered-image}

### Sample source code

<div class="code-example" markdown="1">
<span class="fs-3">
[Component -> Component  ](){: .btn }
</span>
</div>
```markdown
public interface Component {
    void render();
    void move();
}
```

<div class="code-example" markdown="1">
<span class="fs-3">
[Shape -> Leaf  ](){: .btn }
</span>
</div>
```markdown
public class Shape implements Component{
    @Override
    public void render() {
        System.out.println("Render shape.");
    }

    @Override
    public void move() {
        System.out.println("Move shape.");
    }
}
```

<div class="code-example" markdown="1">
<span class="fs-3">
[Group -> Composite  ](){: .btn }
</span>
</div>
```markdown
public class Group implements Component{
    private List<Component> components = new ArrayList<>();

    public void add(Component shape){
        components.add(shape);
    }

    @Override
    public void render() {
        for (Component component: components)
            component.render();
    }

    @Override
    public void move() {
        for (Component component: components)
            component.move();
    }
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[Main: group and subgroup  ](){: .btn }
</span>
</div>
```markdown
    Group group1 = new Group();
    group1.add(new Shape());
    group1.add(new Shape());

    Group group2 = new Group();
    group2.add(new Shape());
    group2.add(new Shape());

    Group group = new Group();
    group.add(group1);
    group.add(group2);

    group.render();
    group.move();
```


### Comment
1. Composite pattern allows groups of objects follow the same feature as the indiviual objects, therefore user could develop hirache of groups, it's useful to define combined groups components.  