# AlIster
una ia XD
ul, .prose-ai ol {
            margin-left: 1.25rem<!DOCTYPE html>
<html lang="es" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="theme-color" content="#09090b">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <meta name="apple-mobile-web-app-title" content="AlIster">
    <title>AlIster</title>
    
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    
    <!-- Google Fonts: Inter -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    
    <!-- Font Awesome para iconos limpios y modernos -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <!-- Marked.js para renderizar Markdown de las respuestas de la IA -->
    <script src="https://cdn.jsdelivr.net/npm/marked/marked.min.js"></script>

    <!-- Configuración personalizada de Tailwind -->
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                    },
                    colors: {
                        dark: {
                            950: '#09090b', // Fondo principal ultra oscuro (Zinc 950)
                            900: '#121215', // Fondo de tarjetas / sidebar
                            800: '#1c1c21', // Elementos interactivos / burbujas
                            700: '#27272e', // Bordes sutiles
                        },
                        accent: {
                            500: '#6366f1', // Indigo vibrante
                            600: '#4f46e5',
                            glow: 'rgba(99, 102, 241, 0.15)'
                        }
                    },
                    animation: {
                        'fade-in': 'fadeIn 0.3s ease-out forwards',
                        'pulse-slow': 'pulse 3s cubic-bezier(0.4, 0, 0.6, 1) infinite',
                    },
                    keyframes: {
                        fadeIn: {
                            '0%': { opacity: '0', transform: 'translateY(8px)' },
                            '100%': { opacity: '1', transform: 'translateY(0)' },
                        }
                    }
                }
            }
        }
    </script>

    <style>
        /* Estilos personalizados para scrollbars y formato Markdown */
        body {
            background-color: #09090b;
            color: #f4f4f5;
            -webkit-font-smoothing: antialiased;
        }

        /* Scrollbar minimalista */
        ::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        ::-webkit-scrollbar-track {
            background: transparent;
        }
        ::-webkit-scrollbar-thumb {
            background: #27272e;
            border-radius: 9999px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #3f3f46;
        }

        /* Estilos para el contenido Markdown generado por la IA */
        .prose-ai p {
            margin-bottom: 0.75rem;
            line-height: 1.65;
        }
        .prose-ai p:last-child {
            margin-bottom: 0;
        }
        .prose-ai ;
            margin-bottom: 0.75rem;
        }
        .prose-ai ul {
            list-style-type: disc;
        }
        .prose-ai ol {
            list-style-type: decimal;
        }
        .prose-ai li {
            margin-bottom: 0.25rem;
            line-height: 1.6;
        }
        .prose-ai strong {
            color: #ffffff;
            font-weight: 600;
        }
        .prose-ai h1, .prose-ai h2, .prose-ai h3 {
            color: #ffffff;
            font-weight: 600;
            margin-top: 1rem;
            margin-bottom: 0.5rem;
        }
        .prose-ai h3 { font-size: 1.1rem; }
        .prose-ai code {
            background-color: #27272e;
            color: #e4e4e7;
            padding: 0.15rem 0.4rem;
            border-radius: 0.375rem;
            font-size: 0.875em;
            font-family: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, monospace;
        }
        .prose-ai pre {
            background-color: #09090b;
            border: 1px solid #27272e;
            padding: 0.875rem;
            border-radius: 0.75rem;
            overflow-x: auto;
            margin-top: 0.5rem;
            margin-bottom: 0.75rem;
        }
        .prose-ai pre code {
            background-color: transparent;
            padding: 0;
            color: #a5b4fc;
        }
        .prose-ai blockquote {
            border-left: 3px solid #6366f1;
            padding-left: 0.875rem;
            color: #a1a1aa;
            font-style: italic;
            margin: 0.75rem 0;
        }

        /* Animación de puntos escribiendo */
        .typing-dot {
            animation: typingBounce 1.4s infinite ease-in-out both;
        }
        .typing-dot:nth-child(1) { animation-delay: -0.32s; }
        .typing-dot:nth-child(2) { animation-delay: -0.16s; }
        @keyframes typingBounce {
            0%, 80%, 100% { transform: scale(0); opacity: 0.4; }
            40% { transform: scale(1); opacity: 1; }
        }

        /* Animación de ondas para modo escucha activa */
        @keyframes voiceRing {
            0% { transform: scale(0.95); box-shadow: 0 0 0 0 rgba(99, 102, 241, 0.65); }
            70% { transform: scale(1); box-shadow: 0 0 0 12px rgba(99, 102, 241, 0); }
            100% { transform: scale(0.95); box-shadow: 0 0 0 0 rgba(99, 102, 241, 0); }
        }
        .voice-listening {
            animation: voiceRing 1.8s infinite;
        }
    </style>
