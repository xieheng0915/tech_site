---
layout: default
title: Visitor Pattern
parent: Behavior Patterns
grand_parent: Design Patterns
permalink: /docs/design-pattern/behavior-pattern/visitor/
nav_order: 10
---

# Visitor Pattern
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

### Overall Diagram

![Visitor Diagram](../../resource/visitor_diagram.png){:height="400px" width="600px" .centered-image}

### Sample source code

<div class="code-example" markdown="1">
<span class="fs-3">
[HtmlNode -> Visitor ](){: .btn }
</span>
</div>
```markdown
public interface HtmlNode {
    void execute(Operation operation);
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[AnchorNode -> ConcreteVisitorA ](){: .btn }
</span>
</div>
```markdown
public class AnchorNode implements HtmlNode{

    @Override
    public void execute(Operation operation) {
        operation.apply(this);
    }
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[HeadingNode -> ConcreteVisitorB ](){: .btn }
</span>
</div>
```markdown
public class HeadingNode implements HtmlNode{

    @Override
    public void execute(Operation operation) {
        operation.apply(this);
    }
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[Operation(apply) -> Element(accept) ](){: .btn }
</span>
</div>
```markdown
public interface Operation {
    void apply(HeadingNode headingNode);
    void apply(AnchorNode anchorNode);
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[HighlightOperation(apply) -> ConcreteElement1(accept) ](){: .btn }
</span>
</div>
```markdown
public class HighlightOperation implements Operation{
    @Override
    public void apply(HeadingNode headingNode) {
        System.out.println("Highlight HeadingNode....");
    }

    @Override
    public void apply(AnchorNode anchorNode) {
        System.out.println("Highlight anchorNode...");
    }
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[PlaintextOperation(apply) -> ConcreteElement2(accept) ](){: .btn }
</span>
</div>
```markdown
public class PlaintextOperation implements Operation{
    @Override
    public void apply(HeadingNode headingNode) {
        System.out.println("plaintext applying headingnode...");
    }

    @Override
    public void apply(AnchorNode anchorNode) {
        System.out.println("plaintext applying anchornode...");
    }
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[HtmlDocument: a canvas ](){: .btn }
</span>
</div>
```markdown
public class HtmlDocument {
    private List<HtmlNode> nodes = new ArrayList<>();

    public void add(HtmlNode node){
        nodes.add(node);
    }

    public void execute(Operation operation){
        for (HtmlNode node: nodes)
            node.execute(operation);
    }
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[Main class ](){: .btn }
</span>
</div>
```markdown
    HtmlDocument document = new HtmlDocument();
    document.add(new HeadingNode());
    document.add(new AnchorNode());
    document.execute(new HighlightOperation());
```

### Comment

1. HtmlDocument could be considered as a canvas or a container. 
2. Key point: visitor put element into itself, then element apply (accept) visitor, mutual connected.