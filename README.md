<!DOCTYPE html>
<html lang="es">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Inkafarma - Sistema Web</title>

    <link rel="stylesheet" href="styles.css">
</head>

<body>

    <header>
        <h1>INKAFARMA</h1>
        <p>Sistema de Registro de Clientes y Productos</p>
    </header>

    <main>

        <!-- REGISTRO DE CLIENTES -->
        <section class="card">

            <h2>Registro de Clientes</h2>

            <form id="clienteForm">

                <input type="text" id="dni" placeholder="DNI" required>

                <input type="text" id="nombre" placeholder="Nombre Completo" required>

                <input type="email" id="correo" placeholder="Correo Electrónico" required>

                <button type="submit">
                    Registrar Cliente
                </button>

            </form>

        </section>

        <!-- PRODUCTOS -->
        <section class="card">

            <h2>Productos Disponibles</h2>

            <div class="productos">

                <div class="producto">
                    <h3>Paracetamol</h3>
                    <p>S/ 5.00</p>
                </div>

                <div class="producto">
                    <h3>Ibuprofeno</h3>
                    <p>S/ 8.50</p>
                </div>

                <div class="producto">
                    <h3>Vitamina C</h3>
                    <p>S/ 12.00</p>
                </div>

                <div class="producto">
                    <h3>Alcohol 70%</h3>
                    <p>S/ 6.00</p>
                </div>

                <div class="producto">
                    <h3>Jarabe para la Tos</h3>
                    <p>S/ 15.00</p>
                </div>

                <div class="producto">
                    <h3>Omeprazol</h3>
                    <p>S/ 18.00</p>
                </div>

            </div>

        </section>

        <!-- LISTA DE CLIENTES -->
        <section class="card">

            <h2>Clientes Registrados</h2>

            <input type="text" id="buscar" placeholder="Buscar por DNI o Nombre">

            <table>

                <thead>
                    <tr>
                        <th>DNI</th>
                        <th>Nombre</th>
                        <th>Correo</th>
                    </tr>
                </thead>

                <tbody id="tablaClientes">

                </tbody>

            </table>

        </section>

    </main>

    <script src="script.js"></script>

</body>

</html> 
css
*{
    margin:0;
    padding:0;
    box-sizing:border-box;
    font-family:Arial, Helvetica, sans-serif;
}

body{
    background:#f5f5f5;
}

header{
    background:#009245;
    color:white;
    text-align:center;
    padding:25px;
}

header h1{
    margin-bottom:10px;
}

main{
    width:90%;
    max-width:1200px;
    margin:20px auto;
}

.card{
    background:white;
    padding:20px;
    border-radius:10px;
    margin-bottom:20px;
    box-shadow:0px 3px 10px rgba(0,0,0,0.2);
}

.card h2{
    margin-bottom:15px;
    color:#009245;
}

form{
    display:flex;
    flex-direction:column;
}

input{
    padding:12px;
    margin-bottom:10px;
    border:1px solid #ccc;
    border-radius:5px;
}

button{
    background:#009245;
    color:white;
    border:none;
    padding:12px;
    border-radius:5px;
    cursor:pointer;
    font-size:16px;
}

button:hover{
    background:#006b32;
}

.productos{
    display:grid;
    grid-template-columns:repeat(auto-fit,minmax(180px,1fr));
    gap:15px;
}

.producto{
    border:1px solid #ddd;
    border-radius:10px;
    padding:15px;
    text-align:center;
    transition:0.3s;
}

.producto:hover{
    transform:scale(1.05);
}

.producto h3{
    color:#009245;
}

.producto p{
    font-weight:bold;
    margin-top:10px;
}

table{
    width:100%;
    border-collapse:collapse;
    margin-top:15px;
}

table th{
    background:#009245;
    color:white;
}

table th,
table td{
    padding:12px;
    border:1px solid #ddd;
    text-align:center;
}

table tr:nth-child(even){
    background:#f2f2f2;
}

#buscar{
    width:100%;
}
jav 
let clientes = [];

const formulario = document.getElementById("clienteForm");
const tablaClientes = document.getElementById("tablaClientes");
const buscador = document.getElementById("buscar");

formulario.addEventListener("submit", function(e){

    e.preventDefault();

    let dni = document.getElementById("dni").value.trim();
    let nombre = document.getElementById("nombre").value.trim();
    let correo = document.getElementById("correo").value.trim();

    if(dni.length !== 8 || isNaN(dni)){
        alert("El DNI debe contener 8 números.");
        return;
    }

    let cliente = {
        dni,
        nombre,
        correo
    };

    clientes.push(cliente);

    mostrarClientes(clientes);

    alert("Cliente registrado correctamente.");

    formulario.reset();

});

function mostrarClientes(lista){

    tablaClientes.innerHTML = "";

    lista.forEach(cliente => {

        tablaClientes.innerHTML += `
            <tr>
                <td>${cliente.dni}</td>
                <td>${cliente.nombre}</td>
                <td>${cliente.correo}</td>
            </tr>
        `;

    });

}

buscador.addEventListener("keyup", function(){

    let texto = buscador.value.toLowerCase();

    let resultado = clientes.filter(cliente =>

        cliente.nombre.toLowerCase().includes(texto) ||
        cliente.dni.includes(texto)

    );

    mostrarClientes(resultado);

});
