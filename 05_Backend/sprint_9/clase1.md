# 📚 Introducción a SQL Básico

## ¿Qué es SQL?

**SQL** (Structured Query Language) es el lenguaje estándar utilizado para **gestionar y consultar bases de datos relacionales**. Es como el idioma universal para hablar con las bases de datos.

### ¿Para qué sirve SQL?

- 📖 **Consultar datos** - Obtener información de la base de datos
- ➕ **Insertar información** - Agregar nuevos registros
- ✏️ **Actualizar datos** - Modificar información existente
- 🗑️ **Eliminar registros** - Remover datos
- 🔗 **Gestionar relaciones** - Conectar tablas entre sí

---

## Conceptos Clave

### 📊 Tabla
Una tabla es como una hoja de Excel donde se organiza la información:
- **Filas (rows)** = Registros individuales
- **Columnas (columns)** = Propiedades de cada registro

**Ejemplo: Tabla movies**

id: 1, title: Matrix, year: 1999
id: 2, title: Interstellar, year: 2014

### 🗄️ Base de Datos
Es el contenedor principal que almacena todas las tablas.

```sql
CREATE DATABASE store;
USE store;
```

---

## Operaciones CRUD

SQL tiene **4 operaciones principales** para trabajar con datos:

**Create** = INSERT (Crear nuevos registros)
**Read** = SELECT (Leer/Consultar datos)
**Update** = UPDATE (Actualizar registros)
**Delete** = DELETE (Eliminar registros)

---

## 💡 Ejemplos Rápidos

### 📖 Consultar datos (SELECT)
```sql
SELECT * FROM movies;
SELECT title, year FROM movies;
```

### ➕ Insertar datos (INSERT)
```sql
INSERT INTO movies (id, title, year)
VALUES (1, 'Matrix', 1999);
```

### ✏️ Actualizar datos (UPDATE)
```sql
UPDATE movies
SET year = 2012
WHERE id = 3;
```

### 🗑️ Eliminar datos (DELETE)
```sql
DELETE FROM movies
WHERE id = 3;
```

---

## 🔍 Filtrado y Búsqueda

### WHERE - Filtrar resultados
```sql
SELECT * FROM movies
WHERE year = 1999;
```

### ORDER BY - Ordenar resultados
```sql
SELECT * FROM movies
ORDER BY year DESC;
```

### LIMIT - Limitar resultados
```sql
SELECT * FROM movies
LIMIT 5;
```

---

## 🔗 Relaciones entre Tablas

Las bases de datos SQL permiten **conectar tablas** usando **claves foráneas (Foreign Keys)**.

**Tabla users:**
id: 1, name: Ana
id: 2, name: Luis

**Tabla orders:**
id: 1, user_id: 1, product: Laptop
id: 2, user_id: 2, product: Phone

**Combinar tablas con JOIN:**
```sql
SELECT users.name, orders.product
FROM users
JOIN orders
ON users.id = orders.user_id;
```

---

## 🎯 Buenas Prácticas

✅ Usar **PRIMARY KEY** para identificar registros únicos
✅ Usar **WHERE** en UPDATE y DELETE para evitar cambios no deseados
✅ Usar **índices** para búsquedas frecuentes
✅ **Normalizar datos** en varias tablas
✅ Especificar columnas en SELECT (evitar SELECT *)

---

## 📌 Resumen

SQL es la base de toda gestión de datos. Las 4 operaciones CRUD (SELECT, INSERT, UPDATE, DELETE) son suficientes para el 90% de tus necesidades en bases de datos.

> 💻 **Siguiente paso:** Aprender a usar SQL con un ORM como **Prisma** para escribir menos código SQL manualmente.