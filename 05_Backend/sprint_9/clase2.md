# 🔧 Introducción a Prisma

## ¿Qué es Prisma?

**Prisma** es un **ORM (Object Relational Mapper)** que permite trabajar con bases de datos SQL usando **JavaScript o TypeScript** en lugar de escribir SQL directamente.

Prisma traduce tus llamadas de JavaScript a queries SQL automáticamente.

### ¿Para qué sirve Prisma?

- 🎯 **Menos SQL manual** - Escribir menos código SQL
- 📝 **Consultas tipadas** - Autocompletado y detección de errores
- 🔄 **Migraciones automáticas** - Gestionar cambios en la base de datos
- 🔗 **Relaciones fáciles** - Conectar tablas sin complicaciones
- ⚡ **Integración con Node.js** - Funciona perfectamente con JavaScript/TypeScript

---

## Bases de Datos Soportadas

Prisma funciona con:
- PostgreSQL
- MySQL
- SQLite
- SQL Server
- MongoDB (modo especial)

---

## 🚀 Instalación y Configuración

### 1. Instalar Prisma

```bash
npm install prisma --save-dev
npm install @prisma/client
```

### 2. Inicializar Prisma

```bash
npx prisma init
```

Esto crea:
- `prisma/schema.prisma` - Definición de modelos
- `.env` - Variables de entorno

### 3. Configurar la base de datos

En `.env`: DATABASE_URL="postgresql://user:password@localhost:5432/mydb"

En `schema.prisma`:
```prisma
datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}
```

---

## 📋 Definir Modelos (Tablas)

En Prisma, las tablas se llaman **models** y se definen en `schema.prisma`:

```prisma
model Movie {
  id    Int     @id @default(autoincrement())
  title String
  year  Int
}
```

Esto crea una tabla `movies` con:
- `id` - Identificador único, auto-incrementado
- `title` - Texto
- `year` - Número entero

---

## 🔄 Crear Migraciones

Después de modificar el schema:

```bash
npx prisma migrate dev --name init
```

Esto:
- Crea la tabla en la base de datos
- Genera el SQL automáticamente
- Actualiza la base de datos

---

## 💾 Generar Prisma Client

```bash
npx prisma generate
```

Crea el cliente para usar en Node.js

---

## 📖 Importar Prisma en Node.js

```javascript
import { PrismaClient } from "@prisma/client";
const prisma = new PrismaClient();
```

---

## 🔨 CRUD con Prisma

### ➕ Crear registro (CREATE)

```javascript
const movie = await prisma.movie.create({
  data: {
    title: "Interstellar",
    year: 2014
  }
});
```

### 📖 Obtener todos los registros (READ)

```javascript
const movies = await prisma.movie.findMany();
```

### 🔍 Obtener por ID

```javascript
const movie = await prisma.movie.findUnique({
  where: {
    id: 1
  }
});
```

### 🔎 Filtrar registros

```javascript
const movies = await prisma.movie.findMany({
  where: {
    year: 2014
  }
});
```

### ✏️ Actualizar registro (UPDATE)

```javascript
const movie = await prisma.movie.update({
  where: { id: 1 },
  data: { year: 2015 }
});
```

### 🗑️ Eliminar registro (DELETE)

```javascript
await prisma.movie.delete({
  where: { id: 1 }
});
```

---

## 🔍 Búsqueda Avanzada

### Ordenar resultados

```javascript
const movies = await prisma.movie.findMany({
  orderBy: {
    year: "desc"
  }
});
```

### Limitar resultados

```javascript
const movies = await prisma.movie.findMany({
  take: 5
});
```

### Paginación

```javascript
const movies = await prisma.movie.findMany({
  skip: 10,
  take: 5
});
```

### Operadores de filtro

```javascript
const movies = await prisma.movie.findMany({
  where: {
    year: {
      gt: 2000  // mayor que
    }
  }
});
```

**Operadores disponibles:**
- `gt` = mayor que
- `gte` = mayor o igual
- `lt` = menor que
- `lte` = menor o igual
- `contains` = contiene texto

---

## 🔗 Relaciones entre Modelos

### Definir relaciones

```prisma
model User {
  id    Int     @id @default(autoincrement())
  name  String
  posts Post[]
}

model Post {
  id     Int     @id @default(autoincrement())
  title  String
  userId Int
  user   User    @relation(fields: [userId], references: [id])
}
```

### Crear con relación

```javascript
await prisma.post.create({
  data: {
    title: "Primer post",
    user: {
      connect: { id: 1 }
    }
  }
});
```

### Incluir relaciones en consultas

```javascript
const users = await prisma.user.findMany({
  include: {
    posts: true
  }
});
```

---

## 💬 Transacciones

Ejecutar varias operaciones juntas:

```javascript
await prisma.$transaction([
  prisma.user.create({
    data: { name: "Ana" }
  }),
  prisma.post.create({
    data: { title: "Post de Ana" }
  })
]);
```

---

## 🎨 Prisma Studio (GUI)

Panel visual para gestionar la base de datos:

```bash
npx prisma studio
```

Se abre en: **http://localhost:5555**

Permite:
- Ver tablas
- Editar datos
- Crear registros

---

## 📋 Comandos Importantes

```bash
prisma init              # Iniciar prisma
prisma migrate dev       # Crear migración
prisma generate          # Generar cliente
prisma studio           # Panel visual
prisma db push          # Sincronizar schema
```

---

## ✅ Ventajas de Prisma

✅ **Consultas tipadas** - Autocompletado en el editor
✅ **Menos SQL manual** - No escribes queries
✅ **Migraciones automáticas** - Control de versiones de BD
✅ **Relaciones fáciles** - Sintaxis clara y simple
✅ **Integración con Node.js** - Perfecto para JavaScript

---

## 📊 Prisma vs SQL

| Tarea | SQL | Prisma |
| --- | --- | --- |
| Consultar | SELECT | findMany() |
| Insertar | INSERT | create() |
| Actualizar | UPDATE | update() |
| Eliminar | DELETE | delete() |

---

## 🎯 Flujo típico con Prisma

**1️⃣ Definir modelo:**
```prisma
model Movie {
  id    Int     @id @default(autoincrement())
  title String
}
```

**2️⃣ Migrar base de datos:**
```bash
npx prisma migrate dev
```

**3️⃣ Usar Prisma Client:**
```javascript
const movies = await prisma.movie.findMany();
```

---

## 📌 Resumen

Prisma simplifica el trabajo con bases de datos. En lugar de escribir SQL, escribes JavaScript tipado que Prisma convierte automáticamente.

> 💡 **Ventaja:** Escribes menos código, cometes menos errores y tu editor te ayuda con autocompletado.