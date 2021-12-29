---
layout: default
title: Command Pattern
parent: Behavior Patterns
grand_parent: Design Patterns
permalink: /docs/design-pattern/behavior-pattern/command/
nav_order: 6
---

# Command Pattern
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

### Overall Diagram

![Command Diagram](../../resource/command_diagram.png){:height="400px" width="600px" .centered-image}

### Sample source code

<div class="code-example" markdown="1">
<span class="fs-3">
[Command-> Command ](){: .btn }
</span>
</div>
```markdown
public interface Command {
    void execute();
}
```

<div class="code-example" markdown="1">
<span class="fs-3">
[AddCustomerCommand-> ConcreteCommand ](){: .btn }
</span>
</div>
```markdown
public class AddCustomerCommand implements Command {
    private CustomerService customerService;

    public AddCustomerCommand(CustomerService customerService) {
        this.customerService = customerService;
    }

    @Override
    public void execute() {
        customerService.addCustomer();
    }
}
```

<div class="code-example" markdown="1">
<span class="fs-3">
[CustomerService-> Receiver ](){: .btn }
</span>
</div>
```markdown
public class CustomerService {
    public void addCustomer(){
        System.out.println("Add customer....");
    }
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[Button-> Invoker ](){: .btn }
</span>
</div>
```markdown
public class Button {
    private String label;
    private Command command;

    public Button(Command command) {
        this.command = command;
    }

    public void click(){
        command.execute();
    }
    public String getLabel() {
        return label;
    }

    public void setLabel(String label) {
        this.label = label;
    }
}
```


### Comment


- By Using list, you could composite several commands and execute them together.

<div class="code-example" markdown="1">
<span class="fs-3">
[CompositeCommand-> Command ](){: .btn }
</span>
</div>
```markdown
public class CompositeCommand implements Command {
    private List<Command> commands = new ArrayList<>();

    public void add(Command command) {
        commands.add(command);
    }

    @Override
    public void execute() {
        for (Command command: commands)
            command.execute();
    }

}
```

-  Command pattern could implement undocommand to rollback, 
   below sample combine command pattern and momento pattern   

<div class="code-example" markdown="1">
<span class="fs-3">
[Command-> Command ](){: .btn }
</span>
</div>
```markdown
public interface Command {
    void execute();
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[Undoable Command-> Command ](){: .btn }
</span>
</div>
```markdown
public interface UndoableCommand extends Command{
    void unexecute();
}
```

<div class="code-example" markdown="1">
<span class="fs-3">
[ConcreteCommand (BoldCommand) implement both command and undoablecommand](){: .btn }
</span>
</div>
```markdown
public class BoldCommand implements UndoableCommand{
    private String preContent;
    private HtmlDocument document;
    private History history;

    public BoldCommand(HtmlDocument document, History history) {
        this.document = document;
        this.history = history;
    }

    @Override
    public void execute() {
        preContent = document.getContent();
        document.MakeBold();
        history.push(this);
    }

    @Override
    public void unexecute() {
        document.setContent(preContent);
    }
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[History(Caretaker) in memento pattern to save command in the queue](){: .btn }
</span>
</div>
```markdown
public class History {
    private Deque<UndoableCommand> commands = new ArrayDeque<>();

    public void push(UndoableCommand command){
        commands.add(command);
    }

    public UndoableCommand pop() {
        return commands.pop();
    }
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[HtmlDocument-> Originator (memento) or Invoker (command)](){: .btn }
</span>
</div>
```markdown
public class HtmlDocument {
    private String content;

    public void MakeBold(){
        content = "<b>" + this.content + "</b>";
    }
    public String getContent() {
        return content;
    }

    public void setContent(String content) {
        this.content = content;
    }
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[It's recommended to implement an undo command to rollback instead of unexecute method in original command, please refer to below sample.](){: .btn }
</span>
</div>

```markdown
public class UndoCommand implements Command{
    private History history;

    public UndoCommand(History history) {
        this.history = history;
    }

    @Override
    public void execute() {
        history.pop().unexecute();
    }
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[And here is an sample show how call undo command in main class:](){: .btn }
</span>
</div>

```markdown
UndoCommand undoCommand = new UndoCommand(hist);
undoCommand.execute();
```