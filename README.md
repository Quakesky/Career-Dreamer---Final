Career Dreamer — Mapeamento Vocacional

Aplicação web desenvolvida para o Projeto Interdisciplinar, na qual estudantes informam seu nome, hobbies e áreas de interesse. Os dados são validados no cliente e enviados para uma API com Inteligência Artificial, que retorna um perfil vocacional em formato JSON exibido na página de resultados.

Repositório / Demo Online (GitHub Pages): https://quakesky.github.io/Career-Dreamer---Final/

Tecnologias: HTML5, CSS3 e JavaScript (ES6+) puro, sem frameworks externos.

Funcionalidades Implementadas

Formulário Validado e Acessível: Validação nativa em HTML5 e regras customizadas em JavaScript para nome (2 a 60 caracteres), hobbies e interesses separados por vírgula (remoção de espaços extras, itens vazios e duplicados).

Design Responsivo e Contraste: Interface adaptável para dispositivos móveis (a partir de 360 px) e desktop, com tema escuro translúcido sobre fundo animado em <canvas> e contraste adequado às diretrizes WCAG.

Acessibilidade e Semântica: Estruturação com tags semânticas (<header>, <main>, <section>, <footer>, <h1>, <ol>, <template>), associação explícita entre <label for="..."> e campos de entrada, indicadores visuais de foco (:focus-visible) e atributo lang="pt-BR".

Feedback Visual e Tratamento de Erros: Modal nativo (<dialog>) estilizado com fechamento por botão ou tecla Esc, controle de estado de carregamento para evitar múltiplos cliques durante requisições e preservação dos dados digitados em caso de falha ou lentidão da API.

Exibição Dinâmica de Resultados: Renderização das carreiras recomendadas com índice de compatibilidade, barra de progresso, competências-chave e roteiro de estudos, além de suporte ao modo de demonstração (resultado.html?exemplo).

Como Executar

Não é necessária nenhuma instalação de dependências.

Opção 1 (Acesso Online): Acesse diretamente pelo GitHub Pages em https://quakesky.github.io/Career-Dreamer---Final/.

Opção 2 (Local): Abra o arquivo index.html diretamente no navegador ou utilize a extensão Live Server no VS Code (Open with Live Server).

Para visualizar a tela de resultados sem depender da API, clique em "Ver um resultado de exemplo" no cabeçalho ou acesse resultado.html?exemplo.

Estrutura do Projeto

Career-Dreamer---Final/
├── index.html                          → Página inicial e formulário de mapeamento
├── resultado.html                      → Página de exibição do perfil e carreiras
├── devita-logo.svg                     → Logotipo vetorial da marca Devita
├── css/
│   └── style.css                       → Estilos globais, tema, responsividade e acessibilidade
├── Javascript/
│   ├── config.js                       → Configurações globais (URL da API, timeout, chave de sessão)
│   ├── app.js                          → Validação do formulário, envio à API e controle do modal
│   ├── resultado.js                    → Leitura dos dados e renderização dinâmica dos resultados
│   ├── dados-exemplo.js                → Massa de dados de exemplo para testes offline
│   └── fundo.js                        → Animação de nebulosa e partículas em HTML5 Canvas
├── ISSUES.md                           → Levantamento original de problemas reportados pelo cliente
├── Relatorio_Correcao_Software.pdf     → Relatório técnico das correções aplicadas
└── README.md                           → Documentação do projeto


Configuração e Contrato da API

As configurações de integração ficam centralizadas em Javascript/config.js:

const CONFIG = Object.freeze({
  API_URL: 'https://google-career-dreamer-api.onrender.com/api/career-match',
  TEMPO_LIMITE_MS: 60000,
  CHAVE_RESULTADO: 'careerDreamer:resultado',
});


Requisição (POST)

Cabeçalho Content-Type: application/json:

{
  "name": "Ana Maria Clara",
  "hobbies": ["dançar", "cantar", "programar"],
  "interests": ["design de jogos", "desenvolvimento de pessoas"]
}


Resposta de Sucesso (200 OK)

{
  "user_name": "Ana Maria Clara",
  "career_identity_statement": "Texto curto que resume o perfil da pessoa.",
  "recommended_careers": [
    {
      "id": "ux-ui-designer",
      "title": "Designer de UX/UI",
      "match_score": 92,
      "summary": "O que essa profissão faz, em uma ou duas frases.",
      "key_skills": ["Figma", "Pesquisa com usuários"],
      "learning_path": ["Passo 1", "Passo 2", "Passo 3"]
    }
  ]
}


Nota sobre hospedagem: Como o backend está hospedado em instância gratuita no Render, a primeira requisição após períodos de inatividade pode levar até 60 segundos para responder. O cliente HTTP está configurado com AbortController compatível com esse tempo limite.

Resumo das Correções Realizadas

Todas as 13 demandas registradas em ISSUES.md foram analisadas e tratadas:

#01 — Envio do formulário: Implementado listener de submit com preventDefault() e fluxo assíncrono em Javascript/app.js.

#02 — Campo Nome: Alterado para type="text" com atributos required, minlength="2", maxlength="60" e validação adicional em JS.

#03 — Layout do formulário: Reestruturado em coluna única (flex-direction: column) com botões ajustados à largura do cartão.

#04 — Responsividade Mobile: Adicionada meta tag viewport, grid adaptativo (@media (min-width: 860px)) e eliminação de estouro horizontal.

#05 — Idioma da página: Definido lang="pt-BR" na tag <html> das páginas para reconhecimento correto por navegadores e leitores de tela.

#06 — Revisão ortográfica: Corrigidos termos como "Mapeamento Vocacional" e "interesses" em toda a interface.

#07 — Contraste visual: Aplicada paleta de alto contraste entre textos e cartões escuros translúcidos em css/style.css.

#08 — Navegação por teclado: Associados todos os <label for="..."> aos respectivos ids e adicionado contorno visível em :focus-visible.

#09 — Estrutura semântica: Substituídas divs genéricas por <header>, <main>, <section>, <footer>, <h1>, <ol> e <template>.

#10 — Sanitização de listas: Criada a função separarLista() para remover espaços, itens vazios e duplicados nos campos de hobbies e interesses.

#11 — Modal customizado: Substituído alert() nativo pelo componente <dialog id="modal-tarde"> estilizado e acessível via teclado (Esc).

#12 — Integração com API: Implementada comunicação fetch (POST) com bloqueio de duplo clique, tratamento de erros HTTP/timeout e armazenamento em sessionStorage.

#13 — Página de resultados: Implementada renderização dinâmica em Javascript/resultado.js com destaque para a melhor combinação, barras de compatibilidade, chips de competências e fallback amigável.

Os detalhes técnicos, evidências de código e ajustes de implantação (deploy no GitHub Pages) encontram-se documentados no arquivo Relatório de Correção de Software (PDF) presente neste repositório.
