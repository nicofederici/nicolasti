<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Guía Interactiva de Electricidad Domiciliaria</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <!-- Chosen Palette: Calm Harmony -->
    <!-- Application Structure Plan: Se ha diseñado una aplicación de página única con navegación por pestañas (Inicio, Conceptos, Instalaciones, Seguridad, Normativa, Recursos). Esta estructura descompone la densa información del informe en secciones temáticas y manejables, permitiendo un acceso no lineal. En lugar de un largo desplazamiento, el usuario puede saltar directamente al área de interés. Las interacciones clave, como una calculadora de la Ley de Ohm, diagramas de circuitos interactivos y un gráfico de normativas, están diseñadas para fomentar la exploración y la comprensión práctica, transformando un documento estático en una herramienta de aprendizaje dinámica y centrada en el usuario. -->
    <!-- Visualization & Content Choices: 1. Ley de Ohm: (Meta: Informar/Calcular) -> Se usa una calculadora HTML/JS para una demostración práctica de la relación V=IR. 2. Identificación de Conductores: (Meta: Informar) -> Tarjetas HTML/CSS interactivas al pasar el cursor para una rápida referencia visual de los colores y funciones. 3. Circuitos Eléctricos: (Meta: Organizar/Explicar) -> Diagramas construidos con HTML/CSS/Tailwind con interacción JS. Al hacer clic, se muestra información detallada en un panel lateral, evitando modales intrusivos y facilitando la comparación. 4. Secciones de Cable (Normativa): (Meta: Comparar/Informar) -> Un gráfico de barras de Chart.js (Canvas) para visualizar y comparar fácilmente las secciones mínimas requeridas, más digerible que una tabla. 5. Consejos de Seguridad: (Meta: Informar/Advertir) -> Una cuadrícula con iconos Unicode (✅/❌) para un impacto visual inmediato. 6. Comparativa de Cursos: (Meta: Comparar/Informar) -> La tabla original se transforma en tarjetas responsivas para una mejor legibilidad en móviles. -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #FDFBF8; /* Warm Neutral */
            color: #374151;
        }
        .nav-link {
            transition: all 0.3s ease;
            cursor: pointer;
        }
        .nav-link.active {
            background-color: #0d9488; /* Teal-600 */
            color: white;
            font-weight: 600;
        }
        .content-section {
            display: none;
            animation: fadeIn 0.5s;
        }
        .content-section.active {
            display: block;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .chart-container {
            position: relative;
            height: 40vh;
            max-height: 400px;
            width: 100%;
            max-width: 700px;
            margin: auto;
        }
        .interactive-diagram-container {
            display: grid;
            grid-template-columns: 2fr 1fr;
            gap: 1.5rem;
        }
        @media (max-width: 768px) {
            .interactive-diagram-container {
                grid-template-columns: 1fr;
            }
        }
        .diagram-component {
            cursor: pointer;
            transition: all 0.2s ease-in-out;
            border-width: 2px;
            border-style: solid;
        }
        .diagram-component:hover, .diagram-component.selected {
            transform: scale(1.05);
            box-shadow: 0 0 15px rgba(13, 148, 136, 0.4);
            border-color: #0d9488;
        }
        .wire {
            position: relative;
            height: 4px;
        }
        .wire-vertical {
            width: 4px;
            height: 100%;
            position: absolute;
        }
    </style>
</head>
<body class="antialiased">

    <div class="container mx-auto p-4 md:p-8">
        <header class="text-center mb-8">
            <h1 class="text-4xl md:text-5xl font-bold text-teal-800">Guía Interactiva de Electricidad Domiciliaria</h1>
            <p class="mt-4 text-lg text-gray-600">Una herramienta para aprender los fundamentos, instalaciones y seguridad eléctrica en el hogar.</p>
        </header>

        <nav class="flex flex-wrap justify-center gap-2 md:gap-4 mb-8 bg-white p-3 rounded-xl shadow-md sticky top-4 z-10">
            <a data-target="inicio" class="nav-link active px-4 py-2 rounded-lg">🏠 Inicio</a>
            <a data-target="conceptos" class="nav-link px-4 py-2 rounded-lg">💡 Conceptos</a>
            <a data-target="instalaciones" class="nav-link px-4 py-2 rounded-lg">🔧 Instalaciones</a>
            <a data-target="seguridad" class="nav-link px-4 py-2 rounded-lg">🛡️ Seguridad</a>
            <a data-target="normativa" class="nav-link px-4 py-2 rounded-lg">📜 Normativa</a>
            <a data-target="recursos" class="nav-link px-4 py-2 rounded-lg">📚 Recursos</a>
        </nav>

        <main>
            <!-- INICIO Section -->
            <section id="inicio" class="content-section active">
                <div class="bg-white p-8 rounded-xl shadow-lg">
                    <h2 class="text-3xl font-bold text-teal-700 mb-4">Tu Primer Paso Hacia la Seguridad Eléctrica</h2>
                    <p class="text-gray-700 leading-relaxed mb-4">Bienvenido a tu guía de inicio en el mundo de la electricidad domiciliaria. El objetivo de esta herramienta es darte los conocimientos fundamentales y las habilidades prácticas básicas para que entiendas mejor el sistema eléctrico de tu casa. Aprenderás a diagnosticar problemas menores y, muy importante, a saber cuándo es crucial llamar a un profesional.</p>
                    <p class="text-gray-700 leading-relaxed mb-4">La electricidad es indispensable, pero también peligrosa si no se trata con respeto. La seguridad es la máxima prioridad. Aquí encontrarás información y ejemplos prácticos que te ayudarán a prevenir accidentes y a mantener tu hogar seguro.</p>
                    <div class="mt-6 p-6 bg-amber-50 border-l-4 border-amber-400 rounded-r-lg">
                        <h3 class="text-xl font-semibold text-amber-800">El Principio más Importante</h3>
                        <p class="mt-2 text-amber-700">El mayor conocimiento que puedes adquirir no es solo cómo hacer las cosas, sino desarrollar el juicio para entender los riesgos, reconocer los límites de tu propia capacidad y **priorizar siempre la seguridad**. Las instalaciones complejas o las reparaciones importantes siempre deben ser realizadas por un electricista matriculado.</p>
                    </div>
                </div>
            </section>

            <!-- CONCEPTOS Section -->
            <section id="conceptos" class="content-section">
                <div class="bg-white p-8 rounded-xl shadow-lg">
                    <h2 class="text-3xl font-bold text-teal-700 mb-2">Fundamentos Clave de la Electricidad</h2>
                    <p class="text-gray-600 mb-8">Antes de manipular cualquier cable, es vital entender los conceptos básicos. Piensa en la electricidad como agua en una tubería: esto te ayudará a visualizar cómo funciona todo.</p>
                    
                    <div class="grid md:grid-cols-2 lg:grid-cols-4 gap-6 mb-8">
                        <div class="p-4 bg-gray-50 rounded-lg border">
                            <h3 class="font-bold text-lg">Tensión (Voltaje) ⚡</h3>
                            <p class="text-sm">Es la "presión" que empuja la electricidad. En Argentina, es de <strong>220V</strong>. Se mide en Voltios (V).</p>
                        </div>
                        <div class="p-4 bg-gray-50 rounded-lg border">
                            <h3 class="font-bold text-lg">Corriente (Intensidad) 🌊</h3>
                            <p class="text-sm">Es el "flujo" de electricidad a través del cable. Se mide en Amperios (A).</p>
                        </div>
                        <div class="p-4 bg-gray-50 rounded-lg border">
                            <h3 class="font-bold text-lg">Resistencia 🛑</h3>
                            <p class="text-sm">Es la "fricción" que se opone al flujo. Se mide en Ohmios (Ω).</p>
                        </div>
                        <div class="p-4 bg-gray-50 rounded-lg border">
                            <h3 class="font-bold text-lg">Potencia 💡</h3>
                            <p class="text-sm">Es la cantidad de "trabajo" que hace la electricidad. Se mide en Vatios (W).</p>
                        </div>
                    </div>

                    <h3 class="text-2xl font-bold text-teal-700 mb-4">Calculadora Interactiva: Ley de Ohm y Ley de Watt</h3>
                    <div class="grid md:grid-cols-2 gap-8">
                        <div class="p-6 bg-teal-50 rounded-xl border border-teal-200">
                            <h4 class="font-semibold text-xl text-teal-800 mb-3">Ley de Ohm (V = I × R)</h4>
                            <p class="text-sm text-teal-700 mb-4">Ingresa dos valores para calcular el tercero.</p>
                            <div class="space-y-3">
                                <div>
                                    <label for="voltaje" class="block text-sm font-medium text-gray-700">Tensión (V)</label>
                                    <input type="number" id="voltaje" placeholder="ej. 220" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-teal-500 focus:ring-teal-500 sm:text-sm p-2">
                                </div>
                                <div>
                                    <label for="corriente" class="block text-sm font-medium text-gray-700">Corriente (A)</label>
                                    <input type="number" id="corriente" placeholder="ej. 10" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-teal-500 focus:ring-teal-500 sm:text-sm p-2">
                                </div>
                                <div>
                                    <label for="resistencia" class="block text-sm font-medium text-gray-700">Resistencia (Ω)</label>
                                    <input type="number" id="resistencia" placeholder="ej. 22" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-teal-500 focus:ring-teal-500 sm:text-sm p-2">
                                </div>
                                <button id="resetOhm" class="w-full text-center px-4 py-2 border border-transparent rounded-md shadow-sm text-sm font-medium text-white bg-teal-600 hover:bg-teal-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-teal-500">Limpiar</button>
                            </div>
                        </div>
                        <div class="p-6 bg-amber-50 rounded-xl border border-amber-200">
                            <h4 class="font-semibold text-xl text-amber-800 mb-3">Ley de Watt (P = V × I)</h4>
                             <p class="text-sm text-amber-700 mb-4">Calcula la potencia de tus electrodomésticos.</p>
                            <div class="space-y-3">
                                <div>
                                    <label for="potencia-v" class="block text-sm font-medium text-gray-700">Tensión (V)</label>
                                    <input type="number" id="potencia-v" value="220" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-amber-500 focus:ring-amber-500 sm:text-sm p-2">
                                </div>
                                <div>
                                    <label for="potencia-i" class="block text-sm font-medium text-gray-700">Corriente (A)</label>
                                    <input type="number" id="potencia-i" placeholder="ej. 1.5" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-amber-500 focus:ring-amber-500 sm:text-sm p-2">
                                </div>
                                <div class="pt-2">
                                     <p class="text-lg text-gray-700">Potencia (W): <strong id="potencia-resultado" class="text-amber-800 font-bold">0 W</strong></p>
                                </div>
                                <button id="resetWatt" class="w-full text-center px-4 py-2 border border-transparent rounded-md shadow-sm text-sm font-medium text-white bg-amber-500 hover:bg-amber-600 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-amber-500">Limpiar</button>
                            </div>
                        </div>
                    </div>
                </div>
            </section>

            <!-- INSTALACIONES Section -->
            <section id="instalaciones" class="content-section">
                <div class="bg-white p-8 rounded-xl shadow-lg">
                    <h2 class="text-3xl font-bold text-teal-700 mb-2">Instalaciones Típicas del Hogar</h2>
                    <p class="text-gray-600 mb-8">Aquí exploraremos cómo se conectan las luces y los tomacorrientes. Toca los componentes en el diagrama para ver más información.</p>
                    
                    <h3 class="text-2xl font-bold text-teal-700 mb-4">Diagrama Interactivo: Circuito de Iluminación y Tomacorriente</h3>
                    <p class="mb-6">Este diagrama simplificado muestra cómo se conectan un interruptor para una lámpara y un tomacorriente en paralelo, que es la configuración estándar en un hogar. Haz clic en cada elemento para aprender sobre su función.</p>

                    <div class="interactive-diagram-container">
                        <div class="bg-gray-50 p-6 rounded-lg border-2 border-gray-200 relative">
                            <!-- Wires -->
                            <div class="absolute top-10 left-0 w-full wire bg-red-500"></div>
                            <div class="absolute top-20 left-0 w-full wire bg-blue-500"></div>
                            <div class="absolute top-30 left-0 w-full wire bg-green-500"></div>
                            
                            <!-- Components -->
                            <div class="relative flex justify-around items-center h-full">
                                <!-- Switch -->
                                <div class="text-center">
                                    <div id="comp-interruptor" class="diagram-component w-20 h-20 bg-white rounded-lg shadow-md flex items-center justify-center border-gray-300">
                                        <span class="text-3xl">🔌</span>
                                    </div>
                                    <p class="mt-2 font-medium">Interruptor</p>
                                </div>
                                
                                <!-- Lamp -->
                                <div class="text-center">
                                    <div id="comp-lampara" class="diagram-component w-20 h-20 bg-white rounded-lg shadow-md flex items-center justify-center border-gray-300">
                                        <span class="text-3xl">💡</span>
                                    </div>
                                    <p class="mt-2 font-medium">Lámpara</p>
                                </div>

                                <!-- Outlet -->
                                <div class="text-center">
                                    <div id="comp-tomacorriente" class="diagram-component w-20 h-20 bg-white rounded-lg shadow-md flex items-center justify-center border-gray-300">
                                        <span class="text-3xl">🔌</span>
                                    </div>
                                    <p class="mt-2 font-medium">Tomacorriente</p>
                                </div>
                            </div>
                        </div>

                        <div id="diagram-info-panel" class="p-6 bg-teal-50 rounded-xl border-2 border-teal-200">
                            <h4 id="info-title" class="font-semibold text-xl text-teal-800 mb-3">Panel de Información</h4>
                            <p id="info-text" class="text-teal-900 leading-relaxed">Haz clic en un componente del diagrama (interruptor, lámpara o tomacorriente) para ver su descripción y cómo se conecta correctamente.</p>
                        </div>
                    </div>
                    
                    <h3 class="text-2xl font-bold text-teal-700 mt-12 mb-4">Identificación de Conductores (Cables)</h3>
                    <p class="text-gray-600 mb-6">Identificar correctamente los cables por su color es crucial para la seguridad. ¡Nunca los confundas!</p>
                    <div class="grid md:grid-cols-3 gap-6">
                        <div class="p-6 rounded-lg text-white text-center bg-red-600 shadow-lg">
                            <h4 class="text-xl font-bold">FASE</h4>
                            <p class="mt-2">Transporta la corriente. ¡Es el peligroso! Colores: <strong>Marrón, Negro o Rojo</strong>.</p>
                        </div>
                        <div class="p-6 rounded-lg text-white text-center bg-blue-600 shadow-lg">
                            <h4 class="text-xl font-bold">NEUTRO</h4>
                            <p class="mt-2">Cierra el circuito. Su color estándar es <strong>Azul Claro</strong>.</p>
                        </div>
                         <div class="p-6 rounded-lg text-white text-center bg-green-600 shadow-lg">
                            <h4 class="text-xl font-bold">TIERRA</h4>
                            <p class="mt-2">Cable de seguridad. Protege de descargas. Su color es <strong>Verde y Amarillo</strong>.</p>
                        </div>
                    </div>
                </div>
            </section>

            <!-- SEGURIDAD Section -->
            <section id="seguridad" class="content-section">
                <div class="bg-white p-8 rounded-xl shadow-lg">
                    <h2 class="text-3xl font-bold text-red-700 mb-2">La Seguridad es lo Primero</h2>
                    <p class="text-gray-600 mb-8">Comprender los dispositivos de protección y las buenas prácticas es innegociable. Estos elementos protegen tu casa y, lo más importante, tu vida.</p>

                    <div class="grid md:grid-cols-2 gap-8 mb-8">
                        <div class="p-6 bg-gray-50 rounded-xl border-l-4 border-blue-500">
                            <h3 class="text-xl font-bold text-blue-800">Interruptor Termomagnético (Llave Térmica)</h3>
                            <p class="mt-2 text-gray-700"><strong>Protege la INSTALACIÓN.</strong> Evita que los cables se sobrecalienten y se incendien por sobrecargas o cortocircuitos.</p>
                        </div>
                        <div class="p-6 bg-gray-50 rounded-xl border-l-4 border-green-500">
                            <h3 class="text-xl font-bold text-green-800">Interruptor Diferencial (Disyuntor)</h3>
                            <p class="mt-2 text-gray-700"><strong>Protege a las PERSONAS.</strong> Detecta pequeñas fugas de corriente (como las que pasan por el cuerpo en una descarga) y corta la luz al instante para salvar vidas.</p>
                            <p class="mt-3 text-sm font-semibold text-red-600">¡Recuerda probarlo cada mes presionando el botón 'T'!</p>
                        </div>
                    </div>

                    <h3 class="text-2xl font-bold text-red-700 mt-8 mb-4">Consejos Rápidos de Seguridad</h3>
                    <div class="space-y-4">
                        <div class="flex items-start gap-4 p-4 bg-green-50 rounded-lg">
                            <span class="text-2xl">✅</span>
                            <p><strong>Desconecta la llave general</strong> antes de cualquier trabajo eléctrico.</p>
                        </div>
                        <div class="flex items-start gap-4 p-4 bg-green-50 rounded-lg">
                            <span class="text-2xl">✅</span>
                            <p>Utiliza siempre <strong>herramientas aisladas</strong> y calzado de goma.</p>
                        </div>
                        <div class="flex items-start gap-4 p-4 bg-green-50 rounded-lg">
                            <span class="text-2xl">✅</span>
                            <p>Compra siempre <strong>materiales eléctricos certificados</strong> con el Sello de Seguridad Argentino.</p>
                        </div>
                        <div class="flex items-start gap-4 p-4 bg-red-50 rounded-lg">
                            <span class="text-2xl">❌</span>
                            <p><strong>Nunca</strong> uses "triples" o "zapatillas" de mala calidad para conectar muchos aparatos.</p>
                        </div>
                        <div class="flex items-start gap-4 p-4 bg-red-50 rounded-lg">
                            <span class="text-2xl">❌</span>
                            <p><strong>Nunca</strong> toques aparatos eléctricos con las manos mojadas o estando descalzo.</p>
                        </div>
                        <div class="flex items-start gap-4 p-4 bg-red-50 rounded-lg">
                            <span class="text-2xl">❌</span>
                            <p><strong>Nunca</strong> reemplaces un fusible o llave térmica por uno de mayor amperaje sin consultar a un profesional.</p>
                        </div>
                    </div>
                </div>
            </section>

            <!-- NORMATIVA Section -->
            <section id="normativa" class="content-section">
                <div class="bg-white p-8 rounded-xl shadow-lg">
                    <h2 class="text-3xl font-bold text-teal-700 mb-2">Normativa Argentina (AEA 90364-7-771)</h2>
                    <p class="text-gray-600 mb-8">Las instalaciones eléctricas no se hacen "a ojo". En Argentina, la Asociación Electrotécnica Argentina (AEA) establece reglas claras para garantizar la seguridad. Aquí tienes un resumen.</p>
                    
                    <h3 class="text-2xl font-bold text-teal-700 mb-4">Secciones Mínimas de Conductores</h3>
                    <p class="text-gray-600 mb-6">El "grosor" (sección) del cable es fundamental para que no se sobrecaliente. Usar un cable demasiado fino es un grave riesgo de incendio. Este gráfico muestra los mínimos exigidos por la norma.</p>
                    <div class="chart-container">
                        <canvas id="wireGaugeChart"></canvas>
                    </div>

                    <div class="mt-12 grid md:grid-cols-2 gap-8">
                        <div class="p-6 bg-gray-50 rounded-xl border">
                            <h4 class="text-lg font-semibold text-gray-800 mb-2">Puesta a Tierra (Esquema TT)</h4>
                            <p>Es <strong>obligatoria</strong>. Consiste en una jabalina de cobre enterrada en el suelo, conectada a todos los tomacorrientes con el cable verde-amarillo. Es tu seguro de vida contra descargas de aparatos defectuosos.</p>
                        </div>
                        <div class="p-6 bg-gray-50 rounded-xl border">
                            <h4 class="text-lg font-semibold text-gray-800 mb-2">Productos Certificados</h4>
                            <p>Utiliza siempre materiales con el <strong>"Sello de Seguridad de Argentina"</strong>. Es la garantía de que el producto fue probado y es seguro. Los productos sin sello son ilegales y peligrosos.</p>
                        </div>
                    </div>
                </div>
            </section>
            
            <!-- RECURSOS Section -->
            <section id="recursos" class="content-section">
                <div class="bg-white p-8 rounded-xl shadow-lg">
                    <h2 class="text-3xl font-bold text-teal-700 mb-2">Cursos y Recursos Gratuitos</h2>
                    <p class="text-gray-600 mb-8">Si quieres profundizar, existen excelentes cursos gratuitos. Aquí tienes una selección de los más recomendados por su enfoque práctico y visual.</p>
                    
                    <div class="space-y-6">
                        <!-- Card 1 -->
                        <div class="border rounded-xl p-6 hover:shadow-md transition-shadow">
                            <h3 class="text-xl font-bold text-teal-800">Curso de Electricidad Básica Residencial</h3>
                            <p class="text-sm text-gray-500 mb-2">Plataforma: VideoCursos.co</p>
                            <p class="mb-4">Muy completo y detallado. Enseña a usar un multímetro y a leer esquemas eléctricos. Ideal para empezar con una base sólida.</p>
                            <div class="flex flex-wrap gap-2 text-sm">
                                <span class="bg-teal-100 text-teal-800 px-2 py-1 rounded-full font-medium">6h 50m</span>
                                <span class="bg-blue-100 text-blue-800 px-2 py-1 rounded-full font-medium">Principiante</span>
                                <span class="bg-green-100 text-green-800 px-2 py-1 rounded-full font-medium">Muy Práctico</span>
                            </div>
                        </div>
                        <!-- Card 2 -->
                        <div class="border rounded-xl p-6 hover:shadow-md transition-shadow">
                            <h3 class="text-xl font-bold text-teal-800">Instalaciones eléctricas para principiantes</h3>
                            <p class="text-sm text-gray-500 mb-2">Plataforma: Cursa.app</p>
                            <p class="mb-4">Enfocado en trucos, consejos y errores comunes a evitar. Muy visual y directo al grano, con lecciones cortas en video.</p>
                             <div class="flex flex-wrap gap-2 text-sm">
                                <span class="bg-teal-100 text-teal-800 px-2 py-1 rounded-full font-medium">3h 59m</span>
                                <span class="bg-blue-100 text-blue-800 px-2 py-1 rounded-full font-medium">Principiante</span>
                                <span class="bg-green-100 text-green-800 px-2 py-1 rounded-full font-medium">Consejos Prácticos</span>
                            </div>
                        </div>
                        <!-- Card 3 -->
                        <div class="border rounded-xl p-6 hover:shadow-md transition-shadow">
                            <h3 class="text-xl font-bold text-teal-800">Tutoriales en Video (YouTube/TikTok)</h3>
                            <p class="text-sm text-gray-500 mb-2">Plataformas: YouTube, TikTok</p>
                            <p class="mb-4">Excelente como complemento. Busca canales como "enchufayaprende" o diagramas de cableado para ver demostraciones visuales y rápidas de tareas específicas.</p>
                             <div class="flex flex-wrap gap-2 text-sm">
                                <span class="bg-teal-100 text-teal-800 px-2 py-1 rounded-full font-medium">Variable</span>
                                <span class="bg-blue-100 text-blue-800 px-2 py-1 rounded-full font-medium">Todos los niveles</span>
                                <span class="bg-green-100 text-green-800 px-2 py-1 rounded-full font-medium">Muy Visual</span>
                            </div>
                        </div>
                         <!-- Card 4 -->
                        <div class="border rounded-xl p-6 hover:shadow-md transition-shadow">
                            <h3 class="text-xl font-bold text-teal-800">Curso online para instaladores electricistas</h3>
                            <p class="text-sm text-gray-500 mb-2">Institución: Universidad Nacional de Córdoba (UNC)</p>
                            <p class="mb-4">Una opción más formal y estructurada, respaldada por una universidad. Ideal si buscas un aprendizaje más profundo y con evaluación.</p>
                             <div class="flex flex-wrap gap-2 text-sm">
                                <span class="bg-yellow-100 text-yellow-800 px-2 py-1 rounded-full font-medium">Formal</span>
                                <span class="bg-purple-100 text-purple-800 px-2 py-1 rounded-full font-medium">Componente Presencial</span>
                            </div>
                        </div>
                    </div>
                </div>
            </section>
        </main>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            // Navigation
            const navLinks = document.querySelectorAll('.nav-link');
            const sections = document.querySelectorAll('.content-section');

            navLinks.forEach(link => {
                link.addEventListener('click', () => {
                    const target = link.getAttribute('data-target');

                    navLinks.forEach(nav => nav.classList.remove('active'));
                    link.classList.add('active');

                    sections.forEach(section => {
                        if (section.id === target) {
                            section.classList.add('active');
                        } else {
                            section.classList.remove('active');
                        }
                    });
                });
            });

            // Ohm's Law Calculator
            const voltajeInput = document.getElementById('voltaje');
            const corrienteInput = document.getElementById('corriente');
            const resistenciaInput = document.getElementById('resistencia');
            const resetOhmBtn = document.getElementById('resetOhm');

            function calculateOhm() {
                const V = parseFloat(voltajeInput.value);
                const I = parseFloat(corrienteInput.value);
                const R = parseFloat(resistenciaInput.value);

                if (!isNaN(V) && !isNaN(I) && R !== 0) {
                    resistenciaInput.value = (V / I).toFixed(2);
                } else if (!isNaN(V) && !isNaN(R) && R !== 0) {
                    corrienteInput.value = (V / R).toFixed(2);
                } else if (!isNaN(I) && !isNaN(R)) {
                    voltajeInput.value = (I * R).toFixed(2);
                }
            }
            
            [voltajeInput, corrienteInput, resistenciaInput].forEach(input => {
                 input.addEventListener('input', () => {
                    const filledInputs = [voltajeInput, corrienteInput, resistenciaInput].filter(i => i.value !== '');
                    if (filledInputs.length === 2) {
                        if (voltajeInput.value === '') calculateOhm();
                        if (corrienteInput.value === '') calculateOhm();
                        if (resistenciaInput.value === '') calculateOhm();
                    }
                 });
            });
            
            resetOhmBtn.addEventListener('click', () => {
                voltajeInput.value = '';
                corrienteInput.value = '';
                resistenciaInput.value = '';
            });


            // Watt's Law Calculator
            const potenciaV = document.getElementById('potencia-v');
            const potenciaI = document.getElementById('potencia-i');
            const potenciaResultado = document.getElementById('potencia-resultado');
            const resetWattBtn = document.getElementById('resetWatt');

            function calculateWatt() {
                const V = parseFloat(potenciaV.value);
                const I = parseFloat(potenciaI.value);
                if (!isNaN(V) && !isNaN(I)) {
                    potenciaResultado.textContent = `${(V * I).toFixed(2)} W`;
                } else {
                    potenciaResultado.textContent = '0 W';
                }
            }

            [potenciaV, potenciaI].forEach(input => input.addEventListener('input', calculateWatt));
            
            resetWattBtn.addEventListener('click', () => {
                potenciaV.value = '220';
                potenciaI.value = '';
                potenciaResultado.textContent = '0 W';
            });

            // Interactive Diagram
            const components = document.querySelectorAll('.diagram-component');
            const infoTitle = document.getElementById('info-title');
            const infoText = document.getElementById('info-text');

            const infoData = {
                interruptor: {
                    title: 'Interruptor Simple',
                    text: 'Controla una luz desde un solo punto. Por seguridad, siempre interrumpe el cable de Fase (marrón/negro/rojo). El cable Neutro (azul) va directo a la lámpara.'
                },
                lampara: {
                    title: 'Lámpara / Luminaria',
                    text: 'Recibe la energía para iluminar. Se conecta al cable de retorno que viene del interruptor y al cable Neutro para cerrar el circuito.'
                },
                tomacorriente: {
                    title: 'Tomacorriente',
                    text: 'Proporciona energía a los aparatos. Se conecta en paralelo al circuito. Los terminales reciben Fase, Neutro y el importantísimo cable de Puesta a Tierra (verde/amarillo).'
                }
            };
            
            components.forEach(comp => {
                comp.addEventListener('click', () => {
                    components.forEach(c => c.classList.remove('selected'));
                    comp.classList.add('selected');
                    const compId = comp.id.split('-')[1];
                    infoTitle.textContent = infoData[compId].title;
                    infoText.textContent = infoData[compId].text;
                });
            });
            
            // Wire Gauge Chart
            const ctx = document.getElementById('wireGaugeChart').getContext('2d');
            const wireGaugeChart = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: ['Línea Principal', 'Línea Seccional', 'Circuitos Uso General', 'Circuitos Uso Especial', 'Derivaciones', 'Línea de Protección'],
                    datasets: [{
                        label: 'Sección Mínima (mm²)',
                        data: [4, 2.5, 2.5, 2.5, 1.5, 2.5],
                        backgroundColor: [
                            'rgba(13, 148, 136, 0.7)',
                            'rgba(8, 126, 116, 0.7)',
                            'rgba(15, 118, 110, 0.7)',
                            'rgba(20, 108, 102, 0.7)',
                            'rgba(17, 94, 89, 0.7)',
                            'rgba(5, 150, 105, 0.7)'
                        ],
                        borderColor: [
                             'rgba(13, 148, 136, 1)',
                            'rgba(8, 126, 116, 1)',
                            'rgba(15, 118, 110, 1)',
                            'rgba(20, 108, 102, 1)',
                            'rgba(17, 94, 89, 1)',
                            'rgba(5, 150, 105, 1)'
                        ],
                        borderWidth: 1
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    scales: {
                        y: {
                            beginAtZero: true,
                            title: {
                                display: true,
                                text: 'Sección en mm²'
                            }
                        },
                        x: {
                           ticks: {
                                autoSkip: false,
                                maxRotation: 45,
                                minRotation: 0
                           }
                        }
                    },
                    plugins: {
                        legend: {
                            display: false
                        },
                        title: {
                            display: true,
                            text: 'Secciones Mínimas de Cables según Norma AEA',
                            font: {
                                size: 18
                            }
                        },
                        tooltip: {
                            callbacks: {
                                label: function(context) {
                                    return ` ${context.dataset.label}: ${context.raw} mm²`;
                                }
                            }
                        }
                    }
                }
            });
        });
    </script>
</body>
</html>
