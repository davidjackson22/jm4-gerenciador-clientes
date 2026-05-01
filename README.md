# jm4-gerenciador-clientes
Gerenciador de Clientes com Integração WhatsApp
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>JM4 Gerenciamento de Clientes</title>

<style>
body{
    margin:0;
    font-family:Arial;
    background:#0f0f0f;
    color:white;
}

header{
    background:#111827;
    padding:20px;
    text-align:center;
    font-size:28px;
    font-weight:bold;
    color:#00bfff;
}

.container{
    padding:20px;
}

.card{
    background:#1f2937;
    padding:20px;
    border-radius:15px;
    margin-bottom:20px;
}

input{
    width:100%;
    padding:12px;
    margin-top:10px;
    border:none;
    border-radius:10px;
    background:#374151;
    color:white;
}

button{
    margin-top:15px;
    width:100%;
    padding:12px;
    border:none;
    border-radius:10px;
    background:#00bfff;
    color:white;
    font-weight:bold;
    cursor:pointer;
}

button:hover{
    background:#0099cc;
}

.cliente{
    background:#111827;
    padding:15px;
    border-radius:10px;
    margin-top:10px;
}

.status{
    color:#00ff88;
    font-weight:bold;
}

.delete{
    background:red;
}
</style>
</head>

<body>

<header>
🚀 JM4 GERENCIADOR DE CLIENTES
</header>

<div class="container">

<div class="card">
<h2>Adicionar Cliente</h2>

<input type="text" id="nome" placeholder="Nome do Cliente">
<input type="text" id="whatsapp" placeholder="WhatsApp">
<input type="text" id="plano" placeholder="Plano">
<input type="date" id="vencimento">

<button onclick="adicionarCliente()">
Adicionar Cliente
</button>
</div>

<div class="card">
<h2>Clientes</h2>
<div id="listaClientes"></div>
</div>

</div>

<script>

let clientes = JSON.parse(localStorage.getItem("clientes")) || [];

function salvar(){
    localStorage.setItem("clientes", JSON.stringify(clientes));
}

function adicionarCliente(){

    let nome = document.getElementById("nome").value;
    let whatsapp = document.getElementById("whatsapp").value;
    let plano = document.getElementById("plano").value;
    let vencimento = document.getElementById("vencimento").value;

    if(nome === "" || whatsapp === ""){
        alert("Preencha os campos!");
        return;
    }

    clientes.push({
        nome,
        whatsapp,
        plano,
        vencimento
    });

    salvar();
    mostrarClientes();

    document.getElementById("nome").value = "";
    document.getElementById("whatsapp").value = "";
    document.getElementById("plano").value = "";
    document.getElementById("vencimento").value = "";
}

function deletarCliente(index){
    clientes.splice(index,1);
    salvar();
    mostrarClientes();
}

function mostrarClientes(){

    let lista = document.getElementById("listaClientes");

    lista.innerHTML = "";

    clientes.forEach((cliente,index)=>{

        lista.innerHTML += `
        <div class="cliente">

            <h3>${cliente.nome}</h3>

            <p>📞 ${cliente.whatsapp}</p>

            <p>📺 Plano: ${cliente.plano}</p>

            <p class="status">
            ⏳ Vence em: ${cliente.vencimento}
            </p>

            <a href="https://wa.me/55${cliente.whatsapp}" target="_blank">
            <button>Chamar no WhatsApp</button>
            </a>

            <button class="delete"
            onclick="deletarCliente(${index})">
            Excluir
            </button>

        </div>
        `;
    });

}

mostrarClientes();

</script>

</body>
</html>
