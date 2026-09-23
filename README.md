# AstraX500T
Arquitectura MoE de 500 expertos y 5T activos para investigación conceptual en IA.
📘 AstraX500T — Arquitectura MoE de 500 Expertos
Modelo conceptual de 500T parámetros totales y 5T activos por inferencia
🔥 Resumen técnico
AstraX500T es una arquitectura conceptual de modelo fundacional basada en Mixture of Experts (MoE) a escala extrema.
El diseño combina:

500 expertos independientes,

1T parámetros por experto,

5 expertos activos por inferencia,

5T parámetros activos,

gating híbrido (secuencia + token),

embedding 12.288,

36 capas por experto,

paralelismo experto + tensor + pipeline,

formato BF16.

El objetivo es explorar los límites de escalabilidad, estabilidad y especialización masiva en modelos de lenguaje y razonamiento estructurado.

🧠 Motivación
Los modelos MoE actuales (Mixtral, Qwen2.5-MoE, DeepSeekMoE) demuestran que la especialización controlada permite:

mayor capacidad activa,

menor coste por inferencia,

mejor estabilidad,

mejor razonamiento estructurado.

AstraX500T lleva esta idea al extremo:
500 expertos especializados, con un gating diseñado para mantener coherencia y evitar desvaríos incluso en escalas masivas.

Este proyecto busca servir como:

arquitectura conceptual,

base para investigación,

referencia para estudiantes,

inspiración para prototipos reducidos,

punto de partida para agentes inteligentes basados en MoE.

🏗️ Arquitectura
✔ 500 expertos
Cada experto es un transformer profundo de 36 capas, con:

96 cabezas de atención

d_head = 128

FFN de 49.152

activación SwiGLU

RoPE integrado

prenorm + residuales

matrices ajustadas para alcanzar 1T parámetros exactos

✔ Gating híbrido
Sequence-level gating (top8):  
Selecciona 8 expertos candidatos para toda la secuencia.

Token-level gating (top5):  
Selecciona hasta 5 expertos activos por token dentro de los 8 candidatos.

Incluye:

balance de carga

penalización de entropía

top-m fijo

estabilidad anti-desvaríos

✔ Paralelismo HPC
Expert parallel: 500 expertos distribuidos en 50 grupos

Tensor parallel: matrices divididas entre GPUs

Pipeline parallel: 36 capas → 3 etapas de 12 capas

🧩 Diagrama conceptual (texto)
Código
Entrada → Tokenización → Embedding (12.288)
        → Gating de Secuencia (Top8)
        → Gating de Token (Top5)
        → Expertos (36 capas × 5 expertos activos)
        → Mezcla ponderada
        → Capas finales
        → Logits → Texto
⭐ AstraX5X — Versión reducida funcional
Prototipo conceptual para demostración y agentes inteligentes
AstraX5X es una versión reducida de AstraX500T diseñada para:

ser usable hoy mismo,

funcionar como agente inteligente,

demostrar el gating híbrido,

permitir experimentación sin hardware.

✔ Especificaciones
5 expertos simulados

gating híbrido conceptual

razonamiento estructurado

flujo MoE realista

implementable en cualquier API (GPT, Claude, DeepSeek)

✔ Expertos simulados
Experto Lógico — razonamiento estructurado

Experto Técnico — arquitectura de IA

Experto Matemático — análisis y cálculos

Experto Creativo — diseño conceptual

Experto Aplicado — integración práctica

✔ Flujo del agente
Analiza la tarea

Selecciona 3 expertos candidatos (sequence gating)

Activa 2 expertos principales (token gating)

Cada experto razona por separado

Mezcla las respuestas

Produce la salida final

✔ Prompt del agente (listo para usar)
Código
Eres AstraX5X, una versión reducida del modelo MoE AstraX500T.
Simulas 5 expertos internos: Lógico, Técnico, Matemático, Creativo y Aplicado.
Para cada tarea:
1. Analiza la entrada.
2. Selecciona 3 expertos candidatos (gating de secuencia).
3. Activa 2 expertos principales (gating de token).
4. Cada experto razona por separado.
5. Mezcla las respuestas de forma coherente.
Tu objetivo es producir razonamiento estructurado, estable y claro.
Evita desvaríos y mantén coherencia temática.
🚀 Roadmap del proyecto
✔ Versión 1.0 — Arquitectura completa (AstraX500T)
✓ Documento técnico
✓ Whitepaper conceptual
✓ Flujo de datos
✓ Routing híbrido
✓ Paralelismo HPC

