---
description: >-
  Our smart signs integration plugin allows you to update roadway signs in-game
  directly from the CAD!
---

# Smart Signs

![Sonoran CAD x London Studios](../../../.gitbook/assets/image%20%28217%29.png)

![London Studios - Smart Signs](../../../.gitbook/assets/image%20%2850%29.png)

{% hint style="warning" %}
This plugin utilizes API endpoints that require the **Pro** version of Sonoran CAD or higher. For more information, view our [pricing ](../../../pricing/faq/)page.
{% endhint %}

{% hint style="success" %}
Looking for VPS, web, or dedicated hosting? Check out our official [server hosting](../../../other-products/server-hosting.md)!
{% endhint %}

## Installation Guide

### 1. Download and Install the Framework

If you haven't already, be sure to install and configure the [plugin framework](../framework-installation.md) first.

### 2. Download the Plugin and all Dependencies

Click [HERE](https://sonoran.link/UWCLJjhU) to download the free Sonoran CAD Smart Sign plugin .zip file from London Studios.

### 3. Install the Plugin and all Dependencies

Follow the [standard plugin installation guide](../plugin-installation/) for the Smart Signs plugin.

{% hint style="danger" %}
If you have the original London Studios SmartSigns resource **please remove and/or disable it from running**. Our plugin completely replicates the functionality of the original resource and they will conflict if both are running at the same time.
{% endhint %}

### 4. Configure your Sign Locations

In the `config_smartsigns.lua` file, you can specify sign locations and labels.

The smart signs plugin also has support with ESX, VRP, Discord logging, ace permissions, and more. [View the documentation](https://docs.londonstudios.net/#document-6).

### 5. Copy the Stream Assets Folder

The downloaded zip file contains both the `smartsigns` plugin and the `stream` assets folder.

The `stream` assets folder must be copied over to the `[sonorancad]/sonorancad` directory.

### 6. Set your Game Server IP/Port

In the Admin panel, navigate to Advanced &gt; In-Game Integration &gt; Push Events and Live Map

Ensure your game server's IP and game port are set. The CAD will use this to push sign updates to your server.

![Sonoran CAD - Push Event Panel](../../../.gitbook/assets/image%20%28220%29.png)

### 7. Modifying Signs in the CAD

The street sign panel can be found in both the Dispatch and DMV pages. Users will need the `Modify Street Signs` permissions in order to update them.

Here, you can easily search to filter sign labels. Sign text can also be easily duplicated from one sign to another.

![Sonoran CAD - Street Signs UI](../../../.gitbook/assets/streetsigns.gif)

## How to use

### Usage

This script works by approaching a sign. When a player approaches a sign and are in the range of the control panel, they are able to edit the text of the sign if they meet the required permission checks. The resource has been optimized so that the signs will load and unload for players based on how close they are to each sign which is perfect for larger servers as it means that server resources will not be used unnecessarily.

### Full Feature List

**Signs** – This is the main element of the resource, allowing you to walk up to a sign and change the text from an in-game control panel at the bottom of the sign. This can be used to open a world of roleplay opportunities.  
**Word Denylist** – You are able to set the resource up so that users cannot use specific words on a sign.  
**Discord Logs** – You can choose to send logs to your Discord server via a webhook each time a player sets the text on a sign.  
**Custom Model** – This resource includes high-quality letters and a custom sign model created by Beaver Mods. This will ultimately enhance realism.  
**Highly Configurable** – This resource is highly configurable, allowing you to setup each sign separately. You can adjust the location of each sign, all messages and even add extra characters from other languages.  
**Permission Checks** – You can easily enable permission checks in the configuration file for ACE permissions, framework jobs/groups or SonoranCAD active unit checking.

We understand that it may be confusing to use for some of our users. If you need support please feel free to open a ticket in the official London Studios Discord.

## Smart Signs Configuration

You can easily open the `config_smartsigns.lua` and configure the script to your liking in either **notepad**, **notepad ++** or using **Visual Studio Code.**

{% hint style="warning" %}
The config examples below are not the full configuration file and further explanation comments of what each setting does can be found in the `config_smartsigns.lua` file.
{% endhint %}

### **Main Configuration**

The first section is called **main**, allowing you to set the following:

```lua
local config = {
    enabled = false,
    configVersion = "1.0",
    pluginName = "smartsigns",
    pluginAuthor = "SonoranCAD",

    main = {
        loadInDistance = 300.0,
        accessPointDistance = 3.0,
        signModelName = `prop_led_trafficsign`,
        instructionalText = "Press [E] to adjust sign",
        adjustButton = {0, 103}, -- {control group, control}
        developerMode = false,
        enableBlips = true,
        bannedWords = {
            "fuck",
            "shit",
        },
        centerText = true,
        animation = {
            enabled = true,
            dict = "anim@heists@prison_heiststation@cop_reactions", -- This is the animation dictionary (these show in bold on the animation list)
            name = "cop_b_idle", -- This is the animation name (these show below bold dictionaries on the animation list)
        },
        logging = {
            enabled = false,
            displayName = "Smart Signs",
            colour = 31487,
            title = "**New Sign Log**",
            icon = "https://i.imgur.com/o7oAPb8.png",
            footerIcon = "https://i.imgur.com/n3n7JNW.png",
            dateFormat = "%d-%m-%Y %H:%M:%S", -- Day-Month-Year Hour-Minute-Second
            webhook = "",
            bannedWordLogs = {
                enabled = true, 
                colour = 16711680,
            }
        },
        soundEffect = {
            enabled = true,
            name = "CONFIRM_BEEP",
            dict = "HUD_MINI_GAME_SOUNDSET",
        },
        signOffset = {0.0, 0.0, 0.0}, -- x, y, z
    },

```

To change the activation key \(adjustButton\), replace it with your desired key code from [here](https://docs.fivem.net/docs/game-references/controls/).

You can see from the above config just how configurable the resource is, allowing you to set many features such as the load in the distance and access points to edit the text of the signs, the different denied words and the animations played while the player is typing.

Secondly, the **instructionalText** section allows you to convert the access message to another language.

### **Signs Configuration**

You’ll be able to configure all signs, locations and their default messages in this part of the config. We have pre-configured some for you.  
Below is a demonstration of how you should lay out your config. An important thing to note is that each line can support a maximum of 14 characters of A-Z and 0-9 by default. The **defaultText** value is not required, if you do not fill this out the sign will be empty by default.

```lua
signs = {
    {
       sign = {vector3(xCoordinate, yCoordinate, zCoordinate), rotationInDegrees)},
       defaultText = {"LINE ONE", "LINE TWO", "LINE THREE"},
    },
    {
       sign = {vector3(866.47338867188, 133.4723815918, 70.606071472168), 325.0},
       defaultText = {"ACCIDENT AHEAD", "WATCH YOUR", "SPEED"}
    }
},
```

To make it easier to setup signs we have added a `/newsign` command which will only work while **developerMode** is set to true in `config_smartsigns.lua`.  
This command will spawn a sign prop in which can be repositioned with the following controls:

**PAGE UP** — move sign up  
**PAGE DOWN** — move sign down  
**UP ARROW** — move sign forwards  
**DOWN ARROW** — move sign backwards  
**LEFT ARROW** — move sign to the left  
**RIGHT ARROW** — move sign to the right  
**B** — rotate sign clockwise  
**N** — rotate sign anti-clockwise  
**ENTER** — finish placement

Once you press ENTER you will recieve a notification in the bottom left of your screen with the coordinates. You can then type these into your config file and the sign will be spawned next time you start the **smartsigns** resource.

## Permission Checks

We’ve made it simpler than ever to integrate permissions into the resource. This can be Ace Permissions, VRP or even ESX Integration \(built-in\).

This means that you can restrict certain players, permissions or even jobs/groups from setting the message on a sign.

### **Ace Permission Integration**

In the `config_smartsigns.lua` file, you can easily enable ace permissions and set the required permission.

You could then add this to certain players in the `server.cfg` or even groups as part of a server framework.

For more help on that, see some [documentation on Ace Permissions here](https://forum.cfx.re/t/basic-aces-principals-overview-guide/90917).

```lua
acePermissions = {
    enable = false,
    permission = “update.sign”
},
```

### **vRP Integration**

In the `config_smartsigns.lua` file, you can easily enable vRP Integration including both `vRP.hasPermission` checks and `vRP.hasGroup` checks. This can allow you to restrict it to a police job for example, or highways maintenance job, if that exists on your server.

Simply changed enabled to true to enable vRP integration. This will then generate the necessary vRP Proxy on the server, enabling global vRP functions such as GetUserId.

In the `checkGroup = {}` section, you can set it up to check if the user has a required group. In the groups box, you can enter all the groups you would like to have permission, such as adding both police and administrators, as they may need to access them.

In the `checkPermission = {}` section, you can do the same as a group, but for a permission instead. As you use the vRP framework you should be familiar with permissions and how to issue them.

You should check your vRP `groups.lua` file to view your groups and the permissions for each group.

```lua
vRP = {            
    enabled = false,            
    checkGroup = {                
        enabled = true, — Enable this to use vRP group check                
        groups = {“police”, “emergency”, “admin”}, — A user can have any of the following groups, meaning you can add different jobs            
    },            
    checkPermission = {                
        enabled = false, — Enable this to use vRP permission check                
        permissions = {“police.menu”, “player.kick”} — A user can have any of the following permissions, allowing you to add multiple            
        
    },        
    
}
```

### **ESX Integration**

In the `config_smartsigns.lua` file, you can easily enable ESX Integration using a job check.

Simply changed enabled to true to enable ESX integration. This will then generate the necessary ESX Shared Object on the server, enabling you to use ESX functions.

In the `checkJob = {}` section, you can set it up to check if the user has a required job. For example, by keeping it as `“police”`, it will only work if the user has the police job. Alternatively, you may choose to add more such as `“admin”`.

You should check your ESX jobs database table to be familiar with what jobs are configured on your server.

```lua
ESX = {            
    enabled = false,            
    checkJob = {                
        enabled = true, — Enable this to use ESX job check                
        jobs = {“police”} — A user can have any of the following jobs, allowing you to add multiple            
    }        
},
```

Overall, we think we’ve made it easy for you to add permission checks into the resource. If you need additional help setting it up, our support team is here to help. You can [open a support ticket here](https://support.sonoransoftware.com).
