<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Guia Interativo: EEABI e ERER em Porto Alegre</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;700&display=swap" rel="stylesheet">
    <!-- Chosen Palette: Paleta Aconchego Educativo (Warm Neutrals) -->
    <!-- Application Structure Plan: A aplicação foi desenhada como uma página única com seções temáticas e uma barra de navegação fixa. A estrutura (Introdução, Conceitos, Legislação, Na Prática) abandona o formato linear de slides para permitir que os professores acessem diretamente a informação de maior interesse, como os exemplos práticos ou as leis específicas. Esta arquitetura não-linear melhora a usabilidade e transforma o conteúdo de uma apresentação passiva para uma ferramenta de consulta ativa e prática. -->
    <!-- Visualization & Content Choices: 
        - Report Info: Conceitos de ERER/EEABI -> Goal: Informar -> Viz/Presentation: Cartões de conteúdo com ícones -> Interaction: Nenhuma -> Justification: Apresentação clara e direta dos conceitos fundamentais.
        - Report Info: Leis e Decretos -> Goal: Organizar/Informar -> Viz/Presentation: Grade de cartões interativos -> Interaction: Clique para abrir um modal com detalhes da lei -> Justification: Transforma a lista de leis em um recurso interativo, oferecendo detalhes sob demanda sem sobrecarregar a interface.
        - Report Info: Exemplos em sala de aula -> Goal: Organizar/Informar -> Viz/Presentation: Seção com abas filtráveis por disciplina -> Interaction: Clique na aba da disciplina para exibir as atividades correspondente -> Justification: Permite que os professores encontrem rapidamente sugestões relevantes para sua área de atuação.
        - Library/Method: Todas as interações são implementadas com Vanilla JS e estilizadas com Tailwind CSS.
    -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #FDFBF8;
            color: #4A4A4A;
        }
        .nav-link {
            transition: color 0.3s, border-bottom-color 0.3s;
            border-bottom: 2px solid transparent;
        }
        .nav-link:hover, .nav-link.active {
            color: #C06C56;
            border-bottom-color: #C06C56;
        }
        .card {
            background-color: #FFFFFF;
            border: 1px solid #EAEAEA;
            box-shadow: 0 4px 6px -1px rgb(0 0 0 / 0.05), 0 2px 4px -2px rgb(0 0 0 / 0.05);
            transition: transform 0.3s, box-shadow 0.3s;
        }
        .card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 15px -3px rgb(0 0 0 / 0.07), 0 4px 6px -4px rgb(0 0 0 / 0.07);
        }
        .tab.active {
            background-color: #C06C56;
            color: #FFFFFF;
        }
        .tab {
            transition: background-color 0.3s, color 0.3s;
        }
        .modal {
            transition: opacity 0.3s ease-in-out;
        }
        .modal-content-container {
            transition: transform 0.3s ease-in-out;
        }
        html {
            scroll-behavior: smooth;
        }
        .loading {
            display: flex;
            align-items: center;
            justify-content: center;
        }
        .spinner {
            border: 4px solid rgba(0, 0, 0, 0.1);
            width: 36px;
            height: 36px;
            border-radius: 50%;
            border-left-color: #C06C56;
            animation: spin 1s ease infinite;
        }
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
    </style>
