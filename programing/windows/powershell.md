PowerShell es un shell orientado a objetos construido sobre .NET,
pensado tanto para administración interactiva como para scripting avanzado.
A continuación encontrarás un repaso de sus elementos fundamentales para
que puedas desarrollar scripts robustos y mantenibles.

---

## 1. Cmdlets básicos y navegación

PowerShell utiliza *cmdlets* (pronunciado “command-lets”),
que son comandos especializados. Algunos de los más útiles al comenzar:

| Cmdlet                 | Descripción                                        | Ejemplo                                                                         |
|------------------------|----------------------------------------------------|---------------------------------------------------------------------------------|
| `Get-Help`             | Muestra la ayuda de un cmdlet                      | `Get-Help Get-Process -Full`                                                    |
| `Get-Command`          | Lista cmdlets, funciones y alias disponibles       | `Get-Command -Name *-Service`                                                   |
| `Get-Process`          | Muestra procesos en ejecución                      | `Get-Process | Where-Object {$_.CPU -gt 100}`                                   |
| `Get-Service`          | Lista servicios del sistema                        | `Get-Service | Where-Object {$_.Status -eq 'Running'}`                           |
| `Get-ChildItem` (alias `gci`) | Lista archivos y carpetas (como `dir` o `ls`) | `Get-ChildItem -Recurse -Filter *.ps1`                                          |
| `Get-Content`          | Lee el contenido de un archivo                     | `Get-Content .\log.txt -Tail 20`                                                |
| `Set-Location` (alias `cd`) | Cambia de directorio                         | `Set-Location C:\Scripts`                                                       |
| `New-Item`             | Crea archivos o carpetas                          | `New-Item -Path . -Name data.csv -ItemType File`                                |
| `Copy-Item`, `Move-Item`, `Remove-Item` | Copiar, mover o eliminar recursos | `Copy-Item .\a.txt .\backup\a.txt`                                              |
| `Import-Module`        | Carga módulos con cmdlets adicionales             | `Import-Module ActiveDirectory`                                                 |

Además, el **pipeline** (`|`) te permite encadenar objetos y
filtrarlos con cmdlets como `Where-Object`, `Select-Object`, `Sort-Object` o
`ForEach-Object`. Por ejemplo:

```powershell
Get-Service |
  Where-Object {$_.Status -eq 'Running'} |
  Select-Object -Property Name, Status |
  Sort-Object Name
```

---

## 2. Variables

- **Declaración y asignación**:  
  ```powershell
  $nombre = "Juan"
  $contador = 0
  $pi = 3.1416
  ```
- **Tipos dinámicos**: no necesitas declarar el tipo; PowerShell los infiere.
- **Arrays**:  
  ```powershell
  $frutas = @("Manzana","Plátano","Cereza")
  $frutas += "Naranja"    # agrega un elemento
  ```
- **Hash tables**:  
  ```powershell
  $persona = @{
    Nombre = "Ana"
    Edad   = 30
    País   = "España"
  }
  ```
- **Variables automáticas**:  
  - `$PSVersionTable` (información de la versión)  
  - `$Error` (colección de errores)  
  - `$args` (argumentos posicionales en un script o función)  
  - `$_` o `$PSItem` (el objeto actual en el pipeline)  
- **Scopes**:  
  - Local (por defecto en funciones/loops)  
  - `script:` (a nivel de fichero .ps1)  
  - `global:` (accesible en toda la sesión)

---

## 3. Estructuras de control

### 3.1. Condicionales `if` / `elseif` / `else`
```powershell
if ($edad -ge 18) {
  "Es mayor de edad"
}
elseif ($edad -ge 13) {
  "Es un adolescente"
}
else {
  "Es un niño"
}
```

### 3.2. `switch`
```powershell
switch ($estadoServicio) {
  'Running' { "El servicio está en ejecución"; break }
  'Stopped' { "El servicio está detenido"; break }
  Default   { "Estado desconocido: $estadoServicio" }
}
```

### 3.3. Manejo de errores con `try`/`catch`/`finally`
```powershell
try {
  Remove-Item "C:\noexisto.txt" -ErrorAction Stop
}
catch [System.IO.IOException] {
  "Error de IO: $_"
}
catch {
  "Otro error: $_"
}
finally {
  "Siempre se ejecuta al final"
}
```

---

## 4. Bucles

### 4.1. `for`
```powershell
for ($i = 0; $i -lt 5; $i++) {
  "Iteración $i"
}
```

### 4.2. `foreach` (statement)
```powershell
foreach ($f in $frutas) {
  "Me gusta $f"
}
```

### 4.3. `ForEach-Object` (pipeline)
```powershell
Get-Process | ForEach-Object {
  "{0} usa {1:N2} CPU" -f $_.Name, $_.CPU
}
```

### 4.4. `while`
```powershell
while ($contador -lt 3) {
  "contador = $contador"
  $contador++
}
```

### 4.5. `do { } while` y `do { } until`
```powershell
do {
  $valor = Get-Random -Minimum 1 -Maximum 10
  "aleatorio = $valor"
} until ($valor -eq 5)
```

---

## 5. Pipeline y objetos

PowerShell pasa **objetos .NET** entre cmdlets, no líneas de texto. Esto te permite:

1. **Filtrar** con `Where-Object { <condición> }`  
2. **Seleccionar** propiedades con `Select-Object -Property Prop1,Prop2`  
3. **Ordenar** con `Sort-Object Propiedad`  
4. **Formatear** la salida con `Format-Table`, `Format-List`, etc.

> **Tip**: antes de formatear, si vas a procesar datos en scripts, evita `Format-*` porque convierte objetos en texto. Úsalo solo para mostrar en pantalla.

---

## 6. Funciones, scripts y módulos

### 6.1. Definir funciones y parámetros
```powershell
function Saludar {
  [CmdletBinding()]
  param(
    [Parameter(Mandatory)]
    [string] $Nombre,

    [int] $Veces = 1
  )
  for ($i=1; $i -le $Veces; $i++) {
    Write-Output "Hola, $Nombre!"
  }
}
```

### 6.2. Creación de scripts
- Guarda tus comandos en archivos `.ps1`.  
- Ejecútalos con `.\script.ps1` (y asegura tu política de ejecución con `Set-ExecutionPolicy`).

### 6.3. Módulos
- Agrupa funciones en un archivo `.psm1` o en una carpeta de módulo.  
- Usa `Export-ModuleMember -Function *` para exponerlas.  
- Cárgalos con `Import-Module MiModulo`.

---

## 7. Aliases y perfil de usuario

- Los **aliases** (`gci`, `ls`, `dir`) simplifican la línea de comandos, pero en scripts es mejor usar el nombre completo del cmdlet.  
- Personaliza tu entorno editando tu perfil en `$PROFILE` (p. ej. para añadir funciones, aliases o variables por defecto).

---

## 8. Buenas prácticas

- **Nombres Verb-Noun**: `Get-Item`, `Set-Location`… en tus funciones usa esta convención.  
- **Comentarios de ayuda** en funciones:
  ```powershell
  <#
  .SYNOPSIS
    Breve descripción.
  .DESCRIPTION
    Descripción detallada.
  .PARAMETER Nombre
    Nombre de la persona.
  #>
  ```
- **Parámetros seguros**: usa `[ValidateNotNullOrEmpty()]`, `[ValidateRange()]`, etc.  
- **Streams de salida**:
  - `Write-Output` (salida normal)  
  - `Write-Error`, `Write-Warning`, `Write-Verbose`, `Write-Debug`  
- **-WhatIf** y **-Confirm**: implementa en tus cmdlets para simular cambios y pedir confirmación.

---
