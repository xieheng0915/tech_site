---
layout: default
title: Memento Pattern
parent: Behavior Patterns
grand_parent: Design Patterns
permalink: /docs/design-pattern/behavior-pattern/memento/
nav_order: 1
---

# Memento Pattern
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

### Overall Diagram

![Memento Diagram](../../resource/memento_diagram.png){:height="400px" width="600px" .centered-image}


### Sample source code

<div class="code-example" markdown="1">
<span class="fs-3">
[Editor -> Originator ](){: .btn }
</span>
</div>
```markdown
public class Editor {
    private String content;

    public String getContent() {
        return content;
    }

    public void setContent(String content) {
        this.content = content;
    }

    public EditorState createState() {
        return new EditorState(this.content);
    }

    public void restore(EditorState state) {
        content = state.getContent();
    }
}
```

<div class="code-example" markdown="1">
<span class="fs-3">
[EditorState -> Memento ](){: .btn }
</span>
</div>

```markdown
public class EditorState {
    private String content;

    public EditorState(String content) {
        this.content = content;
    }

    public String getContent() {
        return content;
    }
}
```

<div class="code-example" markdown="1">
<span class="fs-3">
[History -> Caretaker ](){: .btn }
</span>
</div>

```markdown
import java.util.ArrayList;
import java.util.List;

public class History {
    private List<EditorState> states = new ArrayList<>();


    public void push(EditorState state) {
        states.add(state);
    }
    public EditorState pop() {
        int lastIndex = states.size() - 1;
        EditorState lastState = states.get(lastIndex);
        states.remove(lastState);

        return lastState;
    }
}

```
---

### Comment

1. Record operation status (originator -> memento) 
2. Push to stack(Caretaker)
3. By following stack : First in last out, therefore by backward step to restore operations step by step.




