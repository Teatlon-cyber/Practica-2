# 📊 Práctica 4.2-P8: Encuesta "¿Compras local o global?"

![Institución](https://img.shields.io/badge/Instituto_Tecnológico_de_Mazatlán-Desarrollo_Sustentable-blue)
![Materia](https://img.shields.io/badge/Clave-ACD--0908-green)
![Carrera](https://img.shields.io/badge/Ingeniería-Sistemas_Computacionales-orange)
![Automatización](https://img.shields.io/badge/Automatización-Make_%2B_Google_Sheets_%2B_IA-purple)

Proyecto correspondiente a la **Unidad 4: Escenario económico** de la materia **Desarrollo Sustentable**. Consiste en una aplicación web conectada a un flujo automatizado para recopilar, almacenar, auditar y analizar hábitos de consumo local frente al consumo en plataformas globales.

---

## 🎥 Video de Demostración

Haz clic en la imagen o en el enlace directo para ver la demostración del funcionamiento en YouTube:

[![Ver demostración en YouTube](https://img.youtube.com/vi/WhNS8HQq-dY/hqdefault.jpg)](https://youtube.com/shorts/WhNS8HQq-dY?feature=share)

* **Enlace directo:** [Ver Práctica 4.2 en YouTube](https://youtube.com/shorts/WhNS8HQq-dY?feature=share)

---

## ⚙️ Arquitectura y Flujo de Automatización (Make)

Las respuestas enviadas desde la página web publicada son procesadas mediante un escenario en **Make** (`Encuesta_Equipo#`) dividido en dos rutas principales a través de un **Router**:

1. **Ruta 1 — Registro de respuestas (`acción = respuesta`):**
   * Recibe los datos mediante un **Custom Webhook**.
   * Inserta una nueva fila automáticamente en **Google Sheets** (`Add a Row`).
   * Devuelve una confirmación HTTP `200` a la interfaz web (`Webhook response`).
2. **Ruta 2 — Generación de reporte con IA (`Acción = reporte`):**
   * Consulta los registros acumulados en **Google Sheets** (`Search Rows`).
   * Agrupa los datos en texto plano mediante **Tools (`Text aggregator`)**.
   * Procesa la información con un agente inteligente (**Make AI Agent**) para generar un resumen analítico y lo devuelve vía **Webhook response**.

> 💡 *Nota: Para visualizar tu diagrama aquí, sube tu captura de pantalla al repositorio con el nombre `flujo-make.jpg` y descomenta la siguiente línea:*
> `![Escenario de automatización en Make](./flujo-make.jpg)`

---

## 📈 Resultados de la Encuesta (Verificados en Google Sheets)

Los porcentajes se calcularon utilizando fórmulas `COUNTIF` sobre las **5 respuestas** registradas hasta el momento (todas correspondientes al rango de edad de **18 a 29 años**). 

> *Nota metodológica: Con una muestra inicial de 5 participantes los resultados son indicativos; la meta de la práctica es alcanzar **20 personas**, por lo que las cifras se actualizarán dinámicamente al completar la muestra.*

| Categoría / Pregunta | Opción | Respuestas | Porcentaje |
| :--- | :--- | :---: | :---: |
| **Comida** | Tienda de barrio | 2 | 40% |
| | Mercado o tianguis | 1 | 20% |
| | Supermercado | 1 | 20% |
| | En línea | 1 | 20% |
| **Ropa** | Negocio local | 2 | 40% |
| | Tienda departamental | 2 | 40% |
| | App internacional | 1 | 20% |
| | Segunda mano | 0 | 0% |
| **Apps internacionales** | Una vez al mes | 3 | 60% |
| | Varias veces al mes | 2 | 40% |
| | Nunca | 0 | 0% |
| | Cada semana | 0 | 0% |
| **Criterio de compra** | Calidad | 4 | 80% |
| | Precio | 1 | 20% |
| **Conoce el origen** | A veces | 3 | 60% |
| | No | 2 | 40% |
| | Sí | 0 | 0% |

### Comparación con el reporte de la IA
* **[Pendiente de completar]:** *Pegar aquí los porcentajes arrojados por el Make AI Agent y anotar si coinciden exactamente con los cálculos de Google Sheets.*

---

## 📝 Análisis e Informe de Resultados

### 1. ¿El consumo de su comunidad es más local o más global? ¿En qué productos se nota más?
En los alimentos el consumo se inclina hacia lo local: el **60%** compra su comida en la tienda de barrio o en el mercado o tianguis, mientras que solo el **20%** acude a supermercados y el **20%** compra en línea. En la ropa el reparto es parejo: **40%** compra en negocios locales, **40%** en tiendas departamentales y **20%** en apps internacionales. 

El consumo global se nota sobre todo en el uso de plataformas digitales: el **100%** de los encuestados ha comprado alguna vez en apps internacionales (**60%** una vez al mes y **40%** varias veces al mes; nadie respondió *"Nunca"*). En conjunto, la comunidad encuestada es más local en alimentos y mixta en ropa, pero altamente conectada a plataformas globales. *(Lectura preliminar sujeta a ampliación de muestra).*

### 2. ¿Qué efecto tiene en el PIB y en el empleo de Mazatlán que las personas compren en apps internacionales?
Cuando el producto se fabrica en el extranjero, el gasto entra en el consumo ($C$) pero se resta como importación ($M$), por lo que el valor agregado se contabiliza en el PIB del país productor. En México solo permanece una fracción menor asociada a mensajería de última milla, impuestos y aranceles. 

Para Mazatlán, esto representa menores ventas para comercios y talleres locales, traduciéndose en menos ingresos y menos empleos en comercio, confección y distribución. Además, se reduce el **efecto multiplicador** del dinero dentro de la ciudad, ya que un negocio local reinvierte en proveedores y salarios de la zona. No obstante, las apps ofrecen ventajas competitivas en costo, lo cual se refleja en el **20%** de los encuestados que prioriza el precio como criterio principal.

### 3. ¿Qué impacto ambiental tiene el transporte y el empaque de lo que se compra en línea desde otro país?
Un artículo adquirido en una app internacional recorre miles de kilómetros por barco, avión y camión, incrementando significativamente las emisiones de $CO_2$ frente a un producto de origen local. Asimismo, cada pedido individual genera residuos de un solo uso (cajas, bolsas plásticas, material de relleno y etiquetas). 

El envío individualizado de compras pequeñas es logísticamente menos eficiente que el abastecimiento consolidado hacia un mercado o tienda local, a lo que se suma el impacto de la moda rápida (*fast fashion*) con prendas de corta vida útil. Con un **40%** de la muestra comprando varias veces al mes en estas plataformas, el impacto ambiental se acumula rápidamente.

### 4. ¿Coincidieron los porcentajes de la IA con los de Sheets? ¿Qué aprendieron sobre verificar a la IA?
* **[Completar tras comparar]:** *Anotar aquí la verificación de cada porcentaje.*

Los porcentajes de Google Sheets provienen de fórmulas `COUNTIF` sobre filas reales, lo que los hace auditables y reproducibles. Una IA puede cometer errores de conteo, redondear de forma distinta o agrupar mal las categorías al procesar múltiples líneas de texto. Aprendimos que el reporte automático agiliza la redacción del análisis, pero **sus cifras siempre deben contrastarse contra la fuente de datos**. También comprobamos la importancia de la integridad de datos: las cadenas de texto en la página web y en las fórmulas deben coincidir exactamente (incluyendo acentos), de lo contrario `COUNTIF` omite registros.

### 5. ¿Qué acción concreta propondrían para impulsar el consumo local en su colonia?
Proponemos organizar un **tianguis o mercadito local mensual** en un espacio público de la colonia con productores, pescadores y talleres de Mazatlán, difundido mediante redes sociales y grupos vecinales:
* **Transparencia y calidad:** Dado que el **80%** valora la calidad y el **100%** desconoce total o parcialmente el origen de sus productos (**40%** no lo sabe y **60%** solo a veces), cada puesto exhibirá etiquetas claras con el origen y proceso de elaboración.
* **Directorio digital:** Creación de un catálogo web sencillo con la ubicación y contacto de los negocios locales de la colonia.
* **Sustentabilidad:** Campaña para incentivar el uso de bolsas reutilizables y reducir empaques.
* **Métrica de éxito:** Evaluar en una segunda ronda de encuestas si aumenta el porcentaje de compra local y el conocimiento sobre el origen de los productos.

---

## 👥 Datos del Proyecto

* **Autor / Integrante:** Julio César García
* **Equipo:** `[Número o nombre del equipo]`
* **Otros integrantes:** `[Nombres de integrantes]`
* **Profesor(a):** `[Nombre del docente]`
* **Fecha:** `[Fecha de entrega]`
