---
layout: default
title: ChainOfResponsibility Pattern
parent: Behavior Patterns
grand_parent: Design Patterns
permalink: /docs/design-pattern/behavior-pattern/chainofresponsibility/
nav_order: 9
---

# ChainOfResponsibility Pattern
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

### Overall Diagram

![ChainOfResponsibility Diagram](../../resource/chainofresponsibility_diagram.png){:height="400px" width="600px" .centered-image}

### Sample source code

<div class="code-example" markdown="1">
<span class="fs-3">
[Handler -> Handler  ](){: .btn }
</span>
</div>
```markdown
public abstract class Handler {
    private Handler next;

    public Handler(Handler next) {
        this.next = next;
    }

    public void handle(HttpRequest request){
        if (doHandle(request))
            return;

        if(next != null)
            next.handle(request);
    }

    protected abstract boolean doHandle(HttpRequest request);
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[WebServer -> Sender  ](){: .btn }
</span>
</div>
```markdown
public class WebServer {
    private Handler handler;

    public WebServer(Handler handler) {
        this.handler = handler;
    }

    public void handle(HttpRequest request){
        handler.handle(request);
    }
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[HttpRequest -> request  ](){: .btn }
</span>
</div>
```markdown
public class HttpRequest {
    private String userName;
    private String password;

    public HttpRequest(String userName, String password) {
        this.userName = userName;
        this.password = password;
    }

    public String getPassword() {
        return password;
    }

    public String getUserName() {
        return userName;
    }

}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[Authenticator -> ConcreteHandler1  ](){: .btn }
</span>
</div>
```markdown
public class Authenticator extends Handler{
    public Authenticator(Handler next) {
        super(next);
    }

    @Override
    public boolean doHandle(HttpRequest request) {
        boolean isValid = (request.getUserName() == "admin" && request.getPassword() == "12345");
        System.out.println("Authenticated: " + isValid);
        return !isValid;
    }

}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[Compressor -> ConcreteHandler2  ](){: .btn }
</span>
</div>
```markdown
public class Compressor extends Handler{
    public Compressor(Handler next) {
        super(next);
    }

    @Override
    protected boolean doHandle(HttpRequest request) {
        System.out.println("Compressed.");
        return false;
    }
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[Logger -> ConcreteHandler3  ](){: .btn }
</span>
</div>
```markdown
public class Logger extends Handler{
    public Logger(Handler next) {
        super(next);
    }

    @Override
    protected boolean doHandle(HttpRequest request) {
        System.out.println("Logged ...");
        return false;
    }
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[Encryptor -> ConcreteHandler4  ](){: .btn }
</span>
</div>
```markdown
public class Encryptor extends Handler{
    public Encryptor(Handler next) {
        super(next);
    }

    @Override
    protected boolean doHandle(HttpRequest request) {
        System.out.printf("Encrypted");
        return false;
    }
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[Main class  ](){: .btn }
</span>
</div>
```markdown
        Encryptor encryptor = new Encryptor(null);
        Compressor compressor = new Compressor(encryptor);
        Logger logger = new Logger(compressor);
        Authenticator authenticator = new Authenticator(logger);
        WebServer server = new WebServer(authenticator);
        server.handle(new HttpRequest("admin", "12345"));
```

### Comment

1. In chainOfResponsibility pattern, handler is a trigger, they connected and buit up a chain with serial actions. 
2. By creating a new HttpRequest in main class, a http session is initiated, and all the actions on the chain share the same session.  
3. Pay attention to the trigger condition of each action, sometime false result is trigger, sometime true result of the action is trigger.  