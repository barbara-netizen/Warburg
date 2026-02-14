<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Aby Warburg: Teoría de la Imagen - Mnemosyne</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,600;1,400&family=Inter:wght@300;400;600&display=swap');
        
        body {
            font-family: 'Inter', sans-serif;
            background: #0a0a0a;
            color: #e5e5e5;
            overflow-x: hidden;
        }
        
        .serif {
            font-family: 'Cormorant Garamond', serif;
        }
        
        .grain {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 50;
            opacity: 0.03;
            background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noiseFilter'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='3' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noiseFilter)'/%3E%3C/svg%3E");
        }
        
        .floating-image {
            position: absolute;
            transition: all 0.8s cubic-bezier(0.4, 0, 0.2, 1);
            cursor: pointer;
            filter: sepia(0.3) contrast(1.1);
            box-shadow: 0 20px 50px rgba(0,0,0,0.8);
        }
        
        .floating-image:hover {
            transform: scale(1.1) rotate(2deg);
            filter: sepia(0) contrast(1.2);
            z-index: 100;
        }
        
        .connection-line {
            position: absolute;
            height: 1px;
            background: linear-gradient(90deg, transparent, rgba(212, 175, 55, 0.6), transparent);
            transform-origin: left center;
            pointer-events: none;
            opacity: 0;
            animation: pulseLine 3s infinite;
        }
        
        @keyframes pulseLine {
            0%, 100% { opacity: 0.2; }
            50% { opacity: 0.8; }
        }
        
        .pathos-formula {
            background: linear-gradient(135deg, rgba(212, 175, 55, 0.1), rgba(139, 69, 19, 0.1));
            border: 1px solid rgba(212, 175, 55, 0.3);
        }
        
        .survival-glow {
            animation: survivalPulse 4s infinite;
        }
        
        @keyframes survivalPulse {
            0%, 100% { box-shadow: 0 0 20px rgba(212, 175, 55, 0.2); }
            50% { box-shadow: 0 0 60px rgba(212, 175, 55, 0.6), 0 0 100px rgba(212, 175, 55, 0.3); }
        }
        
        .text-reveal {
            clip-path: polygon(0 0, 100% 0, 100% 100%, 0% 100%);
        }
        
        .atlas-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
            gap: 1rem;
            perspective: 1000px;
        }
        
        .atlas-item {
            transform-style: preserve-3d;
            transition: transform 0.6s;
            overflow: hidden;
        }
        
        .atlas-item:hover {
            transform: rotateY(10deg) rotateX(5deg) scale(1.05);
        }
        
        .atlas-item img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            filter: sepia(0.4) contrast(1.1);
            transition: filter 0.3s;
        }
        
        .atlas-item:hover img {
            filter: sepia(0) contrast(1.2);
        }
        
        .dialectic-node {
            position: relative;
        }
        
        .dialectic-node::before {
            content: '';
            position: absolute;
            inset: -2px;
            background: linear-gradient(45deg, #d4af37, #8b4513, #d4af37);
            border-radius: 50%;
            z-index: -1;
            opacity: 0;
            transition: opacity 0.3s;
        }
        
        .dialectic-node:hover::before {
            opacity: 1;
            animation: rotate 3s linear infinite;
        }
        
        @keyframes rotate {
            from { transform: rotate(0deg); }
            to { transform: rotate(360deg); }
        }
        
        .memory-trace {
            stroke-dasharray: 1000;
            stroke-dashoffset: 1000;
            animation: drawLine 2s forwards;
        }
        
        @keyframes drawLine {
            to { stroke-dashoffset: 0; }
        }
        
        .ekphrasis-text {
            font-style: italic;
            line-height: 1.8;
            position: relative;
        }
        
        .ekphrasis-text::first-letter {
            font-size: 3em;
            float: left;
            line-height: 0.8;
            margin-right: 0.1em;
            color: #d4af37;
        }
        
        .image-comparison {
            position: relative;
            overflow: hidden;
        }
        
        .image-comparison img {
            transition: transform 0.5s, filter 0.5s;
        }
        
        .image-comparison:hover img {
            transform: scale(1.05);
        }
        
        .warburg-photo {
            filter: grayscale(100%) sepia(0.3) contrast(1.2);
            transition: filter 0.5s;
        }
        
        .warburg-photo:hover {
            filter: grayscale(0%) sepia(0) contrast(1.1);
        }
    </style>
</head>
<body class="antialiased">

<div class="grain"></div>

<!-- Navigation -->
<nav class="fixed top-0 w-full z-40 bg-black/80 backdrop-blur-md border-b border-white/10">
    <div class="max-w-7xl mx-auto px-6 py-4 flex justify-between items-center">
        <div class="text-2xl serif italic text-amber-500">Warburg</div>
        <div class="flex gap-8 text-sm tracking-widest uppercase">
            <a href="#supervivencia" class="hover:text-amber-500 transition-colors">Supervivencia</a>
            <a href="#pathos" class="hover:text-amber-500 transition-colors">Pathosformel</a>
            <a href="#mnemosyne" class="hover:text-amber-500 transition-colors">Mnemosyne</a>
            <a href="#dialectica" class="hover:text-amber-500 transition-colors">Dialéctica</a>
        </div>
    </div>
</nav>

<!-- Hero Section -->
<section class="relative min-h-screen flex items-center justify-center overflow-hidden">
    <div class="absolute inset-0 z-0">
        <div id="constellation-bg" class="absolute inset-0"></div>
    </div>
    
    <div class="relative z-10 text-center px-6 max-w-5xl mx-auto">
        <h1 class="serif text-6xl md:text-8xl mb-6 leading-tight">
            <span class="block text-transparent bg-clip-text bg-gradient-to-r from-amber-200 via-amber-500 to-amber-700">
                La Migración
            </span>
            <span class="block text-4xl md:text-6xl mt-4 text-gray-400 italic">
                de los Motivos
            </span>
        </h1>
        <p class="text-xl md:text-2xl text-gray-400 max-w-2xl mx-auto leading-relaxed mt-8">
            Aby Warburg (1866-1929) y la <span class="text-amber-500">supervivencia de la imagen antigua</span> 
            en la memoria cultural del Occidente
        </p>
        
        <!-- Warburg Portrait -->
        <div class="mt-12 flex justify-center">
            <div class="relative w-48 h-48 rounded-full overflow-hidden border-2 border-amber-500/30 warburg-photo">
                <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/e/e8/Aby_Warburg.jpg/440px-Aby_Warburg.jpg" 
                     alt="Aby Warburg" 
                     class="w-full h-full object-cover">
            </div>
        </div>
        <p class="mt-4 text-sm text-gray-500">Aby Warburg en la Biblioteca Kulturwissenschaftliche</p>
        
        <div class="mt-8 flex justify-center gap-4">
            <button onclick="scrollToSection('supervivencia')" class="px-8 py-3 border border-amber-500/50 text-amber-500 hover:bg-amber-500/10 transition-all rounded-full">
                Explorar Teoría
            </button>
        </div>
    </div>
</section>

<!-- Sección 1: Supervivencia (Nachleben) -->
<section id="supervivencia" class="relative py-32 px-6 bg-gradient-to-b from-black to-gray-900">
    <div class="max-w-7xl mx-auto">
        <div class="grid md:grid-cols-2 gap-16 items-center">
            <div>
                <h2 class="serif text-5xl mb-6 text-amber-500">Nachleben</h2>
                <h3 class="text-2xl mb-8 text-gray-300">La Supervivencia de lo Antiguo</h3>
                <div class="space-y-6 text-gray-400 leading-relaxed">
                    <p class="ekphrasis-text text-lg">
                        Warburg rechazaba la idea de que el Renacimiento fuera un "renacimiento" súbito. 
                        Para él, lo antiguo nunca muere completamente: <span class="text-amber-400">sobrevive</span>, 
                        se transforma, migra a través del tiempo como un fantasma cultural.
                    </p>
                    <p>
                        El término alemán <em>Nachleben</em> (supervivencia) implica una continuidad espectral: 
                        los dioses paganos no desaparecen, se vuelven invisibles, demoníacos, o se funden 
                        en la iconografía cristiana.
                    </p>
                </div>
                
                <div class="mt-8 p-6 pathos-formula rounded-lg">
                    <div class="flex items-center gap-4 mb-4">
                        <div class="w-3 h-3 bg-amber-500 rounded-full survival-glow"></div>
                        <span class="text-amber-500 font-semibold tracking-wider">EJEMPLO: La Ninfa</span>
                    </div>
                    <p class="text-sm text-gray-400">
                        Desde las figuras en movimiento de Ghirlandaio hasta las fotografías de la 
                        bailarina Maud Allan (1900), el motivo de la ninfa persiste como 
                        <span class="text-white">fórmula de pathos</span>.
                    </p>
                </div>
            </div>
            
            <div class="relative">
                <!-- Image Comparison: Ancient vs Renaissance -->
                <div class="space-y-6">
                    <div class="image-comparison group relative overflow-hidden rounded-lg border border-amber-500/20">
                        <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/5/57/Nike_of_Samothrake_Louvre_Ma2369_n4.jpg/600px-Nike_of_Samothrake_Louvre_Ma2369_n4.jpg" 
                             alt="Victoria de Samotracia" 
                             class="w-full h-64 object-cover">
                        <div class="absolute bottom-0 left-0 right-0 bg-gradient-to-t from-black to-transparent p-4">
                            <p class="text-amber-400 font-bold">Victoria de Samotracia (190 a.C.)</p>
                            <p class="text-xs text-gray-300">El movimiento congelado, la ropa mojada adherida al cuerpo</p>
                        </div>
                    </div>
                    
                    <div class="flex justify-center">
                        <svg class="w-8 h-8 text-amber-500 animate-bounce" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 14l-7 7m0 0l-7-7m7 7V3"></path>
                        </svg>
                    </div>
                    
                    <div class="image-comparison group relative overflow-hidden rounded-lg border border-amber-500/20">
                        <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/0/0b/Sandro_Botticelli_-_La_nascita_di_Venere_-_Google_Art_Project_-_edited.jpg/800px-Sandro_Botticelli_-_La_nascita_di_Venere_-_Google_Art_Project_-_edited.jpg" 
                             alt="Nacimiento de Venus" 
                             class="w-full h-64 object-cover">
                        <div class="absolute bottom-0 left-0 right-0 bg-gradient-to-t from-black to-transparent p-4">
                            <p class="text-amber-400 font-bold">Botticelli, Nacimiento de Venus (1485)</p>
                            <p class="text-xs text-gray-300">La ninfa/Zéfiro soplando, el mismo movimiento del viento en las telas</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        
        <!-- Migration Timeline with Images -->
        <div class="mt-20 relative">
            <h4 class="text-center text-2xl serif text-amber-500 mb-12">La Migración del Motivo</h4>
            <div class="grid md:grid-cols-3 gap-8">
                <div class="text-center group cursor-pointer" onclick="showDetail('antique')">
                    <div class="relative h-48 mb-4 overflow-hidden rounded-lg border border-amber-500/30">
                        <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/3/3f/Dionysos_sarcophagus_Louvre_Ma_1017.jpg/600px-Dionysos_sarcophagus_Louvre_Ma_1017.jpg" 
                             alt="Sarcófago de Dioniso" 
                             class="w-full h-full object-cover transform group-hover:scale-110 transition-transform duration-700">
                    </div>
                    <h5 class="text-amber-400 font-bold">Antigüedad</h5>
                    <p class="text-xs text-gray-500 mt-2">Sarcófagos romanos, ritos dionisíacos</p>
                </div>
                
                <div class="text-center group cursor-pointer" onclick="showDetail('renaissance')">
                    <div class="relative h-48 mb-4 overflow-hidden rounded-lg border border-amber-500/30">
                        <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/3/3c/Botticelli-primavera.jpg/800px-Botticelli-primavera.jpg" 
                             alt="Primavera de Botticelli" 
                             class="w-full h-full object-cover transform group-hover:scale-110 transition-transform duration-700">
                    </div>
                    <h5 class="text-amber-400 font-bold">Renacimiento</h5>
                    <p class="text-xs text-gray-500 mt-2">Florencia, 1480s. La Primavera</p>
                </div>
                
                <div class="text-center group cursor-pointer" onclick="showDetail('modern')">
                    <div class="relative h-48 mb-4 overflow-hidden rounded-lg border border-amber-500/30">
                        <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/8/86/Muybridge_race_horse_gallop.jpg/800px-Muybridge_race_horse_gallop.jpg" 
                             alt="Muybridge" 
                             class="w-full h-full object-cover transform group-hover:scale-110 transition-transform duration-700">
                    </div>
                    <h5 class="text-amber-400 font-bold">Modernidad</h5>
                    <p class="text-xs text-gray-500 mt-2">Muybridge, cronofotografía</p>
                </div>
            </div>
        </div>
    </div>
</section>

<!-- Sección 2: Pathosformel -->
<section id="pathos" class="relative py-32 px-6 bg-black overflow-hidden">
    <div class="max-w-7xl mx-auto">
        <div class="text-center mb-20">
            <h2 class="serif text-6xl mb-4 text-amber-500">Pathosformel</h2>
            <p class="text-xl text-gray-400 max-w-2xl mx-auto">
                La "fórmula de la emoción" — gestos extremos que migran a través de la historia del arte, 
                portadores de energía afectiva
            </p>
        </div>
        
        <div class="grid md:grid-cols-3 gap-8">
            <!-- Formula 1: The Clutch -->
            <div class="group relative h-[500px] pathos-formula rounded-lg overflow-hidden cursor-pointer" onclick="activateFormula(1)">
                <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/5/57/Nike_of_Samothrake_Louvre_Ma2369_n4.jpg/600px-Nike_of_Samothrake_Louvre_Ma2369_n4.jpg" 
                     alt="Victoria de Samotracia - detalle" 
                     class="absolute inset-0 w-full h-full object-cover opacity-60 group-hover:opacity-40 transition-opacity">
                <div class="absolute inset-0 bg-gradient-to-t from-black via-transparent to-transparent z-10"></div>
                <div class="absolute bottom-0 left-0 right-0 p-6 z-20">
                    <h3 class="text-2xl serif text-amber-400 mb-2">El Agarre</h3>
                    <p class="text-sm text-gray-300">La ropa mojada adherida al cuerpo en movimiento</p>
                </div>
                <div class="formula-detail hidden absolute inset-0 bg-black/95 p-8 flex flex-col justify-center z-30 overflow-y-auto">
                    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/0/0b/Sandro_Botticelli_-_La_nascita_di_Venere_-_Google_Art_Project_-_edited.jpg/400px-Sandro_Botticelli_-_La_nascita_di_Venere_-_Google_Art_Project_-_edited.jpg" 
                         class="w-full h-32 object-cover rounded mb-4" alt="Comparación">
                    <h4 class="text-amber-500 text-xl mb-4">El gesto del vértigo</h4>
                    <p class="text-gray-300 mb-4 text-sm">Warburg identificó cómo el gesto de las telas agitadas por el viento, de la ropa que se adhiere al cuerpo en movimiento (como en la Victoria de Samotracia), se convierte en una fórmula de éxtasis y angustia que reaparece en el Renacimiento.</p>
                    <button onclick="event.stopPropagation(); closeFormula(1)" class="text-amber-500 text-sm underline">Cerrar</button>
                </div>
            </div>
            
            <!-- Formula 2: The Turn -->
            <div class="group relative h-[500px] pathos-formula rounded-lg overflow-hidden cursor-pointer" onclick="activateFormula(2)">
                <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/a/a7/Domenico_Ghirlandaio_-_Birth_of_St_John_the_Baptist_-_WGA08839.jpg/600px-Domenico_Ghirlandaio_-_Birth_of_St_John_the_Baptist_-_WGA08839.jpg" 
                     alt="Ghirlandaio - Nacimiento de San Juan Bautista" 
                     class="absolute inset-0 w-full h-full object-cover opacity-60 group-hover:opacity-40 transition-opacity">
                <div class="absolute inset-0 bg-gradient-to-t from-black via-transparent to-transparent z-10"></div>
                <div class="absolute bottom-0 left-0 right-0 p-6 z-20">
                    <h3 class="text-2xl serif text-amber-400 mb-2">La Entrada</h3>
                    <p class="text-sm text-gray-300">La "ninfa" en el fresco de Ghirlandaio</p>
                </div>
                <div class="formula-detail hidden absolute inset-0 bg-black/95 p-8 flex flex-col justify-center z-30 overflow-y-auto">
                    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/2/2e/Maud_Allan_-_Salome.jpg/400px-Maud_Allan_-_Salome.jpg" 
                         class="w-full h-32 object-cover rounded mb-4" alt="Maud Allan">
                    <h4 class="text-amber-500 text-xl mb-4">La Ninfa Moderna</h4>
                    <p class="text-gray-300 mb-4 text-sm">Warburg rastreó la figura de la "ninfa" desde los frescos florentinos hasta la bailarina Maud Allan (1900), mostrando cómo el mismo gesto de movimiento persiste a través de los siglos.</p>
                    <button onclick="event.stopPropagation(); closeFormula(2)" class="text-amber-500 text-sm underline">Cerrar</button>
                </div>
            </div>
            
            <!-- Formula 3: The Gaze -->
            <div class="group relative h-[500px] pathos-formula rounded-lg overflow-hidden cursor-pointer" onclick="activateFormula(3)">
                <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/c/c5/Edvard_Munch%2C_1893%2C_The_Scream%2C_oil%2C_tempera_and_pastel_on_cardboard%2C_91_x_73_cm%2C_National_Gallery_of_Norway.jpg/450px-Edvard_Munch%2C_1893%2C_The_Scream%2C_oil%2C_tempera_and_pastel_on_cardboard%2C_91_x_73_cm%2C_National_Gallery_of_Norway.jpg" 
                     alt="El Grito de Munch" 
                     class="absolute inset-0 w-full h-full object-cover opacity-60 group-hover:opacity-40 transition-opacity">
                <div class="absolute inset-0 bg-gradient-to-t from-black via-transparent to-transparent z-10"></div>
                <div class="absolute bottom-0 left-0 right-0 p-6 z-20">
                    <h3 class="text-2xl serif text-amber-400 mb-2">El Grito</h3>
                    <p class="text-sm text-gray-300">El pathos extremo en la modernidad</p>
                </div>
                <div class="formula-detail hidden absolute inset-0 bg-black/95 p-8 flex flex-col justify-center z-30 overflow-y-auto">
                    <div class="grid grid-cols-2 gap-2 mb-4">
                        <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/6/6a/Laocoön_and_His_Sons.jpg/300px-Laocoön_and_His_Sons.jpg" 
                             class="w-full h-24 object-cover rounded" alt="Laocoonte">
                        <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/c/c5/Edvard_Munch%2C_1893%2C_The_Scream%2C_oil%2C_tempera_and_pastel_on_cardboard%2C_91_x_73_cm%2C_National_Gallery_of_Norway.jpg/225px-Edvard_Munch%2C_1893%2C_The_Scream%2C_oil%2C_tempera_and_pastel_on_cardboard%2C_91_x_73_cm%2C_National_Gallery_of_Norway.jpg" 
                             class="w-full h-24 object-cover rounded" alt="El Grito">
                    </div>
                    <h4 class="text-amber-500 text-xl mb-4">De Laocoonte al Grito</h4>
                    <p class="text-gray-300 mb-4 text-sm">La mirada fija, los ojos desorbitados, aparecen en momentos de revelación. Warburg relacionó esto con la teoría de la empatía (Einfühlung) y la proyección psíquica, desde la escultura helenística hasta el Expresionismo.</p>
                    <button onclick="event.stopPropagation(); closeFormula(3)" class="text-amber-500 text-sm underline">Cerrar</button>
                </div>
            </div>
        </div>
    </div>
</section>

<!-- Sección 3: Mnemosyne Atlas -->
<section id="mnemosyne" class="relative py-32 px-6 bg-gray-900">
    <div class="max-w-7xl mx-auto">
        <div class="mb-16">
            <h2 class="serif text-6xl mb-6 text-amber-500">Mnemosyne Atlas</h2>
            <p class="text-xl text-gray-400 max-w-3xl">
                El proyecto final de Warburg: 79 paneles cubiertos con fotografías de obras de arte, 
                mapas, textos, dispuestos no cronológicamente sino <span class="text-amber-400">constelacionalmente</span>.
            </p>
        </div>
        
        <!-- Atlas Panel Recreation -->
        <div class="relative bg-black/50 rounded-2xl p-8 border border-white/10 mb-12">
            <div class="grid grid-cols-2 md:grid-cols-4 gap-4" id="atlas-grid">
                <!-- Atlas items with real images -->
                <div class="atlas-item aspect-[3/4] rounded-lg cursor-pointer relative group" onclick="highlightConnections(0)">
                    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/5/57/Nike_of_Samothrake_Louvre_Ma2369_n4.jpg/300px-Nike_of_Samothrake_Louvre_Ma2369_n4.jpg" 
                         alt="Victoria" class="absolute inset-0 w-full h-full object-cover rounded-lg">
                    <div class="absolute inset-0 bg-black/60 opacity-0 group-hover:opacity-100 transition-opacity flex items-center justify-center">
                        <span class="text-amber-500 text-xs text-center px-2">Victoria de Samotracia</span>
                    </div>
                </div>
                
                <div class="atlas-item aspect-[3/4] rounded-lg cursor-pointer relative group" onclick="highlightConnections(1)">
                    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/3/3c/Botticelli-primavera.jpg/300px-Botticelli-primavera.jpg" 
                         alt="Primavera" class="absolute inset-0 w-full h-full object-cover rounded-lg">
                    <div class="absolute inset-0 bg-black/60 opacity-0 group-hover:opacity-100 transition-opacity flex items-center justify-center">
                        <span class="text-amber-500 text-xs text-center px-2">La Primavera</span>
                    </div>
                </div>
                
                <div class="atlas-item aspect-[3/4] rounded-lg cursor-pointer relative group" onclick="highlightConnections(2)">
                    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/a/a7/Domenico_Ghirlandaio_-_Birth_of_St_John_the_Baptist_-_WGA08839.jpg/300px-Domenico_Ghirlandaio_-_Birth_of_St_John_the_Baptist_-_WGA08839.jpg" 
                         alt="Ghirlandaio" class="absolute inset-0 w-full h-full object-cover rounded-lg">
                    <div class="absolute inset-0 bg-black/60 opacity-0 group-hover:opacity-100 transition-opacity flex items-center justify-center">
                        <span class="text-amber-500 text-xs text-center px-2">Ghirlandaio</span>
                    </div>
                </div>
                
                <div class="atlas-item aspect-[3/4] rounded-lg cursor-pointer relative group" onclick="highlightConnections(3)">
                    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/6/6a/Laocoön_and_His_Sons.jpg/300px-Laocoön_and_His_Sons.jpg" 
                         alt="Laocoonte" class="absolute inset-0 w-full h-full object-cover rounded-lg">
                    <div class="absolute inset-0 bg-black/60 opacity-0 group-hover:opacity-100 transition-opacity flex items-center justify-center">
                        <span class="text-amber-500 text-xs text-center px-2">Laocoonte</span>
                    </div>
                </div>
                
                <div class="atlas-item aspect-[3/4] rounded-lg cursor-pointer relative group" onclick="highlightConnections(4)">
                    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/8/86/Muybridge_race_horse_gallop.jpg/300px-Muybridge_race_horse_gallop.jpg" 
                         alt="Muybridge" class="absolute inset-0 w-full h-full object-cover rounded-lg">
                    <div class="absolute inset-0 bg-black/60 opacity-0 group-hover:opacity-100 transition-opacity flex items-center justify-center">
                        <span class="text-amber-500 text-xs text-center px-2">Muybridge</span>
                    </div>
                </div>
                
                <div class="atlas-item aspect-[3/4] rounded-lg cursor-pointer relative group" onclick="highlightConnections(5)">
                    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/c/c5/Edvard_Munch%2C_1893%2C_The_Scream%2C_oil%2C_tempera_and_pastel_on_cardboard%2C_91_x_73_cm%2C_National_Gallery_of_Norway.jpg/225px-Edvard_Munch%2C_1893%2C_The_Scream%2C_oil%2C_tempera_and_pastel_on_cardboard%2C_91_x_73_cm%2C_National_Gallery_of_Norway.jpg" 
                         alt="Munch" class="absolute inset-0 w-full h-full object-cover rounded-lg">
                    <div class="absolute inset-0 bg-black/60 opacity-0 group-hover:opacity-100 transition-opacity flex items-center justify-center">
                        <span class="text-amber-500 text-xs text-center px-2">Munch</span>
                    </div>
                </div>
                
                <div class="atlas-item aspect-[3/4] rounded-lg cursor-pointer relative group" onclick="highlightConnections(6)">
                    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/0/0b/Sandro_Botticelli_-_La_nascita_di_Venere_-_Google_Art_Project_-_edited.jpg/300px-Sandro_Botticelli_-_La_nascita_di_Venere_-_Google_Art_Project_-_edited.jpg" 
                         alt="Venus" class="absolute inset-0 w-full h-full object-cover rounded-lg">
                    <div class="absolute inset-0 bg-black/60 opacity-0 group-hover:opacity-100 transition-opacity flex items-center justify-center">
                        <span class="text-amber-500 text-xs text-center px-2">Venus</span>
                    </div>
                </div>
                
                <div class="atlas-item aspect-[3/4] rounded-lg cursor-pointer relative group" onclick="highlightConnections(7)">
                    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/2/2e/Maud_Allan_-_Salome.jpg/200px-Maud_Allan_-_Salome.jpg" 
                         alt="Maud Allan" class="absolute inset-0 w-full h-full object-cover rounded-lg">
                    <div class="absolute inset-0 bg-black/60 opacity-0 group-hover:opacity-100 transition-opacity flex items-center justify-center">
                        <span class="text-amber-500 text-xs text-center px-2">Maud Allan</span>
                    </div>
                </div>
            </div>
            
            <!-- Constellation Overlay -->
            <svg class="absolute inset-0 w-full h-full pointer-events-none" id="constellation-svg" style="z-index: 10;">
                <!-- Lines will be drawn here -->
            </svg>
        </div>
        
        <!-- Real Atlas Panel Photo -->
        <div class="mt-12 grid md:grid-cols-2 gap-8 items-center">
            <div>
                <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/a/a6/Warburg_Mnemosyne_Atlas_Plate_46.jpg/800px-Warburg_Mnemosyne_Atlas_Plate_46.jpg" 
                     alt="Mnemosyne Atlas Panel 46" 
                     class="w-full rounded-lg border border-amber-500/30 shadow-2xl">
                <p class="text-xs text-gray-500 mt-2 text-center">Panel 46 del Atlas Mnemosyne (c. 1929)</p>
            </div>
            <div class="space-y-4">
                <h4 class="text-2xl serif text-amber-500">El Método Constelacional</h4>
                <p class="text-gray-400 leading-relaxed">
                    Warburg no buscaba una historia lineal del arte, sino <span class="text-white">constelaciones de sentido</span>. 
                    Las imágenes se agrupan por afinidades electivas, no por cronología. Un sarcófago romano puede 
                    dialogar con una fotografía de 1900 si comparten la misma <em>Pathosformel</em>.
                </p>
                <p class="text-gray-400 leading-relaxed">
                    El atlas era un "laboratorio de la memoria cultural" donde el espectador debía 
                    completar las conexiones, activando su propia memoria de las imágenes.
                </p>
            </div>
        </div>
        
        <div class="mt-8 text-center">
            <p class="text-sm text-gray-500 italic">
                Haz clic en las imágenes de arriba para ver las conexiones invisibles. 
                Warburg buscaba "espacios de pensamiento" (Denkräume) más allá de la historia lineal.
            </p>
        </div>
    </div>
</section>

<!-- Sección 4: Dialéctica -->
<section id="dialectica" class="relative py-32 px-6 bg-black">
    <div class="max-w-6xl mx-auto">
        <h2 class="serif text-5xl mb-12 text-amber-500 text-center">La Dialéctica del Monstruo</h2>
        
        <div class="grid md:grid-cols-2 gap-12 items-center mb-16">
            <div class="space-y-6">
                <div class="relative overflow-hidden rounded-lg border border-amber-500/20">
                    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/6/6b/Raffael_058.jpg/600px-Raffael_058.jpg" 
                         alt="Rafael - Escuela de Atenas" 
                         class="w-full h-64 object-cover hover:scale-105 transition-transform duration-700">
                    <div class="absolute bottom-0 left-0 right-0 bg-gradient-to-t from-black to-transparent p-4">
                        <p class="text-amber-400 font-bold">Lo Apolíneo: Orden y Medida</p>
                    </div>
                </div>
                <p class="text-gray-400 text-sm">
                    Rafael, <em>Escuela de Atenas</em>. La claridad, la forma ideal, la distancia contemplativa.
                </p>
            </div>
            
            <div class="space-y-6">
                <div class="relative overflow-hidden rounded-lg border border-amber-500/20">
                    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/6/6a/Laocoön_and_His_Sons.jpg/600px-Laocoön_and_His_Sons.jpg" 
                         alt="Laocoonte" 
                         class="w-full h-64 object-cover hover:scale-105 transition-transform duration-700">
                    <div class="absolute bottom-0 left-0 right-0 bg-gradient-to-t from-black to-transparent p-4">
                        <p class="text-amber-400 font-bold">Lo Dionisíaco: Pathos y Caos</p>
                    </div>
                </div>
                <p class="text-gray-400 text-sm">
                    <em>Laocoonte</em>. El sufrimiento extremo, la contorsión, la pérdida de la forma en el éxtasis.
                </p>
            </div>
        </div>
        
        <div class="prose prose-invert mx-auto text-gray-400 max-w-3xl text-center">
            <p class="text-lg leading-relaxed">
                Warburg no buscaba resolver esta tensión, sino <span class="text-amber-400">mantenerla viva</span>. 
                La cultura occidental oscila entre el deseo de orden (la figura serena) y la necesidad 
                de expresión emocional (el gesto extremo). El "monstruo" es la imagen que habita 
                en el intersticio: ni completamente domada ni completamente salvaje.
            </p>
        </div>
        
        <!-- Biblioteca Warburg -->
        <div class="mt-16 grid md:grid-cols-2 gap-8 items-center">
            <div class="order-2 md:order-1 space-y-4">
                <h4 class="text-2xl serif text-amber-500">La Biblioteca Warburg</h4>
                <p class="text-gray-400 leading-relaxed">
                    Fundada en Hamburgo (ahora en Londres), la <em>Kulturwissenschaftliche Bibliothek Warburg</em> 
                    organizaba los libros no por materia o autor, sino por "caminos del pensamiento" (Denkwege). 
                    Warburg creía que los libros, como las imágenes, debían dialogar entre sí.
                </p>
                <div class="border-l-2 border-amber-500/30 pl-6 mt-6">
                    <p class="text-sm text-gray-500 italic">
                        "El dios está en los detalles" — Aby Warburg
                    </p>
                </div>
            </div>
            <div class="order-1 md:order-2">
                <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/e/e8/Aby_Warburg.jpg/440px-Aby_Warburg.jpg" 
                     alt="Aby Warburg retrato" 
                     class="w-full max-w-md mx-auto rounded-lg border border-amber-500/30 warburg-photo">
            </div>
        </div>
    </div>
</section>

<!-- Footer -->
<footer class="bg-black border-t border-white/10 py-12 px-6">
    <div class="max-w-7xl mx-auto text-center">
        <p class="serif text-2xl text-amber-500/50 italic mb-4">
            "El dios en el detalle"
        </p>
        <p class="text-gray-600 text-sm">
            Aby Warburg (1866-1929) — Mnemosyne Atlas
        </p>
        <div class="mt-8 flex justify-center gap-4 text-xs text-gray-700">
            <span>Victoria de Samotracia</span>
            <span>•</span>
            <span>Botticelli</span>
            <span>•</span>
            <span>Ghirlandaio</span>
            <span>•</span>
            <span>Muybridge</span>
            <span>•</span>
            <span>Munch</span>
        </div>
    </div>
</footer>

<script>
    // Scroll function
    function scrollToSection(id) {
        document.getElementById(id).scrollIntoView({ behavior: 'smooth' });
    }
    
    // Pathos Formula Interaction
    function activateFormula(id) {
        document.querySelectorAll('.formula-detail').forEach(el => el.classList.add('hidden'));
        document.getElementById(`formula-${id}`).classList.remove('hidden');
    }
    
    function closeFormula(id) {
        document.getElementById(`formula-${id}`).classList.add('hidden');
    }
    
    // Mnemosyne Atlas Constellation Effect
    const constellationSvg = document.getElementById('constellation-svg');
    let activeConnections = [];
    
    function highlightConnections(activeIndex) {
        // Clear previous lines
        constellationSvg.innerHTML = '';
        
        // Get all atlas items
        const items = document.querySelectorAll('.atlas-item');
        const activeItem = items[activeIndex];
        const rect = activeItem.getBoundingClientRect();
        const containerRect = document.getElementById('atlas-grid').getBoundingClientRect();
        
        const x1 = rect.left + rect.width / 2 - containerRect.left;
        const y1 = rect.top + rect.height / 2 - containerRect.top;
        
        // Define meaningful connections based on Warburg's actual associations
        const connections = {
            0: [1, 3, 6], // Victoria -> Primavera, Laocoonte, Venus
            1: [0, 6, 2], // Primavera -> Victoria, Venus, Ghirlandaio
            2: [1, 7],    // Ghirlandaio -> Primavera, Maud Allan
            3: [0, 5],    // Laocoonte -> Victoria, Munch
            4: [7],       // Muybridge -> Maud Allan
            5: [3],       // Munch -> Laocoonte
            6: [0, 1],    // Venus -> Victoria, Primavera
            7: [2, 4]     // Maud Allan -> Ghirlandaio, Muybridge
        };
        
        const targets = connections[activeIndex] || [];
        
        targets.forEach(targetIndex => {
            if (targetIndex < items.length) {
                const targetItem = items[targetIndex];
                const targetRect = targetItem.getBoundingClientRect();
                const x2 = targetRect.left + targetRect.width / 2 - containerRect.left;
                const y2 = targetRect.top + targetRect.height / 2 - containerRect.top;
                
                const line = document.createElementNS('http://www.w3.org/2000/svg', 'line');
                line.setAttribute('x1', x1);
                line.setAttribute('y1', y1);
                line.setAttribute('x2', x2);
                line.setAttribute('y2', y2);
                line.setAttribute('stroke', '#d4af37');
                line.setAttribute('stroke-width', '2');
                line.setAttribute('opacity', '0.8');
                line.classList.add('memory-trace');
                
                constellationSvg.appendChild(line);
            }
        });
    }
    
    // Background Constellation Animation
    const canvas = document.createElement('canvas');
    const ctx = canvas.getContext('2d');
    document.getElementById('constellation-bg').appendChild(canvas);
    
    let width, height;
    let particles = [];
    
    function resize() {
        width = canvas.width = window.innerWidth;
        height = canvas.height = window.innerHeight;
    }
    
    class Particle {
        constructor() {
            this.x = Math.random() * width;
            this.y = Math.random() * height;
            this.vx = (Math.random() - 0.5) * 0.5;
            this.vy = (Math.random() - 0.5) * 0.5;
            this.size = Math.random() * 2;
        }
        
        update() {
            this.x += this.vx;
            this.y += this.vy;
            
            if (this.x < 0 || this.x > width) this.vx *= -1;
            if (this.y < 0 || this.y > height) this.vy *= -1;
        }
        
        draw() {
            ctx.fillStyle = 'rgba(212, 175, 55, 0.5)';
            ctx.beginPath();
            ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
            ctx.fill();
        }
    }
    
    function init() {
        resize();
        for (let i = 0; i < 100; i++) {
            particles.push(new Particle());
        }
    }
    
    function animate() {
        ctx.clearRect(0, 0, width, height);
        
        particles.forEach((p, index) => {
            p.update();
            p.draw();
            
            // Connect nearby particles
            for (let j = index + 1; j < particles.length; j++) {
                const p2 = particles[j];
                const dx = p.x - p2.x;
                const dy = p.y - p2.y;
                const distance = Math.sqrt(dx * dx + dy * dy);
                
                if (distance < 150) {
                    ctx.beginPath();
                    ctx.strokeStyle = `rgba(212, 175, 55, ${0.2 * (1 - distance / 150)})`;
                    ctx.lineWidth = 0.5;
                    ctx.moveTo(p.x, p.y);
                    ctx.lineTo(p2.x, p2.y);
                    ctx.stroke();
                }
            }
        });
        
        requestAnimationFrame(animate);
    }
    
    window.addEventListener('resize', () => {
        resize();
        // Recalculate constellation on resize
        constellationSvg.innerHTML = '';
    });
    
    init();
    animate();
    
    // Intersection Observer for scroll animations
    const observerOptions = {
        threshold: 0.1,
        rootMargin: '0px 0px -100px 0px'
    };
    
    const observer = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
            if (entry.isIntersecting) {
                entry.target.style.opacity = '1';
                entry.target.style.transform = 'translateY(0)';
            }
        });
    }, observerOptions);
    
    document.querySelectorAll('section').forEach(section => {
        section.style.opacity = '0';
        section.style.transform = 'translateY(50px)';
        section.style.transition = 'all 1s ease-out';
        observer.observe(section);
    });
</script>

</body>
</html>

