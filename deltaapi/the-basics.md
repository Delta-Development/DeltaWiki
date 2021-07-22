---
description: Learn the basics of the API here!
---

# The Basics

## 🖊 Basics of the API

In order for this API to work, you will need the DeltaCore plugin on your server, or create your own plugin with things similar to what's in DeltaCore, some things need to be initialized. [\[Download\]](https://www.spigotmc.org/resources/deltacore-api-for-all-delta-plugins.94283/) [\[Source Code\]](https://github.com/Delta-Development/DeltaCore)

### Message Util

In DeltaAPI, there is a message util that makes sending messages easier. No more using `ChatColor.translateAlternateColorCodes`. Here are some examples of the util being used:

```java
// To send a message to a player
Player p = (Player) sender;
new Message("&cHello &lworld").send(p); // Sends the message to the player with colour and formatting codes translated.

// To broadcast a message to the entire server
new Message("&4&lTHIS IS A BROADCAST").broadcast(); // Sends a message to everyone on the server with colour and formatting.
```

### Commands

The command system is simple, easy to use, and has many different ways of doing it! You do not need to register the command in plugin.yml. You also don't need to make a separate class for Tab Completion, it's built-in and you can utilize it using one method and registers automatically!

#### **Creating a Command**

**Step 1**

Extend ICommand in the class you want to use. Once you do that, you will get something like this.

```java
public class MyCommand extends ICommand {

    public MyCommand(String name, List<String> aliases) {
        super(name, aliases);
    }


    @Override
    public void onCommand(CommandSender sender, String[] args) {

    }
}
```

You can remove the constructor parameters and fill in the info to make it look like this:

```java
    public MyCommand() {
        super("mycommand", Collections.singletonList("mysinglealias"));
        // To have multiple aliases, use Arrays.asList("alias1", "alias2", "etc"))
    }
```

You can set certain settings for the command such as the permission node, if the player is player-only or console-only, and if it's disabled or not.

```java
        setPermissionNode("my.permission"); // Sets a permission node for the plugin
        setPlayerOnly(true); // Makes it so only players can use the command
        setConsoleOnly(true); // Makes it so only console can use the command
        setDisabled(true); // Makes it so no one can use the command, period.
```

**Alternative ways of creating commands**

Super + Annotation:

```java
@PlayerOnly
@Permission(perm = "my.permission")
// Rather than setting the settings for the commands
// in the constructor, you can use annotations
public class MyCommand extends ICommand {

    public MyCommand() {
        super("mycommand", Arrays.asList("alias1", "alias2", "etc"));
    }
```

Annotation Only:

```java
@CommandInfo(name = "mycommand", aliases = {"alias1", "alias2", "alias3"}, playerOnly = true)
// Rather than using a constructor for your command
// you can just use one annotation!
public class MyCommand extends ICommand {
    @Override
    public void onCommand(CommandSender sender, String[] args) {

    }
}
```

### **Tab Complete**

As mentioned earlier, there is built-in Tab Completion, it's just one method inside of the constructor of the command! This is a simple example of it.

```java
        // This takes in 2 parameters, sender and strings,
        // Sender is the CommandSender (or the player running the command)
        // Strings, otherwise the arguments in the command
        setTabComplete((sender, strings) -> {
            return Arrays.asList("alias1", "alias2", "alias3");
        });
```

#### **Adding SubCommands**

There's SubCommands, which is a replacement for checking for args\[0\] or args\[1\]. It's much more cleaner and it saves time. This section will only teach you about adding SubCommands to a main command.

```java
    public MyCommand() {
        addSubCommands(
                new SubCommand1(),
                new SubCommand2(),
                new SubCommand3()
        );
    }
```

### SubCommands

SubCommands is similar to ICommand, the same way of doing commands, annotations, and supers, so no need to cover it again. The only difference is you need to extends ISubCommand and implement the method.

