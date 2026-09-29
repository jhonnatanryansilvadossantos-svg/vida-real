# vida-real<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>VIDA REAL - Simulador Completo</title>
    <style>
        *{margin:0;padding:0;box-sizing:border-box;font-family:'Segoe UI',sans-serif}
        :root{--fundo:#121212;--escuro:#1e1e1e;--destaque:#b8860b;--texto:#f0f0f0;--botao:#2a2a2a;--sucesso:#008000;--erro:#cc0000}
        body{background:var(--fundo);color:var(--texto);min-height:100vh}
        .tela{display:none;padding:20px;max-width:500px;margin:0 auto}
        .ativa{display:block}
        h1,h2{text-align:center;margin-bottom:20px;color:var(--destaque)}
        input,select,button{width:100%;padding:12px;margin:8px 0;border:none;border-radius:8px;font-size:16px}
        input,select{background:var(--escuro);color:var(--texto);border:1px solid #444}
        button{background:var(--destaque);color:#000;font-weight:bold;cursor:pointer;transition:.2s}
        button:hover{transform:scale(1.02);filter:brightness(1.2)}
        .card{background:var(--escuro);padding:20px;border-radius:12px;margin:15px 0;border-left:3px solid var(--destaque)}
        .linha{display:flex;gap:10px;flex-wrap:wrap}
        .linha button{flex:1;min-width:120px}
        .status{position:fixed;top:10px;right:10px;background:var(--escuro);padding:10px;border-radius:8px;font-size:12px;z-index:100}
        .escondido{display:none}
    </style>
</head>
<body>
    <div class="status" id="status">
        <div id="info-jogo">Carregando...</div>
    </div>

    <!-- TELA DE LOGIN -->
    <div class="tela ativa" id="tela-login">
        <h1>🔒 VIDA REAL</h1>
        <h3 style="text-align:center;opacity:.7;margin-bottom:30px;">Simulador Exclusivo</h3>
        <div class="card">
            <label>Digite seu código de acesso:</label>
            <input type="text" id="codigo-acesso" placeholder="Ex: VR-928-BRASIL-REAL">
            <button onclick="verificarCodigo()">ENTRAR</button>
            <p style="text-align:center;margin-top:15px;font-size:12px;opacity:.6;">Só pessoas com o código conseguem entrar</p>
        </div>
    </div>

    <!-- TELA PRINCIPAL -->
    <div class="tela" id="tela-principal">
        <h1>👤 <span id="nome-jogador">Jogador</span></h1>
        <div class="card">
            <p><strong>Idade:</strong> <span id="idade">0</span> anos</p>
            <p><strong>Dinheiro:</strong> R$ <span id="dinheiro">0</span></p>
            <p><strong>Reputação:</strong> <span id="reputacao">Neutra</span></p>
            <p><strong>Cidade:</strong> <span id="cidade">Brasília - DF</span></p>
        </div>
        
        <h2 style="margin-top:30px;">MENU PRINCIPAL</h2>
        <div class="linha">
            <button onclick="ir('criar')">🧍 Personagem</button>
            <button onclick="ir('vida')">⚖️ Vida</button>
            <button onclick="ir('crime')">🔫 Submundo</button>
            <button onclick="ir('bens')">🏎️ Bens</button>
            <button onclick="ir('familia')">👨‍👩‍👧‍👦 Família</button>
            <button onclick="avancarTempo()">⏩ Avançar 1 Mês</button>
        </div>
    </div>

    <!-- TELA CRIAÇÃO -->
    <div class="tela" id="tela-criar">
        <h1>🧍 Criar Personagem</h1>
        <div class="card">
            <label>Nome:</label>
            <input type="text" id="inp-nome">
            <label>Sobrenome:</label>
            <input type="text" id="inp-sobrenome">
            <label>Idade:</label>
            <input type="number" id="inp-idade" min="0" max="100" value="18">
            <label>Cidade:</label>
            <input type="text" id="inp-cidade" value="Brasília - DF">
            <label>Tipo de cabelo:</label>
            <select id="inp-cabelo">
                <option>Liso</option><option>Cacheado</option><option>Crespo</option>
                <option>Dreads</option><option>Tranças</option><option>Curto</option><option>Longo</option>
            </select>
            <label>Estilo de roupa:</label>
            <select id="inp-roupa">
                <option>Nike</option><option>Gucci</option><option>Supreme</option>
                <option>Lacoste</option><option>Oakley</option><option>Misto</option>
            </select>
            <button onclick="salvarPersonagem()">✅ Salvar</button>
        </div>
        <button onclick="ir('principal')">← Voltar</button>
    </div>

    <!-- TELA SUBMUNDO -->
    <div class="tela" id="tela-crime">
        <h1>🔫 Submundo & Organização</h1>
        <div class="card">
            <h3>Sua Organização</h3>
            <p>Nome: <span id="nome-org">Não criada</span></p>
            <p>Membros: <span id="qtd-membros">0</span></p>
            <p>Territórios: <span id="territorios">0</span></p>
            <button onclick="criarOrganizacao()">🏴 Criar Organização</button>
            <button onclick="recrutar()">👥 Recrutar Membro</button>
            <button onclick="assalto()">💰 Realizar Assalto</button>
            <button onclick="banco()">🏦 Assalto ao Banco</button>
        </div>
        <button onclick="ir('principal')">← Voltar</button>
    </div>

    <!-- TELA BENS -->
    <div class="tela" id="tela-bens">
        <h1>🏎️ Bens & Propriedades</h1>
        <div class="card">
            <h3>Garagem</h3>
            <p id="lista-carros">Nenhum carro ainda</p>
            <button onclick="comprarCarro()">🚘 Comprar Carro</button>
        </div>
        <div class="card">
            <h3>Imóveis</h3>
            <p id="lista-imoveis">Nenhum imóvel ainda</p>
            <button onclick="comprarImovel()">🏠 Comprar Imóvel</button>
        </div>
        <button onclick="ir('principal')">← Voltar</button>
    </div>

    <!-- TELA FAMÍLIA -->
    <div class="tela" id="tela-familia">
        <h1>👨‍👩‍👧‍👦 Família & Códigos</h1>
        <div class="card">
            <p><strong>Seu código principal:</strong></p>
            <input type="text" value="VR-928-BRASIL-REAL" readonly>
            <button onclick="copiarTexto('VR-928-BRASIL-REAL')">📋 Copiar Código</button>
            <br><br>
            <p><strong>Código para família jogar com você:</strong></p>
            <input type="text" value="VR-FAMILIA-7X9P" readonly>
            <button onclick="copiarTexto('VR-FAMILIA-7X9P')">📋 Copiar Código Família</button>
            <p style="margin-top:15px;font-size:13px;opacity:.7;">Só quem tiver o código consegue entrar no seu mundo. Não compartilhe com estranhos.</p>
        </div>
        <button onclick="ir('principal')">← Voltar</button>
    </div>

    <!-- TELA VIDA -->
    <div class="tela" id="tela-vida">
        <h1>⚖️ Vida & Escolhas</h1>
        <div class="card">
            <h3>Relacionamentos</h3>
            <p id="lista-relacionamentos">Solteiro(a)</p>
            <button onclick="relacionamento()">❤️ Novo Relacionamento</button>
        </div>
        <div class="card">
            <h3>Carreira</h3>
            <p id="carreira">Desempregado(a)</p>
            <button onclick="trabalho()">💼 Conseguir Emprego</button>
        </div>
        <button onclick="ir('principal')">← Voltar</button>
    </div>

<script>
// DADOS DO JOGO
let jogo = {
    nome: '', sobrenome: '', idade: 18, dinheiro: 10000, reputacao: 50,
    cidade: 'Brasília - DF', cabelo: '', estilo: '',
    org: {nome: '', membros: 0, territorios: 0},
    carros: [], imoveis: [], relacionamentos: [], carreira: ''
};

const CODIGO_CORRETO = 'VR-928-BRASIL-REAL';

function verificarCodigo(){
    const digitado = document.getElementById('codigo-acesso').value.trim().toUpperCase();
    if(digitado === CODIGO_CORRETO || digitado === 'VR-FAMILIA-7X9P'){
        ir('principal');
        carregarDados();
    }else{
        alert('❌ Código incorreto. Verifique e tente novamente.');
    }
}

function ir(tela){
    document.querySelectorAll('.tela').forEach(t => t.classList.remove('ativa'));
    document.getElementById('tela-'+tela).classList.add('ativa');
    atualizarStatus();
}

function salvarPersonagem(){
    jogo.nome = document.getElementById('inp-nome').value || 'Jogador';
    jogo.sobrenome = document.getElementById('inp-sobrenome').value || '';
    jogo.idade = parseInt(document.getElementById('inp-idade').value);
    jogo.cidade = document.getElementById('inp-cidade').value;
    jogo.cabelo = document.getElementById('inp-cabelo').value;
    jogo.estilo = document.getElementById('inp-roupa').value;
    salvarDados();
    atualizarStatus();
    ir('principal');
    alert('✅ Personagem salvo!');
}

function atualizarStatus(){
    document.getElementById('nome-jogador').textContent = jogo.nome + ' ' + jogo.sobrenome;
    document.getElementById('idade').textContent = jogo.idade;
    document.getElementById('dinheiro').textContent = jogo.dinheiro.toLocaleString('pt-BR');
    document.getElementById('reputacao').textContent = jogo.reputacao > 70 ? 'Excelente' : jogo.reputacao > 40 ? 'Neutra' : 'Perigosa';
    document.getElementById('cidade').textContent = jogo.cidade;
    document.getElementById('nome-org').textContent = jogo.org.nome || 'Não criada';
    document.getElementById('qtd-membros').textContent = jogo.org.membros;
    document.getElementById('territorios').textContent = jogo.org.territorios;
}

function avancarTempo(){
    jogo.idade += 1/12; // 1 mês
    jogo.dinheiro += Math.floor(Math.random() * 500);
    salvarDados();
    atualizarStatus();
    alert('⏩ Um mês se passou...');
}

function criarOrganizacao(){
    const nome = prompt('Digite o nome da sua organização:');
    if(nome){
        jogo.org.nome = nome;
        jogo.org.membros = 1;
        jogo.reputacao -= 5;
        salvarDados();
        atualizarStatus();
        alert(`🏴 Organização "${nome}" criada com sucesso!`);
    }
}

function recrutar(){
    if(!jogo.org.nome){alert('Crie sua organização primeiro!');return;}
    jogo.org.membros++;
    jogo.dinheiro -= 200;
    salvarDados();
    atualizarStatus();
    alert('👥 Novo membro recrutado!');
}

function assalto(){
    const sucesso = Math.random() > 0.3;
    if(sucesso){
        const ganho = Math.floor(Math.random() * 5000) + 1000;
        jogo.dinheiro += ganho;
        alert(`💰 Assalto realizado! Ganhou R$ ${ganho.toLocaleString('pt-BR')}`);
    }else{
        jogo.reputacao -= 10;
        alert('⚠️ Algo deu errado... a polícia passou perto.');
    }
    salvarDados(); atualizarStatus();
}

function banco(){
    if(jogo.org.membros < 3){alert('Precisa de pelo menos 3 membros para assaltar o banco!');return;}
    const sucesso = Math.random() > 0.5;
    if(sucesso){
        const ganho = Math.floor(Math.random() * 50000) + 10000;
        jogo.dinheiro += ganho;
        jogo.reputacao -= 20;
        alert(`🏦 SUCESSO! Levou R$ ${ganho.toLocaleString('pt-BR')}! Agora é o mais procurado.`);
    }else{
        jogo.dinheiro -= 5000;
        alert('🚨 FALHA! Tiveram que fugir a pé. Perdeu dinheiro no processo.');
    }
    salvarDados(); atualizarStatus();
}

function comprarCarro(){
    const carros = ['Lamborghini Huracán', 'Ferrari Roma', 'Mercedes-Benz AMG', 'BMW M5', 'Porsche 911'];
    const preco = [450000, 600000, 180000, 250000, 350000];
    let lista = carros.map((c,i) => `${i+1}. ${c} - R$ ${preco[i].toLocaleString('pt-BR')}`).join('\n');
    const escolha = prompt(`Qual carro quer comprar?\n\n${lista}\n\nDigite o número:`);
    const idx = parseInt(escolha)-1;
    if(idx >= 0 && idx < carros.length){
        if(jogo.dinheiro >= preco[idx]){
            jogo.dinheiro -= preco[idx];
            jogo.carros.push(carros[idx]);
            document.getElementById('lista-carros').innerHTML = jogo.carros.join('<br>');
            alert(`🚘 ${carros[idx]} comprado!`);
        }else{alert('Dinheiro insuficiente!');}
    }
    salvarDados(); atualizarStatus();
}

function relacionamento(){
    const nomes = ['Ana', 'Juliana', 'Beatriz', 'Larissa', 'Camila', 'Mariana'];
    const nome = nomes[Math.floor(Math.random()*nomes.length)];
    jogo.relacionamentos.push(nome);
    document.getElementById('lista-relacionamentos').innerHTML = jogo.relacionamentos.join('<br>');
    alert(`❤️ ${nome} aceitou seu relacionamento! Você tem ${jogo.relacionamentos.length} parceira(s).`);
    salvarDados();
}

function trabalho(){
    const cargos = ['Policial', 'Empresário', 'Advogado', 'Esportista', 'Engenheiro'];
    const escolha = prompt(`Qual carreira quer seguir?\n\n1. Policial\n2. Empresário\n3. Advogado\n4. Esportista\n5. Engenheiro\n\nDigite o número:`);
    const idx = parseInt(escolha)-1;
    if(idx >=0 && idx < cargos.length){
        jogo.carreira = cargos[idx];
        jogo.dinheiro += 3000;
        document.getElementById('carreira').textContent = jogo.carreira;
        alert(`💼 Agora trabalha como ${jogo.carreira}! Salário mensal: R$ 3.000+`);
    }
    salvarDados(); atualizarStatus();
}

function copiarTexto(texto){
    navigator.clipboard.writeText(texto);
    alert('📋 Código copiado! Envie para quem quiser.');
}

function salvarDados(){
    localStorage.setItem('vidaRealJogo', JSON.stringify(jogo));
}

function carregarDados(){
    const salvo = localStorage.getItem('vidaRealJogo');
    if(salvo) jogo = JSON.parse(salvo);
    atualizarStatus();
    document.getElementById('lista-carros').innerHTML = jogo.carros.join('<br>') || 'Nenhum carro ainda';
    document.getElementById('lista-relacionamentos').innerHTML = jogo.relacionamentos.join('<br>') || 'Solteiro(a)';
    document.getElementById('carreira').textContent = jogo.carreira || 'Desempregado(a)';
}
</script>
</body>
</html>