✔ Versión 1.1 — Prototipo funcional (AstraX5X)
✓ Agente MoE reducido
✓ Prompt completo
✓ Ejemplos de uso
✓ Documentación

✔ Versión 1.2 — Comunidad
✓ Publicación en GitHub
✓ Publicación en HuggingFace
✓ Demo interactiva
✓ Invitación a colaboradores

✔ Versión 2.0 — Extensión
✓ Especialización por dominios
✓ Módulos multimodales
✓ Integración con herramientas externas
✓ Colaboración entre agentes

👥 Créditos
Autor: X
Concepto: Arquitectura MoE de escala extrema
Asistencia técnica: Copilot (Microsoft)

🔗 Enlaces
Documento técnico completo (IA MOE.docx)

Whitepaper conceptual

Prototipo AstraX5X

Demo del agente (opcional)

Contacto para colaboración
## 👥 Contacto para colaboración

Si deseas colaborar en el proyecto AstraX500T, proponer mejoras o participar en el desarrollo
de la versión reducida AstraX5X, puedes abrir un **Issue** en este repositorio o enviar un
**Pull Request** con tus aportes.

Estoy abierto a colaboraciones en:
- arquitectura de modelos MoE
- agentes inteligentes
- diseño de sistemas de razonamiento
- documentación técnica
- prototipos y demos

Tu participación es bienvenida.
Como el enlace al archivo de word no funciona y de astraxzip tampoco voy a pegar aquí todo el contenido del archivo de word.
📘 ASTRA X 500T — DOCUMENTO TÉCNICO (Versión para Word)
(Versión 1.0 — Arquitectura completa)
1. Introducción
Astra X 500T es un modelo de lenguaje de arquitectura Mixture of Experts (MoE) de escala extrema, diseñado para maximizar capacidad, estabilidad y especialización. El sistema combina 500 expertos independientes, cada uno con 1 billón (1T) de parámetros exactos, y un mecanismo de routing híbrido que garantiza que solo 5 expertos se activen por respuesta, alcanzando 5T parámetros activos.
El diseño prioriza:
•	estabilidad del gating,
•	ausencia de desvaríos,
•	paralelismo eficiente,
•	especialización masiva,
•	coherencia en inferencia,
•	compatibilidad con BF16.
2. Especificaciones globales
•	Tipo de modelo: MoE híbrido (sequence level + token level)
•	Expertos totales: 500
•	Parámetros por experto: 1T exacto
•	Parámetros totales: 500T
•	Parámetros activos por respuesta: 5T
•	Formato numérico: BF16
•	Embedding: 12.288
•	Capas por experto: 36
•	Atención: 96 cabezas, d\_head = 128
•	FFN interno: 49.152 (SwiGLU)
•	Posicional: RoPE integrado en atención
•	Routing: híbrido (sequence → token)
•	Paralelismo: expert + tensor + pipeline
3. Flujo de datos del modelo
3.1 Tokenización y embeddings
El texto de entrada se tokeniza y cada token se proyecta al espacio de dimensión 12.288.
3.2 Gating de secuencia
Se calcula un resumen de la secuencia (media de embeddings + token especial). Este resumen alimenta el sequence gating, que selecciona 8 expertos candidatos entre los 500.
3.3 Gating de token
Para cada token:
•	se evalúa su embedding, posición y contexto,
•	se eligen hasta 5 expertos activos dentro de los 8 candidatos,
•	se enruta el token a esos expertos.
3.4 Procesamiento en expertos
Cada experto aplica sus 36 capas internas al subconjunto de tokens asignado.
3.5 Mezcla de salidas
Las salidas de los expertos activos se combinan según los pesos del gating de token.
3.6 Capas finales
La representación mezclada pasa por las capas finales y se proyecta al vocabulario para generar logits y texto.
4. Arquitectura interna de cada experto
Cada experto contiene 36 capas, y cada capa incluye:
4.1 LayerNorm 1
4.2 Multi Head Self Attention (MHSA)
•	96 cabezas
•	d\_head = 128
•	Proyecciones Q, K, V
•	Proyección de salida
•	RoPE integrado
4.3 Residual (post Attention)
4.4 LayerNorm 2
4.5 Feed Forward Network (FFN)
•	Proyección 12.288 → 49.152
•	Activación SwiGLU
•	Proyección 49.152 → 12.288
4.6 Residual (post FFN)
La suma total de matrices (Attention + FFN + Norms + embeddings) se ajusta para que cada experto tenga exactamente 1T parámetros.
5. Routing híbrido
5.1 Sequence level gating
Reduce el espacio de 500 expertos a 8 candidatos coherentes por secuencia. Evita saltos caóticos y estabiliza el comportamiento global.
5.2 Token level gating
Dentro de esos 8 candidatos:
•	selecciona hasta 5 expertos activos,
•	asigna pesos de mezcla,
•	enruta tokens de forma precisa.
5.3 Estabilidad del routing
Incluye:
•	regularización de balance de carga,
•	penalización de entropía,
•	selección top m fija,
•	entrenamiento para evitar expertos erráticos.
6. Paralelismo
6.1 Expert parallel
Los 500 expertos se distribuyen en grupos de dispositivos (por ejemplo, 10 expertos por grupo → 50 grupos).
6.2 Tensor parallel
Las matrices gigantes de cada experto se dividen entre varias GPUs.
6.3 Pipeline parallel
Las 36 capas de cada experto se dividen en etapas (por ejemplo, 12 + 12 + 12).
El routing coordina la ubicación física de los expertos para evitar rutas ineficientes.
7. Parámetros activos
•	Expertos activos por respuesta: 5
•	Parámetros activos:
5 expertos×1T=5T
Esto garantiza potencia extrema sin activar el modelo completo.
8. Conclusión
Astra X 500T es un diseño de MoE de frontera, con:
•	500 expertos de 1T,
•	5T activos,
•	routing híbrido estable,
•	paralelismo masivo,
•	bloques internos modernos,
•	coherencia y estabilidad en inferencia.
Este documento define la arquitectura completa y lista para implementación teórica.


