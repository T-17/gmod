![](http://i.imgur.com/4dCCfNF.png)

Powerful is a multi-functional library for starfall. It offers:
- Object Oriented Programming (Multiple Inheritance)
- Network system with less traffic
- Instance-global variables
- Caching for wire inputs



### Object Oriented Programming
```lua
--@server
--@include lib/powerful.txt
local pw = require("lib/powerful.txt")

local Creature = pw.class()

function Creature:new()
  self.hp = 100
end

function Creature:damage(dmg)
  self.hp = self.hp - dmg
end


local Person = pw.class(Creature)

function Person:new(name)
    self.name = name
end

local me = Person("suun")
me:damage(42)
```

### Networking
```lua
--@include lib/powerful.txt
local pw = require("lib/powerful.txt")

pw.net.register {
	"Msg"
}

if SERVER then
	pw.net.onMessage("Msg", function()
		print("Arrived")
	end)
else
	if player() ~= owner() then return end
	pw.net.msg("Msg")
end
```

### Instance-Global variables
```lua
--@include lib/powerful.txt
local pw = require("lib/powerful.txt")

if SERVER then
	pw.globals.a = 1
else
	timer.simple(1, function()
		print(pw.globals.a) -- 1
	end)
end
```
