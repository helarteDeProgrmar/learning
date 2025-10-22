# Advent of neovim

## Day 1: Introducction to nvim

- Porque usar nvim, algunas razones

  - Por la experiencia, porque te abre el cerebro
  - Por hacer las cosas de una mejor forma, aprender el funcionamiento de las
  cosas y mucho mas
  - Por gusto
  - Es open source y altamanet editable con una gran comunidad

- Algunas utilidades de lua

Podemos escribir por ejemplo un fichero con lua:

```lua
print("advent of nvim")

MyCoolFunction = fucntion () print("Here you are in the function") end
```

Y puedes ejecutar con:

- `:source %`: todo el fichero luca actual
- Marcando con `V` despues haciendo `:<,>lua`
- Puedes tambien ejecuta la funcion despues con `:lua MyCoolFunction`

## Day 2: Vim tutor

- Chapa sobre que hay que practicar
- Enseña el tutor, se puede abrir con `:Tutor`
- Insiste con la idea del tutor, completa la leccion 2 entera

## Day 3: Start with lua

Its a long day, you know

- Coments `-- or --[[ ]]--`
- Variables

```lua
local number = 5
local string = "hello"
local string = 'hello'
local multilineal = [[
hehehehe
its cool
]]
local truth, lies = true, false
local elixir = nil
```

- Librerias interesantes

  - Userdata: Interact with C
  - Threat: for schedule task...

- Functions

```lua
local function hello(name)
    print("hello", name)
end

local greet = function (name)
    print("hi " .. name)
end

local higher_order = function (value)
    return function(x)
        return value + x
    end
end

local add_one = higher_order(1)
print(add_one(100)) -- returns 101
```

Las funciones ademas pueden devolver multiple values:

```lua
function multiplevalues() return 1,2,3,4 end

first, second = multiplevalues() -- its correct and catch the values in order

-- cosas mas criminales que seguramente nunca use

local varible_arguments = function ( ... )
    local arguments =  {...}
    for i, v in ipairs({ ... }) do print(i, v) end
    return unpack(arguments)

-- Cosas mas raras existen

local MyTable = {}

function MyTable.one(self, ...) end
function MyTable:one(...) end -- MyTable is the first argument
```

- List and maps

```lua
local list = {1, false, function() print("0") end, "hello"}
print("The first value is obtained with the index 1:", list[1], "equals to 1")
print(list[3]())
```

```lua
local map = {
    literal_key = "jeje",
    [function() return 0 end] = 1234,
    ["rare things inside the ["] = true
}

print(map.literal_key)
print(map[function() return 0 end]) --it doesnt work
print("rare things inside the [")
```

- Modules

Los modulos son simplemente ficheros, no existe una manera de estructurar los
ficheros, simplemente son como una *funcion*. En el caso de abajo se ve como
el fichero devuelve un valor (un mapa) y depues este se utiliza en el fichero
`bar`

```lua
-- foo.lua
local M = {}
M.some_key = function() end
return M
```

```lua
-- bar.lua
local foo = require('foo')
foo.cool_function()
```

- Metatables

Esto es un porrillo pero esta muy guapo, es dar una propiedad a una table y
despues poder hacer operaciones. Es como dar una estructura a las tablas que
tu quieras:

```lua
local vector_mt = {}
vector_mt.__add = fucntion (a, b)
    local result = {}
    for i = 1, #a do
        result[i] = a[i] + b[i]
    end
    return result
end

local v1 = setmetatable({1,2,3}, vector_mt)
local v2 = setmetatable({3,2,1}, vector_mt)
local v3 = v1 + v2

print(v3)
```

Otras *notables fields* para investigar:

- `__index(self)`
- `__newindex(self, key, value)`
- `__cal(self, ...)`

- Bonus :)

### Background info

Simplemente: `Lua uses "Mechanisms over policies"`
Simplemente: `Lua is desinged to be embedded`

### Control flow

#### for

```lua
local list = {1,2,3}
for i = 1, #list do
    print(i, list [i])
end

for index, value in ipairs(list) do
    print(index, value)
end

local map = {
    one = "jaja",
    two = "jeje"
}
for key, value in pairs(map) do
    print(key, value)
end
```

### *falsey* values

En un *if*, aplica como false los valores `false` y `nil`, todo lo demas es
`true`

### Quick neovim goodies

```lua
vim.keymap.set("n", "<space><space>x", "<cmd>source %<CR>")
vim.keymap.set("n", "<space>x", "<cmd>:.lua<CR>")
vim.keymap.set("v", "<space>x", "<cmd>:lua<CR>")
```

## Day 4
