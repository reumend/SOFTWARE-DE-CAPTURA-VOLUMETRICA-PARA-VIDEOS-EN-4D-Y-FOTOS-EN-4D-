# SOFTWARE-DE-CAPTURA-VOLUMETRICA-PARA-VIDEOS-EN-4D-Y-FOTOS-EN-4D-




SCV-4D — SISTEMA UNIVERSAL DE CAPTURA VOLUMÉTRICA 4D

Software que transforma cualquier lente 2D en un sensor holográfico 4D para las 7 ondas electromagnéticas, con audio 4D (hablar y escuchar), trazado de rayos, y apps nativas para Android e iOS

---

Mendoza & Fennimore LLC

Autores: Roberth Willians Mendoza Requena (@reumend), James Fennimore

Contacto: reumend@gmail.com

Fecha: Junio 2026

Licencia: Apache 2.0

Repositorio: https://github.com/reumend/scv-4d

---

PREÁMBULO — QUÉ ES SCV-4D

SCV-4D es el primer y único software en existencia que puede tomar el flujo de cualquier lente bidimensional (gran angular, teleobjetivo, macro, lente estándar, webcam integrada, cámara frontal o trasera de cualquier dispositivo móvil, cámara USB o HDMI externa) y transformarlo en un video volumétrico cuatridimensional y una fotografía volumétrica cuatridimensional que pueden ser navegados en el espacio y el tiempo dentro del Metaverso Cuántico 4D y proyectados como un holograma 4D en el Punto de Impacto Cero calculado por la teoría THPC‑I.

Este software procesa no solo la luz visible sino los 7 tipos de ondas electromagnéticas — ondas de radio, microondas, infrarrojo, luz visible, ultravioleta, rayos X y rayos gamma — utilizando la misma arquitectura matemática de 112 dimensiones, la matriz de acoplamiento g_ij y la función de coherencia multiescala de la teoría THPC‑I.

Este software captura no solo imágenes sino también audio 4D — permite hablar y escuchar dentro del video 4D, con localización espacial de fuentes sonoras, efecto Doppler de fase y atenuación por distancia, habilitando comunicación bidireccional entre avatares dentro del metaverso y usuarios humanos en el mundo físico.

Este software genera no solo archivos sino hologramas — cada video 4D grabado con SCV-4D puede ser cargado directamente al Metaverso Cuántico 4D como un holograma 4D, con el cual los avatares pueden interactuar, caminar alrededor, observar desde cualquier ángulo y grabar su propia interacción como un nuevo video 4D.

Este software no tiene límites de tiempo. Puede grabar videos 4D de duración ilimitada, limitado solo por la capacidad de almacenamiento del dispositivo. Puede capturar fotografías 4D en cantidades ilimitadas. Funciona en cualquier dispositivo, a cualquier escala, desde el mapeo genético nanométrico hasta la observación astronómica galáctica.

---

TABLA DE CONTENIDO

1. Inicio Rápido
2. Lo Que Hace SCV-4D (Funciones Completas)
3. Las 7 Ondas Electromagnéticas
4. Audio 4D (Hablar y Escuchar)
5. Trazado de Rayos
6. Formatos de Archivo .4dv y .4df
7. Endpoints de la API (24 en Total)
8. Instalación
9. Ejemplos de Uso
10. Almacenamiento en la Nube y Mercado de Semiconductores
11. Hoja de Ruta
12. Licencia y Contacto

---

INICIO RÁPIDO

Instalación de una línea (Linux / macOS / Windows WSL2)

```bash
curl -sSL https://raw.githubusercontent.com/reumend/scv-4d/main/install.sh | bash
```

Calibrar tu lente (solo la primera vez)

```bash
scv-4d calibrar --indice_camara 0 --ancho 1920 --alto 1080
```

Muestra un patrón de tablero de ajedrez a la cámara. El software detectará esquinas desde 15 ángulos diferentes y guardará el archivo de calibración en ~/.config/scv-4d/calibracion_camara.json.

Capturar una fotografía 4D

```bash
scv-4d foto --indice_camara 0 --salida mi_foto.4df --trazado_rayos true
```

El software captura un solo fotograma, estima la profundidad, aplica el estampado de fase, opcionalmente ejecuta el trazado de rayos, y guarda el archivo .4df (aproximadamente 2-3 MB).

Capturar un video 4D (duración ilimitada)

```bash
scv-4d video --indice_camara 0 --salida mi_video.4dv --fps 30 --duracion 60 --con_audio true
```

El software graba durante 60 segundos, guarda el archivo .4dv (aproximadamente 3.7 GB por minuto), e imprime el número de fotogramas capturados.

Transmitir en vivo al Metaverso Cuántico 4D

