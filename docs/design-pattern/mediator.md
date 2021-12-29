---
layout: default
title: Mediator Pattern
parent: Behavior Patterns
grand_parent: Design Patterns
permalink: /docs/design-pattern/behavior-pattern/mediator/
nav_order: 8
---

# Mediator Pattern
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

### Overall Diagram

![Mediator Diagram](../../resource/mediator_diagram.png){:height="400px" width="600px" .centered-image}

### Sample source code

<div class="code-example" markdown="1">
<span class="fs-3">
[EventHandler -> Colleague ](){: .btn }
</span>
</div>
```markdown
public interface EventHandler {
    void handle();
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[UIControl -> Mediator ](){: .btn }
</span>
</div>
```markdown
public abstract class UIControl {
    private List<EventHandler> eventHandlers = new ArrayList<>();

    public void attach(EventHandler eventHandler) {
        eventHandlers.add(eventHandler);
    }

    protected void notifyEventHandlers() {
        for (EventHandler eventHandler : eventHandlers)
            eventHandler.handle();
    }

}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[Button -> ConcreteMediator ](){: .btn }
</span>
</div>
```markdown
public class Button extends UIControl {
    private boolean isEnabled;

    public boolean isEnabled() {
        return isEnabled;
    }

    public void setEnabled(boolean enabled) {
        isEnabled = enabled;
        notifyEventHandlers();
    }


}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[ListBox -> ConcreteMediator ](){: .btn }
</span>
</div>
```markdown
public class ListBox extends UIControl {
    private String selection;

    public String getSelection() {
        return selection;
    }

    public void setSelection(String selection) {
        this.selection = selection;
        notifyEventHandlers();
    }

}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[TextBox -> ConcreteMediator ](){: .btn }
</span>
</div>
```markdown
public class TextBox extends UIControl{
    private String content;

    public String getContent() {
        return content;
    }

    public void setContent(String content) {
        this.content = content;
        notifyEventHandlers();
    }

}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[ArticleDialogBox  ](){: .btn }
</span>
</div>
```markdown
public class ArticleDialogBox {
    private ListBox articlesListBox = new ListBox();
    private TextBox titleTextBox = new TextBox();
    private Button saveButton = new Button();

    public ArticleDialogBox() {
        articlesListBox.attach(this::articleSelected);
        titleTextBox.attach(this::titleChanged);
    }

    public void simulateUserInteraction() {
        articlesListBox.setSelection("article1");
        titleTextBox.setContent("");
        articlesListBox.setSelection("article2");
        System.out.println("TextBox: " + titleTextBox.getContent());
        System.out.println("Button: " + saveButton.isEnabled());
    }


    private void articleSelected(){
        titleTextBox.setContent(articlesListBox.getSelection());
        saveButton.setEnabled(true);
    }

    private void titleChanged() {
        String content = titleTextBox.getContent();
        boolean isEmpty = (content == null || content.isEmpty());
        saveButton.setEnabled(!isEmpty);
    }
}

```

### Comment

1. There is no ConcreteColleague implemented in this sample.  
2. The key point is put colleague interface into mediator as eventhandler.  
   A notifyEventHandler is implemented in every mediator, this ensured any update could be notified.
3. In this sample, ArticleDialogBox is a centered dispatcher.  
   It's responsible to define actions to be taken when events are triggered.   