En Haskell, la serie de Fibonacci se puede optimizar de varias maneras. Aquí te presento tres enfoques optimizados:

---

### 1️⃣**Usando Memoization (Lazy Evaluation)**
Haskell permite definir listas infinitas y aprovechar la evaluación diferida para almacenar los resultados de Fibonacci previamente calculados.

```haskell
fibs :: [Integer]
fibs = 0 : 1 : zipWith (+) fibs (tail fibs)

fib :: Int -> Integer
fib n = fibs !! n
```
 **Explicación:**
- `fibs` es una lista infinita donde cada elemento es la suma de los dos anteriores.
- `zipWith (+) fibs (tail fibs)` suma los elementos correspondientes.
- `fib n` extrae el `n`-ésimo elemento en tiempo casi constante gracias a la evaluación diferida.

 **Complejidad:** O(n), pero con espacio O(n) debido a la lista almacenada.

---

### 2️⃣**Usando Recursión con Acumuladores (Tail Recursion)**
Esta versión evita el crecimiento del stack al usar una función auxiliar con acumuladores.

```haskell
fibTail :: Integer -> Integer
fibTail n = fibHelper n 0 1
  where
    fibHelper 0 a _ = a
    fibHelper n a b = fibHelper (n-1) b (a+b)
```

 **Explicación:**
- `fibHelper` recibe dos acumuladores (`a` y `b`) que representan los dos últimos números de Fibonacci.
- La recursión final (`tail recursion`) permite optimización de espacio.

 **Complejidad:** O(n), pero con espacio O(1).

---

### 3️⃣**Usando Matrices (Exponentiación Rápida)**
Para calcular Fibonacci en **O(log n)**, utilizamos multiplicación de matrices.

```haskell
fibMatrix :: Integer -> Integer
fibMatrix n = fst (matrixPower (1,1,1,0) n)

matrixPower :: (Integer, Integer, Integer, Integer) -> Integer -> (Integer, Integer)
matrixPower _ 0 = (0,1)
matrixPower (a,b,c,d) n
  | even n    = matrixPower (a*a + b*c, a*b + b*d, c*a + d*c, c*b + d*d) (n `div` 2)
  | otherwise = let (x, y) = matrixPower (a,b,c,d) (n-1)
                in (a*x + b*y, c*x + d*y)
```

 **Explicación:**
- Se usa la propiedad de que la matriz de transformación de Fibonacci es:

  \[
  \begin{bmatrix} 1 & 1 \\ 1 & 0 \end{bmatrix}^n =
  \begin{bmatrix} F(n+1) & F(n) \\ F(n) & F(n-1) \end{bmatrix}
  \]

- La exponenciación rápida permite reducir la complejidad a **O(log n)**.

 **Complejidad:** O(log n), **muy eficiente para valores grandes**.

---

 **Conclusión**
| Método | Complejidad Tiempo | Complejidad Espacio | Ideal Para |
|--------|-----------------|-----------------|------------|
| Memoization | O(n) | O(n) | Múltiples consultas |
| Tail Recursion | O(n) | O(1) | Valores individuales pequeños/medianos |
| Matrices | O(log n) | O(1) | Valores grandes |

Si necesitas calcular **Fibonacci de números muy grandes**, usa **matrices**. Si necesitas muchos valores, la **lista infinita (memoization)** es mejor.

¿Cuál de estos métodos necesitas usar en tu caso? 
