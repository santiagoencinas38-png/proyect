# #  Proyecto Integrador EC2 - Kiosko Universitario UCB

Mini-sistema de gestión de inventario y ventas desarrollado en Python, diseñado para cumplir con los requisitos de modularidad, persistencia, arreglos 1D/2D y algoritmos de búsqueda/ordenamiento de la Evaluación Continua 2 (EC2) de Programación I.

---

## 1. Estructura y Modularidad (Requisito 4)

El proyecto está dividido en módulos con responsabilidad única, asegurando un código legible y fácil de mantener, tal como exige la guía:

| Archivo | Responsabilidad Principal |
| :--- | :--- |
| **`main.py`** | Punto de entrada. Contiene el bucle del menú principal, la inicialización del sistema y el manejo de la persistencia al inicio y al cierre. |
| **`inventario.py`** | Lógica de Negocio (CRUD). Maneja la creación, alta, baja, modificación, reabastecimiento de productos, y el **registro de ventas** (que actualiza la matriz 2D). |
| **`io_archivos.py`** | Persistencia. Encargado de la lectura y escritura en formatos CSV y Binario. |
| **`busquedas_ordenamientos.py`**| Algoritmos. Contiene las implementaciones requeridas de búsqueda y ordenamiento. |
| **`reportes.py`** | Estadísticas. Genera informes de rendimiento basados en los datos del inventario y la matriz de ventas. |
| **`datos.csv`** | Archivo de datos iniciales. |

---

## 2. Ejecución e Inicialización

### Requisitos

* Python 3.x

### Instrucciones

Asegúrese de que todos los archivos (`.py` y `datos.csv`) se encuentren en el mismo directorio. Ejecute el programa desde la consola:

```bash
python main.py
## 3. Funcionalidad Clave (Requisitos 1, 2 y 3)

### A. Mantenimiento de Inventario (CRUD)

Las opciones 1 a 4 del menú implementan las operaciones fundamentales de gestión de inventario:

* **Alta (1):** Crea un nuevo producto y lo añade a la lista, validando códigos duplicados.
* **Baja (2):** Elimina un producto por su código.
* **Modificar (3):** Permite actualizar el nombre, precio, stock y stock mínimo de un producto existente.
* **Reabastecer (4):** Aumenta el stock de un producto.

### B. Arreglos y Estructuras de Datos

* **Arreglo 1D (Lista de Registros):** La lista `productos` almacena diccionarios (registros) que contienen el modelo de datos (`codigo`, `nombre`, `precio`, `stock`, `stock_minimo`, `vendidos_hoy`).
* **Arreglo 2D (Matriz de Ventas):** La matriz `ventas_semana` (7 días x 3 franjas horarias) se utiliza para registrar los montos totales de ventas por día y por franja, cumpliendo con el requisito de estructuras homogéneas 2D.

### C. Búsqueda y Ordenamiento

El proyecto implementa y aplica los algoritmos de búsqueda y ordenamiento obligatorios:

* **Búsqueda Lineal (6):** Usada para buscar productos por subcadena en el `nombre`.
* **Búsqueda Binaria (7):** Usada para buscar productos por `codigo` (requiere que la lista esté ordenada previamente por código).
* **Ordenamiento por Selección:** Utilizado para ordenar la lista por **Código** y **Nombre** (ascendente).
* **Ordenamiento por Burbuja:** Utilizado para ordenar la lista por **Precio** (ascendente) y **Stock** (descendente).

### D. Reportes (9)

Muestra estadísticas clave del rendimiento del kiosko, incluyendo:

*  **Top 3 Productos Más Vendidos** (del día).
*  **Productos Bajo Stock Mínimo**.
*  **Resumen Monetario** (Total y Ticket Promedio del día).
*  **Resumen Semanal** (Total general, totales por día y totales por franja, procesando la matriz 2D).

---

## 4. Persistencia (Requisito 3)

La persistencia de datos es manejada por el módulo `io_archivos.py`, asegurando la recuperación de la información tras reiniciar el sistema:

* **Carga Inicial desde `datos.csv`:** Se usa si no se encuentra ningún archivo binario.
* **Guardado a Binario:** El inventario (`productos`) y la matriz de ventas (`ventas_semana`) se guardan en archivos binarios (`datos.bin` y `ventas_semana.bin`) usando `pickle`, lo que garantiza una recuperación rápida y precisa de los tipos de datos.
* **Guardado a CSV (`datos.csv`):** Se mantiene el guardado al formato de texto estándar como respaldo.
* **Respaldo Selectivo (10):** Permite exportar únicamente los productos que están bajo stock mínimo a un archivo `alertas.csv`.
