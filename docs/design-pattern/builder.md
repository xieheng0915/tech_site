---
layout: default
title: Builder Pattern
parent: Creational Patterns
grand_parent: Design Patterns
permalink: /docs/design-pattern/structural-pattern/builder/
nav_order: 5
---

# Builder Pattern
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

### Overall Diagram

![Builder Diagram](../../resource/builder_diagram.png){:height="400px" width="600px" .centered-image}

### Sample source code

<div class="code-example" markdown="1">
<span class="fs-3">
[PresentationHandler -> Builder  ](){: .btn }
</span>
</div>
```markdown
public interface PresentationBuilder {
    void addSlide(Slide slide);
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[Presentation -> Director  ](){: .btn }
</span>
</div>
```markdown
public class Presentation {
    private List<Slide> slides = new ArrayList<>();

    public void addSlide(Slide slide){
        slides.add(slide);
    }

    public void export(PresentationBuilder builder){
        builder.addSlide(new Slide("Copyright"));
        for (Slide slide: slides)
            builder.addSlide(slide);
    }


}
```

<div class="code-example" markdown="1">
<span class="fs-3">
[PDFDocumentBuilder-> ConcreteBuilder  ](){: .btn }
</span>
</div>
```markdown
public class PDFDocumentBuilder implements PresentationBuilder{
    private PDFDocument document = new PDFDocument();
    @Override
    public void addSlide(Slide slide) {
        document.addPage(slide.getText());

    }
}
```


<div class="code-example" markdown="1">
<span class="fs-3">
[PDFDocument: Object for PDFDocumentBuilder  ](){: .btn }
</span>
</div>
```markdown
public class PDFDocument {
    public void addPage(String text){
        System.out.println("Adding a PDF page");
    }
}
```

<div class="code-example" markdown="1">
<span class="fs-3">
[Slide: Assistant object  ](){: .btn }
</span>
</div>
```markdown
public class Slide {
    private String text;

    public Slide(String text) {
        this.text = text;
    }

    public String getText() {
        return text;
    }
}
```

### Comment
1. Builder pattern is applied to polymorphism in output side.
2. In case to add another type of outpput, like movie, could add a set of objects as below.

<div class="code-example" markdown="1">
<span class="fs-3">
[MovieBuilder-> ConcreteBuilder  ](){: .btn }
</span>
</div>
```markdown
public class MovieBuidler implements PresentationBuilder{
    private Movie movie = new Movie();
    @Override
    public void addSlide(Slide slide) {
        movie.addFrame(slide.getText(),6);
    }
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[Movie: Object for MovieBuilder  ](){: .btn }
</span>
</div>
```markdown
public class Movie {
    public void addFrame(String text, int duration){
        System.out.println("Adding a frame for movie...");
    }
}
```

<div class="code-example" markdown="1">
<span class="fs-3">
[Main: by loding different concrete builders to export differently without editing core sourcecose  ](){: .btn }
</span>
</div>
```markdown
Presentation presentation = new Presentation();
        presentation.addSlide(new Slide("slide1"));
        PDFDocumentBuilder builder = new PDFDocumentBuilder();
        presentation.export(builder);

        MovieBuidler movieBuidler = new MovieBuidler();
        presentation.export(movieBuidler);
```