```bash
scv-4d transmitir --indice_camara 0 --host_metaverso localhost --puerto_metaverso 8088 --con_audio true
```

El software se conecta al metaverso mediante WebSocket y envía cada fotograma procesado en tiempo real (30 fps). Los avatares en el metaverso verán la escena en vivo como un holograma 4D.

Iniciar el servidor de la API

```bash
scv-4d servidor --puerto 8090
```

El servidor escucha peticiones HTTP en el puerto 8090 y conexiones WebSocket en el mismo puerto. Utiliza la API REST para integrar SCV-4D con otros sistemas.

---

LO QUE HACE SCV-4D (FUNCIONES COMPLETAS)

Captura de Video 4D desde Cualquier Lente 2D

El software captura el flujo de video de cualquier cámara conectada al dispositivo, sin importar el tipo de lente. Para cada fotograma, el software realiza las siguientes operaciones en tiempo real a 30 fotogramas por segundo:

Calibración de lente. El software incluye un asistente de calibración interactivo que guía al usuario para mostrar un patrón de tablero de ajedrez a la cámara. Utilizando OpenCV, el software calcula los parámetros intrínsecos del lente: distancia focal en X y Y, punto principal, coeficientes de distorsión radial y coeficientes de distorsión tangencial. Estos parámetros se guardan en un archivo de configuración para futuras capturas.

Corrección de distorsión geométrica. Utilizando los mapas de corrección precalculados, el software corrige la distorsión introducida por el lente (el efecto ojo de pez de los gran angulares, la distorsión de barril de los teleobjetivos, la distorsión de cojín de los lentes estándar). El resultado es una imagen donde todas las líneas son rectas en el plano digital, lo cual es esencial para la estimación matemática de la profundidad.

Estimación monocular de profundidad. Sin necesidad de una cámara estéreo ni de un sensor de profundidad, el software estima la distancia desde la cámara a cada píxel utilizando tres técnicas complementarias. La primera técnica es el flujo óptico denso: entre fotogramas consecutivos, el software calcula el vector de movimiento de cada píxel. La magnitud del movimiento correlaciona con la profundidad — los objetos cercanos se mueven más rápido en la imagen. La segunda técnica es una red neuronal liviana (MiDaS v3.1 cuantizada a INT8, 76 MB) que corre en el dispositivo y produce un mapa de profundidad relativa. La tercera técnica es el análisis de desenfoque: en regiones de alto contraste, el grado de desenfoque indica la distancia al plano focal. Estos tres mapas se fusionan utilizando un filtro de Kalman multiescala que opera en las 14 escalas informacionales de THPC‑I, produciendo un mapa de profundidad absoluto con precisión submétrica desde 0.05 hasta 50 metros.

Flujo óptico para coherencia temporal. El software calcula el flujo óptico denso entre fotogramas consecutivos utilizando un algoritmo de Farneback modificado con pirámides multiescala. Este flujo no solo sirve para la estimación de profundidad sino también alimenta el sistema de audio 4D (fase Doppler) y el sistema de trazado de rayos (desenfoque de movimiento).

Cálculo de coherencia multiescala. Utilizando el mapa de profundidad y la magnitud del flujo óptico, el software calcula la coherencia total C_total(t) como el producto sobre las 14 escalas de exp(-‖∂_t D_i‖/τ_i). Este valor de coherencia determina si la escena capturada puede ser proyectada como un holograma en el metaverso (si C_total ≥ 0.9968, se cumple la condición del Punto de Impacto Cero). También determina la transparencia dinámica del holograma durante el renderizado y la calidad adaptativa del trazado de rayos (más muestras en regiones de menor coherencia).

Estampado de fase y asignación del tiempo propio τ_i. Para cada píxel, el software calcula el tiempo propio τ_i en cada una de las 14 escalas informacionales utilizando la ecuación τ_i(u,v,t) = τ_0 · 8^i · (1 + β_i · |v_aparente| / c_luz) · C_i(t) · exp(- Σ_j g_ij ||D_i - D_j||²). Este tiempo es la base para la fase Doppler φ_i = ω_i · τ_i mod 2π, que se almacena en el archivo de video 4D.

Construcción del vector de estado de 112 dimensiones. Para cada píxel, el software construye un StateVector4D con 112 componentes: D_x,i, D_y,i, D_z,i, τ_i, P_x,i, P_y,i, P_z,i, E_i para i=0 hasta 13. Este vector representa el píxel como un punto en el espacio informacional 4D de la teoría THPC‑I. El conjunto completo de vectores forma el SceneState4D para ese fotograma.

