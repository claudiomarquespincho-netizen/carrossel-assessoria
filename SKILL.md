---
name: "carrossel-assessoria"
description: "Gera carrosséis de Instagram (1080x1350 PNG) para qualquer criador da assessoria, a partir de tema, áudio ou texto, em 5 estilos: Twitter, Clássico, Giz, Case e Documentação. Antes, consulta a pasta do criador no Drive da assessoria (onboarding, plano de ação, roteiros já entregues) para preencher o briefing e sugerir temas. USE SEMPRE que o usuário pedir 'carrossel pro [criador]', 'sugere temas de carrossel pro [criador]', 'que carrossel eu faço pra [criador]', 'ideias de carrossel', ou mandar criador sem tema."
---

# Carrossel da Assessoria

Gera carrosséis prontos para postar para qualquer criador atendido pela assessoria. O usuário manda um comando com **criador**, **estilo**, **tema** e **conteúdo**. Quando o tema não vem, a skill lê a pasta do criador no Drive e sugere temas. A skill entrega os PNGs numerados e um zip.

## 0. Drive da assessoria: informações do criador e sugestão de temas

Rode esta etapa sempre que o pedido citar um criador da assessoria. Com tema e conteúdo já definidos, ela só preenche o briefing (criador, nicho, oferta, CTA). Sem tema, ela termina com a lista de temas sugeridos.

### Onde fica

- Pasta raiz: **Membros**. Uma subpasta por criador, com o nome completo dele ("Maria Souza", "Ana Clara Ribeiro", "João Pereira - JP Investimentos").
- Para achar a raiz, busque `title contains 'Membros' and mimeType = 'application/vnd.google-apps.folder'`. A busca traz outras pastas com "membros" no nome ("Área de Membros", "Banners Área de Membros"): fique com a que se chama só "Membros" (o título pode ter espaço no fim) e guarde o `id` dela para os passos seguintes. Se ainda sobrar mais de uma, pergunte qual é a da assessoria.
- Acesso pelo conector do Google Drive (`search_files`, `read_file_content`, `get_file_metadata`). Sem o conector ativo, avise o usuário e peça para conectar o Google Drive. Não siga sem os dados nem invente o perfil.
- A etapa é só leitura. Nunca crie, mova, renomeie ou apague nada no Drive.

### Passo a passo

1. **Achar a pasta do criador.** Busque `parentId = '<id da raiz>' and mimeType = 'application/vnd.google-apps.folder' and title contains '<nome>'`. O usuário costuma usar apelido ("Aninha" é Ana Clara Ribeiro): se não achar, liste todas as subpastas da raiz e escolha pelo nome. Achou mais de uma ou nenhuma, mostre as opções e pergunte.
2. **Listar o conteúdo.** `parentId = '<id da pasta>'`, com `excludeContentSnippets: true`, e repita para as subpastas (`material`, `acervo` ou outras). Pagine com `pageToken` até acabar.
3. **Ler na ordem de valor**, e pare quando já tiver o suficiente para o briefing e os temas:
   1. Onboarding e formulários (quem é, nicho, público, oferta, tom).
   2. Plano de ação, anotações de reunião, transcrições de call.
   3. Documentos de acervo (roteiros e levas já entregues), para saber o que já foi dito e o que não repetir.
   4. Prints, PDFs e o restante, só se faltar informação.
   Vídeo e áudio o conector não lê: anote que existem e siga.
4. **Completar com o acervo de roteiros, se existir na máquina.** Se o repo de roteiros da assessoria estiver clonado, procure a pasta `esteira2/clientes/<slug>/` dentro dele. Lá há `retrato.json` (voz, território, crenças, público, história) e `pagina.txt` (levas já entregues, com link). Leia também, sem substituir o que o Drive diz. Se os dois discordarem, vale o mais recente e você avisa.

### Ficha do criador

Monte e mostre uma ficha curta antes de seguir:

- Nome como assina, @ do Instagram e nicho.
- Público e a dor principal dele, com as palavras do material.
- Oferta atual (consultoria, produto, desafio), que vira o CTA.
- Tom e expressões que o criador usa.
- Temas já trabalhados (roteiros, levas, carrosséis), para não repetir.
- Fontes: o nome de cada arquivo lido.

Informação que não está no material fica como "não encontrado", nunca deduzida.

