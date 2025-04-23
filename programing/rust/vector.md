## Metodos principales de `Vec<T>`

`Método` | Descripción
`Vec::new()` | Crea un nuevo vector vacío
`vec![1,` 2, 3] | Macro que crea un vector inicializado
`.push(valor)` | Agrega un elemento al final del vector
`.pop()` | Elimina y devuelve el último elemento (Option<T>)
`.insert(indice, valor)` | Inserta un elemento en una posición específica
`.remove(indice)` | Elimina el elemento en una posición específica y lo devuelve
`.len()` | Devuelve la cantidad de elementos
`.is_empty()` | Devuelve true si está vacío
`.clear()` | Borra todos los elementos
`.contains(&valor)` | Devuelve true si el valor está presente
`.sort()` | Ordena el vector (requiere que los elementos implementen Ord)
`.reverse()` | Invierte el orden de los elementos
`.truncate(n)` | Deja solo los n primeros elementos
`.resize(n, valor)` | Redimensiona a n elementos; si crece, los nuevos se llenan con valor


## Para transformar a iter

Variantes de iter():

Método	Tipo de Iteración	Mutabilidad	Valor que devuelve
.iter()	Iterador inmutable	❌ No	&T (referencia)
.iter_mut()	Iterador mutable	✅ Sí	&mut T
.into_iter()	Iterador de consumo	❌/✅ depende	T (mueve el valor)


### Iterar mientras borras

Necesitas hacer... | Mejor estrategia
Eliminar mientras iteras | while + índice manual + remove
Agregar mientras iteras | while con push()
Solo filtrar elementos | .retain()
Crear nueva lista basada en otra | .iter().filter().map().collect()


### Iterar de manera funcional

Despues de :

```rust
vec.iter()
vec.iter_mut()
vec.into_iter()
```


---

## 🧠 Funciones tipo funcional aplicables a `Vec<T>` (con cabeceras)

Aquí te van agrupadas por categoría:

---

### 🗂️ **Transformaciones**

| Función       | Firma                                                                  | Descripción                           |
|---------------|------------------------------------------------------------------------|----------------------------------------|
| `.map()`      | `fn map<B, F>(self, f: F) -> Map<Self, F>`                              | Aplica una función a cada elemento     |
| `.filter()`   | `fn filter<F>(self, predicate: F) -> Filter<Self, F>`                  | Filtra elementos que cumplen una condición |
| `.filter_map()` | `fn filter_map<B, F>(self, f: F) -> FilterMap<Self, F>`              | Combina `.filter()` + `.map()`         |
| `.flat_map()` | `fn flat_map<U, F>(self, f: F) -> FlatMap<Self, F, U>`                 | Mapea y aplana (devuelve iteradores)   |
| `.enumerate()`| `fn enumerate(self) -> Enumerate<Self>`                                | Devuelve tuplas `(index, valor)`       |
| `.zip()`      | `fn zip<U>(self, other: U) -> Zip<Self, U::IntoIter>`                  | Combina dos iteradores en uno de tuplas|

---

### 📊 **Reducciones / Acumulaciones**

| Función       | Firma                                                                  | Descripción                            |
|---------------|------------------------------------------------------------------------|----------------------------------------|
| `.fold()`     | `fn fold<B, F>(self, init: B, f: F) -> B`                              | Acumula valor inicial con función       |
| `.reduce()`   | `fn reduce<F>(self, f: F) -> Option<T>`                               | Similar a fold pero sin valor inicial  |
| `.sum()`      | `fn sum<S>(self) -> S`                                                | Suma todos los valores                 |
| `.product()`  | `fn product<P>(self) -> P`                                            | Multiplica todos los valores           |
| `.count()`    | `fn count(self) -> usize`                                             | Cuenta cuántos elementos hay           |

---

### 🕵️ **Búsqueda y verificación**

| Función        | Firma                                                                 | Descripción                         |
|----------------|-----------------------------------------------------------------------|--------------------------------------|
| `.find()`      | `fn find<P>(self, predicate: P) -> Option<Self::Item>`                | Primer elemento que cumple condición |
| `.find_map()`  | `fn find_map<B, F>(self, f: F) -> Option<B>`                          | Como `filter_map` pero solo el primero |
| `.any()`       | `fn any<F>(self, f: F) -> bool`                                       | ¿Alguno cumple la condición?         |
| `.all()`       | `fn all<F>(self, f: F) -> bool`                                       | ¿Todos cumplen la condición?         |
| `.position()`  | `fn position<F>(self, f: F) -> Option<usize>`                         | Índice del primer que cumple          |
| `.rposition()` | `fn rposition<F>(self, f: F) -> Option<usize>`                        | Igual que `.position()` pero al revés |

---

### 🔃 **Recolección**

| Función      | Firma                                                         | Descripción                         |
|--------------|----------------------------------------------------------------|--------------------------------------|
| `.collect()` | `fn collect<B>(self) -> B where B: FromIterator<Self::Item>`   | Convierte en `Vec`, `HashSet`, `String`, etc. |

---

### 📚 Ejemplo ilustrativo:

```rust
fn main() {
    let numeros = vec![1, 2, 3, 4, 5];

    let resultado: Vec<i32> = numeros
        .iter()
        .filter(|x| **x % 2 == 0) // solo pares
        .map(|x| x * 10)          // multiplica por 10
        .collect();

    println!("{:?}", resultado); // [20, 40]
}
```

---

## ✅ Bonus: `.into_iter()` vs `.iter()` vs `.iter_mut()`

| Método        | Tipo de elemento devuelto | Toma posesión | Modificable |
|---------------|----------------------------|---------------|-------------|
| `.iter()`     | `&T`                       | ❌ No          | ❌ No        |
| `.iter_mut()` | `&mut T`                   | ❌ No          | ✅ Sí        |
| `.into_iter()`| `T`                        | ✅ Sí          | ✅ (porque ya es tuyo) |

---

