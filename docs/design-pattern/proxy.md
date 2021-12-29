---
layout: default
title: Proxy Pattern
parent: Structural Patterns
grand_parent: Design Patterns
permalink: /docs/design-pattern/structural-pattern/proxy/
nav_order: 7
---

# Proxy Pattern
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

### Overall Diagram

![Proxy Diagram](../../resource/proxy_diagram.png){:height="400px" width="600px" .centered-image}

### Sample source code

<div class="code-example" markdown="1">
<span class="fs-3">
[Ebook -> Subject  ](){: .btn }
</span>
</div>
```markdown
public interface Ebook {
    void show();
    String getFileName();
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[RealBook -> RealSubject  ](){: .btn }
</span>
</div>
```markdown
public class RealBook implements Ebook{
    private String fileName;

    public RealBook(String fileName) {
        this.fileName = fileName;
        load();
    }

    @Override
    public void show() {
        System.out.println("Showing the ebook:  " + fileName);
    }

    @Override
    public String getFileName() {
        return fileName;
    }

    private void load(){
        System.out.println("Loading the ebook: " + fileName);
    }
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[EbookProxy -> Proxy  ](){: .btn }
</span>
</div>
```markdown
public class EbookProxy implements Ebook{
    private String fileName;
    private RealBook ebook;

    public EbookProxy(String fileName) {
        this.fileName = fileName;
    }

    @Override
    public void show() {
        if (ebook == null)
            ebook = new RealBook(fileName);

        ebook.show();
    }

    @Override
    public String getFileName() {
        return fileName;
    }
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[Library -> Client  ](){: .btn }
</span>
</div>
```markdown
public class Library {
    private Map<String, Ebook> ebooks = new HashMap<>();

    public void add(Ebook ebook){
        ebooks.put(ebook.getFileName(),ebook);
    }

    public void openBook(String fileName){
        ebooks.get(fileName).show();
    }
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[Main Class  ](){: .btn }
</span>
</div>
```markdown
    Library library = new Library();
    String[] fileNames = {"a", "b", "c"};
    for (String fileName: fileNames)
        library.add(new EbookProxy(fileName));

    library.openBook("a");
    library.openBook("c");
```
### Comment
1. Show method of Ebook is delegated to EBookProxy, it added a "if" operation to confirm if object exist before creating new Realbook oject, this saves memory and ensure no unused objects are created. 
2. Client use openbook method to call show() method.