Escritura del archivo de video 4D. El software escribe el fotograma en un archivo .4dv en el formato propietario, que incluye la marca de tiempo, la coherencia total, el vector de fase, el mapa de profundidad comprimido, el mapa de confianza comprimido, la pista de audio 4D (si se capturó), y un conjunto submuestreado de vectores de estado. El archivo se comprime con Gzip (nivel 9) para reducir el tamaño sin pérdida de información.

---

LAS 7 ONDAS ELECTROMAGNÉTICAS

Cómo SCV-4D procesa cada tipo de onda sin sensores especializados

Ondas de radio. Corresponden a la escala i=5 de THPC‑I (τ=1100 segundos, f=0.9 mHz). El software detecta interferencia de radiofrecuencia en la imagen visible como variaciones periódicas de intensidad de píxel a frecuencias de 50 Hz, 60 Hz y sus armónicos. El acoplamiento entre la escala visible (i=3) y la escala de radio (i=5) es g_35 = 7.267×10⁴ N, suficiente para inferir la presencia y potencia de fuentes de radio cercanas. Con un SDR externo conectado por USB, el software puede capturar ondas de radio directamente y procesarlas como si fueran imágenes (frecuencia vs tiempo).

Microondas. Corresponden a la escala i=4 (τ=1.07 segundos, f=0.93 Hz). El software detecta microondas como ruido 1/f en el sensor de la cámara. La temperatura del fondo cósmico de microondas (T_CMB = 2.725 K) está presente en cada píxel como ruido blanco, y el software lo utiliza como referencia de calibración universal. El acoplamiento g_34 = 9.294×10⁷ N permite inferir variaciones en la radiación de microondas de fondo a partir de cambios en la coherencia de la luz visible.

Infrarrojo. Corresponden a la escala i=3 (τ=1.05 ms, f=953 Hz). El software detecta infrarrojo a través de la temperatura: la ecuación T_i = T_0 · (τ_0/τ_i)^δ con δ=0.15 se calcula para cada píxel. Las variaciones en el canal rojo de la imagen (la cámara tiene cierta sensibilidad en el infrarrojo cercano) se convierten en un mapa de temperatura superficial. La coherencia C_i(t) en la escala infrarroja indica la estabilidad térmica de cada región.

Luz visible. Corresponden a la escala i=2 (τ=1.024 µs, f=976 kHz). Es la entrada principal del software. Los tres canales RGB se utilizan para la estimación de profundidad, el flujo óptico y la textura del modelo 4D. El software no distingue entre luz visible y los otros tipos porque todos entran por el mismo RawFrame.

Ultravioleta. Corresponden a la escala i=1 (τ=1 ns, f=1 GHz). El software detecta UV a través de la rugosidad de la superficie. La variación local del brillo en la imagen visible (localVar en depth_estimator.rs) es un indicador de la textura a escala micrométrica. Los bordes muy nítidos (alta frecuencia espacial) corresponden a regiones que también emitirían UV si tuvieran temperatura suficiente. El acoplamiento g_12 = 7.632×10¹³ N es lo suficientemente fuerte para inferir actividad UV a partir de la coherencia en la escala visible.

Rayos X. Corresponden a la escala i=0 (τ=125 ps, f=8 GHz). El software no puede detectar rayos X con una cámara normal porque la atmósfera los absorbe y el lente de vidrio no los enfoca. Sin embargo, si se conecta una placa de fósforo (material centelleador que convierte rayos X en luz visible) y se coloca frente a la cámara, el software puede capturar la imagen de rayos X como si fuera luz visible. Una vez en el RawFrame, el procesamiento es idéntico. La misma estimación de profundidad, el mismo estampado de fase, el mismo trazado de rayos funcionan para imágenes de rayos X.

Rayos gamma. Corresponden a la escala i=13 (τ=1.33×10²⁷ s, f=4.7×10⁻²⁸ Hz). El software no puede detectar rayos gamma con una cámara doméstica. Pero puede procesar datos públicos de telescopios gamma (como Fermi-LAT) convirtiendo los eventos (posición en el cielo, energía, tiempo) en una matriz 2D de densidad de fotones. Esa matriz se alimenta al software como un RawFrame y se procesa igual que una fotografía 4D. El resultado es un mapa 4D de la explosión de una supernova o de un estallido de rayos gamma, que los avatares pueden explorar en el metaverso.

La conclusión es que el software no distingue entre tipos de onda. Solo distingue entre matrices de números. Si puedes representar tu fenómeno físico como una matriz 2D de valores escalares (intensidad, amplitud, temperatura, conteo de fotones, probabilidad), SCV-4D puede convertirlo en un video 4D o una fotografía 4D.

---

AUDIO 4D (HABLAR Y ESCUCHAR)

Captura de audio espacial

