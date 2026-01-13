# mi-dashboard-app
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mi Aplicación Dashboard</title>
    <!-- Tailwind CSS para diseño moderno y responsivo -->
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&display=swap');
        
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f8fafc;
        }

        .glass-card {
            background: rgba(255, 255, 255, 0.9);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(226, 232, 240, 0.8);
            transition: all 0.3s ease;
        }

        .glass-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.1);
        }

        /* Personalización de scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #f1f1f1;
        }
        ::-webkit-scrollbar-thumb {
            background: #cbd5e1;
            border-radius: 10px;
        }
    </style>
</head>
<body class="min-h-screen flex flex-col">

    <!-- Navegación -->
    <nav class="bg-slate-900 text-white sticky top-0 z-50 shadow-md">
        <div class="container mx-auto px-6 py-4 flex justify-between items-center">
            <div class="flex items-center space-x-3">
                <div class="bg-blue-500 p-2 rounded-lg">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 3.055A9.001 9.001 0 1020.945 13H11V3.055z" />
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M20.488 9H15V3.512A9.025 9.025 0 0120.488 9z" />
                    </svg>
                </div>
                <span class="text-xl font-bold tracking-tight">DataVision Pro</span>
            </div>
            <div class="hidden md:flex space-x-8 font-medium">
                <a href="#" class="text-blue-400">Dashboard</a>
                <a href="#" class="hover:text-blue-400 transition">Proyectos</a>
                <a href="#" class="hover:text-blue-400 transition">Ajustes</a>
            </div>
            <button onclick="toggleModal('userModal')" class="bg-slate-800 p-2 rounded-full hover:bg-slate-700">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z" />
                </svg>
            </button>
        </div>
    </nav>

    <!-- Contenido -->
    <main class="container mx-auto px-6 py-10 flex-grow">
        <div class="flex flex-col md:flex-row md:items-center justify-between mb-10">
            <div>
                <h1 class="text-4xl font-extrabold text-slate-800">Panel de Resumen</h1>
                <p class="text-slate-500 mt-2">Bienvenido, aquí tienes las métricas de hoy.</p>
            </div>
            <div class="mt-4 md:mt-0">
                <button onclick="addTask()" class="bg-blue-600 hover:bg-blue-700 text-white px-6 py-3 rounded-xl font-bold transition flex items-center shadow-lg shadow-blue-200">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-2" viewBox="0 0 20 20" fill="currentColor">
                        <path fill-rule="evenodd" d="M10 3a1 1 0 011 1v5h5a1 1 0 110 2h-5v5a1 1 0 11-2 0v-5H4a1 1 0 110-2h5V4a1 1 0 011-1z" clip-rule="evenodd" />
                    </svg>
                    Nueva Tarea
                </button>
            </div>
        </div>

        <!-- Estadísticas Rápidas -->
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6 mb-10">
            <div class="glass-card p-6 rounded-2xl">
                <p class="text-sm font-semibold text-slate-400 uppercase">Usuarios Activos</p>
                <h3 class="text-3xl font-bold text-slate-800 mt-1">1,284</h3>
                <span class="text-green-500 text-sm font-bold">↑ 12% vs ayer</span>
            </div>
            <div class="glass-card p-6 rounded-2xl">
                <p class="text-sm font-semibold text-slate-400 uppercase">Tiempo Medio</p>
                <h3 class="text-3xl font-bold text-slate-800 mt-1">4m 32s</h3>
                <span class="text-blue-500 text-sm font-bold">Estable</span>
            </div>
            <div class="glass-card p-6 rounded-2xl">
                <p class="text-sm font-semibold text-slate-400 uppercase">Conversión</p>
                <h3 class="text-3xl font-bold text-slate-800 mt-1">3.2%</h3>
                <span class="text-red-500 text-sm font-bold">↓ 0.4%</span>
            </div>
            <div class="glass-card p-6 rounded-2xl">
                <p class="text-sm font-semibold text-slate-400 uppercase">Ingresos</p>
                <h3 class="text-3xl font-bold text-slate-800 mt-1">$12,400</h3>
                <span class="text-green-500 text-sm font-bold">↑ 8%</span>
            </div>
        </div>

        <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
            <!-- Lista de Tareas -->
            <div class="lg:col-span-2 glass-card p-8 rounded-2xl">
                <h2 class="text-2xl font-bold text-slate-800 mb-6 flex items-center">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 mr-2 text-blue-500" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2" />
                    </svg>
                    Tareas del Proyecto
                </h2>
                <div id="todoList" class="space-y-4">
                    <!-- Tarea Inicial -->
                    <div class="flex items-center justify-between p-4 bg-slate-50 rounded-xl border border-slate-100">
                        <div class="flex items-center space-x-4">
                            <input type="checkbox" class="h-5 w-5 text-blue-600 rounded">
                            <span class="text-slate-700 font-medium">Configurar el repositorio en GitHub</span>
                        </div>
                        <span class="px-3 py-1 bg-blue-100 text-blue-700 text-xs font-bold rounded-full uppercase">Alta</span>
                    </div>
                </div>
            </div>

            <!-- Panel Lateral -->
            <div class="glass-card p-8 rounded-2xl">
                <h2 class="text-2xl font-bold text-slate-800 mb-6">Actividad</h2>
                <div class="space-y-6">
                    <div class="flex items-start space-x-4">
                        <div class="w-2 h-2 mt-2 bg-green-500 rounded-full"></div>
                        <div>
                            <p class="text-sm font-bold text-slate-700">Sistema Online</p>
                            <p class="text-xs text-slate-400">Hace 5 minutos</p>
                        </div>
                    </div>
                    <div class="flex items-start space-x-4">
                        <div class="w-2 h-2 mt-2 bg-blue-500 rounded-full"></div>
                        <div>
                            <p class="text-sm font-bold text-slate-700">Actualización de UI</p>
                            <p class="text-xs text-slate-400">Hace 2 horas</p>
                        </div>
                    </div>
                    <button onclick="generateReport()" class="w-full mt-6 border-2 border-slate-200 text-slate-600 py-3 rounded-xl font-bold hover:bg-slate-50 transition">
                        Exportar Datos
                    </button>
                </div>
            </div>
        </div>
    </main>

    <!-- Modal Personalizado -->
    <div id="modalOverlay" class="hidden fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-[100] flex items-center justify-center p-4">
        <div class="bg-white rounded-3xl p-8 max-w-sm w-full shadow-2xl transform transition-all">
            <div id="modalIcon" class="mb-4 flex justify-center"></div>
            <h3 id="modalTitle" class="text-2xl font-bold text-center text-slate-800 mb-2"></h3>
            <p id="modalMessage" class="text-slate-500 text-center mb-8"></p>
            <button onclick="closeModal()" class="w-full bg-slate-800 text-white py-4 rounded-2xl font-bold hover:bg-slate-700 transition">
                Entendido
            </button>
        </div>
    </div>

    <footer class="bg-white py-8 border-t border-slate-100 text-center text-slate-400 text-sm">
        <p>&copy; 2024 Mi Aplicación Profesional. Hecho con ❤️ para GitHub.</p>
    </footer>

    <script>
        function toggleModal(title, message, type = 'info') {
            const overlay = document.getElementById('modalOverlay');
            const mTitle = document.getElementById('modalTitle');
            const mMsg = document.getElementById('modalMessage');
            const mIcon = document.getElementById('modalIcon');

            mTitle.innerText = title;
            mMsg.innerText = message;
            
            // Icono dinámico según tipo
            mIcon.innerHTML = type === 'success' 
                ? '<div class="bg-green-100 p-4 rounded-full text-green-600"><svg class="w-10 h-10" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path></svg></div>'
                : '<div class="bg-blue-100 p-4 rounded-full text-blue-600"><svg class="w-10 h-10" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"></path></svg></div>';

            overlay.classList.remove('hidden');
        }

        function closeModal() {
            document.getElementById('modalOverlay').classList.add('hidden');
        }

        function addTask() {
            const list = document.getElementById('todoList');
            const tasks = [
                "Analizar métricas semanales",
                "Reunión con el equipo de diseño",
                "Optimizar base de datos",
                "Actualizar documentación"
            ];
            const randomTask = tasks[Math.floor(Math.random() * tasks.length)];
            
            const div = document.createElement('div');
            div.className = "flex items-center justify-between p-4 bg-white rounded-xl border border-slate-100 shadow-sm animate-bounce";
            div.innerHTML = `
                <div class="flex items-center space-x-4">
                    <input type="checkbox" class="h-5 w-5 text-blue-600 rounded">
                    <span class="text-slate-700 font-medium">${randomTask}</span>
                </div>
                <span class="px-3 py-1 bg-slate-100 text-slate-500 text-xs font-bold rounded-full uppercase">Pendiente</span>
            `;
            list.prepend(div);
            setTimeout(() => div.classList.remove('animate-bounce'), 1000);
        }

        function generateReport() {
            toggleModal("Generando Reporte", "Estamos compilando tus datos. Estarán listos en un momento.", "info");
            setTimeout(() => {
                closeModal();
                toggleModal("¡Completado!", "El reporte ha sido generado con éxito y está listo para descargar.", "success");
            }, 2000);
        }
    </script>
</body>
</html>
