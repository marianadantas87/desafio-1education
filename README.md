# desafio-1education
# Aplicação Prática - Fase I
# Neste desafio, você desenvolverá uma aplicação que permita aos usuários inserir nomes de amigos em uma lista para, em seguida, realizar um sorteio aleatório e determinar quem é o "amigo secreto".O usuário deverá adicionar nomes por meio de um campo de texto e de um botão "Adicionar".Os nomes inseridos serão exibidos em uma lista visível na página, e ao finalizar, um botão "Sortear Amigo" selecionará um dos nomes de forma aleatória, exibindo o resultado na tela.#

# Declarar a variável
let amigos = []; 
# Função para inserção do nome no campo
# Condições para nome inválido, repetição e campo em branco
function adicionarAmigo() {
    const inputAmigo = document.getElementById("amigo");
    const nome = inputAmigo.value.trim(); 
    
    if (nome === "") {
        alert("Digite um nome válido.");
        return;
    }
    
    if (amigos.includes(nome)) {
        alert("Esse nome já foi adicionado.");
        return;
    }
    
    amigos.push(nome);
    atualizarLista();
    inputAmigo.value = "";
}                               
# Função para atualização da lista após cada nome inserido
function atualizarLista() {
    const lista = document.getElementById("listaAmigos");
    lista.innerHTML = "";
    amigos.forEach(nome => {
        const li = document.createElement("li");
        li.textContent = nome;
        lista.appendChild(li);
    });
}                            
# Função para ordenação aleatória dos nomes
function embaralhar(array) {
    for (let i = array.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [array[i], array[j]] = [array[j], array[i]];
    }
}                        
# Função número mínimo de nomes
function sortearAmigo() {
    if (amigos.length < 2) {
        alert("Adicione pelo menos dois nomes para realizar o sorteio.");
        return;
    }   
# Declarar variável para a condição de sorteio válido
    let sorteioValido = false; 
# Declarar variável para a lista de nomes sorteados     
    let sorteados;      
# Condição de execução do sorteio (tempo de espera das execuções das funções)
    while (!sorteioValido) {
        sorteados = [...amigos];
        embaralhar(sorteados);
        
        sorteioValido = !sorteados.some((nome, index) => nome === amigos[index]);
    }                
# Interação execução doscódigos do JavaScript com HTML para apresentar o resultado no frontend   
    const resultado = document.getElementById("resultado");
    resultado.innerHTML = "";  
    
    amigos.forEach((nome, index) => {
        const li = document.createElement("li");
        li.textContent = `${nome} → ${sorteados[index]}`;
        resultado.appendChild(li);
    });              
}
