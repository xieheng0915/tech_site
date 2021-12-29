---
layout: default
title: Factory Pattern
parent: Creational Patterns
grand_parent: Design Patterns
permalink: /docs/design-pattern/structural-pattern/factory/
nav_order: 3
---

# Factory Pattern
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

### Overall Diagram

![Factory Diagram](../../resource/factory_diagram.png){:height="400px" width="600px" .centered-image}

### Sample source code

<div class="code-example" markdown="1">
<span class="fs-3">
[Controller-> Creator ](){: .btn }
</span>
</div>
```markdown
public abstract class Controller {
    public void render(String viewName, Map<String, Object> context){
        ViewEngine engine = createViewEngine();
        String html = engine.render(viewName,context);
        System.out.println(html);
    }

    protected abstract ViewEngine createViewEngine();
}
```

<div class="code-example" markdown="1">
<span class="fs-3">
[MatchaController-> ConcreteCreator ](){: .btn }
</span>
</div>
```markdown
public class MatchaController extends Controller {
    @Override
    protected ViewEngine createViewEngine() {
        return new MatchViewEngine();
    }
}
```

<div class="code-example" markdown="1">
<span class="fs-3">
[ViewEngine: Interface of created objects  ](){: .btn }
</span>
</div>
```markdown
public interface ViewEngine {
    String render(String viewName, Map<String, Object> context);
}
```

<div class="code-example" markdown="1">
<span class="fs-3">
[MatchaViewEngine:  created concrete object  ](){: .btn }
</span>
</div>
```markdown
public class MatchViewEngine implements ViewEngine {
    @Override
    public String render(String viewName, Map<String, Object> context) {
        return "<html>View rendered by Matcha template</html>";
    }
}
```

<div class="code-example" markdown="1">
<span class="fs-3">
[ProductController:  a comprehensive rendering controller  ](){: .btn }      
</span>
</div>
```markdown
public class ProductController extends MatchaController {
    public void listProducts(){
        Map<String, Object> context = new HashMap<>();
        render("product.html", context);
    }
}
```

### Comment
1. factory is a method, by creating objects in the concrete controller method, it could adapt to different extended types of objects. (MatchaController)    
2. If apply another ViewEngine, like SharpViewEngine, below is how source code looks like:  


<div class="code-example" markdown="1">
<span class="fs-3">
[SharpController-> ConcreteCreator ](){: .btn }
</span>
</div>
```markdown
public class SharpController extends Controller {
    @Override
    protected ViewEngine createViewEngine() {
        return new SharViewEngine();
    }
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[SharpViewEngine:  created concrete object  ](){: .btn }
</span>
</div>
```markdown
public class SharViewEngine implements ViewEngine {
    @Override
    public String render(String viewName, Map<String, Object> context) {
        return "<html>rendered by sharp template</html>";
    }
}
```

<div class="code-example" markdown="1">
<span class="fs-3">
[ProductController:  a comprehensive rendering controller  ](){: .btn }      
</span>
</div>
```markdown
public class ProductController extends SharpController {
    public void listProducts(){
        Map<String, Object> context = new HashMap<>();
        render("product.html", context);
    }
}
```

- By extending SharpController, ProductController could list sharp ViewEngine objects instead of Matcha ViewEngine.