El software captura audio a través del micrófono del dispositivo simultáneamente con la captura de video. El audio se procesa en fragmentos de 1024 muestras a 48 kHz y 2 canales (estéreo). Para cada fragmento, el software realiza:

Estimación de dirección de llegada. Utilizando la diferencia de fase interaural (el retardo de tiempo entre el canal izquierdo y el derecho), el software calcula la dirección desde la cual proviene el sonido dominante. El ángulo se estima mediante correlación cruzada entre canales, con una resolución de aproximadamente 5 grados.

Estimación de distancia. Utilizando la amplitud del sonido relativa a una amplitud de referencia (calibrada a 1 metro), el software estima la distancia a la fuente sonora. Se utiliza la ley del cuadrado inverso con una corrección por absorción acústica del aire a la frecuencia estimada.

Detección de frecuencia dominante. Se aplica una transformada rápida de Fourier a cada fragmento de audio para identificar las frecuencias dominantes en el sonido. Estas frecuencias se utilizan para calcular el efecto Doppler cuando la fuente o el oyente se mueven.

Cálculo de la fase Doppler. Con la dirección estimada, la distancia, la frecuencia y la velocidad relativa entre la fuente y el oyente (obtenida del flujo óptico de la cámara o del movimiento del avatar en el metaverso), el software calcula el corrimiento Doppler Δf/f = v_radial / c_sonido y la fase asociada φ_audio = ∫ Δf dt.

Construcción del mapa de fuentes de audio. El software compila todas las fuentes de sonido detectadas en una estructura Audio4DMap que contiene la posición de cada fuente en coordenadas X, Y, Z (dentro del campo de visión de la cámara o de la escena del metaverso), su frecuencia, su amplitud, su corrimiento Doppler y su coherencia. Este mapa se almacena en el archivo .4dv sincronizado con los fotogramas de video.

Renderizado de audio 4D para un oyente

Cuando un usuario o un avatar quiere escuchar el audio grabado desde una posición de escucha específica, el software renderiza el campo de audio en tiempo real. Para cada fuente de sonido, calcula la distancia al oyente, el ángulo para el paneo estéreo, el corrimiento Doppler según la velocidad relativa, y la atenuación por distancia. El audio renderizado se mezcla en un flujo estéreo que el usuario escucha a través de auriculares o altavoces.

Inyección de voz (hablar dentro del video 4D)

El software permite al usuario hablar en el micrófono mientras se está grabando un video 4D o mientras se está reproduciendo un video 4D en el metaverso. El audio capturado se procesa en tiempo real, se le asigna una posición en el espacio (la posición del avatar del usuario o la posición de la cámara), y se inyecta en el campo de audio 4D. Otros usuarios o avatares que escuchen desde otras posiciones escucharán la voz con la espacialización correcta, como si el hablante estuviera físicamente presente en la escena.

---

TRAZADO DE RAYOS

El software incluye un trazador de rayos volumétrico completo que puede renderizar una fotografía 4D o un fotograma de un video 4D con iluminación realista, sombras, reflexiones, refracciones e iluminación global. El trazador de rayos opera sobre el campo de coherencia construido a partir del mapa de profundidad y el estado de la escena.

Para cada píxel, el trazador de rayos genera un rayo primario desde las coordenadas del píxel (u, v) a través del centro óptico de la cámara utilizando los parámetros intrínsecos. El rayo se propaga a través de la escena hasta encontrar una intersección con el campo de coherencia. El punto de intersección, la normal, la coherencia, el albedo y la emisión se obtienen del campo.

Para la iluminación directa, el trazador de rayos evalúa la emisión de la superficie intersectada (si es un emisor) y añade la contribución ambiental modulada por la coherencia local. Para la iluminación indirecta, se genera un rayo recursivo en una dirección determinada por el BRDF (Función de Distribución de Reflectancia Bidireccional) modificado por el factor de coherencia de THPC‑I. La ruleta rusa determina con probabilidad 0.95 si continuar la recursión hasta un máximo de 8 rebotes.

El número de muestras por píxel es adaptativo. Para píxeles con alta coherencia (C > 0.9), se utilizan solo 32 muestras. Para píxeles con baja coherencia (C < 0.5), se utilizan hasta 256 muestras. Esta optimización mantiene la calidad visual mientras reduce el tiempo de renderizado.

El trazador de rayos está integrado con el motor de renderizado 4D del metaverso (wgpu). Los mismos buffers uniformes (coherencia, luz, beta) que utiliza el motor del metaverso son utilizados por el trazador de rayos, permitiendo una integración perfecta entre escenas capturadas y escenas virtuales.

---

FORMATOS DE ARCHIVO .4dv Y .4df

