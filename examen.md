# Gato
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gato</title>
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/css/bootstrap.min.css" integrity="sha384-9aIt2nRpC12Uk9gS9baDl411NQApFmC26EwAOH8WgZl5MYYxFfc+NcPb1dKGj7Sk" crossorigin="anonymous">
    <link rel="stylesheet" type="text/css" media="screen" href="style.css">
    <style type=text/css>
        section#principal {
            display: inline-block;
            margin: 0 auto;
            text-align: center;
            width: 100%;
        }
        
        article#comandos {
            display: inline-block;
            border-radius: 2px lightgray;
            box-shadow: 10px salmon;
            min-height: 300px;
            vertical-align: top;
            width: 25%;
        }
        
        article#tablero {
            display: inline-block;
            margin: 0 auto;
            text-align: center;
            width: 50%;
        }
        
        article#tablero input {
            font-size: 3rem;
            height: 80px;
            margin: 10 auto;
            width: 80px;
        }
        
        label {
            font-size: 1rem;
            font-weight: bold;
            text-align: center;
        }
        
        .botoninicial {
            color: #77d;
            background-color: #77d;
        }
        
        .botonJugador1 {
            color: white;
            background-color: #d77;
        }
        
        .botonJugador2 {
            color: white;
            background-color: #7d7;
        }
    </style>
    <script type="text/javascript">
        var bandera = false; // indica si el juego inicia
        var turno = 0; // determina el turno
        var tab = new Array(); // Arreglo de botones
        window.onload = function() {
            var iniciar = document.getElementById("iniciar");
            iniciar.addEventListener("click", comenzar);
        }

        function comenzar() {
            bandera = true;
            var jugador1 = document.getElementById("jugador1");
            var jugador2 = document.getElementById("jugador2");
            if (jugador1.value == "") {
                alert("Falta el nombre del jugador 1");
                jugador1.focus();
            } else {
                if (jugador2.value == "") {
                    alert("Falta el nombre del jugador 2");
                    jugador2.focus();
                } else {
                    tab[0] = document.getElementById("b0");
                    tab[1] = document.getElementById("b1");
                    tab[2] = document.getElementById("b2");
                    tab[3] = document.getElementById("b3");
                    tab[4] = document.getElementById("b4");
                    tab[5] = document.getElementById("b5");
                    tab[6] = document.getElementById("b6");
                    tab[7] = document.getElementById("b7");
                    tab[8] = document.getElementById("b8");
                    for (var i = 0; i < 9; i++) {
                        tab[i].className = "botoninicial";
                        tab[i].value = "I";
                    }
                    turno = 1;
                    document.getElementById("turnoJugador").innerHTML =
                        "Es tu turno " + jugador1.value;
                }
            }
        }

        function colocar(boton) {
            if (bandera == true) {
                if (turno == 1 && boton.value == "I") {
                    turno = 2;
                    document.getElementById("turnoJugador").innerHTML =
                        "Es tu turno " + jugador2.value;
                    boton.value = "X";
                    boton.className = "botonJugador1";
                } else {
                    if (turno == 2 && boton.value == "I") {
                        turno = 1;
                        document.getElementById("turnoJugador").innerHTML =
                            "Es tu turno " + jugador1.value;
                        boton.value = "O";
                        boton.className = "botonJugador2";
                    }
                }
            }
            revisar();
        }

        function revisar() {
            if ((tab[0].value == "X" && tab[1].value == "X" && tab[2].value == "X") ||
                (tab[3].value == "X" && tab[4].value == "X" && tab[5].value == "X") ||
                (tab[6].value == "X" && tab[7].value == "X" && tab[8].value == "X") ||
                (tab[0].value == "X" && tab[3].value == "X" && tab[6].value == "X") ||
                (tab[1].value == "X" && tab[4].value == "X" && tab[7].value == "X") ||
                (tab[2].value == "X" && tab[5].value == "X" && tab[8].value == "X") ||
                (tab[0].value == "X" && tab[4].value == "X" && tab[8].value == "X") ||
                (tab[2].value == "X" && tab[4].value == "X" && tab[6].value == "X")
            ) {
                alert("Felicidades ganaste" + jugador1.value);
                bandera = false;
            }

            if ((tab[0].value == "O" && tab[1].value == "O" && tab[2].value == "O") ||
                (tab[3].value == "O" && tab[4].value == "O" && tab[5].value == "O") ||
                (tab[6].value == "O" && tab[7].value == "O" && tab[8].value == "O") ||
                (tab[0].value == "O" && tab[3].value == "O" && tab[6].value == "O") ||
                (tab[1].value == "O" && tab[4].value == "O" && tab[7].value == "O") ||
                (tab[2].value == "O" && tab[5].value == "O" && tab[8].value == "O") ||
                (tab[0].value == "O" && tab[4].value == "O" && tab[8].value == "O") ||
                (tab[2].value == "O" && tab[4].value == "O" && tab[6].value == "O")
            ) {
                alert("Felicidades ganaste " + jugador2.value);
                bandera = false;
            }
        }
    </script>
</head>

<body>
    <h1 class="text-center">Bienvenido a este juego</h1>
    <section id="principal">
        <div class="row mt-4"></div>
        <article id="comandos">
            Jugador 1:
            <input class="mt-4" type="text" id="jugador1">
            <br> Jugador 2:
            <input class="mt-4" type="text" id="jugador2">
            <br>
            <input class="mt-4" type="button" id="iniciar" value="Comenzar"><br>
            <label id="turnoJugador"></label>
        </article>
        </div>
        <article id="tablero">
            <input type="button" id="b0" onclick="colocar(this)">
            <input type="button" id="b1" onclick="colocar(this)">
            <input type="button" id="b2" onclick="colocar(this)"><br>

            <input type="button" id="b3" onclick="colocar(this)">
            <input type="button" id="b4" onclick="colocar(this)">
            <input type="button" id="b5" onclick="colocar(this)"><br>

            <input type="button" id="b6" onclick="colocar(this)">
            <input type="button" id="b7" onclick="colocar(this)">
            <input type="button" id="b8" onclick="colocar(this)"><br>

        </article>
    </section>
</body>

</html>