</head>
<body class="h-screen w-full overflow-hidden flex flex-col md:flex-row bg-dark-950 text-zinc-100 selection:bg-indigo-500/30 selection:text-indigo-200">

    <!-- Notificación Toast Flotante (Reemplaza cualquier alert/confirm) -->
    <div id="toast-container" class="fixed top-5 right-5 z-50 flex flex-col gap-2 pointer-events-none"></div>

    <!-- Modal de Instrucciones para Instalar App (PC y Celular) -->
    <div id="install-modal" class="fixed inset-0 z-50 hidden items-center justify-center bg-black/75 backdrop-blur-sm p-4">
        <div class="bg-dark-900 border border-dark-700 rounded-2xl max-w-md w-full p-6 shadow-2xl animate-fade-in">
            <div class="flex items-center gap-3 mb-4">
                <div class="w-11 h-11 rounded-2xl bg-gradient-to-br from-indigo-500 to-purple-600 flex items-center justify-center text-white shadow-lg shadow-indigo-500/20">
                    <i class="fa-solid fa-mobile-screen-button text-lg"></i>
                </div>
                <div>
                    <h3 class="text-lg font-bold text-zinc-100">Instalar AlIster como App</h3>
                    <p class="text-xs text-zinc-400">Acceso directo en PC, Android e iPhone</p>
                </div>
            </div>
            
            <div class="space-y-3 text-xs text-zinc-300 mb-6">
                <div class="p-3.5 rounded-xl bg-dark-950/80 border border-dark-700/80">
                    <p class="font-semibold text-indigo-400 mb-1 flex items-center gap-1.5">
                        <i class="fa-solid fa-desktop"></i> En PC (Chrome / Edge):
                    </p>
                    <p class="text-zinc-400 leading-relaxed">Haz clic en el icono de <strong>Instalar (<i class="fa-solid fa-download text-[10px]"></i>)</strong> en la barra de direcciones arriba a la derecha, o abre el menú <span class="text-zinc-200">⋮ &rarr; Guardar y compartir &rarr; Instalar AlIster</span>.</p>
                </div>
                <div class="p-3.5 rounded-xl bg-dark-950/80 border border-dark-700/80">
                    <p class="font-semibold text-emerald-400 mb-1 flex items-center gap-1.5">
                        <i class="fa-brands fa-android"></i> En Android (Chrome):
                    </p>
                    <p class="text-zinc-400 leading-relaxed">Toca el menú <span class="text-zinc-200">⋮</span> arriba a la derecha y selecciona <strong>"Instalar aplicación"</strong> o <strong>"Añadir a pantalla de inicio"</strong>.</p>
                </div>
                <div class="p-3.5 rounded-xl bg-dark-950/80 border border-dark-700/80">
                    <p class="font-semibold text-sky-400 mb-1 flex items-center gap-1.5">
                        <i class="fa-brands fa-apple"></i> En iPhone / iPad (Safari):
                    </p>
                    <p class="text-zinc-400 leading-relaxed">Toca el botón <strong>Compartir (<i class="fa-solid fa-arrow-up-from-bracket text-[10px]"></i>)</strong> abajo y elige <strong>"Añadir a pantalla de inicio"</strong>.</p>
                </div>
            </div>

            <div class="flex justify-end gap-3">
                <button id="close-install-modal-btn" class="px-4 py-2 rounded-xl text-sm font-medium bg-indigo-600 hover:bg-indigo-500 text-white shadow-lg shadow-indigo-600/20 transition-all">
                    Entendido
                </button>
            </div>
        </div>
    </div>

    <!-- Modal para Configurar API Key Personal de Gemini -->
    <div id="apikey-modal" class="fixed inset-0 z-50 hidden items-center justify-center bg-black/75 backdrop-blur-sm p-4">
        <div class="bg-dark-900 border border-dark-700 rounded-2xl max-w-md w-full p-6 shadow-2xl animate-fade-in">
            <div class="flex items-center gap-3 mb-3">
                <div class="w-10 h-10 rounded-xl bg-amber-500/10 border border-amber-500/20 flex items-center justify-center text-amber-400">
                    <i class="fa-solid fa-key"></i>
                </div>
                <div>
                    <h3 class="text-lg font-semibold text-zinc-100">Tu API Key de Gemini</h3>
                    <p class="text-xs text-zinc-400">Se guarda solo en tu navegador (100% privada)</p>
                </div>
            </div>
            <p class="text-xs text-zinc-400 mb-3 leading-relaxed">
                Si ves un error de permisos al usar la app fuera de la vista previa, pega aquí tu clave gratuita de <a href="https://aistudio.google.com/app/apikey" target="_blank" rel="noopener noreferrer" class="text-indigo-400 hover:underline font-medium">Google AI Studio <i class="fa-solid fa-arrow-up-right-from-square text-[10px]"></i></a>.
            </p>
            <input type="password" id="apikey-input" placeholder="AIzaSy..."
                class="w-full bg-dark-950 border border-dark-700 focus:border-indigo-500 rounded-xl px-4 py-2.5 text-sm text-zinc-100 outline-none mb-5 font-mono transition-colors">
            <div class="flex items-center justify-between gap-3">
                <button type="button" id="clear-apikey-btn" class="px-3 py-2 rounded-xl text-xs font-medium text-red-400 hover:bg-red-500/10 transition-all">
                    Borrar clave
                </button>
                <div class="flex gap-2">
                    <button type="button" id="cancel-apikey-btn" class="px-4 py-2 rounded-xl text-sm font-medium text-zinc-400 hover:text-zinc-200 hover:bg-dark-800 transition-all">
                        Cancelar
                    </button>
                    <button type="button" id="save-apikey-btn" class="px-4 py-2 rounded-xl text-sm font-medium bg-indigo-600 hover:bg-indigo-500 text-white shadow-lg shadow-indigo-600/20 transition-all">
                        Guardar clave
                    </button>
                </div>
            </div>
        </div>
    </div>

    <!-- Modal de Confirmación Personalizado para Limpiar Chat -->
    <div id="clear-modal" class="fixed inset-0 z-50 hidden items-center justify-center bg-black/70 backdrop-blur-sm p-4 transition-opacity">
        <div class="bg-dark-900 border border-dark-700 rounded-2xl max-w-sm w-full p-6 shadow-2xl animate-fade-in">
            <div class="flex items-center gap-3 mb-3 text-zinc-100">
                <div class="w-10 h-10 rounded-xl bg-red-500/10 border border-red-500/20 flex items-center justify-center text-red-400">
                    <i class="fa-solid fa-trash-can"></i>
                </div>
                <h3 class="text-lg font-semibold">¿Limpiar conversación?</h3>
            </div>
            <p class="text-sm text-zinc-400 mb-6 leading-relaxed">
                Se borrará todo el historial de mensajes de esta sesión privada. Esta acción no se puede deshacer.
            </p>
            <div class="flex justify-end gap-3">
                <button id="cancel-clear-btn" class="px-4 py-2 rounded-xl text-sm font-medium text-zinc-300 hover:bg-dark-800 border border-transparent hover:border-dark-700 transition-all">
                    Cancelar
                </button>
                <button id="confirm-clear-btn" class="px-4 py-2 rounded-xl text-sm font-medium bg-red-600 hover:bg-red-500 text-white shadow-lg shadow-red-600/20 transition-all">
                    Sí, limpiar chat
                </button>
            </div>
        </div>
    </div>

    <!-- Modal para Personalizar Nombre del Usuario -->
    <div id="name-modal" class="fixed inset-0 z-50 hidden items-center justify-center bg-black/70 backdrop-blur-sm p-4">
        <div class="bg-dark-900 border border-dark-700 rounded-2xl max-w-sm w-full p-6 shadow-2xl animate-fade-in">
            <div class="flex items-center gap-3 mb-3">
                <div class="w-10 h-10 rounded-xl bg-indigo-500/10 border border-indigo-500/20 flex items-center justify-center text-indigo-400">
                    <i class="fa-solid fa-user-pen"></i>
                </div>
                <h3 class="text-lg font-semibold text-zinc-100">Personalizar saludo</h3>
            </div>
            <p class="text-sm text-zinc-400 mb-4">
                ¿Cómo te gustaría que te llame tu asistente privado?
            </p>
            <input type="text" id="username-input" placeholder="Ej. Alex, Sofía, Jefe..." maxlength="25"
                class="w-full bg-dark-950 border border-dark-700 focus:border-indigo-500 rounded-xl px-4 py-2.5 text-sm text-zinc-100 outline-none mb-5 transition-colors">
            <div class="flex justify-end gap-3">
                <button id="cancel-name-btn" class="px-4 py-2 rounded-xl text-sm font-medium text-zinc-400 hover:text-zinc-200 hover:bg-dark-800 transition-all">
                    Cancelar
                </button>
                <button id="save-name-btn" class="px-4 py-2 rounded-xl text-sm font-medium bg-indigo-600 hover:bg-indigo-500 text-white shadow-lg shadow-indigo-600/20 transition-all">
                    Guardar
                </button>
            </div>
        </div>
    </div>

    <!-- BARRA LATERAL (Dashboard Minimalista) -->
    <aside id="sidebar" class="w-full md:w-80 bg-dark-900 border-b md:border-b-0 md:border-r border-dark-700/80 flex flex-col justify-between shrink-0 z-20 transition-all">
        <!-- Parte Superior: Marca y Estado Privado -->
        <div class="p-4 md:p-6">
            <div class="flex items-center justify-between">
                <div class="flex items-center gap-3">
                    <div class="w-10 h-10 rounded-xl bg-gradient-to-br from-indigo-500 to-purple-600 flex items-center justify-center shadow-lg shadow-indigo-500/20">
                        <i class="fa-solid fa-sparkles text-white text-base"></i>
                    </div>
                    <div>
                        <h1 class="font-bold text-base tracking-tight text-zinc-100">AlIster</h1>
                        <div class="flex items-center gap-1.5 mt-0.5">
                            <span class="w-2 h-2 rounded-full bg-emerald-400 animate-pulse"></span>
                            <span class="text-xs text-zinc-400 font-medium">Entorno Privado • Exclusivo</span>
                        </div>
                    </div>
                </div>
                
                <!-- Botón colapsar prompts en móvil -->
                <button id="toggle-mobile-menu" class="md:hidden p-2.5 rounded-xl bg-dark-800 text-zinc-300 hover:text-white border border-dark-700" aria-label="Mostrar accesos rápidos">
                    <i class="fa-solid fa-bolt text-indigo-400"></i>
                </button>
            </div>

            <!-- Botón Instalar App Exclusiva (PC / Móvil) -->
            <button id="install-app-btn" class="mt-4 w-full flex items-center justify-between px-3.5 py-2.5 rounded-xl bg-gradient-to-r from-indigo-600/20 to-purple-600/20 hover:from-indigo-600/30 hover:to-purple-600/30 border border-indigo-500/40 text-indigo-200 text-xs font-semibold transition-all shadow-sm group">
                <span class="flex items-center gap-2">
                    <i class="fa-solid fa-download text-indigo-400 group-hover:translate-y-0.5 transition-transform"></i>
                    <span>Instalar App AlIster</span>
                </span>
                <span class="text-[10px] px-1.5 py-0.5 rounded bg-indigo-500/20 text-indigo-300 border border-indigo-500/30">PC / Móvil</span>
            </button>

            <!-- Botón Configurar API Key Personal -->
            <button id="open-apikey-btn" class="mt-2 w-full flex items-center justify-between px-3.5 py-2 rounded-xl bg-dark-950/80 hover:bg-dark-800 border border-dark-700/80 text-zinc-300 text-xs font-medium transition-all">
                <span class="flex items-center gap-2">
                    <i class="fa-solid fa-key text-amber-400 text-[11px]"></i>
                    <span>Configurar API Key</span>
                </span>
                <span id="apikey-badge" class="text-[10px] px-1.5 py-0.5 rounded bg-zinc-800 text-zinc-400">Predeterminada</span>
            </button>

            <!-- Control de Escucha Activa ("Hey papulince") -->
            <div class="mt-3 p-3 rounded-2xl bg-dark-950/70 border border-dark-700/70 flex items-center justify-between gap-2">
                <div class="min-w-0">
                    <div class="flex items-center gap-1.5">
                        <span id="wake-status-dot" class="w-2 h-2 rounded-full bg-zinc-600"></span>
                        <span class="text-xs font-semibold text-zinc-200 truncate">Modo "Hey papulince"</span>
                    </div>
                    <p id="wake-status-text" class="text-[11px] text-zinc-500 truncate mt-0.5">Apagado • Toca para activar</p>
                </div>
                <button id="toggle-wake-word-btn" type="button" role="switch" aria-checked="false"
                    class="shrink-0 w-11 h-6 rounded-full bg-dark-800 border border-dark-700 p-0.5 transition-colors relative cursor-pointer"
                    title="Activar escucha continua para 'Hey papulince'">
                    <span id="wake-toggle-knob" class="block w-4.5 h-4.5 w-[18px] h-[18px] rounded-full bg-zinc-400 transition-transform transform translate-x-0"></span>
                </button>
            </div>

            <!-- Tarjeta de Bienvenida / Perfil Personal -->
            <div class="mt-3 p-3.5 rounded-2xl bg-dark-950/70 border border-dark-700/70 hidden md:block">
                <div class="flex items-center justify-between mb-1">
                    <span id="sidebar-greeting" class="text-sm font-medium text-zinc-200 truncate">Hola, bienvenido de nuevo</span>
                    <button id="edit-name-btn" class="text-zinc-500 hover:text-indigo-400 transition-colors p-1" title="Personalizar tu nombre">
                        <i class="fa-solid fa-pen text-xs"></i>
                    </button>
                </div>
                <p id="current-date-display" class="text-xs text-zinc-500 capitalize"></p>
            </div>

            <!-- Sección de Prompts Rápidos -->
            <div id="quick-prompts-container" class="hidden md:block mt-4 space-y-3 max-h-[38vh] overflow-y-auto pr-1">
                <div class="text-[11px] font-semibold uppercase tracking-wider text-zinc-500 px-1">
                    Accesos Rápidos
                </div>

                <!-- Categoría: Productividad -->
                <div class="space-y-2">
                    <div class="flex items-center gap-2 text-xs font-medium text-emerald-400/90 px-1">
                        <i class="fa-solid fa-list-check text-[11px]"></i>
                        <span>Productividad</span>
                    </div>
                    <button onclick="useQuickPrompt('Ayúdame a planificar mi día hoy. Tengo las siguientes tareas y quiero organizarlas por prioridad y bloques de tiempo: ')" 
                        class="w-full text-left p-3 rounded-xl bg-dark-800/60 hover:bg-dark-800 border border-dark-700/60 hover:border-indigo-500/40 transition-all group">
                        <p class="text-xs font-medium text-zinc-200 group-hover:text-indigo-300 transition-colors">Planificar mi día (Time-blocking)</p>
                        <p class="text-[11px] text-zinc-500 mt-0.5 line-clamp-1">Estructura tus prioridades por horas</p>
                    </button>
                    <button onclick="useQuickPrompt('Resume los puntos clave y acciones concretas del siguiente texto:\n\n')" 
                        class="w-full text-left p-3 rounded-xl bg-dark-800/60 hover:bg-dark-800 border border-dark-700/60 hover:border-indigo-500/40 transition-all group">
                        <p class="text-xs font-medium text-zinc-200 group-hover:text-indigo-300 transition-colors">Resumir y extraer tareas</p>
                        <p class="text-[11px] text-zinc-500 mt-0.5 line-clamp-1">Convierte notas largas en acción</p>
                    </button>
                </div>

                <!-- Categoría: Escritura -->
                <div class="space-y-2 pt-1">
                    <div class="flex items-center gap-2 text-xs font-medium text-sky-400/90 px-1">
                        <i class="fa-solid fa-feather-pointed text-[11px]"></i>
                        <span>Escritura</span>
                    </div>
                    <button onclick="useQuickPrompt('Redacta un correo profesional, claro y persuasivo sobre el siguiente tema: ')" 
                        class="w-full text-left p-3 rounded-xl bg-dark-800/60 hover:bg-dark-800 border border-dark-700/60 hover:border-indigo-500/40 transition-all group">
                        <p class="text-xs font-medium text-zinc-200 group-hover:text-indigo-300 transition-colors">Redactar correo profesional</p>
                        <p class="text-[11px] text-zinc-500 mt-0.5 line-clamp-1">Tono ejecutivo y directo al grano</p>
                    </button>
                    <button onclick="useQuickPrompt('Mejora la redacción, claridad y estilo del siguiente texto manteniendo mi voz original:\n\n')" 
                        class="w-full text-left p-3 rounded-xl bg-dark-800/60 hover:bg-dark-800 border border-dark-700/60 hover:border-indigo-500/40 transition-all group">
                        <p class="text-xs font-medium text-zinc-200 group-hover:text-indigo-300 transition-colors">Pulir y mejorar estilo</p>
                        <p class="text-[11px] text-zinc-500 mt-0.5 line-clamp-1">Corrige y eleva cualquier borrador</p>
                    </button>
                </div>

                <!-- Categoría: Lluvia de Ideas -->
                <div class="space-y-2 pt-1">
                    <div class="flex items-center gap-2 text-xs font-medium text-amber-400/90 px-1">
                        <i class="fa-solid fa-lightbulb text-[11px]"></i>
                        <span>Lluvia de Ideas</span>
                    </div>
                    <button onclick="useQuickPrompt('Dame 5 ideas creativas, innovadoras y accionables para resolver este reto: ')" 
                        class="w-full text-left p-3 rounded-xl bg-dark-800/60 hover:bg-dark-800 border border-dark-700/60 hover:border-indigo-500/40 transition-all group">
                        <p class="text-xs font-medium text-zinc-200 group-hover:text-indigo-300 transition-colors">5 ángulos creativos</p>
                        <p class="text-[11px] text-zinc-500 mt-0.5 line-clamp-1">Pensamiento lateral para proyectos</p>
                    </button>
                    <button onclick="useQuickPrompt('Actúa como un mentor estratégico. Analiza pros, contras y riesgos ocultos de esta idea: ')" 
                        class="w-full text-left p-3 rounded-xl bg-dark-800/60 hover:bg-dark-800 border border-dark-700/60 hover:border-indigo-500/40 transition-all group">
                        <p class="text-xs font-medium text-zinc-200 group-hover:text-indigo-300 transition-colors">Validar idea (Pros y Contras)</p>
                        <p class="text-[11px] text-zinc-500 mt-0.5 line-clamp-1">Análisis crítico antes de decidir</p>
                    </button>
                </div>
            </div>
        </div>

        <!-- Parte Inferior Sidebar: Privacidad y Limpiar Chat -->
        <div class="hidden md:flex flex-col gap-3 p-5 border-t border-dark-700/80 bg-dark-900/50">
            <button id="sidebar-clear-btn" class="w-full flex items-center justify-center gap-2 px-4 py-2.5 rounded-xl bg-dark-800 hover:bg-red-500/10 text-zinc-300 hover:text-red-400 border border-dark-700 hover:border-red-500/30 text-xs font-medium transition-all">
                <i class="fa-solid fa-rotate-right"></i>
                <span>Limpiar conversación</span>
            </button>
            <div class="flex items-center justify-center gap-2 text-[11px] text-zinc-500">
                <i class="fa-solid fa-shield-halved text-zinc-600"></i>
                <span>Historial efímero solo en tu sesión</span>
            </div>
        </div>
    </aside>

    <!-- ÁREA PRINCIPAL DE CHAT -->
    <main id="chat-drop-zone" class="flex-1 flex flex-col h-full relative bg-dark-950 overflow-hidden">
        
        <!-- Indicador Visual de Arrastrar y Soltar (Drag & Drop Overlay) -->
        <div id="drag-overlay" class="hidden absolute inset-0 z-40 bg-dark-950/90 backdrop-blur-md border-2 border-dashed border-indigo-500 rounded-2xl m-3 flex-col items-center justify-center p-6 pointer-events-none transition-all animate-fade-in">
            <div class="w-16 h-16 rounded-2xl bg-indigo-500/20 border border-indigo-500/40 flex items-center justify-center text-indigo-400 mb-4 shadow-lg shadow-indigo-500/20">
                <i class="fa-solid fa-cloud-arrow-up text-3xl animate-bounce"></i>
            </div>
            <h3 class="text-xl font-bold text-white mb-1">Suelta tus archivos aquí</h3>
            <p class="text-sm text-zinc-400 text-center max-w-md">
                Soporta imágenes (PNG, JPG, WEBP), documentos PDF y archivos de texto o código (TXT, CSV, JSON, MD, JS, PY, HTML...)
            </p>
        </div>

        <!-- Sub-barra superior en móvil/tablet para acciones rápidas -->
        <header class="flex items-center justify-between px-4 md:px-8 py-3.5 border-b border-dark-700/60 bg-dark-950/80 backdrop-blur-md z-10">
            <div class="flex items-center gap-2.5">
                <span class="inline-flex items-center gap-1.5 px-2.5 py-1 rounded-full text-xs font-medium bg-indigo-500/10 text-indigo-300 border border-indigo-500/20">
                    <i class="fa-solid fa-lock text-[10px]"></i> Modo Privado
                </span>
                <span id="message-counter" class="text-xs text-zinc-500 hidden sm:inline">0 mensajes en sesión</span>
            </div>

            <div class="flex items-center gap-2">
                <!-- Botón de Voz Respuesta (TTS) -->
                <button id="toggle-tts-btn" class="px-2.5 py-1.5 rounded-xl bg-dark-900 hover:bg-dark-800 border border-dark-700 text-xs text-indigo-400 transition-all flex items-center gap-1.5" title="Activar/Silenciar voz de AlIster">
                    <i id="tts-icon" class="fa-solid fa-volume-high"></i>
                    <span class="hidden sm:inline">Voz ON</span>
                </button>
                <button id="mobile-name-btn" class="md:hidden px-3 py-1.5 rounded-xl bg-dark-900 hover:bg-dark-800 border border-dark-700 text-xs text-zinc-300 transition-colors">
                    <i class="fa-solid fa-user-pen mr-1 text-indigo-400"></i> Perfil
                </button>
                <button id="header-clear-btn" class="px-3 py-1.5 rounded-xl bg-dark-900 hover:bg-red-500/10 border border-dark-700 hover:border-red-500/30 text-xs text-zinc-300 hover:text-red-400 transition-all flex items-center gap-1.5" title="Limpiar chat">
                    <i class="fa-solid fa-broom"></i>
                    <span>Limpiar chat</span>
                </button>
            </div>
        </header>

        <!-- Contenedor de Mensajes -->
        <div id="chat-messages" class="flex-1 overflow-y-auto px-4 md:px-8 py-6 space-y-6 scroll-smooth">
            
            <!-- Pantalla de Bienvenida / Estado Vacío -->
            <div id="welcome-screen" class="max-w-2xl mx-auto my-auto pt-4 md:pt-10 pb-6 animate-fade-in">
                <div class="inline-flex items-center justify-center w-14 h-14 rounded-2xl bg-gradient-to-br from-indigo-500/20 to-purple-500/20 border border-indigo-500/30 mb-5 shadow-inner">
                    <i class="fa-solid fa-wand-magic-sparkles text-2xl text-indigo-400"></i>
                </div>
                
                <h2 id="main-greeting" class="text-2xl sm:text-3xl font-bold text-white tracking-tight mb-2">
                    Buenas noches, ¿en qué nos enfocamos hoy?
                </h2>
                <p class="text-zinc-400 text-sm sm:text-base leading-relaxed mb-8">
                    Este es tu espacio personal y exclusivo. Sin distracciones ni ruido externo: pídeme que organice tus ideas, redacte textos impecables o resuelva problemas complejos.
                </p>

                <!-- Tarjetas de Inicio Rápido en el Área Central -->
                <div class="grid grid-cols-1 sm:grid-cols-3 gap-3.5">
                    <button onclick="useQuickPrompt('Ayúdame a estructurar mis objetivos prioritarios para esta semana en 3 pasos claros.')" 
                        class="p-4 rounded-2xl bg-dark-900/90 hover:bg-dark-800 border border-dark-700/80 hover:border-indigo-500/50 text-left transition-all group flex flex-col justify-between">
                        <div class="w-8 h-8 rounded-lg bg-emerald-500/10 text-emerald-400 flex items-center justify-center mb-3 group-hover:scale-110 transition-transform">
                            <i class="fa-solid fa-bullseye text-sm"></i>
                        </div>
                        <div>
                            <h3 class="text-sm font-semibold text-zinc-100 mb-1">Enfoque Semanal</h3>
                            <p class="text-xs text-zinc-400 leading-relaxed">Define prioridades y elimina lo urgente pero innecesario.</p>
                        </div>
                    </button>

                    <button onclick="useQuickPrompt('Necesito redactar un mensaje importante. Hazme 3 preguntas rápidas para entender el contexto y escribirlo por mí.')" 
                        class="p-4 rounded-2xl bg-dark-900/90 hover:bg-dark-800 border border-dark-700/80 hover:border-indigo-500/50 text-left transition-all group flex flex-col justify-between">
                        <div class="w-8 h-8 rounded-lg bg-sky-500/10 text-sky-400 flex items-center justify-center mb-3 group-hover:scale-110 transition-transform">
                            <i class="fa-solid fa-pen-nib text-sm"></i>
                        </div>
                        <div>
                            <h3 class="text-sm font-semibold text-zinc-100 mb-1">Asistente de Escritura</h3>
                            <p class="text-xs text-zinc-400 leading-relaxed">Redacción guiada para correos, artículos o propuestas.</p>
                        </div>
                    </button>

                    <button onclick="useQuickPrompt('Hagamos una sesión de lluvia de ideas. Te contaré un proyecto y quiero que me des perspectivas fuera de lo común.')" 
                        class="p-4 rounded-2xl bg-dark-900/90 hover:bg-dark-800 border border-dark-700/80 hover:border-indigo-500/50 text-left transition-all group flex flex-col justify-between">
                        <div class="w-8 h-8 rounded-lg bg-amber-500/10 text-amber-400 flex items-center justify-center mb-3 group-hover:scale-110 transition-transform">
                            <i class="fa-solid fa-brain text-sm"></i>
                        </div>
                        <div>
                            <h3 class="text-sm font-semibold text-zinc-100 mb-1">Lluvia de Ideas</h3>
                            <p class="text-xs text-zinc-400 leading-relaxed">Explora conceptos nuevos y desbloquea tu creatividad.</p>
                        </div>
                    </button>
                </div>
            </div>

        </div>

        <!-- Barra Inferior de Entrada de Texto y Archivos -->
        <div class="p-3 sm:p-5 bg-gradient-to-t from-dark-950 via-dark-950 to-transparent z-10">
            <div class="max-w-3xl mx-auto">
                <form id="chat-form" class="bg-dark-900 border border-dark-700 focus-within:border-indigo-500/70 rounded-2xl p-2 shadow-xl transition-colors">
                    
                    <!-- Vista Previa de Archivos Adjuntos -->
                    <div id="attachments-preview" class="hidden flex-wrap gap-2 px-1.5 pt-1 pb-2 border-b border-dark-700/60 mb-1.5"></div>

                    <!-- Vista Previa en Vivo de Pantalla Compartida (Video + Audio del Sistema) -->
                    <div id="screen-share-bar" class="hidden flex-wrap items-center justify-between gap-2.5 px-2.5 py-2 mb-1.5 rounded-xl bg-indigo-950/50 border border-indigo-500/40">
                        <div class="flex items-center gap-2.5 min-w-0">
                            <video id="screen-video" autoplay muted playsinline class="w-16 h-10 rounded-lg object-cover bg-black border border-indigo-500/40 shrink-0"></video>
                            <div class="min-w-0">
                                <div class="flex items-center gap-1.5">
                                    <span class="w-2 h-2 rounded-full bg-red-500 animate-ping"></span>
                                    <span class="text-xs font-semibold text-indigo-200 truncate">Viendo pantalla</span>
                                    <span id="screen-audio-badge" class="hidden text-[10px] px-1.5 py-0.5 rounded bg-emerald-500/20 text-emerald-300 border border-emerald-500/30">
                                        <i class="fa-solid fa-ear-listen mr-0.5"></i> Audio activo
                                    </span>
                                </div>
                                <p id="screen-share-hint" class="text-[11px] text-zinc-400 truncate">AlIster captura imagen y escucha el audio de pantalla</p>
                            </div>
                        </div>
                        <div class="flex items-center gap-1.5 shrink-0">
                            <button type="button" id="record-screen-audio-btn" class="hidden px-2.5 py-1.5 rounded-lg bg-emerald-500/20 hover:bg-emerald-500/30 border border-emerald-500/40 text-emerald-300 text-xs font-medium transition-colors flex items-center gap-1.5" title="Grabar audio de la pantalla para que AlIster lo escuche">
                                <i id="screen-audio-icon" class="fa-solid fa-wave-square"></i>
                                <span id="screen-audio-btn-text">Escuchar audio</span>
                            </button>
                            <button type="button" id="stop-screen-btn" class="px-2.5 py-1.5 rounded-lg bg-red-500/20 hover:bg-red-500/30 border border-red-500/40 text-red-300 text-xs font-medium transition-colors">
                                Detener
                            </button>
                        </div>
                    </div>

                    <!-- Fila de controles de entrada -->
                    <div class="flex items-end gap-2 w-full">
                        <!-- Input oculto para selección de archivos -->
                        <input 
                            type="file" 
                            id="file-input" 
                            multiple 
                            accept="image/png,image/jpeg,image/webp,application/pdf,.txt,.csv,.json,.md,.js,.ts,.jsx,.tsx,.py,.html,.css,.xml,.yaml,.yml,.sql,.sh,.log"
                            class="hidden"
                        >
                        
                        <!-- Botón Clip (+) para adjuntar archivos -->
                        <button 
                            type="button" 
                            id="attach-btn" 
                            class="shrink-0 w-10 h-10 rounded-xl bg-dark-800 hover:bg-dark-700 text-zinc-400 hover:text-indigo-400 border border-dark-700/80 flex items-center justify-center transition-all cursor-pointer"
                            title="Adjuntar archivo (Imágenes, PDF, Texto/Código)">
                            <i class="fa-solid fa-paperclip text-sm"></i>
                        </button>

                        <!-- Botón Compartir Pantalla -->
                        <button 
                            type="button" 
                            id="screen-share-btn" 
                            class="shrink-0 w-10 h-10 rounded-xl bg-dark-800 hover:bg-dark-700 text-zinc-400 hover:text-indigo-400 border border-dark-700/80 flex items-center justify-center transition-all cursor-pointer"
                            title="Compartir pantalla con AlIster">
                            <i class="fa-solid fa-display text-sm"></i>
                        </button>

                        <!-- Botón Micrófono para hablar con AlIster -->
                        <button 
                            type="button" 
                            id="mic-btn" 
                            class="shrink-0 w-10 h-10 rounded-xl bg-dark-800 hover:bg-dark-700 text-zinc-400 hover:text-indigo-400 border border-dark-700/80 flex items-center justify-center transition-all cursor-pointer"
                            title="Hablar con AlIster (o di 'Hey papulince')">
                            <i id="mic-icon" class="fa-solid fa-microphone text-sm"></i>
                        </button>

                        <textarea 
                            id="user-input" 
                            rows="1" 
                            placeholder="Escribe, adjunta o di 'Hey papulince'..." 
                            class="w-full bg-transparent text-zinc-100 placeholder-zinc-500 text-sm sm:text-base px-2 py-2.5 max-h-40 resize-none outline-none leading-relaxed"
                        ></textarea>
                        
                        <button 
                            type="submit" 
                            id="send-btn" 
                            disabled
                            class="shrink-0 w-10 h-10 rounded-xl bg-indigo-600 hover:bg-indigo-500 disabled:bg-dark-800 disabled:text-zinc-600 text-white flex items-center justify-center transition-all shadow-md disabled:shadow-none cursor-pointer disabled:cursor-not-allowed"
                            title="Enviar mensaje (Enter)">
                            <i class="fa-solid fa-arrow-up text-sm"></i>
                        </button>
                    </div>
                </form>
                <div class="flex items-center justify-between mt-2 px-2 text-[11px] text-zinc-500">
                    <span><kbd class="px-1.5 py-0.5 bg-dark-900 border border-dark-700 rounded text-zinc-400 font-mono">Enter</kbd> enviar • Arrastra archivos o usa <i class="fa-solid fa-paperclip text-zinc-400"></i></span>
                    <span class="hidden sm:inline">Impulsado por Gemini</span>
                </div>
            </div>
        </div>
    </main>

    <!-- Lógica de la Aplicación e Integración con Gemini API -->
    <script>
        // ==========================================
        // CONFIGURACIÓN DE LA API DE GEMINI
        // ==========================================
        const defaultApiKey = ""; // La plataforma inyecta la clave automáticamente en tiempo de ejecución
        const MODEL_NAME = "gemini-3-flash-preview";
        let customApiKey = localStorage.getItem('alister_custom_apikey') || '';

        function getGeminiApiUrl() {
            const activeKey = customApiKey.trim() || defaultApiKey;
            return `https://generativelanguage.googleapis.com/v1beta/models/${MODEL_NAME}:generateContent?key=${activeKey}`;
        }

        // Instrucción de sistema para que actúe como asistente personal privado en español
        const SYSTEM_INSTRUCTION = `Eres AlIster, el asistente de inteligencia artificial personal, privado y exclusivo del usuario en su dashboard personal. 
Tu tono es cercano, inteligente, elegante, proactivo y altamente resolutivo. 
Responde siempre en español natural y claro. 
Cuando el usuario adjunte imágenes, capturas de pantalla, audio de la pantalla, documentos PDF o archivos de texto/código, analízalos y escúchalos en profundidad con precisión y responde directamente a lo que solicita.
Estructura tus respuestas con formato Markdown limpio (negritas, listas con viñetas, bloques de código o pasos numerados) para facilitar una lectura rápida y ejecutiva. 
Adapta tus respuestas para maximizar la productividad, creatividad y claridad mental del usuario.`;

        // ==========================================
        // ESTADO DE LA APLICACIÓN
        // ==========================================
        let conversationHistory = []; // Almacena el historial en formato Gemini { role: 'user'|'model', parts: [...] }
        let pendingAttachments = [];  // Archivos preparados para el siguiente envío
        let isGenerating = false;
        let userName = localStorage.getItem('personal_ai_username') || '';
        let dragCounter = 0;

        // Estado de Voz, Frase Clave ("Hey papulince"), Pantalla + Audio e Instalación PWA
        let deferredInstallPrompt = null;
        let recognition = null;
        let isRecordingManual = false;
        let isWakeWordEnabled = false;
        let isAwakeListeningCommand = false;
        let ttsEnabled = true;
        let screenStream = null;
        let screenMediaRecorder = null;
        let screenAudioChunks = [];
        let isRecordingScreenAudio = false;
        const WAKE_PHRASES = [
            'hey papulince', 'ey papulince', 'ei papulince', 'oye papulince', 
            'hey papu lince', 'ey papu lince', 'hey papulense', 'hey populince'
        ];

        // Límites y extensiones permitidas
        const MAX_FILE_SIZE_MB = 15;
        const MAX_ATTACHMENTS = 5;
        const TEXT_EXTENSIONS = [
            'txt', 'csv', 'json', 'md', 'markdown', 'js', 'ts', 'jsx', 'tsx', 
            'py', 'html', 'htm', 'css', 'xml', 'yaml', 'yml', 'sql', 'sh', 
            'bash', 'log', 'env', 'ini', 'java', 'c', 'cpp', 'h', 'go', 'rs', 'php', 'rb'
        ];

        // ==========================================
        // ELEMENTOS DEL DOM
        // ==========================================
        const chatMessagesEl = document.getElementById('chat-messages');
        const welcomeScreenEl = document.getElementById('welcome-screen');
        const chatForm = document.getElementById('chat-form');
        const userInput = document.getElementById('user-input');
        const sendBtn = document.getElementById('send-btn');
        const messageCounterEl = document.getElementById('message-counter');
        
        // Elementos de archivos y Drag & Drop
        const chatDropZone = document.getElementById('chat-drop-zone');
        const dragOverlay = document.getElementById('drag-overlay');
        const fileInput = document.getElementById('file-input');
        const attachBtn = document.getElementById('attach-btn');
        const attachmentsPreviewEl = document.getElementById('attachments-preview');
        
        // Modales y controles
        const clearModal = document.getElementById('clear-modal');
        const nameModal = document.getElementById('name-modal');
        const installModal = document.getElementById('install-modal');
        const apikeyModal = document.getElementById('apikey-modal');
        const apikeyInput = document.getElementById('apikey-input');
        const apikeyBadge = document.getElementById('apikey-badge');
        const usernameInput = document.getElementById('username-input');
        const quickPromptsContainer = document.getElementById('quick-prompts-container');

        // Elementos de Voz e Instalación
        const micBtn = document.getElementById('mic-btn');
        const micIcon = document.getElementById('mic-icon');
        const screenShareBtn = document.getElementById('screen-share-btn');
        const screenShareBar = document.getElementById('screen-share-bar');
        const screenVideo = document.getElementById('screen-video');
        const screenAudioBadge = document.getElementById('screen-audio-badge');
        const recordScreenAudioBtn = document.getElementById('record-screen-audio-btn');
        const screenAudioBtnText = document.getElementById('screen-audio-btn-text');
        const stopScreenBtn = document.getElementById('stop-screen-btn');
        const toggleWakeWordBtn = document.getElementById('toggle-wake-word-btn');
        const wakeToggleKnob = document.getElementById('wake-toggle-knob');
        const wakeStatusDot = document.getElementById('wake-status-dot');
        const wakeStatusText = document.getElementById('wake-status-text');
        const toggleTtsBtn = document.getElementById('toggle-tts-btn');
        const ttsIcon = document.getElementById('tts-icon');
        const installAppBtn = document.getElementById('install-app-btn');

        // ==========================================
        // COMPARTIR PANTALLA Y ESCUCHAR AUDIO CON ALISTER
        // ==========================================
        async function startScreenShare() {
            if (!navigator.mediaDevices || !navigator.mediaDevices.getDisplayMedia) {
                showToast('Tu navegador o dispositivo no permite compartir pantalla', 'error');
                return;
            }
            try {
                // Solicitar video y audio de la pestaña/sistema
                screenStream = await navigator.mediaDevices.getDisplayMedia({
                    video: { cursor: 'always' },
                    audio: true
                });
                screenVideo.srcObject = screenStream;
                screenShareBar.classList.remove('hidden');
                screenShareBar.classList.add('flex');
                screenShareBtn.classList.add('bg-indigo-600', 'text-white', 'border-indigo-400');
                screenShareBtn.classList.remove('bg-dark-800', 'text-zinc-400');

                const audioTracks = screenStream.getAudioTracks();
                if (audioTracks.length > 0) {
                    screenAudioBadge.classList.remove('hidden');
                    recordScreenAudioBtn.classList.remove('hidden');
                    showToast('Pantalla y audio compartidos. Pulsa "Escuchar audio" para capturar sonido', 'success');
                } else {
                    screenAudioBadge.classList.add('hidden');
                    recordScreenAudioBtn.classList.add('hidden');
                    showToast('Pantalla compartida (marca "Compartir audio" en la ventana si quieres que escuche)', 'info');
                }

                // Detectar si el usuario detiene la compartición desde la barra del navegador
                screenStream.getVideoTracks()[0].addEventListener('ended', () => {
                    stopScreenShare();
                });

                updateSendButtonState();
            } catch (err) {
                if (err.name !== 'NotAllowedError') {
                    showToast('No se pudo compartir la pantalla', 'error');
                }
            }
        }

        function toggleScreenAudioRecording() {
            if (!screenStream) return;
            const audioTracks = screenStream.getAudioTracks();
            if (audioTracks.length === 0) {
                showToast('No se detectó pista de audio. Vuelve a compartir marcando "Compartir audio"', 'error');
                return;
            }

            if (isRecordingScreenAudio && screenMediaRecorder) {
                screenMediaRecorder.stop();
                return;
            }

            try {
                const audioOnlyStream = new MediaStream(audioTracks);
                const mimeType = MediaRecorder.isTypeSupported('audio/webm') ? 'audio/webm' : 'audio/ogg';
                screenMediaRecorder = new MediaRecorder(audioOnlyStream, { mimeType });
                screenAudioChunks = [];

                screenMediaRecorder.ondataavailable = (e) => {
                    if (e.data && e.data.size > 0) screenAudioChunks.push(e.data);
                };

                screenMediaRecorder.onstop = async () => {
                    isRecordingScreenAudio = false;
                    recordScreenAudioBtn.classList.remove('bg-red-600', 'text-white', 'border-red-400', 'animate-pulse');
                    recordScreenAudioBtn.classList.add('bg-emerald-500/20', 'text-emerald-300', 'border-emerald-500/40');
                    screenAudioBtnText.textContent = 'Escuchar audio';

                    if (screenAudioChunks.length === 0) return;
                    const blob = new Blob(screenAudioChunks, { type: mimeType });
                    const reader = new FileReader();
                    reader.onload = () => {
                        const base64Data = reader.result.split(',')[1];
                        pendingAttachments.push({
                            id: 'screen-audio-' + Date.now(),
                            name: 'Audio de pantalla.webm',
                            size: formatFileSize(blob.size),
                            category: 'audio',
                            mimeType: mimeType,
                            ext: 'webm',
                            base64Data: base64Data
                        });
                        renderAttachmentsPreview();
                        updateSendButtonState();
                        showToast('Audio de pantalla capturado y listo para enviar a AlIster', 'success');
                    };
                    reader.readAsDataURL(blob);
                };

                screenMediaRecorder.start();
                isRecordingScreenAudio = true;
                recordScreenAudioBtn.classList.remove('bg-emerald-500/20', 'text-emerald-300', 'border-emerald-500/40');
                recordScreenAudioBtn.classList.add('bg-red-600', 'text-white', 'border-red-400', 'animate-pulse');
                screenAudioBtnText.textContent = 'Detener y adjuntar';
                showToast('Escuchando el audio de tu pantalla... Pulsa de nuevo para enviarlo', 'info');
            } catch (err) {
                showToast('No se pudo grabar el audio de la pantalla', 'error');
            }
        }

        function stopScreenShare() {
            if (isRecordingScreenAudio && screenMediaRecorder) {
                try { screenMediaRecorder.stop(); } catch (e) {}
            }
            if (screenStream) {
                screenStream.getTracks().forEach(track => track.stop());
                screenStream = null;
            }
            screenVideo.srcObject = null;
            screenShareBar.classList.add('hidden');
            screenShareBar.classList.remove('flex');
            screenAudioBadge.classList.add('hidden');
            recordScreenAudioBtn.classList.add('hidden');
            screenShareBtn.classList.remove('bg-indigo-600', 'text-white', 'border-indigo-400');
            screenShareBtn.classList.add('bg-dark-800', 'text-zinc-400');
            updateSendButtonState();
        }

        function captureScreenFrame() {
            if (!screenStream || !screenVideo || screenVideo.videoWidth === 0) return null;
            try {
                const canvas = document.createElement('canvas');
                // Redimensionar manteniendo proporción (máx 1280px ancho) para envío rápido y nítido
                const maxWidth = 1280;
                const scale = Math.min(1, maxWidth / screenVideo.videoWidth);
                canvas.width = Math.round(screenVideo.videoWidth * scale);
                canvas.height = Math.round(screenVideo.videoHeight * scale);
                const ctx = canvas.getContext('2d');
                ctx.drawImage(screenVideo, 0, 0, canvas.width, canvas.height);
                const dataUrl = canvas.toDataURL('image/jpeg', 0.85);
                return {
                    id: 'screen-' + Date.now(),
                    name: 'Captura de pantalla.jpg',
                    size: 'En vivo',
                    category: 'image',
                    mimeType: 'image/jpeg',
                    ext: 'jpg',
                    base64Data: dataUrl.split(',')[1],
                    previewUrl: dataUrl
                };
            } catch (e) {
                return null;
            }
        }

        // ==========================================
        // RECONOCIMIENTO DE VOZ Y FRASE CLAVE ("HEY PAPULINCE")
        // ==========================================
        function initVoiceRecognition() {
            const SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
            if (!SpeechRecognition) {
                micBtn.title = 'Tu navegador no soporta reconocimiento de voz';
                return;
            }

            recognition = new SpeechRecognition();
            recognition.lang = 'es-ES';
            recognition.interimResults = true;
            recognition.continuous = false;

            recognition.onstart = () => {
                if (isRecordingManual || isAwakeListeningCommand) {
                    micBtn.classList.add('bg-indigo-600', 'text-white', 'voice-listening', 'border-indigo-400');
                    micBtn.classList.remove('bg-dark-800', 'text-zinc-400');
                }
                updateWakeUI();
            };

            recognition.onresult = (event) => {
                let interimTranscript = '';
                let finalTranscript = '';

                for (let i = event.resultIndex; i < event.results.length; i++) {
                    const transcript = event.results[i][0].transcript;
                    if (event.results[i].isFinal) {
                        finalTranscript += transcript;
                    } else {
                        interimTranscript += transcript;
                    }
                }

                const currentText = (finalTranscript || interimTranscript).trim();
                const lowerText = currentText.toLowerCase().normalize("NFD").replace(/[\u0300-\u036f]/g, "");

                // Caso 1: Dictado manual con el botón de micrófono
                if (isRecordingManual) {
                    userInput.value = currentText;
                    autoResizeTextarea();
                    if (finalTranscript) {
                        isRecordingManual = false;
                        recognition.stop();
                        if (userInput.value.trim()) {
                            handleSendMessage();
                        }
                    }
                    return;
                }

                // Caso 2: Modo escucha continua ("Hey papulince")
                if (isWakeWordEnabled) {
                    if (!isAwakeListeningCommand) {
                        // Buscar si dijo la frase clave
                        const matchedPhrase = WAKE_PHRASES.find(phrase => lowerText.includes(phrase));
                        if (matchedPhrase) {
                            // Extraer si dijo algo inmediatamente después de "hey papulince"
                            const idx = lowerText.indexOf(matchedPhrase);
                            const commandAfterWake = currentText.slice(idx + matchedPhrase.length).replace(/^[,.\s!?]+/, '').trim();

                            playActivationBeep();
                            isAwakeListeningCommand = true;
                            updateWakeUI();

                            if (commandAfterWake && finalTranscript) {
                                // Dijo frase clave + comando de corrido (ej: "Hey papulince qué hora es")
                                isAwakeListeningCommand = false;
                                userInput.value = commandAfterWake;
                                autoResizeTextarea();
                                handleSendMessage();
                            } else if (finalTranscript) {
                                // Solo dijo "Hey papulince": saludar y esperar su pregunta
                                showToast('¡Dime! Te escucho...', 'info');
                                speakText('¡Dime! Te escucho.');
                            }
                        }
                    } else {
                        // Ya está despierto escuchando la orden del usuario
                        userInput.value = currentText;
                        autoResizeTextarea();
                        if (finalTranscript && currentText) {
                            isAwakeListeningCommand = false;
                            updateWakeUI();
                            handleSendMessage();
                        }
                    }
                }
            };

            recognition.onerror = (event) => {
                if (event.error === 'not-allowed') {
                    isRecordingManual = false;
                    isWakeWordEnabled = false;
                    isAwakeListeningCommand = false;
                    showToast('Permiso de micrófono denegado en el navegador', 'error');
                    updateWakeUI();
                }
            };

            recognition.onend = () => {
                micBtn.classList.remove('bg-indigo-600', 'text-white', 'voice-listening', 'border-indigo-400');
                micBtn.classList.add('bg-dark-800', 'text-zinc-400');

                if (isRecordingManual) {
                    isRecordingManual = false;
                }

                // Reiniciar escucha automáticamente si el modo "Hey papulince" sigue activo y no está hablando la IA
                if (isWakeWordEnabled && !window.speechSynthesis?.speaking) {
                    setTimeout(() => {
                        if (isWakeWordEnabled) {
                            try { recognition.start(); } catch (e) {}
                        }
                    }, 300);
                }
                updateWakeUI();
            };
        }

        function toggleManualMic() {
            if (!recognition) {
                showToast('Tu navegador no soporta reconocimiento de voz', 'error');
                return;
            }
            if (window.speechSynthesis) window.speechSynthesis.cancel();

            if (isRecordingManual) {
                isRecordingManual = false;
                recognition.stop();
            } else {
                isRecordingManual = true;
                isAwakeListeningCommand = false;
                try {
                    recognition.stop();
                } catch (e) {}
                setTimeout(() => {
                    try { recognition.start(); } catch (e) {}
                }, 150);
                showToast('Escuchando tu voz...', 'info');
            }
        }

        function toggleWakeWordMode() {
            if (!recognition) {
                showToast('Tu navegador no soporta reconocimiento de voz', 'error');
                return;
            }
            isWakeWordEnabled = !isWakeWordEnabled;
            isAwakeListeningCommand = false;
            isRecordingManual = false;

            if (isWakeWordEnabled) {
                try { recognition.start(); } catch (e) {}
                showToast('Escucha activa: di "Hey papulince" cuando quieras', 'success');
            } else {
                try { recognition.stop(); } catch (e) {}
                showToast('Modo "Hey papulince" desactivado', 'info');
            }
            updateWakeUI();
        }

        function updateWakeUI() {
            if (!toggleWakeWordBtn) return;
            toggleWakeWordBtn.setAttribute('aria-checked', isWakeWordEnabled);

            if (isWakeWordEnabled) {
                toggleWakeWordBtn.classList.remove('bg-dark-800', 'border-dark-700');
                toggleWakeWordBtn.classList.add('bg-indigo-600', 'border-indigo-500');
                wakeToggleKnob.classList.remove('translate-x-0', 'bg-zinc-400');
                wakeToggleKnob.classList.add('translate-x-5', 'bg-white');

                if (isAwakeListeningCommand) {
                    wakeStatusDot.className = 'w-2 h-2 rounded-full bg-emerald-400 animate-ping';
                    wakeStatusText.textContent = '¡Te escucho! Habla ahora...';
                    wakeStatusText.className = 'text-[11px] text-emerald-400 font-medium truncate mt-0.5';
                } else {
                    wakeStatusDot.className = 'w-2 h-2 rounded-full bg-indigo-400 animate-pulse';
                    wakeStatusText.textContent = 'Esperando "Hey papulince"...';
                    wakeStatusText.className = 'text-[11px] text-indigo-300 truncate mt-0.5';
                }
            } else {
                toggleWakeWordBtn.classList.add('bg-dark-800', 'border-dark-700');
                toggleWakeWordBtn.classList.remove('bg-indigo-600', 'border-indigo-500');
                wakeToggleKnob.classList.add('translate-x-0', 'bg-zinc-400');
                wakeToggleKnob.classList.remove('translate-x-5', 'bg-white');
                wakeStatusDot.className = 'w-2 h-2 rounded-full bg-zinc-600';
                wakeStatusText.textContent = 'Apagado • Toca para activar';
                wakeStatusText.className = 'text-[11px] text-zinc-500 truncate mt-0.5';
            }
        }

        function playActivationBeep() {
            try {
                const ctx = new (window.AudioContext || window.webkitAudioContext)();
                const osc = ctx.createOscillator();
                const gain = ctx.createGain();
                osc.type = 'sine';
                osc.frequency.setValueAtTime(587.33, ctx.currentTime); // D5
                osc.frequency.exponentialRampToValueAtTime(880, ctx.currentTime + 0.12); // A5
                gain.gain.setValueAtTime(0.15, ctx.currentTime);
                gain.gain.exponentialRampToValueAtTime(0.001, ctx.currentTime + 0.18);
                osc.connect(gain);
                gain.connect(ctx.destination);
                osc.start();
                osc.stop(ctx.currentTime + 0.18);
            } catch (e) {}
        }

        function speakText(rawText) {
            if (!ttsEnabled || !('speechSynthesis' in window)) return;
            window.speechSynthesis.cancel();

            // Limpiar símbolos Markdown para una lectura natural
            const cleanText = rawText
                .replace(/```[\s\S]*?```/g, ' Te dejo el código en pantalla. ')
                .replace(/[#*_`~>-]/g, '')
                .replace(/\[([^\]]+)\]\([^)]+\)/g, '$1')
                .trim();

            if (!cleanText) return;

            const utterance = new SpeechSynthesisUtterance(cleanText);
            utterance.lang = 'es-ES';
            utterance.rate = 1.05;

            const voices = window.speechSynthesis.getVoices();
            const spanishVoice = voices.find(v => v.lang.startsWith('es') && (v.name.includes('Google') || v.name.includes('Natural') || v.name.includes('Microsoft'))) 
                              || voices.find(v => v.lang.startsWith('es'));
            if (spanishVoice) utterance.voice = spanishVoice;

            // Pausar escucha mientras AlIster habla para que no se escuche a sí mismo
            if (isWakeWordEnabled && recognition) {
                try { recognition.stop(); } catch (e) {}
            }

            utterance.onend = () => {
                if (isWakeWordEnabled && recognition) {
                    setTimeout(() => {
                        try { recognition.start(); } catch (e) {}
                    }, 300);
                }
            };

            window.speechSynthesis.speak(utterance);
        }

        // ==========================================
        // CONFIGURACIÓN PWA (INSTALABLE EN PC Y MÓVIL)
        // ==========================================
        function setupPWA() {
            const svgIcon = `<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><defs><linearGradient id="g" x1="0" y1="0" x2="1" y2="1"><stop offset="0%" stop-color="#6366f1"/><stop offset="100%" stop-color="#9333ea"/></linearGradient></defs><rect width="512" height="512" rx="112" fill="url(#g)"/><text x="256" y="330" font-family="sans-serif" font-size="250" font-weight="bold" fill="#ffffff" text-anchor="middle">A</text></svg>`;
            const iconUrl = 'data:image/svg+xml;charset=utf-8,' + encodeURIComponent(svgIcon);

            const manifest = {
                name: 'AlIster - IA Personal',
                short_name: 'AlIster',
                description: 'Tu asistente de inteligencia artificial personal y privado',
                start_url: '.',
                display: 'standalone',
                background_color: '#09090b',
                theme_color: '#09090b',
                icons: [
                    { src: iconUrl, sizes: '192x192', type: 'image/svg+xml', purpose: 'any maskable' },
                    { src: iconUrl, sizes: '512x512', type: 'image/svg+xml', purpose: 'any maskable' }
                ]
            };

            try {
                const manifestBlob = new Blob([JSON.stringify(manifest)], { type: 'application/manifest+json' });
                const manifestUrl = URL.createObjectURL(manifestBlob);
                const link = document.createElement('link');
                link.rel = 'manifest';
                link.href = manifestUrl;
                document.head.appendChild(link);
            } catch (e) {}

            window.addEventListener('beforeinstallprompt', (e) => {
                e.preventDefault();
                deferredInstallPrompt = e;
            });

            window.addEventListener('appinstalled', () => {
                deferredInstallPrompt = null;
                showToast('¡AlIster instalado correctamente como app!', 'success');
            });
        }

        async function handleInstallAppClick() {
            if (deferredInstallPrompt) {
                deferredInstallPrompt.prompt();
                const { outcome } = await deferredInstallPrompt.userChoice;
                if (outcome === 'accepted') {
                    deferredInstallPrompt = null;
                }
            } else {
                installModal.classList.remove('hidden');
                installModal.classList.add('flex');
            }
        }

        // ==========================================
        // INICIALIZACIÓN Y UTILIDADES DE INTERFAZ
        // ==========================================
        function updateApiKeyBadge() {
            if (!apikeyBadge) return;
            if (customApiKey.trim()) {
                apikeyBadge.textContent = 'Personalizada';
                apikeyBadge.className = 'text-[10px] px-1.5 py-0.5 rounded bg-emerald-500/20 text-emerald-300 border border-emerald-500/30';
            } else {
                apikeyBadge.textContent = 'Predeterminada';
                apikeyBadge.className = 'text-[10px] px-1.5 py-0.5 rounded bg-zinc-800 text-zinc-400';
            }
        }

        function initApp() {
            setupPWA();
            initVoiceRecognition();
            updateGreetings();
            updateApiKeyBadge();
            setupEventListeners();
            updateMessageCounter();
            userInput.focus();
        }

        function updateGreetings() {
            const hour = new Date().getHours();
            let timeGreeting = 'Buenas noches';
            if (hour >= 5 && hour < 12) timeGreeting = 'Buenos días';
            else if (hour >= 12 && hour < 19) timeGreeting = 'Buenas tardes';

            const namePart = userName.trim() ? `, ${userName.trim()}` : '';
            
            const mainGreetingEl = document.getElementById('main-greeting');
            const sidebarGreetingEl = document.getElementById('sidebar-greeting');
            const dateDisplayEl = document.getElementById('current-date-display');

            if (mainGreetingEl) {
                mainGreetingEl.textContent = `${timeGreeting}${namePart}, ¿en qué nos enfocamos hoy?`;
            }
            if (sidebarGreetingEl) {
                sidebarGreetingEl.textContent = userName.trim() ? `Hola, ${userName.trim()}` : 'Hola, bienvenido de nuevo';
            }
            if (dateDisplayEl) {
                const options = { weekday: 'long', day: 'numeric', month: 'long' };
                dateDisplayEl.textContent = new Date().toLocaleDateString('es-ES', options);
            }
        }

        function updateMessageCounter() {
            if (!messageCounterEl) return;
            const count = conversationHistory.length;
            messageCounterEl.textContent = `${count} ${count === 1 ? 'mensaje' : 'mensajes'} en sesión`;
        }

        window.useQuickPrompt = function(promptText) {
            userInput.value = promptText;
            autoResizeTextarea();
            userInput.focus();
            
            if (window.innerWidth < 768 && !quickPromptsContainer.classList.contains('hidden')) {
                quickPromptsContainer.classList.add('hidden');
            }
        };

        function showToast(message, type = 'info') {
            const container = document.getElementById('toast-container');
            if (!container) return;

            const toast = document.createElement('div');
            
            const colors = {
                success: 'bg-dark-900 border-emerald-500/40 text-emerald-300',
                error: 'bg-dark-900 border-red-500/40 text-red-300',
                info: 'bg-dark-900 border-indigo-500/40 text-indigo-300'
            };
            const icons = {
                success: 'fa-circle-check text-emerald-400',
                error: 'fa-circle-exclamation text-red-400',
                info: 'fa-circle-info text-indigo-400'
            };

            toast.className = `flex items-center gap-2.5 px-4 py-3 rounded-xl border shadow-xl text-xs font-medium backdrop-blur-md animate-fade-in ${colors[type] || colors.info}`;
            toast.innerHTML = `<i class="fa-solid ${icons[type] || icons.info}"></i><span>${escapeHTML(message)}</span>`;
            
            container.appendChild(toast);
            setTimeout(() => {
                toast.style.opacity = '0';
                toast.style.transform = 'translateY(-6px)';
                toast.style.transition = 'all 0.25s ease';
                setTimeout(() => toast.remove(), 250);
            }, 3000);
        }

        // ==========================================
        // GESTIÓN DE ARCHIVOS ADJUNTOS (CLIP Y DRAG & DROP)
        // ==========================================
        function formatFileSize(bytes) {
            if (bytes === 0) return '0 B';
            const k = 1024;
            const sizes = ['B', 'KB', 'MB', 'GB'];
            const i = Math.floor(Math.log(bytes) / Math.log(k));
            return parseFloat((bytes / Math.pow(k, i)).toFixed(1)) + ' ' + sizes[i];
        }

        function getFileIconClass(category, ext) {
            if (category === 'pdf') return 'fa-solid fa-file-pdf text-rose-400';
            if (category === 'audio') return 'fa-solid fa-volume-high text-emerald-400';
            if (ext === 'csv') return 'fa-solid fa-file-csv text-emerald-400';
            if (['js', 'ts', 'jsx', 'tsx', 'py', 'html', 'css', 'json', 'sql', 'java', 'cpp', 'go', 'rs'].includes(ext)) {
                return 'fa-solid fa-file-code text-sky-400';
            }
            return 'fa-solid fa-file-lines text-indigo-400';
        }

        function classifyFile(file) {
            const name = file.name || 'archivo';
            const ext = name.includes('.') ? name.split('.').pop().toLowerCase() : '';
            const mime = file.type || '';

            if (mime.startsWith('image/') && ['image/png', 'image/jpeg', 'image/webp', 'image/gif'].includes(mime)) {
                return { category: 'image', mimeType: mime, ext };
            }
            if (mime === 'application/pdf' || ext === 'pdf') {
                return { category: 'pdf', mimeType: 'application/pdf', ext: 'pdf' };
            }
            if (mime.startsWith('text/') || TEXT_EXTENSIONS.includes(ext) || mime === 'application/json') {
                return { category: 'text', mimeType: mime || 'text/plain', ext: ext || 'txt' };
            }
            return null;
        }

        async function processSelectedFiles(fileList) {
            const files = Array.from(fileList);
            if (!files.length) return;

            for (const file of files) {
                if (pendingAttachments.length >= MAX_ATTACHMENTS) {
                    showToast(`Máximo ${MAX_ATTACHMENTS} archivos por mensaje`, 'error');
                    break;
                }

                if (file.size > MAX_FILE_SIZE_MB * 1024 * 1024) {
                    showToast(`"${file.name}" supera el límite de ${MAX_FILE_SIZE_MB} MB`, 'error');
                    continue;
                }

                const classification = classifyFile(file);
                if (!classification) {
                    showToast(`Formato no soportado: "${file.name}"`, 'error');
                    continue;
                }

                try {
                    const attachmentId = 'att-' + Date.now() + '-' + Math.random().toString(36).substr(2, 5);
                    
                    if (classification.category === 'image' || classification.category === 'pdf') {
                        const dataUrl = await readFileAsDataURL(file);
                        const base64Data = dataUrl.split(',')[1];
                        
                        pendingAttachments.push({
                            id: attachmentId,
                            name: file.name,
                            size: formatFileSize(file.size),
                            category: classification.category,
                            mimeType: classification.mimeType,
                            ext: classification.ext,
                            base64Data: base64Data,
                            previewUrl: classification.category === 'image' ? dataUrl : null
                        });
                    } else if (classification.category === 'text') {
                        const textContent = await readFileAsText(file);
                        pendingAttachments.push({
                            id: attachmentId,
                            name: file.name,
                            size: formatFileSize(file.size),
                            category: 'text',
                            mimeType: classification.mimeType,
                            ext: classification.ext,
                            textContent: textContent
                        });
                    }
                } catch (err) {
                    showToast(`Error al leer "${file.name}"`, 'error');
                }
            }

            renderAttachmentsPreview();
            updateSendButtonState();
            fileInput.value = ''; // Permitir reseleccionar el mismo archivo
        }

        function readFileAsDataURL(file) {
            return new Promise((resolve, reject) => {
                const reader = new FileReader();
                reader.onload = () => resolve(reader.result);
                reader.onerror = () => reject(reader.error);
                reader.readAsDataURL(file);
            });
        }

        function readFileAsText(file) {
            return new Promise((resolve, reject) => {
                const reader = new FileReader();
                reader.onload = () => resolve(reader.result);
                reader.onerror = () => reject(reader.error);
                reader.readAsText(file);
            });
        }

        window.removePendingAttachment = function(attachmentId) {
            pendingAttachments = pendingAttachments.filter(att => att.id !== attachmentId);
            renderAttachmentsPreview();
            updateSendButtonState();
        };

        function renderAttachmentsPreview() {
            if (pendingAttachments.length === 0) {
                attachmentsPreviewEl.innerHTML = '';
                attachmentsPreviewEl.classList.add('hidden');
                attachmentsPreviewEl.classList.remove('flex');
                return;
            }

            attachmentsPreviewEl.classList.remove('hidden');
            attachmentsPreviewEl.classList.add('flex');

            attachmentsPreviewEl.innerHTML = pendingAttachments.map(att => {
                if (att.category === 'image') {
                    return `
                        <div class="relative group flex items-center gap-2.5 bg-dark-800 border border-dark-700 rounded-xl p-1.5 pr-7 max-w-[200px] animate-fade-in">
                            <img src="${att.previewUrl}" alt="${escapeHTML(att.name)}" class="w-10 h-10 rounded-lg object-cover shrink-0 border border-dark-700">
                            <div class="min-w-0">
                                <p class="text-xs font-medium text-zinc-200 truncate">${escapeHTML(att.name)}</p>
                                <p class="text-[10px] text-zinc-500">${att.size}</p>
                            </div>
                            <button type="button" onclick="removePendingAttachment('${att.id}')" 
                                class="absolute top-1.5 right-1.5 w-5 h-5 rounded-full bg-dark-950/90 hover:bg-red-500 text-zinc-400 hover:text-white flex items-center justify-center text-[10px] transition-colors"
                                title="Quitar archivo">
                                <i class="fa-solid fa-xmark"></i>
                            </button>
                        </div>
                    `;
                } else {
                    const iconClass = getFileIconClass(att.category, att.ext);
                    return `
                        <div class="relative group flex items-center gap-2.5 bg-dark-800 border border-dark-700 rounded-xl px-3 py-2 pr-8 max-w-[220px] animate-fade-in">
                            <div class="w-8 h-8 rounded-lg bg-dark-900 border border-dark-700 flex items-center justify-center shrink-0">
                                <i class="${iconClass} text-sm"></i>
                            </div>
                            <div class="min-w-0">
                                <p class="text-xs font-medium text-zinc-200 truncate">${escapeHTML(att.name)}</p>
                                <p class="text-[10px] text-zinc-500 uppercase">${escapeHTML(att.ext)} • ${att.size}</p>
                            </div>
                            <button type="button" onclick="removePendingAttachment('${att.id}')" 
                                class="absolute top-1/2 -translate-y-1/2 right-2 w-5 h-5 rounded-full bg-dark-950/80 hover:bg-red-500 text-zinc-400 hover:text-white flex items-center justify-center text-[10px] transition-colors"
                                title="Quitar archivo">
                                <i class="fa-solid fa-xmark"></i>
                            </button>
                        </div>
                    `;
                }
            }).join('');
        }

        // ==========================================
        // MANEJO DE INTERFAZ DE CHAT Y MENSAJES
        // ==========================================
        function updateSendButtonState() {
            const hasContent = userInput.value.trim().length > 0 || pendingAttachments.length > 0 || Boolean(screenStream);
            sendBtn.disabled = !hasContent || isGenerating;
        }

        function autoResizeTextarea() {
            userInput.style.height = 'auto';
            userInput.style.height = Math.min(userInput.scrollHeight, 160) + 'px';
            updateSendButtonState();
        }

        function appendMessageToUI(role, text, isError = false, attachments = []) {
            // Ocultar pantalla de bienvenida al iniciar conversación
            if (welcomeScreenEl && !welcomeScreenEl.classList.contains('hidden')) {
                welcomeScreenEl.classList.add('hidden');
            }

            const wrapper = document.createElement('div');
            wrapper.className = `max-w-3xl mx-auto flex gap-3.5 animate-fade-in ${role === 'user' ? 'justify-end' : 'justify-start'}`;

            const timestamp = new Date().toLocaleTimeString('es-ES', { hour: '2-digit', minute: '2-digit' });

            if (role === 'user') {
                // Renderizar archivos adjuntos dentro de la burbuja del usuario si existen
                let attachmentsHTML = '';
                if (attachments && attachments.length > 0) {
                    const itemsHTML = attachments.map(att => {
                        if (att.category === 'image') {
                            return `
                                <div class="relative overflow-hidden rounded-xl border border-indigo-400/30 bg-indigo-950/40 max-w-[220px]">
                                    <img src="${att.previewUrl}" alt="${escapeHTML(att.name)}" class="max-h-44 w-auto object-cover block">
                                    <div class="px-2.5 py-1 bg-black/50 backdrop-blur-sm text-[10px] text-indigo-100 truncate">
                                        ${escapeHTML(att.name)}
                                    </div>
                                </div>
                            `;
                        } else {
                            const iconClass = getFileIconClass(att.category, att.ext);
                            return `
                                <div class="flex items-center gap-2 bg-indigo-700/70 border border-indigo-400/30 rounded-xl px-3 py-2 max-w-[230px]">
                                    <div class="w-7 h-7 rounded-lg bg-indigo-950/60 flex items-center justify-center shrink-0">
                                        <i class="${iconClass} text-xs"></i>
                                    </div>
                                    <div class="min-w-0">
                                        <p class="text-xs font-medium text-white truncate">${escapeHTML(att.name)}</p>
                                        <p class="text-[10px] text-indigo-200 uppercase">${escapeHTML(att.ext)} • ${att.size}</p>
                                    </div>
                                </div>
                            `;
                        }
                    }).join('');

                    attachmentsHTML = `<div class="flex flex-wrap justify-end gap-2 mb-2">${itemsHTML}</div>`;
                }

                const escapedText = text ? escapeHTML(text).replace(/\n/g, '<br>') : '';
                const textBubbleHTML = escapedText 
                    ? `<div class="bg-indigo-600 text-white px-4 py-3 rounded-2xl rounded-tr-sm shadow-md text-sm sm:text-[15px] leading-relaxed">${escapedText}</div>` 
                    : '';

                wrapper.innerHTML = `
                    <div class="flex flex-col items-end max-w-[85%] sm:max-w-[75%]">
                        ${attachmentsHTML}
                        ${textBubbleHTML}
                        <span class="text-[11px] text-zinc-500 mt-1 px-1">Tú • ${timestamp}</span>
                    </div>
                `;
            } else {
                // Burbuja del Asistente IA
                const renderedHtml = isError 
                    ? `<p class="text-red-400 flex items-center gap-2"><i class="fa-solid fa-circle-exclamation"></i> ${escapeHTML(text)}</p>`
                    : (typeof marked !== 'undefined' ? marked.parse(text) : escapeHTML(text));

                const messageId = 'msg-' + Date.now() + '-' + Math.random().toString(36).substr(2, 5);

                wrapper.innerHTML = `
                    <div class="w-8 h-8 rounded-xl bg-gradient-to-br from-indigo-500/20 to-purple-500/20 border border-indigo-500/30 flex items-center justify-center shrink-0 mt-0.5">
                        <i class="fa-solid fa-sparkles text-indigo-400 text-xs"></i>
                    </div>
                    <div class="flex flex-col items-start max-w-[88%] sm:max-w-[82%] min-w-0">
                        <div id="${messageId}" class="bg-dark-900 border ${isError ? 'border-red-500/30' : 'border-dark-700/80'} text-zinc-200 px-4 py-3.5 rounded-2xl rounded-tl-sm shadow-sm text-sm sm:text-[15px] prose-ai w-full overflow-x-auto">
                            ${renderedHtml}
                        </div>
                        <div class="flex items-center gap-3 mt-1.5 px-1">
                            <span class="text-[11px] text-zinc-500">AlIster • ${timestamp}</span>
                            ${!isError ? `
                            <button onclick="copyMessageText('${messageId}')" class="text-[11px] text-zinc-500 hover:text-indigo-400 transition-colors flex items-center gap-1" title="Copiar respuesta">
                                <i class="fa-regular fa-copy"></i> Copiar
                            </button>` : ''}
                        </div>
                    </div>
                `;
            }

            chatMessagesEl.appendChild(wrapper);
            scrollToBottom();
        }

        function showTypingIndicator() {
            if (welcomeScreenEl && !welcomeScreenEl.classList.contains('hidden')) {
                welcomeScreenEl.classList.add('hidden');
            }

            const indicator = document.createElement('div');
            indicator.id = 'typing-indicator';
            indicator.className = 'max-w-3xl mx-auto flex gap-3.5 animate-fade-in';
            indicator.innerHTML = `
                <div class="w-8 h-8 rounded-xl bg-gradient-to-br from-indigo-500/20 to-purple-500/20 border border-indigo-500/30 flex items-center justify-center shrink-0">
                    <i class="fa-solid fa-sparkles text-indigo-400 text-xs"></i>
                </div>
                <div class="bg-dark-900 border border-dark-700/80 px-4 py-3.5 rounded-2xl rounded-tl-sm flex items-center gap-1.5">
                    <span class="w-2 h-2 rounded-full bg-indigo-400 typing-dot"></span>
                    <span class="w-2 h-2 rounded-full bg-indigo-400 typing-dot"></span>
                    <span class="w-2 h-2 rounded-full bg-indigo-400 typing-dot"></span>
                </div>
            `;
            chatMessagesEl.appendChild(indicator);
            scrollToBottom();
        }

        function removeTypingIndicator() {
            const indicator = document.getElementById('typing-indicator');
            if (indicator) indicator.remove();
        }

        function scrollToBottom() {
            chatMessagesEl.scrollTop = chatMessagesEl.scrollHeight;
        }

        function escapeHTML(str) {
            const div = document.createElement('div');
            div.textContent = str;
            return div.innerHTML;
        }

        // Copiar al portapapeles usando document.execCommand para compatibilidad en iframes
        window.copyMessageText = function(elementId) {
            const el = document.getElementById(elementId);
            if (!el) return;
            
            const textToCopy = el.innerText;
            const tempTextArea = document.createElement('textarea');
            tempTextArea.value = textToCopy;
            tempTextArea.style.position = 'fixed';
            tempTextArea.style.left = '-9999px';
            document.body.appendChild(tempTextArea);
            tempTextArea.select();
            
            try {
                document.execCommand('copy');
                showToast('Respuesta copiada al portapapeles', 'success');
            } catch (err) {
                showToast('No se pudo copiar el texto', 'error');
            } finally {
                document.body.removeChild(tempTextArea);
            }
        };

        // ==========================================
        // COMUNICACIÓN CON GEMINI API (CON REINTENTOS)
        // ==========================================
        async function fetchGeminiWithRetry(payload, maxRetries = 3) {
            let delay = 1000;
            
            for (let attempt = 0; attempt <= maxRetries; attempt++) {
                try {
                    const response = await fetch(getGeminiApiUrl(), {
                        method: 'POST',
                        headers: { 'Content-Type': 'application/json' },
                        body: JSON.stringify(payload)
                    });

                    if (!response.ok) {
                        const errBody = await response.json().catch(() => ({}));
                        const apiMsg = errBody?.error?.message || `Error HTTP ${response.status}`;
                        if ((response.status === 429 || response.status >= 500) && attempt < maxRetries) {
                            await new Promise(res => setTimeout(res, delay));
                            delay *= 2;
                            continue;
                        }
                        throw new Error(apiMsg);
                    }

                    const data = await response.json();
                    const candidate = data?.candidates?.[0];
                    const text = candidate?.content?.parts?.map(p => p.text || '').join('').trim();
                    
                    if (!text) {
                        const finishReason = candidate?.finishReason || 'sin respuesta';
                        throw new Error(`El modelo no devolvió texto (${finishReason}).`);
                    }

                    return text;
                } catch (error) {
                    if (attempt === maxRetries) {
                        throw error;
                    }
                    await new Promise(res => setTimeout(res, delay));
                    delay *= 2;
                }
            }
        }

        async function handleSendMessage(e) {
            if (e) e.preventDefault();
            
            const messageText = userInput.value.trim();
            const screenCapture = captureScreenFrame();
            if ((!messageText && pendingAttachments.length === 0 && !screenCapture) || isGenerating) return;

            // Capturar adjuntos actuales (incluyendo pantalla compartida si está activa) y limpiar barra
            const currentAttachments = [...pendingAttachments];
            if (screenCapture) {
                currentAttachments.unshift(screenCapture);
            }
            pendingAttachments = [];
            renderAttachmentsPreview();

            // Actualizar estado UI
            isGenerating = true;
            userInput.value = '';
            autoResizeTextarea();
            sendBtn.disabled = true;

            // Mostrar mensaje del usuario (con sus archivos o captura de pantalla) en la UI
            const displayPromptText = messageText || (screenCapture && currentAttachments.length === 1
                ? 'Observa mi pantalla actual y dime qué ves o cómo puedes ayudarme con lo que aparece.'
                : (currentAttachments.length === 1 
                    ? `Analiza el archivo adjunto: ${currentAttachments[0].name}` 
                    : `Analiza los ${currentAttachments.length} archivos adjuntos`));
            
            appendMessageToUI('user', messageText, false, currentAttachments);

            // Construir partes multimodales para la API de Gemini
            const geminiParts = [];
            
            for (const att of currentAttachments) {
                if (att.category === 'image' || att.category === 'pdf' || att.category === 'audio') {
                    geminiParts.push({
                        inlineData: {
                            mimeType: att.mimeType,
                            data: att.base64Data
                        }
                    });
                } else if (att.category === 'text') {
                    geminiParts.push({
                        text: `--- INICIO DEL ARCHIVO ADJUNTO: "${att.name}" ---\n${att.textContent}\n--- FIN DEL ARCHIVO ADJUNTO: "${att.name}" ---`
                    });
                }
            }

            // Añadir el texto del usuario
            geminiParts.push({ text: displayPromptText });

            // Guardar en el historial de conversación
            conversationHistory.push({
                role: 'user',
                parts: geminiParts
            });
            updateMessageCounter();

            // Mostrar indicador de carga
            showTypingIndicator();

            // Construir payload con contexto completo de la sesión e instrucción personalizada
            const personalizedSystemPrompt = userName.trim() 
                ? `${SYSTEM_INSTRUCTION}\nEl usuario se llama "${userName.trim()}". Dirígete a él/ella de forma natural cuando sea oportuno.`
                : SYSTEM_INSTRUCTION;

            const payload = {
                contents: conversationHistory.map(msg => ({
                    role: msg.role,
                    parts: msg.parts
                })),
                systemInstruction: {
                    parts: [{ text: personalizedSystemPrompt }]
                }
            };

            try {
                const aiResponseText = await fetchGeminiWithRetry(payload);
                removeTypingIndicator();
                
                // Guardar respuesta en el historial de la sesión
                conversationHistory.push({
                    role: 'model',
                    parts: [{ text: aiResponseText }]
                });
                
                appendMessageToUI('model', aiResponseText);
                updateMessageCounter();
                
                // Leer respuesta en voz alta si se usó voz o está activo el modo voz
                if (isWakeWordEnabled || ttsEnabled) {
                    speakText(aiResponseText);
                }
            } catch (err) {
                removeTypingIndicator();
                // Eliminar el último mensaje de usuario del historial fallido para mantener coherencia
                conversationHistory.pop();
                updateMessageCounter();
                const rawErr = err?.message || '';
                const detail = rawErr ? ` (${rawErr})` : '';
                appendMessageToUI('model', `Lo siento, ocurrió un problema al procesar tu mensaje${detail}. Inténtalo de nuevo.`, true);
                if (rawErr.toLowerCase().includes('permission') || rawErr.toLowerCase().includes('api key')) {
                    showToast('Haz clic en "Configurar API Key" en el menú izquierdo para usar tu clave gratuita', 'info');
                }
            } finally {
                isGenerating = false;
                autoResizeTextarea();
                userInput.focus();
            }
        }

        // ==========================================
        // LIMPIAR CHAT Y GESTIÓN DE PERFIL
        // ==========================================
        function openClearModal() {
            if (conversationHistory.length === 0) {
                showToast('El chat ya está limpio', 'info');
                return;
            }
            clearModal.classList.remove('hidden');
            clearModal.classList.add('flex');
        }

        function closeClearModal() {
            clearModal.classList.add('hidden');
            clearModal.classList.remove('flex');
        }

        function clearChatSession() {
            conversationHistory = [];
            pendingAttachments = [];
            renderAttachmentsPreview();
            updateSendButtonState();
            updateMessageCounter();
            
            // Eliminar todos los mensajes excepto la pantalla de bienvenida
            Array.from(chatMessagesEl.children).forEach(child => {
                if (child.id !== 'welcome-screen') {
                    child.remove();
                }
            });
            
            if (welcomeScreenEl) {
                welcomeScreenEl.classList.remove('hidden');
            }
            
            closeClearModal();
            showToast('Conversación limpiada', 'success');
        }

        function openNameModal() {
            usernameInput.value = userName;
            nameModal.classList.remove('hidden');
            nameModal.classList.add('flex');
            setTimeout(() => usernameInput.focus(), 50);
        }

        function closeNameModal() {
            nameModal.classList.add('hidden');
            nameModal.classList.remove('flex');
        }

        function saveUserName() {
            userName = usernameInput.value.trim();
            localStorage.setItem('personal_ai_username', userName);
            updateGreetings();
            closeNameModal();
            showToast(userName ? `¡Hola, ${userName}! Nombre guardado` : 'Saludo restablecido', 'success');
        }

        function setupEventListeners() {
            chatForm.addEventListener('submit', handleSendMessage);
            userInput.addEventListener('input', autoResizeTextarea);
            attachBtn.addEventListener('click', () => fileInput.click());

            // Compartir Pantalla y Audio de Pantalla
            screenShareBtn.addEventListener('click', () => {
                if (screenStream) {
                    stopScreenShare();
                } else {
                    startScreenShare();
                }
            });
            recordScreenAudioBtn.addEventListener('click', toggleScreenAudioRecording);
            stopScreenBtn.addEventListener('click', stopScreenShare);

            // Modal de API Key Personal
            document.getElementById('open-apikey-btn').addEventListener('click', () => {
                apikeyInput.value = customApiKey;
                apikeyModal.classList.remove('hidden');
                apikeyModal.classList.add('flex');
                setTimeout(() => apikeyInput.focus(), 50);
            });
            document.getElementById('cancel-apikey-btn').addEventListener('click', () => {
                apikeyModal.classList.add('hidden');
                apikeyModal.classList.remove('flex');
            });
            document.getElementById('save-apikey-btn').addEventListener('click', () => {
                customApiKey = apikeyInput.value.trim();
                localStorage.setItem('alister_custom_apikey', customApiKey);
                updateApiKeyBadge();
                apikeyModal.classList.add('hidden');
                apikeyModal.classList.remove('flex');
                showToast(customApiKey ? 'API Key personal guardada' : 'Usando configuración predeterminada', 'success');
            });
            document.getElementById('clear-apikey-btn').addEventListener('click', () => {
                customApiKey = '';
                apikeyInput.value = '';
                localStorage.removeItem('alister_custom_apikey');
                updateApiKeyBadge();
                apikeyModal.classList.add('hidden');
                apikeyModal.classList.remove('flex');
                showToast('API Key borrada', 'info');
            });
            apikeyModal.addEventListener('click', (e) => {
                if (e.target === apikeyModal) {
                    apikeyModal.classList.add('hidden');
                    apikeyModal.classList.remove('flex');
                }
            });

            // Controles de Voz ("Hey papulince", Micrófono y Silenciar TTS)
            micBtn.addEventListener('click', toggleManualMic);
            toggleWakeWordBtn.addEventListener('click', toggleWakeWordMode);
            toggleTtsBtn.addEventListener('click', () => {
                ttsEnabled = !ttsEnabled;
                if (!ttsEnabled && window.speechSynthesis) {
                    window.speechSynthesis.cancel();
                }
                ttsIcon.className = ttsEnabled ? 'fa-solid fa-volume-high' : 'fa-solid fa-volume-xmark';
                toggleTtsBtn.querySelector('span').textContent = ttsEnabled ? 'Voz ON' : 'Voz OFF';
                toggleTtsBtn.classList.toggle('text-indigo-400', ttsEnabled);
                toggleTtsBtn.classList.toggle('text-zinc-500', !ttsEnabled);
                showToast(ttsEnabled ? 'Respuesta por voz activada' : 'Respuesta por voz silenciada', 'info');
            });

            // Botones de instalación como App
            installAppBtn.addEventListener('click', handleInstallAppClick);
            document.getElementById('close-install-modal-btn').addEventListener('click', () => {
                installModal.classList.add('hidden');
                installModal.classList.remove('flex');
            });
            installModal.addEventListener('click', (e) => {
                if (e.target === installModal) {
                    installModal.classList.add('hidden');
                    installModal.classList.remove('flex');
                }
            });

            fileInput.addEventListener('change', (e) => {
                if (e.target.files) {
                    processSelectedFiles(e.target.files);
                }
            });

            // Soporte Drag & Drop en toda el área principal del chat
            chatDropZone.addEventListener('dragenter', (e) => {
                e.preventDefault();
                e.stopPropagation();
                dragCounter++;
                if (e.dataTransfer && e.dataTransfer.types.includes('Files')) {
                    dragOverlay.classList.remove('hidden');
                    dragOverlay.classList.add('flex');
                }
            });

            chatDropZone.addEventListener('dragover', (e) => {
                e.preventDefault();
                e.stopPropagation();
            });

            chatDropZone.addEventListener('dragleave', (e) => {
                e.preventDefault();
                e.stopPropagation();
                dragCounter--;
                if (dragCounter <= 0) {
                    dragCounter = 0;
                    dragOverlay.classList.add('hidden');
                    dragOverlay.classList.remove('flex');
                }
            });

            chatDropZone.addEventListener('drop', (e) => {
                e.preventDefault();
                e.stopPropagation();
                dragCounter = 0;
                dragOverlay.classList.add('hidden');
                dragOverlay.classList.remove('flex');

                if (e.dataTransfer && e.dataTransfer.files && e.dataTransfer.files.length > 0) {
                    processSelectedFiles(e.dataTransfer.files);
                }
            });

            // Soporte para pegar imágenes directamente desde el portapapeles (Ctrl+V)
            userInput.addEventListener('paste', (e) => {
                const items = e.clipboardData?.items;
                if (!items) return;
                const pastedFiles = [];
                for (const item of items) {
                    if (item.kind === 'file') {
                        const file = item.getAsFile();
                        if (file) pastedFiles.push(file);
                    }
                }
                if (pastedFiles.length > 0) {
                    e.preventDefault();
                    processSelectedFiles(pastedFiles);
                }
            });

            // Enviar con Enter, salto de línea con Shift+Enter
            userInput.addEventListener('keydown', (e) => {
                if (e.key === 'Enter' && !e.shiftKey) {
                    e.preventDefault();
                    if (!sendBtn.disabled) {
                        handleSendMessage();
                    }
                }
            });

            // Botones de limpiar chat
            document.getElementById('sidebar-clear-btn').addEventListener('click', openClearModal);
            document.getElementById('header-clear-btn').addEventListener('click', openClearModal);
            document.getElementById('cancel-clear-btn').addEventListener('click', closeClearModal);
            document.getElementById('confirm-clear-btn').addEventListener('click', clearChatSession);

            // Botones de personalizar nombre
            document.getElementById('edit-name-btn').addEventListener('click', openNameModal);
            document.getElementById('mobile-name-btn').addEventListener('click', openNameModal);
            document.getElementById('cancel-name-btn').addEventListener('click', closeNameModal);
            document.getElementById('save-name-btn').addEventListener('click', saveUserName);
            usernameInput.addEventListener('keydown', (e) => {
                if (e.key === 'Enter') {
                    e.preventDefault();
                    saveUserName();
                }
            });

            // Menú desplegable de accesos rápidos en móvil
            document.getElementById('toggle-mobile-menu').addEventListener('click', () => {
                quickPromptsContainer.classList.toggle('hidden');
            });

            // Cerrar modales al hacer clic fuera
            clearModal.addEventListener('click', (e) => {
                if (e.target === clearModal) closeClearModal();
            });
            nameModal.addEventListener('click', (e) => {
                if (e.target === nameModal) closeNameModal();
            });
        }

        // Arrancar aplicación al cargar
        window.addEventListener('DOMContentLoaded', initApp);
    </script>
</body>
</html>