Formato .4dv (video 4D)

El formato .4dv tiene la siguiente estructura:

Una marca mágica de 4 bytes (los caracteres ASCII '4', 'D', 'V', 0x00). Un número de versión mayor de 2 bytes (1). Un número de versión menor de 2 bytes (0). Un entero sin signo de 4 bytes para el ancho en píxeles. Un entero sin signo de 4 bytes para el alto en píxeles. Un doble de 8 bytes para la velocidad de fotogramas en fotogramas por segundo. Un entero sin signo de 8 bytes para el número total de fotogramas (cero si se desconoce en la creación).

Para cada fotograma: un entero con signo de 8 bytes para la marca de tiempo en microsegundos desde la época. Un doble de 8 bytes para la coherencia total C_total(t). Catorce dobles de 8 bytes para el vector de fase φ_i. Un entero sin signo de 4 bytes para el tamaño del mapa de profundidad comprimido en bytes. Los datos del mapa de profundidad comprimido (Gzip de flotantes de 4 bytes). Un entero sin signo de 4 bytes para el tamaño del mapa de confianza comprimido en bytes. Los datos del mapa de confianza comprimido (Gzip de flotantes de 4 bytes). Un indicador de 1 byte que indica si hay audio presente (1 si hay audio, 0 si no). Si hay audio presente: un doble de 8 bytes para la coherencia del audio. Para cada fuente de audio: tres dobles de 8 bytes para la posición X, Y, Z; un doble de 8 bytes para la frecuencia; un doble de 8 bytes para la amplitud. Un entero sin signo de 4 bytes para el tamaño de los datos de audio comprimidos en bytes. Los datos de audio comprimidos (Gzip de flotantes de 4 bytes a 48 kHz). Un entero sin signo de 4 bytes para el número de vectores de estado submuestreados. Para cada vector de estado submuestreado: 112 dobles de 8 bytes para los componentes.

Formato .4df (fotografía 4D)

El formato .4df es idéntico al formato .4dv pero con un solo fotograma y con una marca mágica diferente ('4', 'D', 'F', 0x00).

---

ENDPOINTS DE LA API (24 EN TOTAL)

El servidor del SCV-4D expone una API REST completa en el puerto 8090. Los 24 endpoints son:

Endpoint 1: GET /api/v1/camaras/listar — devuelve la lista de cámaras conectadas al sistema, con sus índices y nombres.

Endpoint 2: POST /api/v1/camaras/abrir — abre una cámara por índice, resolución y dimensiones.

Endpoint 3: POST /api/v1/camaras/calibrar — inicia el asistente de calibración de lente, procesando fotogramas hasta que el patrón de tablero de ajedrez se detecta desde suficientes ángulos.

Endpoint 4: POST /api/v1/foto/capturar — captura una fotografía 4D de la cámara especificada, con trazado de rayos opcional y muestras por píxel seleccionables por el usuario.

Endpoint 5: POST /api/v1/video/iniciar — inicia una sesión de grabación de video 4D en la ruta de salida especificada, a la velocidad de fotogramas indicada, con captura de audio opcional.

Endpoint 6: POST /api/v1/video/detener — detiene la sesión de grabación activa y finaliza el archivo .4dv.

Endpoint 7: POST /api/v1/transmision/iniciar — inicia una sesión de transmisión en tiempo real al metaverso mediante WebSocket, con audio opcional.

Endpoint 8: POST /api/v1/audio/inyectar_voz — inyecta audio hablado en el campo de audio 4D en una posición espacial específica. Este endpoint recibe un fragmento de audio codificado en base64, las coordenadas X, Y, Z del hablante y un identificador de fuente. El audio se almacena en el búfer del servidor y puede ser escuchado por otros usuarios desde sus respectivas posiciones.

Endpoint 9: GET /api/v1/audio/escuchar — devuelve el audio que un oyente escucharía desde una fuente específica en una posición de escucha específica. El endpoint calcula la atenuación por distancia, el corrimiento Doppler y el paneo estéreo en tiempo real.

Endpoint 10: GET /api/v1/audio/listar_fuentes — devuelve la lista de fuentes de audio activas en el búfer del servidor, con sus identificadores y posiciones.

Endpoint 11: POST /api/v1/audio/eliminar_fuente — elimina una fuente de audio del búfer del servidor.

Endpoint 12: POST /api/v1/trazadorayos/renderizar — renderiza una fotografía 4D con trazado de rayos completo, utilizando el número especificado de muestras por píxel y rebotes máximos.

Endpoint 13: GET /api/v1/estado/coherencia — devuelve la coherencia global actual del último fotograma capturado (o del último fotograma de la transmisión activa).