### Sugerir temas

Quando o usuário não trouxe tema, ou pediu ideias, sugira de 5 a 8 temas. Cada um com:

- **Capa**: a promessa em uma frase, no tom do criador.
- **Estilo** sugerido (ver "Qual estilo usar") e a estrutura (seção 3).
- **De onde veio**: o arquivo e o trecho do Drive que sustenta o tema.
- **Material real** que o carrossel vai precisar (prints, fotos, resultado de aluno) e se ele já existe na pasta.
- **CTA** ligado à oferta do criador.

Regras para os temas:

- Todo tema nasce de algo que está no material: uma dor que o público relata, uma crença do criador, um caso real, uma pergunta frequente. Tema genérico do nicho, que serviria para qualquer criador, não entra.
- Não repita assunto que já foi entregue em leva ou carrossel. Um roteiro que já foi entregue pode virar carrossel, desde que você sinalize ("versão carrossel do roteiro X da leva de 12/10").
- Varie os estilos na lista. Não sugira cinco Twitters.
- Nada de dado ou resultado que não esteja no material. Em saúde, sem promessa de resultado.
- Mostre a lista e pergunte qual seguir. Escolhido o tema, vá para a seção 1 com a ficha já preenchida e pergunte só o que faltar.

## 1. Comando e briefing

Exemplos de comando:

- "carrossel twitter pro Dr. Rafael: 5 mitos sobre testosterona" + áudio
- "carrossel clássico pro Bruno Lima: estratégias do Alfredo Soares" + análise
- "carrossel case pra Lívia: aluna que secou 8 kg no Desafio 30 Dias" + prints

Use a ficha do criador (seção 0) para preencher o que der. Extraia ou pergunte (numa única pergunta, só o que faltar):

1. **Criador**: nome como assina, @ do Instagram, nicho e foto de perfil (pegar do perfil se não vier).
2. **Estilo**: `twitter`, `classico`, `giz`, `case` ou `documentacao`. Se não vier, sugira o mais adequado (veja "Qual estilo usar") e pergunte.
3. **Tema / promessa da capa.**
4. **Conteúdo-base**: texto, áudio (transcrever) ou análise do usuário.
5. **Material real**: prints, fotos, resultados ou referências que vão aparecer.
6. **CTA**: palavra-chave para comentar e o que a pessoa recebe. Use a oferta do criador (consultoria, desafio, produto). Sem oferta definida, peça.

Se o criador tiver um design system ou identidade salva, use as cores e fontes dele no estilo escolhido, trocando só os tokens.

### Qual estilo usar

| Estilo | Quando usar |
|---|---|
| Twitter | Opinião, frase forte, lista de ideias, polêmica leve. É o mais rápido de produzir. |
| Clássico | Análise, estratégia e autoridade. Tom maduro e editorial. |
| Giz | Didático, leve, bastidor ou explicação com personagem. |
| Case | Resultado de aluno ou cliente, antes e depois, análise de um caso real. |
| Documentação | Bastidor, processo, "dia 1 de...", rotina, construção em público. |

## 2. Regras de texto (todos os estilos)

- **Use as palavras de quem mandou o conteúdo.** Pode corrigir, enxugar e cortar, mas sem reescrever com cara de IA.
- O que você escrever por conta própria (contexto, síntese, "na prática") deve ser pouco e sinalizado na resposta, para o usuário revisar.
- Pediu N itens e mandou menos: não complete com itens genéricos. Ajuste o número ou pergunte.
- Uma ideia por card, frases curtas, letra maiúscula no começo de cada frase.
- Nunca usar travessão. Trocar por vírgula ou ponto.
- Nunca colocar a marca da assessoria no material. A marca é sempre o nome e o @ do criador.
- A capa faz gancho e não revela o conteúdo (sem índice com as respostas).
- Títulos com respiro da margem de cima.
- Nada de dado inventado. Em saúde, sem promessa de resultado e sem afirmação clínica que o criador não fez.
- Referências de pessoas: da bolha certa do nicho, sem figuras polarizantes ou políticas e sem prints com conteúdo político.
- CTA no formato: pergunta + "Comente PALAVRA" + o que a pessoa recebe.

## 3. Estrutura por tipo de conteúdo

