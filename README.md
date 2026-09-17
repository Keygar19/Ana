<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Árbol de Flores Amarillas</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            width: 100%;
            height: 100vh;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            display: flex;
            justify-content: center;
            align-items: center;
            font-family: 'Arial', sans-serif;
            overflow: hidden;
        }

        .contenedor {
            position: relative;
            width: 100%;
            height: 100%;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        /* Lluvia de flores */
        .lluvia-flores {
            position: absolute;
            width: 100%;
            height: 100%;
            overflow: hidden;
            pointer-events: none;
        }

        .flor {
            position: absolute;
            font-size: 2rem;
            opacity: 0.7;
            animation: caida linear infinite;
        }

        @keyframes caida {
            to {
                transform: translateY(100vh) rotate(360deg);
                opacity: 0;
            }
        }

        /* Sección principal */
        .seccion-arbol {
            position: relative;
            z-index: 10;
            text-align: center;
        }

        /* Botón inicial */
        .boton-inicio {
            width: 120px;
            height: 120px;
            border-radius: 50%;
            background: linear-gradient(135deg, #FFD700 0%, #FFA500 100%);
            border: none;
            font-size: 60px;
            cursor: pointer;
            box-shadow: 0 10px 40px rgba(0, 0, 0, 0.3);
            transition: all 0.3s ease;
            display: flex;
            justify-content: center;
            align-items: center;
            position: relative;
        }

        .boton-inicio:hover {
            transform: scale(1.1);
            box-shadow: 0 15px 60px rgba(255, 215, 0, 0.5);
        }

        .boton-inicio:active {
            transform: scale(0.95);
        }

        /* Contenedor de opciones */
        .opciones {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 100%;
            height: 100%;
            display: flex;
            justify-content: center;
            align-items: center;
            opacity: 0;
            visibility: hidden;
            transition: all 0.5s ease;
            z-index: 20;
        }

        .opciones.activo {
            opacity: 1;
            visibility: visible;
        }

        .grid-botones {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 30px;
            position: relative;
            max-width: 450px;
        }
        
        .boton-especial {
            grid-column: 1 / -1;
            width: 180px;
            margin: 0 auto;
        }

        .boton-opcion {
            width: 180px;
            height: 180px;
            border-radius: 50%;
            border: none;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
            transition: all 0.3s ease;
            color: white;
            display: flex;
            justify-content: center;
            align-items: center;
            text-align: center;
            padding: 20px;
        }

        .boton-opcion:hover {
            transform: scale(1.1);
        }

        .boton-opcion:active {
            transform: scale(0.95);
        }

        .boton-esperanza {
            background: linear-gradient(135deg, #FFD700 0%, #FFA500 100%);
        }

        .boton-amor {
            background: linear-gradient(135deg, #FF6B6B 0%, #FF4757 100%);
        }

        .boton-dudas {
            background: linear-gradient(135deg, #4ECDC4 0%, #44A08D 100%);
        }

        .boton-fe {
            background: linear-gradient(135deg, #9B59B6 0%, #8E44AD 100%);
        }

        .boton-foto {
            background: linear-gradient(135deg, #FF69B4 0%, #FF1493 100%);
        }

        /* Mensaje emergente */
        .mensaje-emergente {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%) scale(0);
            background: white;
            padding: 40px;
            border-radius: 20px;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.4);
            max-width: 500px;
            text-align: center;
            z-index: 30;
            transition: transform 0.4s ease;
            color: #333;
        }

        .mensaje-emergente.mostrar {
            transform: translate(-50%, -50%) scale(1);
        }

        .mensaje-emergente h2 {
            color: #667eea;
            margin-bottom: 20px;
            font-size: 28px;
        }

        .mensaje-emergente p {
            line-height: 1.6;
            margin-bottom: 30px;
            font-size: 16px;
        }

        .boton-cerrar {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            padding: 12px 30px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 14px;
            transition: all 0.3s ease;
        }

        .boton-cerrar:hover {
            transform: scale(1.05);
        }

        /* Título */
        h1 {
            position: absolute;
            top: 30px;
            color: white;
            font-size: 32px;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
        }

        /* Instrucción */
        .instruccion {
            position: absolute;
            bottom: 30px;
            color: rgba(255, 255, 255, 0.8);
            font-size: 14px;
        }
    </style>
</head>
<body>
    <div class="contenedor">
        <h1>✨ Eres la razón de mis días 💛</h1>
        
        <!-- Lluvia de flores -->
        <div class="lluvia-flores" id="lluviaFlores"></div>

        <!-- Sección del árbol -->
        <div class="seccion-arbol">
            <button class="boton-inicio" id="botonInicio" title="Toca para explorar">❓</button>
            
            <div class="opciones" id="opciones">
                <div class="grid-botones">
                    <button class="boton-opcion boton-esperanza" id="btn-esperanza">💫 Esperanza</button>
                    <button class="boton-opcion boton-amor" id="btn-amor">❤️ Amor</button>
                    <button class="boton-opcion boton-dudas" id="btn-dudas">❓ Dudas</button>
                    <button class="boton-opcion boton-fe" id="btn-fe">✨ Fe</button>
                    <button class="boton-opcion boton-foto boton-especial" id="btn-foto">📱 Tu Foto</button>
                </div>
            </div>
        </div>

        <!-- Mensaje emergente -->
        <div class="mensaje-emergente" id="mensaje">
            <h2 id="tituloMensaje"></h2>
            <p id="contenidoMensaje"></p>
            <button class="boton-cerrar" onclick="cerrarMensaje()">Cerrar</button>
        </div>

        <div class="instruccion">Presiona el botón con ❓ para comenzar</div>
    </div>

    <script>
        const botonInicio = document.getElementById('botonInicio');
        const opciones = document.getElementById('opciones');
        const mensaje = document.getElementById('mensaje');
        const lluviaFlores = document.getElementById('lluviaFlores');

        const mensajes = {
            esperanza: {
                titulo: "💫 Esperanza",
                contenido: "Hice este árbol para ti porque crees en cosas hermosas. Espero que en tu silencio encuentres claridad y que cuando regreses, podamos construir algo hermoso juntos. Nunca pierdo la esperanza en nosotros. 🌅"
            },
            amor: {
                titulo: "❤️ Amor",
                contenido: "Cada flor amarilla representa lo que siento por ti. No es fácil cuando no me respondes, pero el amor verdadero espera. Quiero que sepas que aquí estoy, dispuesto a escuchar todo lo que tengas que decirme. 💛"
            },
            dudas: {
                titulo: "❓ Dudas",
                contenido: "Tengo dudas también. ¿Qué pasó? ¿Qué hice mal? Pero más que dudas, tengo certeza de que tú importas. No me importa cuál sea tu respuesta, solo quiero que hables conmigo. Merecemos una conversación honesta. 🤔"
            },
            fe: {
                titulo: "✨ Fe",
                contenido: "Tengo fe en que esto que creamos juntos es real y vale la pena. Tengo fe en que tu silencio no es el final, sino tal vez el comienzo de algo mejor. Te pido que tengas fe en nosotros también. ✨"
            },
            foto: {
                titulo: "📱 Tu Foto",
                contenido: "Cada mañana enciendo mi celular y lo primero que veo es tu foto. No importa cuántas veces la haya visto, siempre me sonríes igual. Eres lo primero en mi día y lo último en mis pensamientos. Eres mi razón para encender la pantalla. 📸💕"
            }
        };

        // Crear lluvia de flores
        function crearFlor() {
            const flor = document.createElement('div');
            flor.className = 'flor';
            flor.textContent = '🌼';
            flor.style.left = Math.random() * 100 + '%';
            flor.style.animationDuration = (Math.random() * 2 + 3) + 's';
            flor.style.animationDelay = Math.random() * 2 + 's';
            flor.style.fontSize = (Math.random() * 1.5 + 1.5) + 'rem';
            lluviaFlores.appendChild(flor);

            setTimeout(() => flor.remove(), 5000);
        }

        // Generar lluvia continua - más flores
        setInterval(crearFlor, 100);

        // Eventos de los botones
        botonInicio.addEventListener('click', () => {
            opciones.classList.add('activo');
            botonInicio.style.display = 'none';
        });

        document.getElementById('btn-esperanza').addEventListener('click', () => {
            mostrarMensaje('esperanza');
        });

        document.getElementById('btn-amor').addEventListener('click', () => {
            mostrarMensaje('amor');
        });

        document.getElementById('btn-dudas').addEventListener('click', () => {
            mostrarMensaje('dudas');
        });

        document.getElementById('btn-fe').addEventListener('click', () => {
            mostrarMensaje('fe');
        });

        document.getElementById('btn-foto').addEventListener('click', () => {
            mostrarMensaje('foto');
        });

        function mostrarMensaje(tipo) {
            document.getElementById('tituloMensaje').textContent = mensajes[tipo].titulo;
            document.getElementById('contenidoMensaje').textContent = mensajes[tipo].contenido;
            mensaje.classList.add('mostrar');
        }

        function cerrarMensaje() {
            mensaje.classList.remove('mostrar');
            opciones.classList.remove('activo');
            botonInicio.style.display = 'flex';
        }
    </script>
</body>
</html>
