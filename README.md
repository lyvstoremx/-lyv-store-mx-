<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Lyv Store MX - Recargas Pro</title>
    <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="bg-black text-white min-h-screen flex flex-col justify-between font-sans selection:bg-red-600 selection:text-white">

    <!-- LOGIN -->
    <div id="loginSection" class="fixed inset-0 bg-black/95 z-50 flex items-center justify-center p-4 backdrop-blur-md">
        <div class="w-full max-w-sm bg-zinc-950 border border-red-900/40 rounded-3xl p-8 shadow-2xl text-center relative overflow-hidden">
            <div class="absolute -top-20 -left-20 w-40 h-40 bg-red-600/10 rounded-full blur-3xl"></div>
            
            <h1 class="text-3xl font-black tracking-widest text-red-600 mb-1">LYV STORE <span class="text-amber-400 text-sm">MX</span></h1>
            <p class="text-xs text-zinc-400 tracking-wider uppercase mb-6">Recargas de Free Fire y Robux</p>

            <button onclick="iniciarSesion('Google')" class="w-full mb-3 py-3 px-4 rounded-xl bg-zinc-900 hover:bg-zinc-800 border border-zinc-800 text-white font-semibold text-sm flex items-center justify-center gap-3 transition">
                Continuar con Google
            </button>
            <button onclick="iniciarSesion('Apple')" class="w-full py-3 px-4 rounded-xl bg-zinc-900 hover:bg-zinc-800 border border-zinc-800 text-white font-semibold text-sm flex items-center justify-center gap-3 transition">
                Continuar con Apple
            </button>
        </div>
    </div>

    <!-- TIENDA -->
    <header class="w-full p-4 border-b border-zinc-900 flex justify-between items-center bg-black/80 backdrop-blur sticky top-0 z-40">
        <h1 class="text-lg font-black tracking-wider text-red-600">LYV STORE <span class="text-amber-400 text-xs">MX</span></h1>
        <div class="flex items-center gap-3">
            <button onclick="verificarAdmin()" class="text-xs bg-zinc-900 hover:bg-zinc-800 border border-zinc-800 px-3 py-1.5 rounded-lg text-amber-400 font-bold">Admin</button>
            <button onclick="cerrarSesion()" class="text-xs text-red-500 font-semibold">Salir</button>
        </div>
    </header>

    <main class="w-full max-w-md mx-auto p-4 my-auto">
        <div class="bg-zinc-950 border border-zinc-900 rounded-3xl p-6 shadow-2xl">
            <h2 class="text-base font-bold mb-4 text-zinc-200 flex justify-between">
                <span>Selecciona tu Recarga</span>
                <span class="text-xs text-amber-400">💎 Automático</span>
            </h2>

            <div class="mb-5">
                <label class="block text-xs font-semibold text-zinc-400 uppercase tracking-wider mb-2">ID de Free Fire / Usuario</label>
                <input type="text" id="playerId" placeholder="Ej. 1234567890" class="w-full px-4 py-3 rounded-xl bg-black border border-zinc-800 text-white focus:outline-none focus:border-red-600 text-sm">
            </div>

            <div class="mb-6">
                <label class="block text-xs font-semibold text-zinc-400 uppercase tracking-wider mb-2">Paquetes</label>
                <div class="grid grid-cols-2 gap-3">
                    <button onclick="seleccionarPaquete(this, '100 Diamantes', '12.00')" class="paquete-btn p-3 rounded-xl bg-black border border-zinc-900 text-left hover:border-red-600 transition">
                        <div class="font-bold text-sm text-zinc-100">100 Diamantes</div>
                        <div class="text-xs text-amber-400 font-semibold">$12.00 MXN</div>
                    </button>
                    <button onclick="seleccionarPaquete(this, '310 Diamantes', '35.00')" class="paquete-btn p-3 rounded-xl bg-black border border-zinc-900 text-left hover:border-red-600 transition">
                        <div class="font-bold text-sm text-zinc-100">310 Diamantes</div>
                        <div class="text-xs text-amber-400 font-semibold">$35.00 MXN</div>
                    </button>
                    <button onclick="seleccionarPaquete(this, '520 Diamantes', '58.00')" class="paquete-btn p-3 rounded-xl bg-black border border-zinc-900 text-left hover:border-red-600 transition">
                        <div class="font-bold text-sm text-zinc-100">520 Diamantes</div>
                        <div class="text-xs text-amber-400 font-semibold">$58.00 MXN</div>
                    </button>
                    <button onclick="seleccionarPaquete(this, '400 Robux', '95.00')" class="paquete-btn p-3 rounded-xl bg-black border border-zinc-900 text-left hover:border-red-600 transition">
                        <div class="font-bold text-sm text-zinc-100">400 Robux</div>
                        <div class="text-xs text-amber-400 font-semibold">$95.00 MXN</div>
                    </button>
                </div>
            </div>

            <button onclick="realizarCompra()" class="w-full py-4 rounded-xl bg-red-600 hover:bg-red-500 text-white font-black tracking-wide transition shadow-lg shadow-red-600/20">
                PROCESAR RECARGA
            </button>
        </div>
    </main>

    <!-- PANEL ADMIN -->
    <div id="adminPanel" class="hidden fixed inset-0 bg-black z-50 p-4 overflow-y-auto">
        <div class="max-w-md mx-auto bg-zinc-950 border border-amber-500/30 rounded-3xl p-6">
            <div class="flex justify-between items-center mb-6">
                <h2 class="text-lg font-black text-amber-400">🛡️ Panel de Control - Lyv</h2>
                <button onclick="cerrarAdmin()" class="text-xs bg-zinc-900 px-3 py-1 rounded-lg text-zinc-400 hover:text-white">Cerrar</button>
            </div>

            <div class="grid grid-cols-2 gap-3 mb-6">
                <div class="bg-black border border-zinc-900 p-4 rounded-2xl text-center">
                    <div class="text-xs text-zinc-500 uppercase">Ventas Totales</div>
                    <div id="totalVentas" class="text-xl font-black text-amber-400">$0.00</div>
                </div>
                <div class="bg-black border border-zinc-900 p-4 rounded-2xl text-center">
                    <div class="text-xs text-zinc-500 uppercase">Pedidos</div>
                    <div id="totalPedidos" class="text-xl font-black text-red-500">0</div>
                </div>
            </div>

            <h3 class="text-xs font-semibold text-zinc-400 uppercase tracking-wider mb-3">Últimas Solicitudes</h3>
            <div id="listaPedidos" class="space-y-3">
                <p class="text-xs text-zinc-600 text-center py-4">No hay pedidos registrados aún.</p>
            </div>
        </div>
    </div>

    <footer class="text-center py-4 text-[10px] text-zinc-600 border-t border-zinc-900">
        Lyv Store MX &bull; Panel Operado desde iPhone
    </footer>

    <script>
        let itemSeleccionado = null;
        let pedidos = [];

        function iniciarSesion(proveedor) {
            document.getElementById('loginSection').style.display = 'none';
        }

        function cerrarSesion() {
            document.getElementById('loginSection').style.display = 'flex';
        }

        function seleccionarPaquete(elemento, nombre, precio) {
            document.querySelectorAll('.paquete-btn').forEach(btn => {
                btn.classList.remove('border-red-600', 'bg-red-950/20');
            });
            elemento.classList.add('border-red-600', 'bg-red-950/20');
            itemSeleccionado = { nombre, precio: parseFloat(precio) };
        }

        function realizarCompra() {
            const playerId = document.getElementById('playerId').value.trim();
            if (!playerId) {
                alert('⚠️ Ingresa tu ID de jugador.');
                return;
            }
            if (!itemSeleccionado) {
                alert('⚠️ Selecciona un paquete.');
                return;
            }

            const nuevoPedido = {
                id: playerId,
                paquete: itemSeleccionado.nombre,
                monto: itemSeleccionado.precio,
                fecha: new Date().toLocaleTimeString()
            };
            pedidos.push(nuevoPedido);
            actualizarPanelAdmin();

            alert(`✅ ¡Recarga solicitada con éxito!\nID: ${playerId}\nPaquete: ${itemSeleccionado.nombre}`);
            document.getElementById('playerId').value = '';
        }

        function verificarAdmin() {
            const pin = prompt("🔐 Ingresa tu PIN de Administrador:");
            if (pin === "1234") {
                document.getElementById('adminPanel').classList.remove('hidden');
            } else if (pin !== null) {
                alert("❌ PIN incorrecto");
            }
        }

        function cerrarAdmin() {
            document.getElementById('adminPanel').classList.add('hidden');
        }

        function actualizarPanelAdmin() {
            document.getElementById('totalPedidos').innerText = pedidos.length;
            let suma = pedidos.reduce((acc, curr) => acc + curr.monto, 0);
            document.getElementById('totalVentas').innerText = `$${suma.toFixed(2)} MXN`;

            const contenedor = document.getElementById('listaPedidos');
            if (pedidos.length === 0) {
                contenedor.innerHTML = `<p class="text-xs text-zinc-600 text-center py-4">No hay pedidos registrados aún.</p>`;
                return;
            }

            contenedor.innerHTML = pedidos.map(p => `
                <div class="bg-black border border-zinc-900 p-3 rounded-xl flex justify-between items-center">
                    <div>
                        <div class="text-xs font-bold text-white">ID: ${p.id}</div>
                        <div class="text-[10px] text-amber-400">${p.paquete} - $${p.monto} MXN</div>
                    </div>
                    <span class="text-[10px] bg-red-950/40 text-red-500 border border-red-900/50 px-2 py-1 rounded">Pendiente</span>
                </div>
            `).join('');
        }
    </script>
</body>
</html>