- **Lista / análise**: capa → (contexto) → um card por item → (síntese) → CTA.
- **Tipos / arquétipos**: capa com colagem e rótulos → erro comum → um card por tipo → CTA.
- **Passo a passo**: capa → problema → um passo por card → resultado → CTA.
- **Case**: capa com o resultado → ponto de partida → o que foi feito (2 a 4 cards) → resultado com prova → lição → CTA.
- **Documentação**: capa "Dia X / Semana X de..." → contexto do projeto → cards em ordem cronológica → aprendizado → próximo passo → CTA.
- Entre 7 e 14 cards.

## 4. Material visual real

O carrossel fica original quando usa material real: prints de posts e reels, fotos do criador, prints de resultado e mensagens de aluno (com dados pessoais borrados). Não use banco de imagem.

- Use o Claude in Chrome. Se houver mais de um navegador conectado, pergunte qual usar. O usuário precisa estar logado no Instagram.
- No grid ou em `/reels/`, capture cada tile com `zoom` + `save_to_disk: true`. A imagem salva tem o tamanho da imagem devolvida: use `scale` 0.6 para prints de card e `scale` 1 (ou abra o post) para capa.
- Para achar um @, use a busca do Instagram e confira o selo verificado.
- Recorte com PIL os ícones do Instagram (fixado, play) e os anéis de story. Nunca use a foto de perfil circular cortada com o anel em área grande.
- Sem extensão conectada, peça os prints ao usuário. Não tente baixar do Instagram por outros meios.
- Em print de aluno ou cliente: borre nome, foto e telefone, a menos que o usuário diga que a pessoa autorizou.

## 5. Pipeline de produção

1. Crie uma pasta no scratchpad para o carrossel e uma subpasta `img/` para o material.
2. Escreva um `build.py` com a lista de cards e uma função por layout, gerando um HTML de 1080x1350 por card (`c-01.html`...). Fontes do Google Fonts no `<head>`.
3. Escreva um `shot.js` com Playwright (rode com `NODE_PATH=$(npm root -g)`): para cada HTML, `goto file://`, espere `networkidle` e `document.fonts.ready`, aguarde 300 ms e tire screenshot do viewport 1080x1350.
4. **Revisão obrigatória**: monte uma folha de contato com PIL e olhe. Confira texto cortado, sobreposição, título colado no topo, imagem borrada ou mal cortada, card vazio demais e texto genérico escrito por você. Corrija antes de entregar.
5. Entrega: `/mnt/user-data/outputs/carrossel-<criador>-<tema>/slide-01.png...` + zip. Envie todos os slides e o zip.
6. Ajustes: refaça só o card afetado, re-renderize, atualize a pasta e o zip e reenvie.

Na resposta final: uma linha sobre o que foi feito, a lista dos cards e o que foi decisão sua para conferir.

Rodapé padrão de todos os estilos (exceto Twitter): `@criador` ou o nome à esquerda e `03/10` à direita.

---

## Estilo 1: Twitter

Cada card parece um tweet: foto de perfil redonda, nome, selo verificado, @ e o texto. Visual limpo, foco total na frase.

- Canvas 1080x1350, fundo `#ffffff` (modo claro) ou `#000000` (modo escuro). Escolha um modo por carrossel.
- Bloco do tweet centralizado verticalmente, margem lateral 90px.
- Cabeçalho: avatar circular 110px, nome em `Inter` 40px peso 700, selo azul `#1d9bf0` (SVG de círculo com check) ao lado do nome, @ em 34px `#536471` (claro) ou `#71767b` (escuro).
- Texto: Inter 50 a 58px, line-height 1.3, cor `#0f1419` ou `#e7e9ea`. Negrito em no máximo uma expressão por card. Letra maiúscula no início de cada frase.
- Pode ter imagem abaixo do texto (radius 32px, borda 1px `#cfd9de`), como tweet com foto.
- Sem contador de curtidas falso. Nada de métrica inventada.
- Rodapé: só `n/N` discreto em 26px no canto inferior direito.
- Capa: tweet com o gancho. CTA: tweet com a pergunta e "Comente PALAVRA".
- Texto longo demais para 1 card vira 2 cards, nunca fonte menor que 44px.

