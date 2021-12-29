---
layout: default
title: Iterator Pattern
parent: Behavior Patterns
grand_parent: Design Patterns
permalink: /docs/design-pattern/behavior-pattern/iterator/
nav_order: 3
---

# Iterator Pattern
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

### Overall Diagram

![Iterator Diagram](../../resource/iterator_diagram.png){:height="400px" width="600px" .centered-image}

### Sample source code

<div class="code-example" markdown="1">
<span class="fs-3">
[Iterator -> Iterator ](){: .btn }
</span>
</div>
```markdown
public interface Iterator<T> {
    boolean hasNext();
    T current();
    void next();
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[ArrayIterator -> ConcreteIterator ](){: .btn }
</span>
</div>
```markdown
public class ArrayIterator implements Iterator<String> {
    private ArrayBrowserHistory history;
    private int index;

    public ArrayIterator(ArrayBrowserHistory history) {
        this.history = history;
    }

    @Override
    public boolean hasNext() {
        return (index < history.getSize());
    }

    @Override
    public String current() {
        return history.getUrl(index);
    }

    @Override
    public void next() {
        index++;
    }
}
```

<div class="code-example" markdown="1">
<span class="fs-3">
[ArrayBrowserHistory-> ConcreteAggregate ](){: .btn }
</span>
</div>

```markdown
public class ArrayBrowserHistory {
    private String[] urls = new String[10];
    private int count;

    public void push(String url) {
        urls[count++] = url;
    }

    public String pop(){
        return urls[--count];
    }

    public String getUrl(int index) {
        return urls[index];
    }

    public int getSize() {
        return 10;
    }

    public Iterator createIterator() {
        return new ArrayIterator(this);
    }
}
```



### Comment


When we change arraylist to array with fix length, we could just add below classes, 
We don't need to refine iterator operation but add new classes outside as below.


<div class="code-example" markdown="1">
<span class="fs-3">
[ListIterator -> ConcreteIterator ](){: .btn }
</span>
</div>

```markdown
public class ListIterator implements Iterator<String>{
    private BrowserHistory history;
    private int index;

    public ListIterator(BrowserHistory history) {
        this.history = history;
    }

    @Override
    public boolean hasNext() {
        return (index < history.getSize());
    }

    @Override
    public String current() {
        return history.getUrl(index);
    }

    @Override
    public void next() {
        index++;
    }
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[BrowserHistory-> ConcreteAggregate ](){: .btn }
</span>
</div>
```markdown
import java.util.ArrayList;
import java.util.List;

public class BrowserHistory {
    private List<String> urls = new ArrayList<>();

    public String getUrl(int index) {
        return urls.get(index);
    }

    public int getSize() {
        return urls.size();
    }

    public void push(String url) {
        urls.add(url);
    }

    public String pop() {
        int lastIndex = urls.size() - 1;
        String lastUrl = urls.get(lastIndex);
        urls.remove(lastUrl);

        return lastUrl;

    }

    public Iterator createIterator(){
        return new ListIterator(this    );
    }
}
```