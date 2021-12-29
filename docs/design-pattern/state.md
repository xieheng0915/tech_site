---
layout: default
title: State Pattern
parent: Behavior Patterns
grand_parent: Design Patterns
permalink: /docs/design-pattern/behavior-pattern/state/
nav_order: 2
---

# State Pattern
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

### Overall Diagram

![State Diagram](../../resource/state_diagram.png){:height="400px" width="600px" .centered-image}

### Sample source code

<div class="code-example" markdown="1">
<span class="fs-3">
[Tool -> State ](){: .btn }
</span>
</div>
```markdown
public interface Tool {
    void MouseUp();
    void MouseDown();
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[SelectionTool -> ConcreteStateA ](){: .btn }
</span>
</div>
```markdown
public class SelectionTool implements Tool{
    @Override
    public void MouseUp() {
        System.out.println("Selection mouse up");
    }

    @Override
    public void MouseDown() {
        System.out.println("Selection mouse down");
    }
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[BrushTool -> ConcreteStateB ](){: .btn }
</span>
</div>
```markdown
public class BrushTool implements Tool{
    @Override
    public void MouseUp() {
        System.out.println("Brush mouse up");
    }

    @Override
    public void MouseDown() {
        System.out.println("Brush mouse down");
    }
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[Canvas -> Context ](){: .btn }
</span>
</div>
```markdown
public class Canvas {
    private Tool currentTool;

    public Tool getCurrentTool() {
        return currentTool;
    }

    public void setCurrentTool(Tool currentTool) {
        this.currentTool = currentTool;
    }

    public void mouseDown() {
        currentTool.MouseDown();
    }
    public void mouseUp() {
        currentTool.MouseUp();
    }


}
```

### Comment 

1. Difference between state and strategy:   
   State methods are defined in advance, all concrete classes follow it.  
   While strategy concrete class have no limitation.
 