```css
.s{width:1080px;height:1350px;position:relative;display:flex;align-items:center;padding:0 90px;box-sizing:border-box;font-family:"Inter",Arial,sans-serif;background:#fff;color:#0f1419}
.hd{display:flex;align-items:center;gap:24px;margin-bottom:36px}
.av{width:110px;height:110px;border-radius:50%;background-size:cover;background-position:center}
.nm{font-size:40px;font-weight:700;display:flex;align-items:center;gap:10px}
.at{font-size:34px;color:#536471}
.tx{font-size:54px;line-height:1.3;white-space:pre-line}
.pic{margin-top:36px;height:520px;border-radius:32px;border:1px solid #cfd9de;background-size:cover;background-position:center}
```

---

## Estilo 2: Clássico (editorial)

Revista, não panfleto. Maduro e tradicional.

- Claro: fundo `#f6f5f1`, título `#141414`, lead `#55524d`, texto `#6f6c66`, fio `#dcd9d2`.
- Escuro: fundo `#0e0e0e`, título `#f4f3ee`, texto `#a9a7a1`, fio `#2e2d2a`.
- Acento único: amarelo `#ffd31a` (ou a cor de acento do criador), no máximo uma vez por card. Como texto, só sobre fundo escuro. Sobre fundo claro, só como pílula marca-texto com texto escuro.
- Fontes: Newsreader (serifa com itálico), Geist (sans), Anton (impacto).
- Margem 72px. Imagem com radius 22px. Sem sombra, sem degradê e sem borda colorida.
- headline: Newsreader 64px, line-height 1.04, letter-spacing -1px, com **uma expressão em itálico** que carrega a tese.
- lead: Geist 36px, peso 600. body: Geist 32 a 34px, line-height 1.38, com no máximo 2 negritos. Nunca abaixo de 28px.
- kicker no topo: nome do criador em caixa alta, 22px, letter-spacing 3px, seguido de um fio de 2px até a margem.
- Número do item: Newsreader itálico 44px ("01").

Layouts:

- **Capa (escura)**: kicker, display 84px com o nome-chave em itálico, linha de apoio e uma foto grande bem enquadrada.
- **Contexto (claro)**: "Antes, *os números.*" + lead + body + print.
- **Item**: número, headline, duas colunas (texto à esquerda, imagem 430x575 à direita) e o bloco "NA PRÁTICA" no rodapé (fio em cima, kicker e frase Newsreader 42px).
- **Síntese (escura)**: Anton 96px em 2 linhas, a segunda no acento, + body.
- **CTA (claro)**: headline 76px com itálico, "Comente" + pílula de acento com a palavra.
- Alterne claro e escuro. Não repita o mesmo layout mais de duas vezes seguidas.

```css
.s{width:1080px;height:1350px;position:relative;overflow:hidden;box-sizing:border-box;padding:72px;font-family:"Geist",Arial,sans-serif}
.light{background:#f6f5f1;color:#141414}.dark{background:#0e0e0e;color:#f4f3ee}
.top{display:flex;align-items:center;gap:24px;font-size:22px;font-weight:500;letter-spacing:3px}
.rule{flex:1;height:2px}
.num{font-family:"Newsreader",serif;font-style:italic;font-size:44px;margin-top:64px}
.hd{font-family:"Newsreader",serif;font-size:64px;line-height:1.04;letter-spacing:-1px}
.lead{font-size:36px;line-height:1.3;font-weight:600;margin-top:16px}
.body{font-size:32px;line-height:1.38;margin-top:28px}
.cols{display:flex;gap:48px;margin-top:48px;align-items:flex-start}
.img{flex:none;width:430px;height:575px;border-radius:22px;background-size:cover;background-position:center}
.np{position:absolute;left:72px;right:72px;bottom:130px;padding-top:28px;border-top:2px solid #dcd9d2}
.mark{background:#ffd31a;color:#141414;border-radius:999px;padding:0 16px}
.foot{position:absolute;left:72px;right:72px;bottom:56px;display:flex;justify-content:space-between;font-size:22px}
.imp{font-family:"Anton",sans-serif;font-size:96px;line-height:1.02}
```

---

## Estilo 3: Giz

Desenho de criança com giz de cera e um personagem fixo. Para o Bruno Lima o personagem é o **Clodoaldo** (boneco palito, cabelo espetado, camisa listrada azul, gravata vermelha). Para outro criador, use o mesmo boneco com a roupa do nicho (jaleco de médico ou nutri, regata de treino) ou crie um personagem próprio no mesmo padrão. Nunca desenhe personagens conhecidos ou de marca.

