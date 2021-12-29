---
layout: default
title: Flyweight Pattern
parent: Structural Patterns
grand_parent: Design Patterns
permalink: /docs/design-pattern/structural-pattern/flyweight/
nav_order: 5
---

# Flyweight Pattern
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

### Overall Diagram

![Flyweight Diagram](../../resource/flyweight_diagram.png){:height="400px" width="600px" .centered-image}

### Sample source code

<div class="code-example" markdown="1">
<span class="fs-3">
[PointIconFactory -> FlyweightFactory  ](){: .btn }
</span>
</div>
```markdown
public class PointIconFactory {
    private Map<PointType,PointIcon> icons= new HashMap<>();

    public PointIcon getPointIcon(PointType type){
        if(!icons.containsKey(type)){
            PointIcon icon = new PointIcon(type, null);
            icons.put(type,icon);
        }

        return icons.get(type);
    }

}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[PointService -> Client  ](){: .btn }
</span>
</div>
```markdown
public class PointService {
    private PointIconFactory iconFactory;

    public PointService(PointIconFactory iconFactory) {
        this.iconFactory = iconFactory;
    }

    public List<Point> getPoints() {
        List<Point> points = new ArrayList<>();
        Point point = new Point(1,1,iconFactory.getPointIcon(PointType.CAFE));
        points.add(point);
        Point point2 = new Point(3,5,iconFactory.getPointIcon(PointType.RESTAURANT));
        points.add(point2);

        return points;
    }
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[Point :   ](){: .btn }
</span>
</div>
```markdown
public class Point {
    private int x;
    private int y;
    private PointIcon icon;

    public Point(int x, int y, PointIcon icon) {
        this.x = x;
        this.y = y;
        this.icon = icon;
    }

    public void draw() {
        System.out.printf("%s at (%s, %s)\n", icon.getType(),x,y);
    }
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[PointIcon :   ](){: .btn }
</span>
</div>
```markdown
public class PointIcon {
    private final PointType type;
    private final byte[] icon;

    public PointIcon(PointType type, byte[] icon) {
        this.type = type;
        this.icon = icon;
    }

    public PointType getType() {
        return type;
    }
}
```


### Comment
1. Flyweight help to defer creating objects like point Icon to save memory.
2. Here is how flyweight pattern works: 
    1. Point and PointIcon are all features of a point on the Map, but they are separated. 
    2. In PointIcon, byte[] icon component is memory costly, so it is created and stored in the list, when needed it is loaded not created.
    3. PointIconFactory is responsible for creating pointIcon, and ensure no over creation. 
    4. PointService use factory to get point Icon.