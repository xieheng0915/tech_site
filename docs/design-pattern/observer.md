---
layout: default
title: Observer Pattern
parent: Behavior Patterns
grand_parent: Design Patterns
permalink: /docs/design-pattern/behavior-pattern/observer/
nav_order: 7
---

# Observer Pattern
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

### Overall Diagram

![Observer Diagram](../../resource/observer_diagram.png){:height="400px" width="600px" .centered-image}

### Sample source code

<div class="code-example" markdown="1">
<span class="fs-3">
[Subject -> Subject ](){: .btn }
</span>
</div>
```markdown
public class Subject {
    private List<Observer> observers = new ArrayList<>();

    public void addObserver(Observer obj) {
        observers.add(obj);
    }

    public void removeObserver(Observer obj){
        observers.remove(obj);
    }

    public void notifyObserver(){
        for (Observer obj : observers)
            obj.update();
    }
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[Observer -> Observer ](){: .btn }
</span>
</div>
```markdown
public interface Observer {
    void update();
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[SpreadSheet -> ConcreteObserverA ](){: .btn }
</span>
</div>
```markdown
public class SpreadSheet implements Observer{
    private DataSource dataSource;

    public SpreadSheet(DataSource dataSource) {
        this.dataSource = dataSource;
    }

    @Override
    public void update() {
        System.out.println("Updated spreadsheet with the value: " + dataSource.getValue());
    }
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[Chart -> ConcreteObserverB ](){: .btn }
</span>
</div>
```markdown
public class Chart implements Observer{
    private DataSource dataSource;

    public Chart(DataSource dataSource) {
        this.dataSource = dataSource;
    }

    @Override
    public void update() {
        System.out.println("Updated chart with value: " + dataSource.getValue());
    }
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[DataSource -> ConcreteSubject ](){: .btn }
</span>
</div>
```markdown
public class DataSource extends Subject{
    private int value;

    public int getValue() {
        return value;
    }

    public void setValue(int value) {
        this.value = value;
        notifyObserver();
    }


}
```

### Comment 

