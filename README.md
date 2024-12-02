# Proyecto: Segmentación y Clasificación de Clientes Mayoristas y Minoristas

Este proyecto tiene como objetivo identificar y clasificar a los clientes de un comercio minorista en línea con sede en el Reino Unido. La empresa busca diferenciar entre clientes mayoristas y minoristas para implementar estrategias de precios personalizados. Se emplean técnicas de exploración de datos, clustering y modelado supervisado.

---

## Descripción del Dataset

El dataset contiene 541,908 registros y las siguientes columnas:

- **InvoiceNo:** Número de factura. Si inicia con 'C', indica cancelación.
- **StockCode:** Código único del producto.
- **Description:** Nombre del producto.
- **Quantity:** Cantidad de productos por transacción.
- **InvoiceDate:** Fecha y hora de la factura.
- **UnitPrice:** Precio unitario del producto en libras esterlinas.
- **CustomerID:** Identificador único del cliente.
- **Country:** País de residencia del cliente.

---

## Estructura del Proyecto

### 1. Preprocesamiento de Datos

- **Valores nulos:** Se eliminaron los registros con valores faltantes en `CustomerID` y duplicados.
- **Atípicos:** Se eliminaron valores extremos en `Quantity` y `UnitPrice` (percentil 0.5% y 99.5%).
- **Agregación de variables:** 
  - **precio_total:** Producto de `Quantity` y `UnitPrice`.
  - **consumo_total:** Suma de `precio_total` por cliente.
  - **ultimo_dia:** Días desde la última compra.
  - **set_pack:** Frecuencia de productos con "SET" o "PACK" en su descripción.
  - **frecuencia:** Número de facturas únicas por cliente.
  - **variedad_producto:** Número de productos únicos adquiridos por cliente.

---

### 2. Clusterización de Clientes

- **Estandarización:** Variables escaladas con `StandardScaler`.
- **Modelo:** K-Means con el número óptimo de clústeres determinado por las métricas del codo e índice de Silhouette.
- **Resultados:**
  - **Cluster 0 (Mayoristas):**
    - Gasto promedio alto (3686.89).
    - Alta frecuencia de compras (10.74).
    - Variedad de productos significativa (150.30).
  - **Cluster 1 (Minoristas):**
    - Gasto promedio bajo (696.07).
    - Menor frecuencia de compras (2.71).
    - Menor variedad de productos (34.83).

---

### 3. Clasificación de Clientes

#### Modelos Evaluados

1. **Regresión Logística**
   - Precisión: 100%.
   - AUC: 1.0.
   - Sobresaliente en precisión y recall.

2. **Árbol de Decisión**
   - Precisión: 97%.
   - AUC: 0.946.
   - Desempeño sólido en interpretación y precisión.

3. **Gaussian Naive Bayes**
   - Precisión: 96%.
   - AUC: 0.995.
   - Buen recall en clases minoritarias.

4. **K-Nearest Neighbors (KNN)**
   - Precisión: 98%.
   - AUC: 0.999.
   - Alto desempeño con `k=7`.

5. **Random Forest**
   - Precisión: 99%.
   - AUC: 0.999.
   - Robusto y consistente.

#### Comparación de Modelos

| Modelo                | Precisión | Recall | F1-Score | AUC   |
|-----------------------|-----------|--------|----------|-------|
| **Regresión Logística** | 100%      | 99%    | 99%      | 1.000 |
| **Árbol de Decisión**   | 97%       | 95%    | 96%      | 0.946 |
| **Gaussian Naive Bayes** | 96%       | 97%    | 96%      | 0.995 |
| **KNN**               | 98%       | 96%    | 97%      | 0.999 |
| **Random Forest**     | 99%       | 97%    | 98%      | 0.999 |

---

## Conclusiones

1. **Clusterización:**
   - El **Cluster 0** representa a los mayoristas: clientes de alto gasto, frecuencia y diversidad de productos.
   - El **Cluster 1** agrupa a los minoristas: clientes menos activos y con menor variedad de compras.

2. **Clasificación:**
   - La **Regresión Logística** demostró ser el mejor modelo por su precisión perfecta y AUC de 1.0, lo que la hace ideal para este problema.
   - **Random Forest** y **KNN** también ofrecen resultados altamente confiables.

3. **Recomendaciones Estratégicas:**
   - **Mayoristas:** Desarrollar descuentos por volumen y servicios personalizados para fidelización.
   - **Minoristas:** Implementar programas de fidelización y campañas promocionales para incrementar la frecuencia de compra.

---

## Requisitos

Librerías necesarias:
```plaintext
numpy, pandas, matplotlib, seaborn, scikit-learn, plotly, imblearn