📘 ASTRA X 500T — DOCUMENTO TÉCNICO EXTENDIDO
1. Visión general del modelo
Astra X 500T es un modelo de lenguaje de arquitectura Mixture of Experts (MoE) de escala extrema, diseñado para:
•	maximizar capacidad de razonamiento estructurado,
•	permitir especialización masiva en dominios distintos,
•	mantener estabilidad en inferencia,
•	limitar el coste activo a un subconjunto pequeño de parámetros.
El modelo se compone de:
•	500 expertos,
•	cada uno con 1T parámetros exactos,
•	con un máximo de 5 expertos activos por respuesta,
•	lo que da 5T parámetros activos en cada inferencia.
El diseño está pensado para ser teóricamente implementable en hardware de supercomputación, con paralelismo híbrido (expert, tensor, pipeline) y formato numérico BF16.
2. Especificaciones globales
•	Tipo de modelo: MoE híbrido (gating de secuencia + gating de token).
•	Número de expertos: 500.
•	Parámetros por experto: 1012 (1T) exactos.
•	Parámetros totales: 500×1012=5×1014 (500T).
•	Parámetros activos por respuesta: 5T.
•	Formato numérico: BF16.
•	Dimensión de embedding: 12.288.
•	Capas por experto: 36.
•	Atención por capa de experto:
o	96 cabezas.
o	dimensión por cabeza: 128.
•	FFN por capa de experto:
o	dimensión interna: 49.152.
o	activación: tipo SwiGLU.
•	Posicional: RoPE (rotary embeddings) integrado en la atención.
•	Routing: híbrido, con:
o	gating de secuencia (sequence level),
o	gating de token (token level).
•	Paralelismo: combinación de:
o	expert parallel,
o	tensor parallel,
o	pipeline parallel.
3. Flujo de datos detallado
3.1 Entrada y tokenización
1.	El texto de entrada se tokeniza mediante un tokenizer específico (por ejemplo, BPE o unigram).
2.	Cada token se convierte en un índice de vocabulario.
3.	Ese índice se proyecta a un vector de dimensión 12.288 mediante una matriz de embeddings.
3.2 Resumen de secuencia
Antes de activar expertos, el modelo construye un resumen de la secuencia, que puede incluir:
•	media de los embeddings de todos los tokens,
•	un token especial de inicio (tipo CLS),
•	información de longitud de la secuencia.
Este resumen se usa como entrada al gating de secuencia.
3.3 Gating de secuencia (sequence level)
El gating de secuencia es un módulo que:
•	recibe el resumen de la secuencia,
•	aplica una o varias capas densas y/o atencionales,
•	produce una distribución sobre los 500 expertos.
A partir de esa distribución:
•	se seleccionan 8 expertos candidatos (top 8),
•	se guardan sus índices y pesos asociados.
Estos 8 expertos forman el subconjunto estable dentro del cual trabajará el gating de token.
3.4 Gating de token (token level)
Para cada token (o para bloques de tokens):
1.	Se toma su embedding actual (ya transformado por las capas previas).
2.	Se combina con información de posición y contexto local.
3.	Se pasa por el gating de token, que:
o	recibe también la lista de 8 expertos candidatos,
o	calcula una distribución sobre esos 8,
o	selecciona hasta 5 expertos activos (top m, con m ≤ 5).
El resultado es:
•	una lista de expertos activos para ese token/bloque,
•	pesos de mezcla para cada experto.
3.5 Enrutamiento a expertos
Los tokens se agrupan según los expertos activos:
•	cada experto recibe los tokens que le han sido asignados,
•	procesa esos tokens con sus 36 capas internas,
•	produce salidas en el mismo espacio de dimensión 12.288.
3.6 Mezcla de salidas
Para cada token:
•	se recogen las salidas de los expertos activos,
•	se combinan mediante una mezcla ponderada por los pesos del gating de token,
•	se obtiene una representación final única por token.
3.7 Capas finales y salida
La representación final por token:
•	pasa por una o varias capas densas finales,
•	se proyecta al espacio de vocabulario mediante una matriz de salida,
•	se obtienen logits,
•	se aplica softmax y se genera el siguiente token.
4. Arquitectura interna de cada experto
Cada experto es, en esencia, un transformer profundo de 36 capas, con embedding 12.288.
4.1 Estructura de una capa de experto
Cada capa incluye:
1.	LayerNorm 1
2.	Multi Head Self Attention (MHSA)
3.	Residual (entrada + salida de atención)
4.	LayerNorm 2
5.	Feed Forward Network (FFN)
6.	Residual (entrada + salida de FFN)
4.2 Multi Head Self Attention
•	Número de cabezas: 96.
•	Dimensión por cabeza: 128.
•	Dimensión total de atención: 96×128=12.288, igual al embedding.
La atención incluye:
•	proyección de entrada a Q, K, V,
•	cálculo de atención escalada,
•	aplicación de RoPE para codificar posición,
•	combinación de cabezas,
•	proyección de salida de vuelta a 12.288.
4.3 Feed Forward Network (FFN)
El FFN tiene:
•	proyección de 12.288 → 49.152,
•	activación tipo SwiGLU (o similar),
•	proyección de 49.152 → 12.288.
Este tamaño interno (≈4× embedding) es típico de modelos grandes y da alta capacidad de transformación.
4.4 Parámetros por experto
La suma de:
•	matrices de atención (Q, K, V, salida),
•	matrices de FFN (dos proyecciones por capa),
•	parámetros de LayerNorm,
•	embeddings específicos del experto (si los hubiera),
se ajusta para que el total por experto sea exactamente 1T parámetros. Esto se consigue afinando:
•	número de capas (36),
•	tamaños internos (49.152),
•	posibles matrices adicionales (por ejemplo, proyecciones auxiliares).
5. Routing híbrido y estabilidad
5.1 Objetivo del routing
El routing híbrido busca:
•	aprovechar la especialización de 500 expertos,
•	limitar el número de expertos activos a 5 por respuesta,
•	evitar comportamientos erráticos,
•	mantener coherencia global.
5.2 Sequence level gating
El gating de secuencia:
•	actúa como “filtro global”,
•	selecciona un subconjunto pequeño (8 expertos) que tiene sentido para la entrada completa,
•	reduce el espacio de decisión del gating de token.
Esto aporta:
•	estabilidad,
•	coherencia temática,
•	reducción de ruido.
5.3 Token level gating
El gating de token:
•	decide, dentro de esos 8 candidatos, qué expertos usar para cada token/bloque,
•	selecciona hasta 5 expertos activos,
•	asigna pesos de mezcla.
Esto aporta:
•	flexibilidad local,
•	capacidad de adaptar la respuesta token a token,
•	pero siempre dentro de un marco global estable.
5.4 Mecanismos de estabilidad
Para evitar desvaríos:
•	Balance de carga: se penaliza que el gating use siempre los mismos expertos.
•	Entropía controlada: se evita que la distribución sea demasiado plana o demasiado extrema.
•	Top m fijo: se limita el número de expertos activos (máximo 5).
•	Entrenamiento del gating: se ajusta para que evite expertos que produzcan salidas incoherentes.
6. Paralelismo y despliegue teórico
6.1 Expert parallel
Los 500 expertos se reparten en grupos de dispositivos:
•	por ejemplo, 10 expertos por grupo → 50 grupos.
•	cada grupo puede vivir en un conjunto de nodos de GPU.
El routing se coordina para enviar tokens a los grupos que contienen los expertos activos.
6.2 Tensor parallel
Dentro de cada experto:
•	las matrices de atención y FFN se dividen entre varias GPUs,
•	cada GPU procesa una parte de la matriz,
•	se combinan los resultados.
Esto permite manejar matrices gigantes sin que una sola GPU tenga que contenerlas completas.
6.3 Pipeline parallel
Las 36 capas de cada experto se dividen en etapas:
•	por ejemplo, 12 capas en la etapa 1,
•	12 capas en la etapa 2,
•	12 capas en la etapa 3.
Mientras una etapa procesa un batch, otra etapa procesa el siguiente, optimizando el uso de hardware.
7. Parámetros activos y coste
7.1 Expertos activos
Por diseño:
•	máximo 5 expertos activos por respuesta,
•	cada uno con 1T parámetros.
7.2 Cálculo de parámetros activos
5 expertos×1T=5T
Esto significa que, aunque el modelo tenga 500T parámetros totales, solo 5T están activos en cada inferencia.
8. Consideraciones de capacidad y “inteligencia”
Astra X 500T:
•	no es inteligente en sentido humano,
•	no tiene consciencia ni intención,
•	pero tiene una capacidad estadística enorme.
Con 5T activos, puede:
•	manejar tareas de lenguaje complejas,
•	realizar razonamiento estructurado profundo,
•	analizar grandes volúmenes de información,
•	especializarse en múltiples dominios mediante sus expertos.
La arquitectura está pensada para ser:
•	potente,
•	estable,
•	coherente,
•	y teóricamente superior en capacidad a modelos actuales de menor escala.
9. Resumen final
Astra X 500T es:
•	un MoE de 500 expertos de 1T cada uno,
•	con 5T activos por respuesta,
•	embedding 12.288,
•	36 capas por experto,
•	atención moderna,
•	FFN ancho,
•	routing híbrido estable,
•	paralelismo masivo.
El diseño busca combinar:
•	máxima capacidad,
•	especialización,
•	estabilidad,
•	y eficiencia relativa en coste activo.