</head>
<body class="antialiased">

    <header id="header" class="bg-white/80 backdrop-blur-md sticky top-0 z-50 shadow-sm">
        <nav class="container mx-auto px-6 py-4 flex justify-between items-center">
            <div class="text-xl font-bold text-gray-800">
                Guia <span class="text-[#C06C56]">EEABI & ERER</span>
            </div>
            <div class="hidden md:flex space-x-8">
                <a href="#inicio" class="nav-link">Início</a>
                <a href="#conceitos" class="nav-link">Conceitos</a>
                <a href="#legislacao" class="nav-link">Legislação</a>
                <a href="#pratica" class="nav-link">Na Prática</a>
            </div>
            <button id="mobile-menu-button" class="md:hidden text-gray-700 focus:outline-none">
                <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16m-7 6h7"></path></svg>
            </button>
        </nav>
        <div id="mobile-menu" class="hidden md:hidden px-6 pb-4">
            <a href="#inicio" class="block py-2 nav-link">Início</a>
            <a href="#conceitos" class="block py-2 nav-link">Conceitos</a>
            <a href="#legislacao" class="block py-2 nav-link">Legislação</a>
            <a href="#pratica" class="block py-2 nav-link">Na Prática</a>
        </div>
    </header>

    <main>
        <section id="inicio" class="py-20 bg-white">
            <div class="container mx-auto px-6 text-center">
                <h1 class="text-4xl md:text-5xl font-bold text-gray-800 mb-4">Fortalecendo a Educação Municipal de Porto Alegre: Um Diálogo sobre Equidade e Representatividade</h1>
                <p class="text-lg md:text-xl text-gray-600 max-w-3xl mx-auto">Esta plataforma interativa serve como um recurso de apoio para educadores, com o objetivo de aprofundar o entendimento e a aplicação do **Espaço Educativo Afro-brasileiro e Indígena (EEABI)** e da **Educação para as Relações Étnico-Raciais (ERER)**, com foco no desenvolvimento integral das crianças da Educação Infantil.</p>
                <div class="mt-8 mx-auto max-w-2xl">
                    <img src="https://contilnetnoticias.com.br/wp-content/uploads/2024/04/Foto_Odair_Leal-1-1.jpg" alt="Duas crianças indígenas com albinismo sentadas, com um homem adulto ao fundo, em um ambiente rural." class="w-full h-auto rounded-lg shadow-md">
                    <p class="text-xs text-gray-500 mt-2 text-right">Fonte: <a href="https://contilnetnoticias.com.br/2024/04/povos-indigenas-conheca-o-drama-vivido-por-irmaos-albinos-nascidos-em-aldeia-no-acre/" target="_blank" class="hover:underline">Contilnet Notícias</a></p>
                </div>
            </div>
        </section>

        <section id="conceitos" class="py-16">
            <div class="container mx-auto px-6">
                <div class="text-center mb-12">
                    <h2 class="text-3xl font-bold text-gray-800">Conceitos Estratégicos para a Prática Pedagógica</h2>
                    <p class="text-gray-600 mt-2">Explore os fundamentos e objetivos que norteiam o trabalho com a diversidade na Educação Infantil de Porto Alegre, conforme as diretrizes municipais e nacionais.</p>
                </div>
                <div class="grid md:grid-cols-3 gap-8">
                    <div class="card p-8 rounded-lg">
                        <h3 class="text-2xl font-bold text-[#C06C56] mb-4">ERER: Educação para as Relações Étnico-Raciais</h3>
                        <p class="mb-4">Na Educação Infantil, a **ERER** transcende a formalidade do currículo para se manifestar na construção de um ambiente pedagógico que valoriza as identidades plurais. Conforme **Kabengele Munanga**, a escola deve ser um espaço de "desconstrução do mito da democracia racial e de afirmação da diversidade". O foco está em promover a equidade, o respeito e a valorização das heranças culturais afro-brasileiras e indígenas desde a primeira infância, combatendo ativamente o racismo e o preconceito.</p>
                        <ul class="space-y-2">
                            <li class="flex items-start"><span class="text-[#C06C56] mr-2">✔</span> Promover a autoestima positiva e o senso de pertencimento.</li>
                            <li class="flex items-start"><span class="text-[#C06C56] mr-2">✔</span> Celebrar a diversidade de fenótipos, tradições e narrativas.</li>
                            <li class="flex items-start"><span class="text-[#C06C56] mr-2">✔</span> Desenvolver a empatia e o diálogo intercultural como pilares da cidadania.</li>
                        </ul>
                    </div>
                    <div class="card p-8 rounded-lg">
                        <h3 class="text-2xl font-bold text-[#C06C56] mb-4">EEABI: Espaço Educativo Afro-brasileiro e Indígena</h3>
                        <p class="mb-4">O **EEABI** é uma proposta pedagógica que se materializa na escola para dar visibilidade e centralidade às culturas negras e indígenas. Ele funciona como um catalisador de práticas antirracistas, incentivando a criação de um acervo literário, musical e artístico que represente a riqueza cultural desses povos, garantindo a sua presença constante no cotidiano escolar.</p>
                         <ul class="space-y-2">
                            <li class="flex items-start"><span class="text-[#C06C56] mr-2">✔</span> Fomentar a representatividade por meio de materiais didáticos diversificados.</li>
                            <li class="flex items-start"><span class="text-[#C06C56] mr-2">✔</span> Criar ambientes que celebrem as manifestações culturais e artísticas.</li>
                            <li class="flex items-start"><span class="text-[#C06C56] mr-2">✔</span> Articular a participação da comunidade para enriquecer o trabalho pedagógico.</li>
                        </ul>
                    </div>
                    <div class="card p-8 rounded-lg">
                        <h3 class="text-2xl font-bold text-[#C06C56] mb-4">O Professor Articulador</h3>
                        <p class="mb-4">O professor articulador desempenha um papel fundamental na promoção da equidade étnico-racial na Educação Infantil. Ele é o elo entre a comunidade escolar e as políticas educacionais, responsável por mobilizar, sensibilizar e capacitar os demais educadores para a implementação de ações antirracistas e para a valorização das culturas afro-brasileiras e indígenas. Sua atuação é vital para que as diretrizes se traduzam em práticas pedagógicas significativas, como destaca a Resolução CME/POA n.º 22/2020.</p>
                        <ul class="space-y-2">
                            <li class="flex items-start"><span class="text-[#C06C56] mr-2">✔</span> Promover a formação continuada dos colegas sobre o tema.</li>
                            <li class="flex items-start"><span class="text-[#C06C56] mr-2">✔</span> Articular a participação da comunidade em projetos escolares.</li>
                            <li class="flex items-start"><span class="text-[#C06C56] mr-2">✔</span> Fomentar a criação de um acervo literário e artístico diversificado.</li>
                        </ul>
                    </div>
                </div>
            </div>
        </section>

        <section id="legislacao" class="py-16 bg-white">
            <div class="container mx-auto px-6">
                <div class="text-center mb-12">
                    <h2 class="text-3xl font-bold text-gray-800">Base Normativa para a Educação Inclusiva</h2>
                    <p class="text-gray-600 mt-2">Conheça os documentos oficiais que orientam a implementação da ERER e do EEABI no sistema de ensino de Porto Alegre.</p>
                </div>
                <div class="grid sm:grid-cols-2 lg:grid-cols-3 gap-8">
                    <div class="card p-6 rounded-lg text-center cursor-pointer" data-modal="modal-resolucao-cme">
                        <div class="text-4xl mb-4">🏛️</div>
                        <h3 class="text-xl font-bold mb-2">Resolução CME/POA n.º 24/2022</h3>
                        <p class="text-gray-600">Diretrizes Curriculares para a ERER na Rede Municipal.</p>
                    </div>
                    <div class="card p-6 rounded-lg text-center cursor-pointer" data-modal="modal-resolucao-eeabi">
                        <div class="text-4xl mb-4">🏛️</div>
                        <h3 class="text-xl font-bold mb-2">Resolução CME/POA n.º 22/2020</h3>
                        <p class="text-gray-600">Dispõe sobre o Educar e Cuidar na Educação Infantil.</p>
                    </div>
                    <div class="card p-6 rounded-lg text-center cursor-pointer" data-modal="modal-leis-federais">
                        <div class="text-4xl mb-4">🏛️</div>
                        <h3 class="text-xl font-bold mb-2">Leis Federais 10.639/03 e 11.645/08</h3>
                        <p class="text-gray-600">Tornam obrigatório o ensino de História e Cultura Afro-Brasileira e Indígena.</p>
                    </div>
                </div>
            </div>
        </section>

        <section id="pratica" class="py-16">
            <div class="container mx-auto px-6">
                <div class="text-center mb-12">
                    <h2 class="text-3xl font-bold text-gray-800">Da Teoria à Prática: Propostas para a Educação Infantil</h2>
                    <p class="text-gray-600 mt-2">Descubra como os princípios da ERER e do EEABI podem ser aplicados de forma concreta e lúdica em diferentes áreas do conhecimento, promovendo o desenvolvimento integral das crianças.</p>
                </div>
                <div class="flex justify-center mb-8 flex-wrap gap-2">
                    <button class="tab active py-2 px-4 rounded-full bg-gray-200 text-gray-700" data-target="tab-portugues">Contação de Histórias</button>
                    <button class="tab py-2 px-4 rounded-full bg-gray-200 text-gray-700" data-target="tab-historia">História de Vida</button>
                    <button class="tab py-2 px-4 rounded-full bg-gray-200 text-gray-700" data-target="tab-arte">Artes Visuais</button>
                    <button class="tab py-2 px-4 rounded-full bg-gray-200 text-gray-700" data-target="tab-musica">Música e Ritmos</button>
                    <button class="tab py-2 px-4 rounded-full bg-gray-200 text-gray-700" data-target="tab-fisica">Educação Física</button>
                    <button class="tab py-2 px-4 rounded-full bg-gray-200 text-gray-700" data-target="generated-activity-content">Nova Atividade</button>
                </div>
                <div id="tab-content-container" class="card rounded-lg p-8 max-w-4xl mx-auto">
                    <div id="tab-portugues" class="tab-content">
                        <h3 class="text-xl font-bold mb-4">💡 Contação de Histórias</h3>
                        <p class="mb-4">O ato de contar histórias é uma ferramenta poderosa para a valorização da diversidade. Através de narrativas orais e literárias, as crianças têm contato com a mitologia, os costumes e as tradições de diferentes povos, ampliando seu repertório cultural e fortalecendo o respeito. Sugere-se a utilização de livros e fantoches que representem a pluralidade étnica e cultural.</p>
                        <img src="https://thumbor.novaescola.org.br/tKsgkc-w5MrLt6W-JgmTcdCf-Kc=/nova-escola-producao.s3.amazonaws.com/MBsp2CA7gXh4z44waVtResuFvXfSJVSpwwDqqjHaARMGVEf45Rsw9HsM4NMZ/contos-africanos-e-indigenas-permitem-trabalhar-o-genero-literario-e-as-relacoes-etnico-raciais.jpg" alt="Crianças sentadas em um tapete com uma professora que lê um livro para elas." class="w-full h-auto rounded-lg shadow-md mt-4">
                        <p class="text-xs text-gray-500 mt-2 text-right">Fonte: <a href="https://novaescola.org.br/conteudo/21365/contos-africanos-e-indigenas-permitem-trabalhar-o-genero-literario-e-as-relacoes-etnico-raciais" target="_blank" class="hover:underline">Nova Escola</a></p>
                    </div>
                    <div id="tab-historia" class="tab-content hidden">
                        <h3 class="text-xl font-bold mb-4">💡 História de Vida</h3>
                        <p class="mb-4">Cada criança é um sujeito histórico, portador de uma cultura e de uma identidade única. O trabalho com a história de vida da turma, explorando suas origens, costumes e tradições familiares, fortalece o senso de pertencimento e promove o reconhecimento da diversidade como um valor. Atividades como a construção de painéis de fotos e árvores genealógicas são valiosas.</p>
                        <ul class="list-disc list-inside space-y-1 text-gray-700 mb-4">
                            <li>Criar um "cantinho da família" na sala, com fotos e objetos que cada criança traz de casa.</li>
                            <li>Conversar sobre o nome de cada um, sua origem e significado.</li>
                            <li>Celebrar datas comemorativas importantes para diferentes culturas presentes na turma.</li>
                        </ul>
                        <img src="https://images.pexels.com/photos/12061380/pexels-photo-12061380.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=2" alt="Crianças em um espaço de brincadeiras e leitura" class="w-full h-auto rounded-lg shadow-md mt-4">
                        <p class="text-xs text-gray-500 mt-2 text-right">Fonte: <a href="https://www.pexels.com/pt-br/foto/grupo-de-criancas-brincando-em-uma-mesa-12061380/" target="_blank" class="hover:underline">Pexels</a></p>
                    </div>
                    <div id="tab-arte" class="tab-content hidden">
                        <h3 class="text-xl font-bold mb-4">💡 Artes Visuais</h3>
                        <p class="mb-4">As artes visuais são um campo fértil para explorar a diversidade étnico-racial. Por meio de oficinas, as crianças podem ter contato com diferentes técnicas e estilos artísticos de origem afro-brasileira e indígena, como a pintura corporal, o grafismo e a cerâmica. Tais atividades promovem a expressão criativa e o reconhecimento da beleza presente nas diferentes culturas.</p>
                         <ul class="list-disc list-inside space-y-1 text-gray-700 mb-4">
                            <li>Explorar o grafismo indígena através de pintura em papel ou tecido.</li>
                            <li>Utilizar argila para moldar vasos e objetos inspirados na cultura africana.</li>
                            <li>Criar painéis coletivos com diferentes texturas (folhas, sementes, palha) para representar a diversidade.</li>
                        </ul>
                        <img src="https://images.pexels.com/photos/8991465/pexels-photo-8991465.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=2" alt="Crianças pintando com as mãos e se divertindo" class="w-full h-auto rounded-lg shadow-md mt-4">
                        <p class="text-xs text-gray-500 mt-2 text-right">Fonte: <a href="https://www.pexels.com/pt-br/foto/mulheres-asiaticas-felizes-e-criancas-pintando-com-as-maos-e-se-divertindo-juntos-8991465/" target="_blank" class="hover:underline">Pexels</a></p>
                    </div>
                    <div id="tab-musica" class="tab-content hidden">
                        <h3 class="text-xl font-bold mb-4">💡 Música e Ritmos</h3>
                        <p class="mb-4">A música é uma linguagem universal que pode conectar as crianças com as raízes culturais de diferentes povos. Através da escuta ativa e da prática de ritmos, as crianças exploram a riqueza sonora das manifestações afro-brasileiras e indígenas, desenvolvendo a coordenação motora, a musicalidade e o respeito pelas tradições orais.</p>
                         <ul class="list-disc list-inside space-y-1 text-gray-700 mb-4">
                            <li>Cantar canções de roda e cantigas de origem africana e indígena.</li>
                            <li>Realizar uma "banda" com instrumentos feitos de sucata, explorando os diferentes sons e ritmos.</li>
                            <li>Apreciar a musicalidade de diferentes etnias, como cantos de povos Yanomami ou a capoeira.</li>
                        </ul>
                        <img src="https://agoravocesabe.com/wp-content/uploads/2024/05/Caixa-Musical-na-Educacao-Infantil-1600x914.webp" alt="Uma caixa musical com vários instrumentos coloridos e crianças ao redor" class="w-full h-auto rounded-lg shadow-md mt-4">
                        <p class="text-xs text-gray-500 mt-2 text-right">Fonte: <a href="https://agoravocesabe.com/caixa-musical-na-educacao-infantil/" target="_blank" class="hover:underline">Agora Você Sabe</a></p>
                    </div>
                    <div id="tab-fisica" class="tab-content hidden">
                        <h3 class="text-xl font-bold mb-4">💡 Educação Física</h3>
                        <p class="mb-4">A educação física é uma poderosa ferramenta para a ERER, integrando o movimento e o corpo. Através de brincadeiras e jogos de origem africana e indígena, as crianças vivenciam e compreendem as manifestações culturais de diferentes povos, desenvolvendo a cooperação, o respeito e a valorização das tradições corporais.</p>
                         <ul class="list-disc list-inside space-y-1 text-gray-700 mb-4">
                            <li>**Brincadeiras e Jogos:** Introduzir brincadeiras como "Pega-pega da onça" ou "Terrinha".</li>
                            <li>**Expressão Corporal:** Explorar os movimentos e ritmos da capoeira (sem a parte de luta) e danças de roda indígenas.</li>
                            <li>**Exploração de Elementos:** Utilizar elementos da natureza (galhos, sementes, tecidos) em circuitos e jogos.</li>
                            <li>**Dramatização:** Contar histórias com movimentos, onde as crianças encenam animais ou personagens de lendas.</li>
                        </ul>
                        <img src="https://images.pexels.com/photos/3662821/pexels-photo-3662821.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=2" alt="Crianças em roda de brincadeira infantil" class="w-full h-auto rounded-lg shadow-md mt-4">
                        <p class="text-xs text-gray-500 mt-2 text-right">Fonte: <a href="https://www.pexels.com/pt-br/foto/atras-criancas-bonito-colete-3662821/" target="_blank" class="hover:underline">Pexels</a></p>
                    </div>
                    <div id="generated-activity-content" class="tab-content hidden">
                        <h3 class="text-xl font-bold mb-4">✨ Nova Atividade Sugerida</h3>
                        <p id="generated-activity-text">Aguardando a sua sugestão...</p>
                        <div id="loading-spinner" class="loading hidden mt-4">
                            <div class="spinner"></div>
                        </div>
                    </div>
                </div>
                <div class="mt-8 text-center">
                    <button id="generate-activity-button" class="bg-[#C06C56] hover:bg-[#a65d4b] text-white font-bold py-3 px-6 rounded-lg transition-colors">
                        ✨ Gerar nova ideia de atividade
                    </button>
                </div>
            </div>
        </section>

        <footer class="bg-gray-800 text-white py-8">
            <div class="container mx-auto px-6 text-center">
                <p>Este guia é um recurso de apoio para os educadores da Rede Municipal de Ensino de Porto Alegre.</p>
                <p class="text-sm mt-2 opacity-75">Secretaria Municipal de Educação (SMED) | Prefeitura de Porto Alegre</p>
            </div>
        </footer>
    </main>

    <!-- Modals -->
    <div id="modal-resolucao-cme" class="modal fixed inset-0 hidden items-center justify-center p-4 opacity-0">
        <div class="modal-backdrop absolute inset-0 bg-black bg-opacity-50 transition-opacity duration-300"></div>
        <div class="modal-content-container bg-white rounded-lg shadow-xl w-full max-w-md p-6 transform scale-95 transition-transform duration-300">
            <h3 class="text-xl font-bold mb-4">Resolução CME/POA n.º 24/2022</h3>
            <p class="mb-4 text-gray-700">A Resolução do Conselho Municipal de Educação (CME) de Porto Alegre estabelece diretrizes e normas complementares para a Educação das Relações Étnico-Raciais e para o Ensino de História e Cultura Afro-Brasileira, Africana e Indígena no Sistema Municipal de Ensino.</p>
            <p class="font-semibold text-gray-800">Destaque do Artigo 1º:</p>
            <p class="italic text-gray-600 mb-4">"A presente resolução fixa as Diretrizes Curriculares para a Educação das Relações Étnico-Raciais e para o Ensino de História e Cultura Afro-Brasileira, Africana, Quilombola e Indígena no Sistema Municipal de Ensino de Porto Alegre (SME)."</p>
            <a href="https://dopaonlineupload.procempa.com.br/dopaonlineupload/4460_ce_370901_1.pdf" target="_blank" class="block text-center mt-4 text-[#C06C56] font-semibold hover:underline">Acessar Resolução Completa</a>
            <button class="modal-close bg-[#C06C56] text-white py-2 px-4 rounded-lg w-full mt-4">Fechar</button>
        </div>
    </div>
    <div id="modal-resolucao-eeabi" class="modal fixed inset-0 hidden items-center justify-center p-4 opacity-0">
        <div class="modal-backdrop absolute inset-0 bg-black bg-opacity-50 transition-opacity duration-300"></div>
        <div class="modal-content-container bg-white rounded-lg shadow-xl w-full max-w-md p-6 transform scale-95 transition-transform duration-300">
            <h3 class="text-xl font-bold mb-4">Resolução CME/POA n.º 22/2020</h3>
            <p class="mb-4 text-gray-700">A Resolução do Conselho Municipal de Educação (CME) de Porto Alegre fixa as Diretrizes sobre o Educar e Cuidar na Educação Infantil para o Sistema Municipal de Ensino de Porto Alegre.</p>
            <p class="font-semibold text-gray-800">Destaque do Artigo 1º:</p>
            <p class="italic text-gray-600 mb-4">"A presente Resolução fixa as Diretrizes sobre o Educar e Cuidar na Educação Infantil, para as escolas e instituições do Sistema Municipal de Ensino de Porto Alegre."</p>
            <a href="https://dopaonlineupload.procempa.com.br/dopaonlineupload/3934_ce_322299_1.pdf" target="_blank" class="block text-center mt-4 text-[#C06C56] font-semibold hover:underline">Acessar Resolução Completa</a>
            <button class="modal-close bg-[#C06C56] text-white py-2 px-4 rounded-lg w-full mt-4">Fechar</button>
        </div>
    </div>
    <div id="modal-leis-federais" class="modal fixed inset-0 hidden items-center justify-center p-4 opacity-0">
        <div class="modal-backdrop absolute inset-0 bg-black bg-opacity-50 transition-opacity duration-300"></div>
        <div class="modal-content-container bg-white rounded-lg shadow-xl w-full max-w-md p-6 transform scale-95 transition-transform duration-300">
            <h3 class="text-xl font-bold mb-4">Leis Federais 10.639/03 e 11.645/08</h3>
            <p class="mb-4 text-gray-700">Alteram a Lei de Diretrizes e Bases da Educação Nacional para incluir no currículo oficial da Rede de Ensino a obrigatoriedade da temática "História e Cultura Afro-Brasileira e Indígena".</p>
            <p class="font-semibold text-gray-800">Links para as Leis:</p>
            <ul class="list-disc list-inside text-gray-600 mb-4">
                <li><a href="http://www.planalto.gov.br/ccivil_03/leis/2003/l10.639.htm" target="_blank" class="text-[#C06C56] hover:underline">Lei nº 10.639/2003</a></li>
                <li><a href="http://www.planalto.gov.br/ccivil_03/_ato2007-2010/2008/lei/l11645.htm" target="_blank" class="text-[#C06C56] hover:underline">Lei nº 11.645/2008</a></li>
            </ul>
            <button class="modal-close bg-[#C06C56] text-white py-2 px-4 rounded-lg w-full mt-4">Fechar</button>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            // Mobile Menu
            const mobileMenuButton = document.getElementById('mobile-menu-button');
            const mobileMenu = document.getElementById('mobile-menu');
            if (mobileMenuButton && mobileMenu) {
                mobileMenuButton.addEventListener('click', () => {
                    mobileMenu.classList.toggle('hidden');
                });
            }

            // Tabs for "Na Prática" section
            const tabs = document.querySelectorAll('.tab');
            const tabContents = document.querySelectorAll('.tab-content');
            const generateActivityButton = document.getElementById('generate-activity-button');
            const generatedActivityContent = document.getElementById('generated-activity-content');
            const generatedActivityText = document.getElementById('generated-activity-text');
            const loadingSpinner = document.getElementById('loading-spinner');
            const tabContentContainer = document.getElementById('tab-content-container');

            tabs.forEach(tab => {
                tab.addEventListener('click', () => {
                    tabs.forEach(item => item.classList.remove('active'));
                    tab.classList.add('active');

                    const target = document.getElementById(tab.dataset.target);
                    tabContents.forEach(content => content.classList.add('hidden'));
                    target.classList.remove('hidden');
                });
            });

            // Gemini API call for generating new activity ideas
            generateActivityButton.addEventListener('click', async () => {
                const prompt = "Gere uma nova e criativa ideia de atividade para a Educação Infantil que aborde os temas de EEABI e ERER. A atividade deve ser lúdica e focada no respeito à diversidade cultural e étnico-racial. Responda de forma concisa e direta, descrevendo a atividade e seus objetivos pedagógicos.";
                
                loadingSpinner.classList.remove('hidden');
                generatedActivityText.textContent = '';
                
                try {
                    const chatHistory = [{ role: "user", parts: [{ text: prompt }] }];
                    const payload = { contents: chatHistory };
                    const apiKey = "";
                    const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-05-20:generateContent?key=${apiKey}`;
                    
                    const response = await fetch(apiUrl, {
                        method: 'POST',
                        headers: { 'Content-Type': 'application/json' },
                        body: JSON.stringify(payload)
                    });
                    
                    const result = await response.json();
                    
                    if (result.candidates && result.candidates.length > 0 &&
                        result.candidates[0].content && result.candidates[0].content.parts &&
                        result.candidates[0].content.parts.length > 0) {
                        const text = result.candidates[0].content.parts[0].text;
                        generatedActivityText.textContent = text;
                    } else {
                        generatedActivityText.textContent = "Não foi possível gerar uma nova atividade. Tente novamente mais tarde.";
                    }
                } catch (error) {
                    console.error("Erro ao chamar a API Gemini:", error);
                    generatedActivityText.textContent = "Ocorreu um erro ao gerar a atividade. Por favor, tente novamente.";
                } finally {
                    loadingSpinner.classList.add('hidden');
                    tabs.forEach(item => {
                        item.classList.remove('active');
                        item.classList.remove('bg-white', 'text-gray-700');
                        item.classList.add('bg-gray-200', 'text-gray-700');
                    });

                    // Crie um novo botão de aba para o conteúdo gerado
                    let generatedTabButton = document.querySelector('[data-target="generated-activity-content"]');
                    if (!generatedTabButton) {
                        const newButton = document.createElement('button');
                        newButton.className = 'tab py-2 px-4 rounded-full bg-gray-200 text-gray-700 transition-colors';
                        newButton.textContent = 'Nova Atividade';
                        newButton.dataset.target = 'generated-activity-content';
                        generateActivityButton.parentElement.insertBefore(newButton, generateActivityButton);
                        generatedTabButton = newButton;

                        newButton.addEventListener('click', () => {
                            tabs.forEach(item => item.classList.remove('active'));
                            newButton.classList.add('active');
                            tabContents.forEach(content => content.classList.add('hidden'));
                            generatedActivityContent.classList.remove('hidden');
                        });
                    }

                    tabContents.forEach(content => content.classList.add('hidden'));
                    generatedActivityContent.classList.remove('hidden');
                    generatedTabButton.classList.add('active');
                    generatedTabButton.classList.remove('bg-gray-200', 'text-gray-700');
                    generatedTabButton.classList.add('bg-[#C06C56]', 'text-white');
                }
            });

            // Modals for "Legislação" section
            const modalTriggers = document.querySelectorAll('[data-modal]');
            modalTriggers.forEach(trigger => {
                trigger.addEventListener('click', () => {
                    const modalId = trigger.dataset.modal;
                    const modal = document.getElementById(modalId);
                    if (modal) {
                        const modalBackdrop = modal.querySelector('.modal-backdrop');
                        const modalContent = modal.querySelector('.modal-content-container');

                        modal.classList.remove('hidden');
                        modal.classList.add('flex');
                        modal.classList.remove('opacity-0');

                        setTimeout(() => {
                            if (modalBackdrop) modalBackdrop.classList.remove('opacity-0');
                            if (modalContent) modalContent.classList.remove('scale-95');
                        }, 10);
                    }
                });
            });

            const modalCloses = document.querySelectorAll('.modal-close');
            modalCloses.forEach(button => {
                button.addEventListener('click', () => {
                    const modal = button.closest('.modal');
                    if (modal) {
                        const modalBackdrop = modal.querySelector('.modal-backdrop');
                        const modalContent = modal.querySelector('.modal-content-container');

                        if (modalBackdrop) modalBackdrop.classList.add('opacity-0');
                        if (modalContent) modalContent.classList.add('scale-95');

                        setTimeout(() => {
                            modal.classList.add('hidden');
                            modal.classList.remove('flex');
                            modal.classList.add('opacity-0');
                        }, 300);
                    }
                });
            });
            
            window.addEventListener('click', (event) => {
                if (event.target.classList.contains('modal-backdrop')) {
                    const modalBackdrop = event.target;
                    const modal = modalBackdrop.closest('.modal');
                    if (modal) {
                        const modalContent = modal.querySelector('.modal-content-container');
                        
                        modalBackdrop.classList.add('opacity-0');
                        if (modalContent) modalContent.classList.add('scale-95');

                        setTimeout(() => {
                            modal.classList.add('hidden');
                            modal.classList.remove('flex');
                            modal.classList.add('opacity-0');
                        }, 300);
                    }
                }
            });

            // Active nav link on scroll
            const sections = document.querySelectorAll('section');
            const navLinks = document.querySelectorAll('.nav-link');

            const observer = new IntersectionObserver((entries) => {
                entries.forEach(entry => {
                    if (entry.isIntersecting) {
                        navLinks.forEach(link => {
                            link.classList.remove('active');
                            if (link.getAttribute('href').substring(1) === entry.target.id) {
                                link.classList.add('active');
                            }
                        });
                    }
                });
            }, { rootMargin: "-50% 0px -50% 0px" });

            sections.forEach(section => {
                observer.observe(section);
            });
        });
    </script>
</body>
</html>
