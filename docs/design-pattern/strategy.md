---
layout: default
title: Strategy Pattern
parent: Behavior Patterns
grand_parent: Design Patterns
permalink: /docs/design-pattern/behavior-pattern/strategy/
nav_order: 4
---

# Strategy Pattern
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

### Overall Diagram

![Strategy Diagram](../../resource/strategy_diagram.png){:height="400px" width="600px" .centered-image}

### Sample source code

<div class="code-example" markdown="1">
<span class="fs-3">
[Compressor -> Strategy ](){: .btn }
</span>
</div>
```markdown
public interface Compressor {
    void compress(String fileName);
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[JpegCompressor -> ConcreteStrategyA ](){: .btn }
</span>
</div>
```markdown
public class JpegCompressor implements Compressor{
    @Override
    public void compress(String fileName) {
        System.out.println("Compress JPEG file");
    }
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[PngCompressor -> ConcreteStrategyB ](){: .btn }
</span>
</div>
```markdown
public class PngCompressor implements Compressor{
    @Override
    public void compress(String fileName) {
        System.out.println("Compress PNG file");
    }
}
```

<div class="code-example" markdown="1">
<span class="fs-3">
[ImageStorage -> Context ](){: .btn }
</span>
</div>
```markdown
public class ImageStorage {
    private Compressor compressor;
    private Filter filter;

    public ImageStorage(Compressor compressor, Filter filter) {
        this.compressor = compressor;
        this.filter = filter;
    }

    public void store(String fileName){
        compressor.compress(fileName);
        filter.filter(fileName);
    }
}
```
### Comment

1. Compared with state pattern, strategy pattern is more high-level defined, which allow more flexibity for concrete class to implement detail by their own. 
2. Here is the sample if we want to add one more strategy interface, and we don't need to modify context, just call it and it switched to another process, from compressor to filter. 

<div class="code-example" markdown="1">
<span class="fs-3">
[Filter -> Strategy ](){: .btn }
</span>
</div>
```markdown
public interface Filter {
    void filter(String fileName);
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[HighContrastFilter -> ConcreteStrategyA ](){: .btn }
</span>
</div>
```markdown
public class HighContrastFilter implements Filter{
    @Override
    public void filter(String fileName) {
        System.out.println("Applying High-Contrast Filter");
    }
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[BlackAndWhiteFilter -> ConcreteStrategyB ](){: .btn }
</span>
</div>
```markdown
public class BlackAndWhiteFilter implements Filter{
    @Override
    public void filter(String fileName) {
        System.out.println("Applying Black and White filter");
    }
}
```