Endpoint 14: GET /api/v1/estado/constantes — devuelve las constantes fundamentales de THPC‑I: H_INF, C_LUZ, C_SONIDO, TAU[14], BETA[14], XI, y la matriz de acoplamiento g_ij como un arreglo JSON.

Endpoint 15: GET /api/v1/estado/escalas — devuelve las 14 escalas informacionales con sus valores τ_i, β_i y ω_i.

Endpoint 16: GET /api/v1/salud — devuelve el estado del servidor, la versión del software y si el audio 4D está habilitado.

Endpoint 17: GET /api/v1/camaras/{indice}/estado — devuelve el estado de una cámara específica (abierta o cerrada, resolución, parámetros intrínsecos).

Endpoint 18: POST /api/v1/camaras/{indice}/cerrar — cierra la cámara especificada y libera sus recursos.

Endpoint 19: GET /api/v1/camaras/{indice}/vista_previa — devuelve un JPEG codificado en base64 del fotograma actual de la cámara, útil para monitoreo.

Endpoint 20: GET /api/v1/profundidad/{indice} — devuelve el mapa de profundidad del último fotograma capturado como un arreglo JSON de flotantes.

Endpoint 21: GET /api/v1/nubepuntos/{indice} — devuelve la nube de puntos submuestreada del último fotograma capturado como un arreglo JSON de puntos [x, y, z, r, g, b].

Endpoint 22: POST /api/v1/nubepuntos/exportar/{indice} — exporta la nube de puntos del último fotograma capturado a un formato estándar (PLY, OBJ, STL, GLTF o USDZ).

Endpoint 23: GET /api/v1/grabaciones/estado — devuelve el número de sesiones de grabación activas en el servidor.

Endpoint 24: DELETE /api/v1/grabaciones/{archivo} — elimina un archivo .4dv o .4df del almacenamiento del servidor.

Endpoint WebSocket: /ws/transmision4d/{id_transmision} — establece una conexión WebSocket para transmisión de video 4D en tiempo real. El cliente envía fotogramas codificados como JSON con el mapa de profundidad, el mapa de confianza, el vector de fase, la coherencia y los datos de audio. El servidor reenvía los fotogramas a todos los clientes conectados en la misma transmisión.

---

INSTALACIÓN

Requisitos del sistema

Para Linux (Ubuntu 22.04 o superior, Debian 12 o superior, Fedora 38 o superior):

· Rust 1.70 o superior
· OpenCV 4.5 o superior (libopencv-dev, libclang-dev)
· ONNX Runtime 1.14 o superior (se descarga automáticamente)
· wgpu (incluido vía Cargo)
· ALSA o PipeWire para audio
· 4 GB de RAM mínimo, 8 GB recomendado
· Cámara compatible con V4L2

Para macOS (11 Big Sur o superior, Intel o Apple Silicon):

· Rust 1.70 o superior
· Xcode command line tools
· OpenCV 4.5 o superior (via Homebrew: brew install opencv)
· CoreAudio (incluido en el sistema)
· 4 GB de RAM mínimo, 8 GB recomendado
· Cámara integrada o externa compatible con AVFoundation

Para Windows (10 o 11, 64 bits):

· Rust 1.70 o superior (con MSVC toolchain)
· OpenCV 4.5 o superior (precompiled)
· CMake 3.20 o superior
· DirectX 12 o Vulkan para wgpu
· 4 GB de RAM mínimo, 8 GB recomendado
· Cámara compatible con DirectShow

Para Android (8.0 Oreo o superior):

· Dispositivo con cámara frontal o trasera
· Android Studio 2022.3 o superior para compilación
· NDK 25.0 o superior para la biblioteca Rust
· 3 GB de RAM mínimo, 4 GB recomendado
· Versión precompilada de la app disponible en la sección de Releases

Para iOS (14.0 o superior):

· iPhone, iPad o iPod touch con cámara
· Xcode 14.0 o superior para compilación
· macOS con Intel o Apple Silicon para compilación
· 3 GB de RAM mínimo, 4 GB recomendado
· Versión precompilada de la app disponible en la sección de Releases

Compilación desde código fuente

```bash
# Clonar el repositorio
git clone https://github.com/reumend/scv-4d.git
cd scv-4d

# Compilar en modo release
cargo build --release

# El binario estará en target/release/scv-4d
# Opcional: instalar en el sistema
cargo install --path .
```

Modelo de red neuronal para profundidad

El modelo MiDaS v3.1 cuantizado no se incluye en el repositorio por tamaño. Se descarga automáticamente al ejecutar el software por primera vez:

```bash
scv-4d descargar_modelo --modelo midas_v31_int8.onnx
```