- Fundo `#fffdf7`, tinta `#2b2b2b`. Paleta: `#e63946` vermelho, `#2a6fdb` azul, `#2a9d4b` verde, `#ff8c1a` laranja, `#7b4fd6` roxo, `#ff6fa8` rosa, `#8b5a2b` marrom. Destaque `#ffc914`. Pele `#ffcf9e`.
- Fonte Schoolbell em tudo. Título 76 a 84px, texto 44 a 56px, levemente rotacionados (-1.5° / 1.2°).
- Traços com rough.js (`npm install roughjs`, inline `node_modules/roughjs/bundled/rough.js`) num `<svg id="art">` de 1080x1350 com filtro de giz:
  `<filter id="giz"><feTurbulence type="fractalNoise" baseFrequency="1.4" numOctaves="2" result="n"/><feDisplacementMap in="SourceGraphic" in2="n" scale="3"/></filter>` aplicado ao `#art`.
- Moldura rabiscada de 7px na cor do card: `rect(30,30,1020,1290,{stroke:cor,strokeWidth:7,roughness:3})`. Em séries, cada item tem cor fixa, repetida na capa.
- Marca-texto: `background:linear-gradient(transparent 50%,rgba(255,201,20,.8) 50%,rgba(255,201,20,.8) 92%,transparent 92%)`.
- Prints com borda 5 a 6px na cor do card, radius 16 a 24px e rotação de -5° a 5°.
- Rodapé `@criador` + `n/N`, 30px, `#8a8a8a`.

Helpers (lib.js):

