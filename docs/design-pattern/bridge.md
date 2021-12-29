---
layout: default
title: Bridge Pattern
parent: Structural Patterns
grand_parent: Design Patterns
permalink: /docs/design-pattern/structural-pattern/bridge/
nav_order: 6
---

# Bridge Pattern
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

### Overall Diagram

![Bridge Diagram](../../resource/bridge_diagram.png){:height="400px" width="600px" .centered-image}

### Sample source code

<div class="code-example" markdown="1">
<span class="fs-3">
[RemoteControl -> RemoteControl  ](){: .btn }
</span>
</div>
```markdown
public class RemoteControl {
    protected Device device;

    public RemoteControl(Device device) {
        this.device = device;
    }

    public void turnOn(){
        device.turnOn();
    }

    public void turnOff(){
        device.turnOff();
    }
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[AdvancedRemoteControl -> AdvancedRemoteControl  ](){: .btn }
</span>
</div>
```markdown
public class AdvancedRemoteControl extends RemoteControl{
    public AdvancedRemoteControl(Device device) {
        super(device);
    }

    public void setChannel(int number){
        device.setChannel(number);
    }
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[Device -> Device  ](){: .btn }
</span>
</div>
```markdown
public interface Device {
    public void turnOn();
    public void turnOff();
    public void setChannel(int number);
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[SonyTV -> SonyTV  ](){: .btn }
</span>
</div>
```markdown
public class SonyTV implements Device{
    @Override
    public void turnOn() {
        System.out.println("Sony turn on");
    }

    @Override
    public void turnOff() {
        System.out.println("sony turn off");
    }

    @Override
    public void setChannel(int number) {
        System.out.println("Sony set Channel: " + number);
    }
}
```


<div class="code-example" markdown="1">
<span class="fs-3">
[Main:  ](){: .btn }
</span>
</div>

```markdown
    AdvancedRemoteControl advancedRemoteControl = new AdvancedRemoteControl(new SonyTV());
    advancedRemoteControl.turnOn();
    advancedRemoteControl.setChannel(33);
    advancedRemoteControl.turnOff();*
```
### Comment
1. In bridget pattern sample, a object has two dimensions of features, one is control related, the other is device depended. 
2. In Main class, by combine device part and remoteControl part, SonyTV's advanced remotecontrol operations are combined and applied. 