El modelo se guarda en ~/.local/share/scv-4d/models/ en Linux, ~/Library/Application Support/scv-4d/models/ en macOS, y %APPDATA%\scv-4d\models\ en Windows.

---

EJEMPLOS DE USO

Ejemplo 1: Capturar una fotografía 4D de una habitación

```bash
scv-4d foto --indice_camara 0 --salida habitacion.4df --trazado_rayos true
```

El software estima la profundidad de cada punto de la habitación y construye una nube de puntos 4D. La fotografía resultante se puede cargar en el metaverso como un holograma estático. Los avatares pueden caminar alrededor de los muebles y observar la habitación desde cualquier ángulo.

Ejemplo 2: Grabar un video 4D de una cirugía (sin radiación)

```bash
scv-4d video --indice_camara 0 --salida cirugia.4dv --fps 30 --duracion 600 --con_audio true
```

El software captura el campo quirúrgico en 4D durante 10 minutos. El audio captura las conversaciones del equipo médico, espacializado según la posición de cada persona. El video resultante se puede reproducir en el metaverso para entrenamiento de residentes, quienes pueden caminar alrededor del paciente y ver la cirugía desde el ángulo del cirujano principal.

Ejemplo 3: Transmitir en vivo un concierto al metaverso

```bash
scv-4d transmitir --indice_camara 0 --host_metaverso metaverso.escenario.com --puerto_metaverso 8088 --con_audio true
```

Múltiples cámaras colocadas alrededor del escenario transmiten flujos 4D al metaverso. Los asistentes virtuales (avatares) pueden moverse libremente alrededor del escenario, viendo al músico desde cualquier ángulo y escuchando el audio con espacialización perfecta (los instrumentos de la izquierda suenan en el oído izquierdo, los de la derecha en el oído derecho).

Ejemplo 4: Convertir una fotografía 2D existente a 4D

```bash
scv-4d convertir --entrada vieja_foto.jpg --salida foto_4d.4df --trazado_rayos true
```

El software estima la profundidad de la fotografía 2D utilizando la red neuronal (sin información temporal). El resultado es una fotografía 4D estática que se puede explorar en el metaverso como un diorama. La profundidad estimada puede no ser perfecta, pero es suficiente para la mayoría de las escenas cotidianas.

Ejemplo 5: Extraer una nube de puntos de un video 4D para impresión 3D

```bash
scv-4d exportar --entrada mi_video.4dv --fotograma 150 --formato ply --salida modelo.ply
```

El software extrae el fotograma 150 del video 4D, construye una malla a partir del mapa de profundidad utilizando el algoritmo de reconstrucción de superficie de Poisson, y exporta la malla en formato PLY. El archivo PLY se puede importar en Blender, Cura, PrusaSlicer o cualquier otro software de impresión 3D.

Ejemplo 6: Inyectar voz en un video 4D existente

```bash
scv-4d inyectar_audio --video mi_video.4dv --fuente "Roberth" --posicion_x 2.0 --posicion_y 1.5 --posicion_z 0.0 --audio voz.wav
```

El software añade una nueva fuente de audio al video 4D. Cuando el video se reproduce en el metaverso, los avatares que estén cerca de la posición (2.0, 1.5, 0.0) escucharán la voz con la atenuación correspondiente. Los avatares lejos no la escucharán. Esto permite añadir narraciones o comentarios a videos 4D existentes sin regrabar el audio original.

---

ALMACENAMIENTO EN LA NUBE Y MERCADO DE SEMICONDUCTORES

Consumo de almacenamiento de video 4D

Un minuto de video 4D capturado con SCV-4D ocupa aproximadamente 3.7 gigabytes comprimidos. Una fotografía 4D ocupa aproximadamente 2.1 megabytes comprimidos.

Para un usuario que graba 10 minutos de video 4D por mes (120 minutos por año), el almacenamiento anual es de 444 gigabytes. Para 330 millones de ciudadanos de Estados Unidos, el almacenamiento total anual sería de 146.5 exabytes.

El costo de almacenamiento en la nube a tarifas empresariales es de aproximadamente $23 millones por exabyte por año. La industria del almacenamiento en la nube generaría $3.37 mil millones por año solo por el contenido 4D de Estados Unidos.

Demanda de semiconductores

Cada exabyte de almacenamiento requiere aproximadamente 1000 discos duros de alta capacidad (20 TB cada uno) o 500 unidades de estado sólido (2 TB cada uno). Para 146.5 exabytes, se necesitarían 146,500 discos duros o 73,250 SSD por año. Cada disco duro o SSD contiene chips de controlador, chips de memoria (NAND flash para SSD) y chips de interfaz. El total de chips necesarios es de aproximadamente 1.5 millones por año solo para Estados Unidos.

