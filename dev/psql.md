# psql

**Para interartuar con una base de datos post.**

---

## 1. Comandos para navegación y ayuda

* `\q`
  Salir de `psql`.

* `\h [comando_sql]`
  Ayuda para un comando SQL. Ej: `\h SELECT` te muestra la sintaxis.

* `\?`
  Lista todos los comandos internos de `psql`.

---

## 2. Información sobre bases de datos y conexiones

* `\l` o `\list`
  Lista todas las bases de datos.

* `\c <dbname> [usuario]`
  Cambiar a la base de datos `<dbname>`, opcionalmente como otro usuario.

* `\conninfo`
  Muestra información de la conexión actual.

---

## 3. Información sobre esquemas, tablas y objetos

* `\dn`
  Lista los esquemas existentes.

* `\dt [esquema.]`
  Lista las tablas en un esquema (por defecto el público `public`).

* `\dv`
  Lista las vistas.

* `\di`
  Lista los índices.

* `\df`
  Lista funciones.

* `\ds`
  Lista secuencias.

---

## 4. Información detallada de tablas y otros objetos

* `\d <tabla>`
  Muestra la estructura de la tabla, columnas, tipos y claves.

* `\d+ <tabla>`
  Igual que `\d` pero con detalles extras, como tamaño y descripciones.

---

## 5. Ejecución y gestión de consultas SQL

* Ejecutar consultas SQL normales:

```sql
SELECT * FROM tabla LIMIT 10;
```

* Para terminar una consulta que ocupa varias líneas, termina con punto y coma `;`.

---

## 6. Gestión de transacciones

* `BEGIN;`
  Inicia una transacción.

* `COMMIT;`
  Guarda los cambios hechos en la transacción.

* `ROLLBACK;`
  Deshace los cambios hechos en la transacción.

---

## 7. Exportar e importar datos

* `\copy <tabla> TO 'archivo.csv' CSV HEADER;`
  Exporta tabla a archivo CSV (desde cliente local).

* `\copy <tabla> FROM 'archivo.csv' CSV HEADER;`
  Importa archivo CSV a tabla.

---

## 8. Comandos para variables y scripts

* `\set nombre valor`
  Define una variable dentro de `psql`.

* Usar variable: `:nombre`
  Ejemplo:

```sql
\set id 10
SELECT * FROM tabla WHERE id = :id;
```

* `\i archivo.sql`
  Ejecuta comandos SQL desde un archivo.

---

## 9. Mostrar y cambiar configuración

* `SHOW nombre_parametro;`
  Ejemplo: `SHOW search_path;`

* `SET nombre_parametro = valor;`
  Cambia configuración en sesión actual. Ejemplo:

```sql
SET search_path TO myschema;
```

---

## 10. Comandos para manejar roles y permisos

* Listar roles:

```sql
\du
```

* Crear un rol:

```sql
CREATE ROLE nombre;
```

---

## Tips extra:

* Puedes usar flechas arriba/abajo para navegar por el historial de comandos.
* Usa `TAB` para autocompletar nombres de tablas, columnas y comandos.
* Comandos comienzan con `\` y son específicos de `psql`.
* SQL termina con `;` para ejecutar.

---
