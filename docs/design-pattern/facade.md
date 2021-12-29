---
layout: default
title: Facade Pattern
parent: Structural Patterns
grand_parent: Design Patterns
permalink: /docs/design-pattern/structural-pattern/facade/
nav_order: 4
---

# Facade Pattern
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

### Overall Diagram

![Facade Diagram](../../resource/facade_diagram.png){:height="400px" width="600px" .centered-image}

### Sample source code

<div class="code-example" markdown="1">
<span class="fs-3">
[NotificationService -> facade  ](){: .btn }
</span>
</div>
```markdown
public class NotificationService {
    public void send(String message, String target){
        NotificationServer server = new NotificationServer();
        Connection connect = server.connect("10.123.233.21");
        AuthToken authToken = server.authenticate("applicationID","key1232");
        server.send(authToken,new Message(message),target);
        connect.disconnect();
    }
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[NotificationServer : provdie serveral options under facade  ](){: .btn }
</span>
</div>
```markdown
public class NotificationServer {

    public Connection connect(String IPAddress){
        return new Connection();
    }


    public AuthToken authenticate(String AppID, String key){
        return new AuthToken();
    }

    public void send(AuthToken authToken, Message message,String target){
        System.out.println("Sending data....");
    }
}
```



### Comment
1. NotificationServer provide several methods while NotificationService combine them together with specific consequence, ensureing they are used properly. 