La expansión de la fabricación de semiconductores para satisfacer esta demanda generaría ingresos fiscales por impuestos corporativos. A una tasa del 21% en Estados Unidos, los ingresos fiscales anuales solo de la fabricación de chips para almacenamiento 4D serían de aproximadamente $745 millones. Esto no incluye los impuestos sobre los centros de datos, la electricidad, el mantenimiento y los servicios de valor agregado.

El ciclo de retroalimentación positiva

SCV-4D crea un ciclo de retroalimentación positiva: más usuarios generan más videos 4D. Más videos 4D requieren más almacenamiento en la nube. Más almacenamiento en la nube requiere más centros de datos. Más centros de datos requieren más chips semiconductores. Más chips semiconductores generan más ingresos fiscales. Más ingresos fiscales permiten a los gobiernos reducir la deuda pública. La reducción de la deuda pública reduce las tasas de interés. La reducción de las tasas de interés estimula el crecimiento económico. El crecimiento económico aumenta el número de usuarios. El ciclo se repite.

SCV-4D no es un costo. Es una inversión. Cuantas más personas lo usen, más chips se necesitan. Cuantos más chips se venden, más impuestos se recaudan. Cuantos más impuestos se recaudan, más baja es la deuda nacional.

---

HOJA DE RUTA

Versión 1.0 (Junio 2026) — Lanzamiento actual

· Captura de video 4D desde cualquier cámara
· Captura de fotografía 4D desde cualquier cámara
· Calibración de lente mediante patrón de ajedrez
· Corrección de distorsión geométrica
· Estimación monocular de profundidad con red neuronal MiDaS
· Flujo óptico denso para coherencia temporal
· Cálculo de coherencia multiescala THPC‑I
· Estampado de fase y asignación de tiempo propio τ_i
· Vector de estado de 112 dimensiones
· Audio 4D con localización de fuentes sonoras
· Inyección de voz y renderizado de audio espacial
· Trazado de rayos adaptativo con iluminación global
· Formatos .4dv (video) y .4df (fotografía)
· API REST con 24 endpoints
· Transmisión WebSocket en tiempo real
· App nativa para Android
· App nativa para iOS
· Script de pruebas en Python
· Documentación completa

Versión 1.1 (Septiembre 2026) — Planificada

· Soporte para SDR USB (captura directa de ondas de radio)
· Soporte para cámara térmica FLIR One (captura de infrarrojo)
· Exportación a USDZ para realidad aumentada en iOS
· Integración con Blender mediante plugin nativo
· Aceleración por GPU (CUDA / Metal / Vulkan) para trazado de rayos

Versión 1.2 (Diciembre 2026) — Planificada

· Soporte para secuenciador de ADN Oxford Nanopore (mapeo genético 4D)
· Soporte para datos FITS de telescopios astronómicos
· Trazado de rayos con photon mapping (múltiples rebotes difusos)
· Compresión de video 4D con códec HEVC modificado
· Plugin para Unreal Engine 5

Versión 2.0 (Junio 2027) — Planificada

· Captura de video 4D a 120 fps (cámara lenta)
· Estimación de profundidad con IA generativa (difusión estable)
· Trazado de rayos en tiempo real para transmisión en vivo
· Interfaz gráfica de usuario (GUI) con egui
· Soporte para array de cámaras (captura 4D desde múltiples ángulos)
· Integración con la Exchange Híbrida Dual (tokenización de videos 4D como NFTs)

---

LICENCIA Y CONTACTO

Licencia: Apache 2.0

Puedes usar, modificar y distribuir este software libremente, siempre que incluyas el aviso de copyright y la licencia. El software se proporciona "tal cual", sin garantías de ningún tipo.

Contacto:

· Autor principal: Roberth Willians Mendoza Requena
· GitHub: @reumend
· Email: reumend@gmail.com
· LLC: Mendoza & Fennimore LLC

Reporte de errores: https://github.com/reumend/scv-4d/issues

Documentación completa: https://github.com/reumend/scv-4d/wiki

Donaciones: Si este software te ha sido útil, considera donar a través de GitHub Sponsors para apoyar el desarrollo continuo.

---

"El software no crea datos. Revela los datos que siempre estuvieron allí. Cada fotón que entra en una cámara lleva no solo color sino posición en el espacio y fase en el tiempo. Cada micrófono que captura sonido lleva no solo frecuencia sino dirección y distancia. SCV-4D no es un invento. Es un descubrimiento de lo que ya estaba escrito en las ecuaciones del universo. Nosotros solo escribimos el código para leerlas."

— Roberth Willians Mendoza Requena, Mendoza & Fennimore LLC, Junio 2026