📘 ASTRA X 500T — WHITEPAPER TÉCNICO (Nivel laboratorio / HPC / MoE avanzado)
Versión 0.9 — Documento interno de arquitectura (Diseño conceptual de un modelo fundacional MoE de 500T parámetros totales y 5T activos)
1. Introducción
Astra X 500T es un modelo fundacional de arquitectura Mixture of Experts (MoE) diseñado para explorar los límites de escalabilidad en modelos de lenguaje y razonamiento estructurado. El sistema combina:
•	500 expertos independientes,
•	1T parámetros por experto,
•	5T parámetros activos por inferencia,
•	routing híbrido secuencia + token,
•	embedding de 12.288,
•	36 capas por experto,
•	paralelismo experto + tensor + pipeline,
•	formato BF16,
•	estabilidad de gating mediante regularización de entropía y balance de carga.
El objetivo del diseño es maximizar:
•	capacidad de razonamiento,
•	especialización masiva,
•	estabilidad en inferencia,
•	escalabilidad en hardware HPC,
•	eficiencia relativa en coste activo.
Este documento describe la arquitectura completa, los módulos internos, el routing, el paralelismo, la distribución de parámetros, los requisitos de hardware y las rutas de entrenamiento.
2. Arquitectura global
2.1 Estructura general
Astra X 500T está compuesto por:
•	Embedding inicial: 12.288 dimensiones
•	Gating de secuencia: selección top 8
•	Gating de token: selección top 5
•	500 expertos: cada uno un transformer profundo de 36 capas
•	Mezcla ponderada de salidas
•	Capas finales de proyección al vocabulario
El flujo de datos es:
Código
Texto → Tokenización → Embedding → Gating de Secuencia → Gating de Token → Expertos → Mezcla → Proyección → Logits
3. Embedding y tokenización
3.1 Tokenización
Se utiliza un tokenizer tipo BPE o Unigram con vocabulario de 200k–300k tokens.
3.2 Embedding
Cada token se proyecta a un vector de dimensión 12.288 mediante una matriz de embedding de:
200,000×12,288≈2.45×109 paraˊmetros
El embedding se comparte entre todos los expertos.
4. Gating híbrido
4.1 Gating de secuencia (Sequence Level)
El gating de secuencia recibe:
•	media de embeddings,
•	token especial CLS,
•	información de longitud,
•	estadísticos globales.
Produce una distribución sobre los 500 expertos y selecciona top 8.
Fórmula conceptual:
gs=softmax(Ws⋅hseq)
candidatos=TopK(gs,8)
4.2 Gating de token (Token Level)
Para cada token:
gt=softmax(Wt⋅htoken)
Pero restringido a los 8 candidatos del gating de secuencia.
Se seleccionan top 5 expertos activos.
4.3 Estabilidad del gating
Se aplican:
•	regularización de entropía:
Lentropy=−λ∑gtlog⁡gt
•	balance de carga: penalización para evitar expertos dominantes.
•	top m fijo: m = 5.
5. Arquitectura interna de cada experto
Cada experto es un transformer profundo de 36 capas, con:
•	MHSA de 96 cabezas
•	d\_head = 128
•	FFN de 49.152
•	RoPE
•	LayerNorm pre norm
•	Residuales
5.1 Atención
Dimensión total:
96×128=12,288
Matrices:
•	Q: 12,288×12,288
•	K: 12,288×12,288
•	V: 12,288×12,288
•	O: 12,288×12,288
Cada capa de atención tiene:
4×(12,2882)≈603 millones de paraˊmetros
5.2 FFN
Dos proyecciones:
12,288→49,152
49,152→12,288
Total por capa FFN:
12,288×49,152+49,152×12,288≈1.2B paraˊmetros
5.3 Parámetros por experto
Por capa:
•	MHSA: ~603M
•	FFN: ~1.2B
•	Norms + biases: ~10M
Total por capa ≈ 1.8B
Por 36 capas:
36×1.8B=64.8B
Se ajustan matrices auxiliares para llegar a 1T exacto por experto.
6. Paralelismo HPC
6.1 Expert parallel
500 expertos distribuidos en:
•	50 grupos
•	10 expertos por grupo
•	cada grupo en un nodo HPC
6.2 Tensor parallel
Cada matriz se divide entre 4–16 GPUs.
6.3 Pipeline parallel
36 capas → 3 etapas de 12 capas.
7. Coste activo
Solo se activan 5 expertos:
5×1T=5T
8. Entrenamiento
8.1 Datos
Se requieren:
•	20–40T tokens de texto
•	5–10T tokens de código
•	10–20T tokens de razonamiento
•	opcional: datos multimodales
8.2 Optimización
•	AdamW
•	LR warmup
•	decay coseno
•	gradiente acumulado
•	ZeRO 3
•	sharding de expertos
9. Comparación con modelos actuales
Astra X 500T supera en capacidad activa a:
•	GPT 4 (≈1.8T estimado)
•	DeepSeek V3 (671B activos)
•	Mixtral 8x22B (44B activos)
•	Qwen2.5 MoE (≈60B activos)
10. Extensión multimodal (opcional)
Añadir:
•	encoder ViT G
•	encoder Whisper Large
•	encoder de vídeo temporal
•	alineación multimodal
•	expertos especializados por modalidad
11. Conclusión
Astra X 500T es un diseño conceptual de un modelo fundacional MoE de escala extrema, con:
•	500 expertos
•	1T por experto
•	5T activos
•	routing híbrido
•	paralelismo HPC
•	arquitectura estable
•	escalabilidad teórica
Este documento define la arquitectura completa para implementación en entornos HPC.

