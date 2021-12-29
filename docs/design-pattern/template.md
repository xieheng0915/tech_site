---
layout: default
title: Template Pattern
parent: Behavior Patterns
grand_parent: Design Patterns
permalink: /docs/design-pattern/behavior-pattern/template/
nav_order: 5
---

# Template Pattern
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

### Overall Diagram

![Template Diagram](../../resource/template_diagram.png){:height="400px" width="600px" .centered-image}

### Sample source code

<div class="code-example" markdown="1">
<span class="fs-3">
[Task -> AbstractClass ](){: .btn }
</span>
</div>
```markdown
public abstract class Task {
    private AuditTrail auditTrail;

    public Task(){
        this.auditTrail = new AuditTrail();
    }

    public void execute(){
        auditTrail.record();
        doExecute();
    }
    protected abstract void doExecute();
}
```

<div class="code-example" markdown="1">
<span class="fs-3">
[AuditTrail: Member in Abstract class ](){: .btn }
</span>
</div>

```markdown
public class AuditTrail {
    public void record(){
        System.out.println("Record audit.");
    }
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[GenerateReportTask -> ConcreteClassA ](){: .btn }
</span>
</div>
```markdown
public class GenerateReportTask extends Task{

    @Override
    protected void doExecute() {
        System.out.println("Process to generate report...");
    }
}
```

<div class="code-example" markdown="1">
<span class="fs-3">
[GenerateReportTask -> ConcreteClassB ](){: .btn }
</span>
</div>
```markdown
public class TransferMoneyTask extends Task{
    @Override
    protected void doExecute() {
        System.out.println("Process to transfer money....");
    }
}
```

### Comment

1. In Abstract class "Task", method "execute", defined process template,  
   like step1 is record(), step2 is doExecute().  
   While concrete class only implement step2 doExecute(),  
   This is the reason it's called template pattern.  
2. The abstract class defines template. 