```js
const C={ink:'#2b2b2b',red:'#e63946',blue:'#2a6fdb',yellow:'#ffc914',green:'#2a9d4b',orange:'#ff8c1a',pink:'#ff6fa8',purple:'#7b4fd6',skin:'#ffcf9e',brown:'#8b5a2b',gray:'#8a8a8a'};
let rc,SV;function init(){SV=document.getElementById('art');rc=rough.svg(SV);}
function o(x){return Object.assign({stroke:C.ink,strokeWidth:5,roughness:2.6,bowing:2.2,fillWeight:4,hachureGap:11},x||{});}
function add(n){SV.appendChild(n);return n;}
function circ(x,y,d,p){return add(rc.circle(x,y,d,o(p)));}function ell(x,y,w,h,p){return add(rc.ellipse(x,y,w,h,o(p)));}
function line(a,b,c,d,p){return add(rc.line(a,b,c,d,o(p)));}function rect(x,y,w,h,p){return add(rc.rectangle(x,y,w,h,o(p)));}
function poly(q,p){return add(rc.polygon(q,o(p)));}function curve(q,p){return add(rc.curve(q,o(p)));}
function arc(x,y,w,h,a,b,p){return add(rc.arc(x,y,w,h,a,b,false,o(p)));}
// personagem. mood: feliz|susto|cansado|bravo. arms: baixo|cima|aponta|fala. roupa: window.ROUPA='camisa'|'jaleco'
function boneco(x,y,s,mood,arms){s=s||1;const h=y,r=48*s;
 line(x-14*s,h+190*s,x-34*s,h+300*s,{strokeWidth:6});line(x+14*s,h+190*s,x+34*s,h+300*s,{strokeWidth:6});
 ell(x-44*s,h+304*s,40*s,18*s,{fill:C.ink,fillStyle:'solid'});ell(x+44*s,h+304*s,40*s,18*s,{fill:C.ink,fillStyle:'solid'});
 if(window.ROUPA==='jaleco'){poly([[x-46*s,h+56*s],[x+46*s,h+56*s],[x+44*s,h+206*s],[x-44*s,h+206*s]],{fill:'#fff',fillStyle:'solid'});poly([[x-18*s,h+56*s],[x+18*s,h+56*s],[x,h+122*s]],{fill:C.blue,fillStyle:'solid',strokeWidth:3});curve([[x-26*s,h+58*s],[x-30*s,h+110*s],[x-12*s,h+140*s],[x+4*s,h+120*s]],{stroke:C.gray,strokeWidth:5});circ(x+6*s,h+124*s,18*s,{fill:C.gray,fillStyle:'solid',strokeWidth:3});}
 else{poly([[x-42*s,h+56*s],[x+42*s,h+56*s],[x+36*s,h+196*s],[x-36*s,h+196*s]],{fill:C.blue,fillStyle:'hachure'});poly([[x-9*s,h+58*s],[x+9*s,h+58*s],[x+14*s,h+140*s],[x,h+160*s],[x-14*s,h+140*s]],{fill:C.red,fillStyle:'solid',strokeWidth:4});}
 if(arms==='cima'){line(x-40*s,h+70*s,x-100*s,h-10*s,{strokeWidth:6});line(x+40*s,h+70*s,x+100*s,h-10*s,{strokeWidth:6});circ(x-104*s,h-16*s,26*s,{fill:C.skin,fillStyle:'solid'});circ(x+104*s,h-16*s,26*s,{fill:C.skin,fillStyle:'solid'});}
 else if(arms==='aponta'){line(x-40*s,h+70*s,x-80*s,h+150*s,{strokeWidth:6});line(x+40*s,h+70*s,x+130*s,h+40*s,{strokeWidth:6});circ(x+136*s,h+38*s,24*s,{fill:C.skin,fillStyle:'solid'});}
 else if(arms==='fala'){line(x-40*s,h+70*s,x-96*s,h+40*s,{strokeWidth:6});line(x+40*s,h+70*s,x+96*s,h+40*s,{strokeWidth:6});circ(x-100*s,h+36*s,24*s,{fill:C.skin,fillStyle:'solid'});circ(x+100*s,h+36*s,24*s,{fill:C.skin,fillStyle:'solid'});}
 else{line(x-40*s,h+70*s,x-74*s,h+160*s,{strokeWidth:6});line(x+40*s,h+70*s,x+74*s,h+160*s,{strokeWidth:6});}
 circ(x,h,r*2,{fill:C.skin,fillStyle:'hachure',hachureGap:8});
 const n=mood==='bravo'?9:7;for(let i=0;i<n;i++){const a=Math.PI*(1.12+0.76*i/(n-1));const bx=x+Math.cos(a)*r*.95,by=h+Math.sin(a)*r*.95;const len=(mood==='bravo'?62:30)*s;line(bx,by,bx+Math.cos(a)*len*.5,by-len,{stroke:C.brown,strokeWidth:6});}
 circ(x-18*s,h-6*s,12*s,{fill:C.ink,fillStyle:'solid',strokeWidth:2});circ(x+18*s,h-6*s,12*s,{fill:C.ink,fillStyle:'solid',strokeWidth:2});
 if(mood==='bravo'){line(x-34*s,h-34*s,x-8*s,h-20*s,{strokeWidth:6});line(x+34*s,h-34*s,x+8*s,h-20*s,{strokeWidth:6});arc(x,h+30*s,40*s,24*s,Math.PI,Math.PI*2,{strokeWidth:5});}
 else if(mood==='feliz'){arc(x,h+12*s,52*s,40*s,0,Math.PI,{strokeWidth:5});circ(x-32*s,h+14*s,14*s,{fill:C.pink,fillStyle:'solid',stroke:'none'});circ(x+32*s,h+14*s,14*s,{fill:C.pink,fillStyle:'solid',stroke:'none'});}
 else if(mood==='susto'){ell(x,h+24*s,20*s,26*s,{fill:C.ink,fillStyle:'solid',strokeWidth:2});}
 else if(mood==='cansado'){line(x-14*s,h+26*s,x+14*s,h+26*s,{strokeWidth:5});}
}
function seta(x1,y1,x2,y2,c){line(x1,y1,x2,y2,{stroke:c||C.ink,strokeWidth:6});const a=Math.atan2(y2-y1,x2-x1);line(x2,y2,x2-Math.cos(a-.5)*36,y2-Math.sin(a-.5)*36,{stroke:c||C.ink,strokeWidth:6});line(x2,y2,x2-Math.cos(a+.5)*36,y2-Math.sin(a+.5)*36,{stroke:c||C.ink,strokeWidth:6});}
function estrela(x,y,r,c){const p=[];for(let i=0;i<10;i++){const a=-Math.PI/2+i*Math.PI/5;const rr=i%2?r*.45:r;p.push([x+Math.cos(a)*rr,y+Math.sin(a)*rr]);}poly(p,{fill:c||C.yellow,fillStyle:'solid',stroke:C.orange,strokeWidth:3});}
function lupa(x,y,d){circ(x,y,d,{strokeWidth:9,fill:'rgba(124,199,255,.35)',fillStyle:'solid'});line(x+d*.36,y+d*.36,x+d*.8,y+d*.8,{stroke:C.brown,strokeWidth:16});}
```

