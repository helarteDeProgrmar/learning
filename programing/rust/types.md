Es muy imporntate entender varios conceptos básicos:

1. En Gestion de Memoria: no garbage collector, ownership, move
2. Algunos tipo tienen la propriedad `Copy`.
3. Scope: región de codigo
4. REFERENCIA Y PROPIEDAD

---

#  Tipos de Datos en Rust

###  Tipos Primitivos o Básicos (Stack)

1. **Enteros**: con o sin signo, de distintos tamaños.
   - Ej: `i8`, `i16`, `i32`, `i64`, `i128`, `isize` (con signo)
   - Ej: `u8`, `u16`, `u32`, `u64`, `u128`, `usize` (sin signo)

2. **Flotantes**:
   - `f32`, `f64`

3. **Booleanos**:
   - `bool` (`true` o `false`)

4. **Caracteres**:
   - `char`: representa un caracter Unicode (no solo ASCII), ocupa 4 bytes.

---

###  Tipos Compuestos (Stack)

1. **Tuplas**: combinación ordenada y fija de valores de distintos tipos.
   ```rust
   let tupla: (i32, f64, char) = (42, 6.7, 'a');
   ```

2. **Arrays**: lista de tamaño fijo con elementos del mismo tipo.
   ```rust
   let arr: [i32; 3] = [1, 2, 3];
   ```

---

###  Tipos Más Complejos

1. **String**:
   - `String` es un tipo dinámico que puede crecer.
   - Se almacena en el **heap**.
   ```rust
   let mut s = String::from("Hola");
   s.push_str(", mundo!");
   ```

2. **Vec<T>** (vector):
   - Similar a un array, pero de tamaño **dinámico**.
   ```rust
   let mut v: Vec<i32> = Vec::new();
   v.push(1);
   v.push(2);
   ```

3. **Option<T>** y **Result<T, E>**:
   - Tipos para manejo de errores o ausencia de valor.
   - `Option`: `Some(valor)` o `None`
   - `Result`: `Ok(valor)` o `Err(error)`

---

###  Tipos Definidos por el Usuario

1. **Struct**:
   - Permiten crear tus propios tipos de datos agrupando varios campos.
   ```rust
   struct Persona {
       nombre: String,
       edad: u8,
   }

   let p = Persona {
       nombre: String::from("Ana"),
       edad: 30,
   };
   ```

2. **Enum**:
   - Tipo que puede ser uno de varios valores posibles.
   ```rust
   enum Estado {
       Encendido,
       Apagado,
   }
   ```

---

##  Gestión de Memoria en Rust

Rust **no usa un garbage collector**. Se basa en:

###  Propiedad (Ownership)

Cada valor en Rust tiene un **dueño**. Cuando el dueño sale del scope, el valor se libera automáticamente.

###  Movimiento (Move)

Al asignar un valor a otra variable, se transfiere la propiedad (excepto tipos con `Copy` como enteros).

```rust
let a = String::from("hola");
let b = a; // `a` ya no es usable, porque `b` tomó posesión.
```

###  Referencias y Préstamos (Borrowing)

Puedes prestar referencias a valores sin transferir la propiedad:
- `&T`: referencia inmutable.
- `&mut T`: referencia mutable (solo una a la vez).

---

##  Operadores `*` y `&`

### `&` (Referencia)

Crea una **referencia a un valor** sin tomar la propiedad.

```rust
let a = 5;
let r = &a; // r es una referencia a a
```

### `*` (Desreferencia)

Accede al valor al que apunta una referencia o un puntero.

```rust
let a = 5;
let r = &a;
println!("{}", *r); // desreferencia de r
```

Cuando defines tus propias estructuras con referencias o punteros, estos operadores te permiten controlar el acceso sin copiar.

---

##  Ejemplo Combinado

```rust
fn imprimir(nombre: &String) {
    println!("Hola, {}", nombre);
}

fn main() {
    let nombre = String::from("Carlos");
    imprimir(&nombre); // se pasa referencia, no propiedad
}
```

---
