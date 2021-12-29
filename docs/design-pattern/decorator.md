---
layout: default
title: Decorator Pattern
parent: Structural Patterns
grand_parent: Design Patterns
permalink: /docs/design-pattern/structural-pattern/decorator/
nav_order: 3
---

# Decorator Pattern
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

### Overall Diagram

![Decorator Diagram](../../resource/decorator_diagram.png){:height="400px" width="600px" .centered-image}

### Sample source code

<div class="code-example" markdown="1">
<span class="fs-3">
[Stream -> Component  ](){: .btn }
</span>
</div>
```markdown
public interface Stream {
    void write(String data);
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[CloudStream -> Component and Decorator ](){: .btn }
</span>
</div>
```markdown
public class CloudStream implements Stream{
    @Override
    public void write(String data) {
        System.out.println("Storing " + data);
    }
}
```

<div class="code-example" markdown="1">
<span class="fs-3">
[CompressedCloudStream -> Component and Decorator ](){: .btn }
</span>
</div>
```markdown
public class CompressedCloudStream implements Stream{
    private Stream stream;

    public CompressedCloudStream(Stream stream) {
        this.stream = stream;
    }

    @Override
    public void write(String data) {
        String compressData = compress(data);
        stream.write(compressData);
    }

    private String compress(String data){
        return data.substring(0,8);
    }
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[EncryptedCloudStream -> Component and Decorator ](){: .btn }
</span>
</div>
```markdown
public class EncryptedCloudStream implements Stream{
    private Stream stream;

    public EncryptedCloudStream(Stream stream) {
        this.stream = stream;
    }

    @Override
    public void write(String data) {
        String encryptedData = Encrypt(data);
        stream.write(encryptedData);
    }

    private String Encrypt(String data){
        return "#$%&'($%&'#$%&0((&&'";
    }
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[Main class: an example of using decorator  ](){: .btn }
</span>
</div>
```markdown
storeCreditCard(new EncryptedCloudStream(new CompressedCloudStream(new CloudStream())));
```


### Comment
1. Decoration could be applied repeatedly.
2. By adjusting the consequence of steps of decorators, it could easily combine options freely.
3. In main class, CloudStream message is compressed then encrypted before being written out.