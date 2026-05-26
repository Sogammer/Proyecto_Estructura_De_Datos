# Sistema Inteligente de Gestión de Entregas (SIGE)

---

## Integrantes del Grupo

| Nombre Completo | Código UIS |
| :--- | :--- |
| Hanner Ferley Sogamoso Jimenez | 2201447 |

---

##  Descripción del Problema

En el sector logístico de distribución de mercancías en la ciudad de Bucaramanga, la asignación, programación y despacho de pedidos hacia los diferentes barrios padece de ineficiencias críticas cuando se planifica de forma lineal o empírica. Los vehículos repartidores suelen recorrer rutas redundantes, incrementando drásticamente los costos de combustible, los tiempos de entrega y el desgaste de la flota vehicular.

**Objetivo:** Desarrollar un sistema de software optimizado que permita registrar barrios de la ciudad, modelar las conexiones viales reales entre ellos y calcular de forma automática la ruta transitable más corta y eficiente en recursos para la entrega de los pedidos.

---

## Etapas de Desarrollo del Proyecto

El sistema evolucionó a través de tres fases de diseño de estructuras de datos para evaluar las ganancias en eficiencia computacional:

### Etapa 2 — Árbol Binario de Búsqueda (BST) y Cola de Prioridad (Heap)
* **Implementación:** Un árbol BST encargado de organizar los barrios de acuerdo con su distancia lineal al centro de distribución principal. Adicionalmente, cada nodo del árbol (`NodoBarrio`) integraba internamente un Min-Heap (`heapq`) para gestionar los pedidos acumulados, asegurando el despacho inmediato de los paquetes con mayor prioridad de urgencia.
* **Limitación:** Aunque optimizó la jerarquía de las entregas críticas, los árboles no permiten modelar "ciclos" o rutas alternativas interconectadas (mallas viales urbanas).

### Etapa 3 — Grafos y Algoritmo de Dijkstra (Entrega Final)
* **Implementación:** Modelado de la red logística de Bucaramanga mediante un **Grafo Ponderado No Dirigido**. 
  * **Vértices (Nodos):** Representan los barrios o tiendas (Centro, Cabecera, San Alonso, Floridablanca).
  * **Aristas (Enlaces):** Representan las avenidas o calles transitables que los conectan.
  * **Pesos:** Representan la distancia real en kilómetros entre cada punto.
* **Optimización:** Integración del **Algoritmo de Dijkstra** asistido por una cola de prioridad para calcular de manera exacta el camino mínimo entre cualquier origen y destino en tiempo real.

---

## Operaciones del Grafo Final

| Operación | Descripción |
| :--- | :--- |
| `agregar_barrio` | Inserta un nuevo barrio (vértice) en el mapa logístico. |
| `agregar_ruta` | Crea una arista bidireccional entre dos barrios con un peso (distancia en km). Si un barrio no existe, lo crea automáticamente. |
| `eliminar_barrio` | Remueve un barrio del sistema y rompe de forma segura todas sus conexiones existentes. |
| `eliminar_ruta` | Quita la arista que conecta a dos barrios específicos. |
| `buscar_barrio` | Verifica la existencia de un barrio y despliega todas sus rutas vecinas y distancias. |
| `mostrar_grafo` | Renderiza la topología completa del mapa en consola para auditoría visual. |
| `ruta_mas_corta` | Ejecuta el algoritmo de Dijkstra para hallar y reconstruir el camino óptimo en km. |

---

## Comparación de Eficiencia entre Estructuras

| Operación / Criterio | Etapa 1: Lista Enlazada | Etapa 2: Árbol BST + Heap | Etapa 3: Grafo + Dijkstra |
| :--- | :--- | :--- | :--- |
| **Insertar Barrio / Nodo** | $O(1)$ / $O(n)$ | $O(\log n)$ promedio | $O(1)$ (Diccionario Hash) |
| **Buscar Ruta / Relación** | No permitido | No permitido | $O(1)$ de forma directa |
| **Priorización de Pedido** | Requiere ordenar $O(n \log n)$ | $O(1)$ en la cima del Heap | No aplica al mapa de red |
| **Cálculo de Ruta Mínima** | Imposible | Imposible | **$O((V + E) \log V)$** (Óptimo) |
| **Modelado Urbano Real** | No (Estructura lineal) | No (Estructura jerárquica) | **Sí (Estructura de Red)** |

---

## Estructura Más Eficiente para el Contexto

Basado en el análisis de ingeniería del software, **el Grafo No Dirigido con el Algoritmo de Dijkstra es la estructura definitiva y más eficiente** para este problema debido a:

1. **Fidelidad del Modelo:** Una ciudad no se comporta de forma lineal (Listas) ni de forma jerárquica corporativa (Árboles). Las calles forman una red mallada con rutas alternativas y dobles vías, lo cual solo puede ser representado de manera matemática mediante un grafo.
2. **Complejidad Temporal Eficiente:** Gracias a que el grafo se almacena mediante listas de adyacencia usando diccionarios de Python (Tablas Hash), el acceso a los vecinos de un barrio toma un tiempo constante de $O(1)$.
3. **Optimización de Recursos (Dijkstra):** El algoritmo implementado resuelve la ruta mínima con una complejidad de $O((V + E) \log V)$ al estar optimizado con un Heap Binario. Esto se traduce directamente en un ahorro de combustible, reducción de tiempos muertos y planificación automatizada escalable para miles de barrios.

---

## Cómo Ejecutar

El sistema está construido en Python 3 puro y no requiere la instalación de dependencias externas.

```bash
# Asegúrese de estar en el directorio raíz del proyecto
python etapa3_grafo/grafo_empleados.py
