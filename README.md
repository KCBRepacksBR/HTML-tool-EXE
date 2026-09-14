# HTML tool EXE
HTML tool EXE e um aplicativo baseado no Electron, para criar outros aplicativos usando o Electron, Node.JS e NPM.

HTML tool EXE é um aplicativo desktop para Windows 10 e 11 que transforma páginas web em programas executáveis (.exe). Ele funciona como um gerador: você preenche os dados, escolhe um arquivo HTML ou informa um link de site, e recebe um projeto pronto para rodar e empacotar.

Para que serve

O aplicativo resolve o problema de quem quer distribuir uma página web, um dashboard, um jogo HTML5, uma ferramenta interna ou qualquer interface web como se fosse um programa de computador. Em vez de pedir para o usuário final abrir um navegador, ele abre uma janela própria, com ícone, menu, servidor local embutido e atualização automática.

Tela principal do gerador

A interface do HTML tool EXE é dividida em campos de configuração e uma barra lateral com recursos. Os campos são:

- Nome do Aplicativo: define o título da janela e o nome do executável.
- Versão: número da versão, usado também nas checagens de atualização.
- Ícone do aplicativo: arquivo `.ico` ou `.png` que vira o ícone do programa.
- Arquivo HTML: arquivo local que será embutido dentro do executável.
- Link do site: alternativa ao arquivo HTML. Você pode usar um endereço URL em vez de um arquivo local.
- Link do arquivo de versão: endereço de um arquivo de texto ou JSON no GitHub (ou outro servidor) que indica a versão mais recente.
- Link fixo do download: endereço direto do arquivo de atualização, geralmente um `.zip` de release.
- Porta do servidor local: porta usada internamente para servir o HTML.
- Limites de tamanho da janela: largura e altura mínimas e máximas, em pixels, para controlar até onde o usuário pode redimensionar a janela.
- Instalação automática do Node.js: opção para instalar o Node.js automaticamente no computador, com um marcador para forçar a reinstalação mesmo se já houver uma versão instalada.
- Botão Tutorial: abre uma janela explicando passo a passo como instalar o Node.js, rodar `npm install` e empacotar o aplicativo manualmente.
- Botão Gerar aplicativo para Windows: cria e baixa o projeto compactado em `.zip`.

No rodapé ficam os créditos: Contato Pessoal (link para o Telegram) e KCB Launcher (link para outro projeto).

O que vem dentro do ZIP gerado

Ao clicar em gerar, o usuário baixa um arquivo `.zip` contendo:

- `package.json` com as dependências do Electron.
- `electron/main.cjs` com a lógica principal do aplicativo.
- `electron/updater.cjs` com o sistema de atualização.
- `electron/assets.cjs` com o HTML embutido em memória.
- `app/` com o arquivo HTML original.
- `build/` com o ícone do aplicativo.
- `README.md` com instruções de instalação, execução e empacotamento.
- `version.txt` com a versão inicial.

Tecnologia dos aplicativos gerados

Cada aplicativo gerado usa:

- Electron 33: framework que embarca Chromium + Node.js para criar janelas desktop.
- Servidor HTTP local: rodando em `127.0.0.1` em uma porta configurada, serve o HTML e outros recursos.
- HTML embutido na memória: o conteúdo principal é compactado com gzip e codificado em base64, ficando dentro do próprio executável para dificultar acesso direto ao código fonte.
- Atualizações via GitHub: ao abrir, o app consulta o arquivo de versão remoto. Se a versão for maior, baixa o arquivo do link fixo. Se for `.zip`, extrai na pasta de dados do usuário e reinicia. Se for outro tipo, abre o instalador.

Menu do botão direito dos aplicativos gerados

Ao clicar com o botão direito dentro do app gerado, aparece um menu com as opções:

- Recortar
- Copiar
- Colar
- Selecionar tudo
- Sobrepor Janelas: ativa ou desativa a janela sempre no topo das outras.
- Verificar atualizações
- Recarregar

A versão atual do aplicativo aparece no menu, junto com um item para baixar outras versões, que abre a página de releases do GitHub.

Segurança e proteção do código

O HTML principal não fica exposto como arquivo solto. Ele é convertido para uma string compactada e incluído no código do Electron. O servidor local serve esse conteúdo a partir da memória. Atualizações futuras são extraídas para uma pasta dentro dos dados do usuário, mas o conteúdo original permanece protegido dentro do executável.

Idiomas

O gerador suporta Português (Brasil) e Inglês. A escolha fica em um seletor no topo da tela e é salva no `localStorage` do navegador. Todos os rótulos, placeholders, mensagens e o tutorial mudam de idioma automaticamente.

Fluxo de uso típico

1. O usuário abre o HTML tool EXE.
2. Preenche nome, versão, ícone e escolhe um arquivo HTML ou um link de site.
3. Configura os links do GitHub para atualização automática.
4. Ajusta os limites de tamanho da janela, se quiser.
5. Clica em Gerar aplicativo para Windows.
6. Recebe o `.zip`, extrai e, se necessário, clica em Instalar Node.js agora.
7. Abre a pasta no Prompt de Comando, executa `npm install` e depois `npm run package`.
8. O executável final fica na pasta `dist/NomeDoApp-win32-x64/`.

Resumo

HTML tool EXE é um gerador de aplicativos Windows feito em Electron. Ele pega um arquivo HTML ou um site, empacota tudo em um executável com servidor local, menu de contexto, janela sempre no topo, limites de tamanho, proteção do código e atualização automática via GitHub. Toda a interface do gerador está em português e inglês, e o processo de instalação do Node.js pode ser feito automaticamente ou seguindo o tutorial embutido.