Layouts do Giz:

- **Capa**: título em 2 blocos (o segundo em vermelho), colagem de prints e o personagem com susto ou lupa.
- **Item com print**: título numerado na cor do item, texto à esquerda (420px, 50 a 54px), print 460x620 à direita e o personagem `feliz`/`aponta` embaixo com `seta` até o print.
- **CTA**: pergunta, "Comente" + selo amarelo (`background:#ffc914;border:5px solid #2b2b2b;border-radius:18px;transform:rotate(-3deg)`) e o personagem comemorando com estrelas.

---

## Estilo 4: Case (provisório, calibrar com a referência)

> A referência visual é o post instagram.com/p/De4WoRiALdw. Quando houver acesso ao navegador ou aos prints, abra os cards, ajuste esta seção à referência e avise o usuário.

Conta um caso real com prova: aluno, cliente, empresa ou a pessoa analisada.

- Fundo escuro `#111111` com texto claro, ou claro `#ffffff` com texto `#111111`. Acento na cor do criador (padrão verde resultado `#22c55e`).
- Fonte: Inter. Títulos 64 a 80px peso 800, texto 34 a 38px.
- **Número gigante** como protagonista quando houver resultado ("−8 kg", "3x", "R$ 40 mil"): Inter 200 a 260px peso 800 na cor de acento, com a legenda do número embaixo.
- **Antes e depois**: dois blocos lado a lado com rótulos "ANTES" e "DEPOIS" (22px, caixa alta, letter-spacing 3px).
- **Prova**: print real (mensagem, gráfico, foto) em moldura de celular ou card com radius 28px, dados pessoais borrados.
- Kicker no topo: "CASE" + nome do caso.
- Sequência: capa com o resultado → ponto de partida → o que foi feito (2 a 4 cards) → resultado com prova → lição → CTA.
- Só números que o usuário forneceu ou que estão no print. Em saúde, sem promessa de resultado para o leitor.

---

## Estilo 5: Documentação (provisório, calibrar com a referência)

> A referência visual é o post instagram.com/p/De2lVPQDn_9. Quando houver acesso ao navegador ou aos prints, abra os cards, ajuste esta seção à referência e avise o usuário.

Registra um processo em andamento, como um diário de bordo. Passa verdade e bastidor.

- Fotos reais do criador e do processo ocupando o card inteiro (sangradas), com degradê escuro na parte de baixo (`linear-gradient(transparent, rgba(0,0,0,.75))`) e o texto branco por cima.
- Fonte: Inter ou a fonte do criador. Texto 40 a 48px peso 600, curto, em primeira pessoa ("Hoje eu...").
- Marcador de tempo em cada card: "DIA 3", "SEMANA 2" ou a data, num selo pequeno no topo (fundo branco, texto preto, radius 999px, 24px, caixa alta).
- Pode alternar com cards de texto puro em fundo off-white `#f4f1ea` com anotações, como uma página de caderno.
- Ordem cronológica. Sem produção excessiva: a imagem deve parecer foto de celular.
- Sequência: capa ("Dia 1 de...") → contexto → cards cronológicos → aprendizado → próximo passo → CTA.

---

## Exemplos que já funcionaram (Bruno Lima)

- **"Existem 7 formatos de conteúdo. Só um combina com você."** (Giz). Arquétipos com print de reel de uma pessoa da bolha para cada um, e capa com colagem e o nome do formato em cima de cada print. CTA FORMATO.
- **"O que está por trás dos 32 conteúdos por dia do Alfredo Soares"** (Clássico). Capa, contexto, 6 estratégias com print do próprio perfil e "Na prática", síntese e CTA ASSESSORIA.
- **Stories automáticos com o Claude** (Giz com jaleco). Passo a passo em 5 etapas.

Lições:

- Quadrados coloridos genéricos não chamam atenção, prints reais chamam.
- A capa não entrega a lista.
- Itens inventados para completar número soam genéricos e são cortados.
- Quando o usuário pede mais maturidade, troque para o Clássico e reorganize a estrutura, não só o visual.