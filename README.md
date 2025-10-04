# atv-ar — AR markers com A-Frame / AR.js + Vue (Vite)

Projeto de demonstração que combina A-Frame + AR.js para detectar marcadores e exibir modelos GLB. Usa Vue para mostrar um card lateral com informações do carro e tocar áudios da pasta `public/sounds`.

## Requisitos
- Node.js 16+ (ou compatível com Vite)
- Navegador moderno com suporte a getUserMedia (Chrome/Edge/Firefox)
- Webcam (para teste de AR)

## Instalação
No Windows (pasta do projeto: d:\Faculdade\setimo_periodo\VR_AR\atividade1\atv-ar):

1. Instalar dependências:
   npm install

2. Iniciar dev server:
   npm run dev

O Vite geralmente expõe em http://localhost:5173 (ou porta diferente mostrada no terminal).

## Estrutura principal
- public/
  - models/ — arquivos .glb (acessíveis em `/models/...`)
  - sounds/ — eclipse.mp3, gtr.mp3, huracan.mp3 (acessíveis em `/sounds/...`)
  - pattern-dobby_cat.patt, pattern-damn.patt
- index.html — cena A-Frame + AR.js e lógica de detecção / reprodução de áudio
- src/
  - App.vue, main.js — app Vue (opcional se usar Vue apenas para UI)

> Observação: arquivos em `public/` são servidos na raiz — use caminhos como `/models/xxx.glb` e `/sounds/xxx.mp3`.

## Uso / Teste
1. faça `cd atv-ar` 
2. Abra o site no navegador via `npm run dev`.
3. Permita o acesso à câmera quando solicitado.
4. Mostre um marcador (hiro, kanji ou os `.patt` personalizados) à webcam.
5. Ao detectar um marcador:
   - O modelo GLB é exibido pelo A-Frame.
   - O card lateral (`CarInfo.vue`) mostra informações por 50s.
   - O áudio associado em `/sounds` é reproduzido (clique na página se o navegador bloquear autoplay).

Para testar sem marcador, há botões temporários no componente para forçar a exibição do card.

## Como adicionar/alterar itens
- Modelos: coloque `.glb` em `public/models/` e use `gltf-model="/models/nome.glb"` no `<a-entity>`.
- Sons: coloque em `public/sounds/` e referencie pelo id do `<audio>` (ex.: `audio-huracan`) em `index.html` e em `carData`.
- Marcadores personalizados: adicione `.patt` em `public/` e use `<a-marker type="pattern" url="/pattern-meu.patt" id="meu-marker">`.

## Problemas comuns / solução rápida
- Áudio não toca: Verifique nomes em `public/sounds`.
- Modelo não aparece / erro `abort()` do AR.js: verifique caminhos (`/models/...`), nomes, e IDs únicos nos elementos `<a-marker>`.
- IDs duplicados em `<a-marker>` fazem um ou mais marcadores não funcionarem — use IDs únicos.
