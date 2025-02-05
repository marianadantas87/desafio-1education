# Desafio OneEducation

## Aplicação Prática - Fase I

Neste desafio, você desenvolverá uma aplicação que permita aos usuários inserir nomes de amigos em uma lista para, em seguida, realizar um sorteio aleatório e determinar quem será o "amigo secreto".

### Funcionalidades:
- Adicionar nomes de amigos a uma lista por meio de um campo de texto e um botão "Adicionar".
- Exibir os nomes adicionados em uma lista visível na página.
- Realizar um sorteio aleatório ao pressionar o botão "Sortear Amigo".
- Garantir que o sorteio seja válido e exibir o resultado na tela.

### Como usar:
1. Digite um nome no campo de entrada e clique em "Adicionar".
2. Repita o processo para adicionar mais participantes.
3. Após adicionar pelo menos dois nomes, clique em "Sortear Amigo" para ver o resultado.


// Lista para armazenar os amigos
let amigos = [];

// Função para adicionar um amigo à lista
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

// Atualiza a lista exibida na tela
function atualizarLista() {
    const lista = document.getElementById("listaAmigos");
    lista.innerHTML = "";
    
    amigos.forEach(nome => {
        const li = document.createElement("li");
        li.textContent = nome;
        lista.appendChild(li);
    });
}

// Embaralha a lista de amigos usando o algoritmo de Fisher-Yates
function embaralhar(array) {
    for (let i = array.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [array[i], array[j]] = [array[j], array[i]];
    }
}

// Função para sortear um amigo secreto
function sortearAmigo() {
    if (amigos.length < 2) {
        alert("Adicione pelo menos dois nomes para realizar o sorteio.");
        return;
    }

    let sorteioValido = false;
    let sorteados;
    let tentativas = 0;
    const maxTentativas = 100; // Para evitar loops infinitos

    while (!sorteioValido && tentativas < maxTentativas) {
        sorteados = [...amigos];
        embaralhar(sorteados);

        // Garante que ninguém tire a si mesmo
        sorteioValido = !sorteados.some((nome, index) => nome === amigos[index]);
        tentativas++;
    }

    if (!sorteioValido) {
        alert("Não foi possível realizar um sorteio válido. Tente novamente.");
        return;
    }

    // Exibir resultado
    const resultado = document.getElementById("resultado");
    resultado.innerHTML = "<h3>Resultado do Sorteio:</h3>";
    amigos.forEach((nome, index) => {
        resultado.innerHTML += `<p>${nome} → ${sorteados[index]}</p>`;
    });
}

    
    amigos.forEach((nome, index) => {
        const li = document.createElement("li");
        li.textContent = `${nome} → ${sorteados[index]}`;
        resultado.appendChild(li);
    });              
}
