---
layout: default
title: Singleton Pattern
parent: Creational Patterns
grand_parent: Design Patterns
permalink: /docs/design-pattern/structural-pattern/singleton/
nav_order: 1
---

# Singleton Pattern
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

### Overall Diagram

![Singleton Diagram](../../resource/singleton_diagram.png){:height="400px" width="600px" .centered-image}

### Sample source code

<div class="code-example" markdown="1">
<span class="fs-3">
[ConfigManager-> Singleton ](){: .btn }
</span>
</div>

```markdown
public class ConfigManager {
    private Map<String, Object> settings = new HashMap<>();
    private static ConfigManager instance = new ConfigManager();

    private ConfigManager(){}

    public static ConfigManager getInstance() {
        return instance;
    }

    public Object get(String key) {
        return settings.get(key);
    }

    public void set(String key, Object value ) {
        this.settings.put(key,value);
    }
}
```
<div class="code-example" markdown="1">
<span class="fs-3">
[Main class : Here is a sample how to load configurations ](){: .btn }
</span>
</div>
```markdown
    ConfigManager manager = ConfigManager.getInstance();
    manager.set("name", "Helen xie");
    System.out.println(manager.get("name"));

    ConfigManager other = ConfigManager.getInstance();
    System.out.println(other.get("name"));
```

### Comment
1. Singleton pattern is widely used for configuration loading, such as environment parameters and common settings.
2. ConfigManager has private Construction class, and a public method to get instance, to ensure using the same object and data synchronization.
