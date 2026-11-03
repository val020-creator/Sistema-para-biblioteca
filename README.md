# 🏛️ SGB — Sistema de Gestión Bibliotecaria

Sistema de gestión bibliotecaria en **Python**, con interfaz de consola y persistencia en archivos de texto. Permite administrar usuarios, catálogo de libros, préstamos, reservas y multas, e incluye un módulo de análisis de datos.

Está hecho para ejecutarse en un notebook (Google Colab o Jupyter) y **no requiere instalar librerías externas**: solo usa la biblioteca estándar de Python.

## ✨ Funcionalidades

| Módulo | Qué permite hacer |
|---|---|
| 👥 **Usuarios** | Registrar, consultar y actualizar usuarios (correo, teléfono, estado activo/suspendido) y listarlos |
| 📚 **Catálogo** | Registrar categorías y libros; buscar por ISBN o título; listar libros disponibles |
| 🔁 **Préstamos** | Registrar préstamos y devoluciones, ver el historial de un usuario y listar préstamos vencidos |
| 📋 **Reservas y multas** | Crear y cancelar reservas, pagar multas y consultar la deuda de un usuario |
| 📊 **Análisis** | Libros más prestados, préstamos por categoría, tasa de morosidad, duración promedio y reporte de multas |

## 📏 Reglas de negocio

**Tipos de usuario**

| Tipo | Plazo de préstamo | Libros simultáneos |
|---|---|---|
| Estudiante | 7 días | 3 |
| Docente | 15 días | 5 |
| Externo | 5 días | 2 |

- **Multas:** $1.000 COP por cada día de retraso en la devolución.
- **Para prestar**, el usuario debe existir, estar activo, no tener multas pendientes, no haber superado su cupo y no tener ya ese libro prestado.
- **Reservas:** solo se pueden crear cuando no hay ejemplares libres. Se atienden por **orden de llegada**: los ejemplares que se liberan se asignan primero a quienes reservaron antes.
- Un libro no puede registrarse con un ISBN repetido ni con una categoría que no exista.

## 🧱 Arquitectura

El código está organizado en capas, cada una en su propia sección del notebook:

```
Sección 1 — Modelo          Usuario, Categoria, Libro, Prestamo, Multa, Reserva + Enums
Sección 2 — Repositorios    Lectura y escritura en archivos .txt (ArchivoUtil, *Repository)
Sección 3 — Servicios       Reglas de negocio (Usuario, Libro, Prestamo, Reserva, Multa, Análisis)
Sección 4 — Interfaz        Menús de consola (print/input)
Sección 5 — Ejecución       Inicio del sistema con menu_principal()
```

## 💾 Persistencia

Los datos se guardan en archivos de texto, un registro por línea, con los campos separados por `|`:

```
datos/
├── usuarios.txt
├── libros.txt
├── categorias.txt
├── prestamos.txt
├── multas.txt
└── reservas.txt
```

- Las fechas usan el formato `AAAA-MM-DD`.
- Los códigos se generan automáticamente con prefijo: `PRE-` (préstamos), `MUL-` (multas) y `RES-` (reservas).

## 🚀 Cómo ejecutarlo

### Requisitos

- Python 3.8 o superior
- Un entorno de notebooks: [Google Colab](https://colab.research.google.com/) o Jupyter

### En Google Colab

1. Sube `SGB.ipynb` a Colab (o ábrelo desde GitHub).
2. Ejecuta las celdas en orden. La primera monta tu Google Drive y los datos se guardan en `MyDrive/SGB/datos/`.
3. La última celda ejecuta `menu_principal()` e inicia el sistema.

### En local (Jupyter)

```bash
jupyter notebook SGB.ipynb
```

Ejecuta todas las celdas en orden. Fuera de Colab, los archivos de datos se crean en la carpeta `SGB/datos/` junto al notebook.

## 🕹️ Uso

Al iniciar aparece el menú principal:

```
=============================================
 🏛️ SISTEMA DE GESTIÓN BIBLIOTECARIA (SGB)
=============================================
1. Gestión de Usuarios
2. Catálogo de Libros
3. Préstamos y Devoluciones
4. Reservas y Multas
5. Análisis de Datos
0. Salir del SGB
```

Un flujo típico sería: registrar una categoría → registrar un libro → registrar un usuario → hacer un préstamo → registrar la devolución.

## 📁 Estructura del repositorio

```
.
├── SGB.ipynb    # Código completo del sistema
└── README.md
```
### Autores
- Valery Montes Echaves
- Jose Gabriel Plata Ariza
