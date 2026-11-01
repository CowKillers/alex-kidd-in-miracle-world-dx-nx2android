# Alex Kidd in Miracle World DX — Release alpha02

## O que é

Segundo alpha público do port experimental de Alex Kidd in Miracle
World DX (Switch, versão 1.4.0) para Android, feito com o nx2android.
O jogo abre, chega ao menu principal e ao início da gameplay a 60 FPS
no Galaxy S23, nos modos retrô e DX — provado pelas capturas no README.
**Não é um teste do jogo completo.**

## Asset

- `AlexKiddInMiracleWorldDx-launcher-v12.apk`
- 2.468.175 bytes
- SHA-256:
  `3c06642528c5867c8a4ff88e2f284c75069987f1a27ed61e19b4dac9803b3daf`
- Pacote: `org.nx2a.t010025d01221a000`
- versionCode 14 / versionName 1.4.0
- Única permissão: VIBRATE
- Signer: nx2a probe,
  SHA-256 `2551deaa93bb03dcdafb689f1efab76afd8e29538814c770048aba30d88697a0`
- Instala por cima da alpha01 (mesma assinatura, versionCode maior),
  sem apagar os dados nem os saves em `files/`.

## O que mudou em relação à alpha01

A alpha01 era só o APK do jogo com o Hide/Show. A alpha02 traz o
**launcher** no lugar do ícone do jogo, com o jogo dentro, e refaz o
visual do menu interno e do controle virtual. O Hide/Show da alpha01
continua lá, igual.

### Launcher (novo)

- O ícone na gaveta agora abre o launcher, não o jogo direto. Ele é
  o mesmo pacote, com a mesma assinatura — por isso atualiza por cima
  sem perder nada.
- Tela temática (arte do jogo, sem mockup): barra superior e rodapé
  transparentes, logo em texto, **JOGAR** laranja com ✔️ quando os
  dados estão prontos e ✖️ quando faltam, e botões bege espaçados com
  efeito ao tocar.
- **JOGAR** com trava de segurança: sem RomFS/shaders/env, ele não
  abre o jogo — abre o Importar.
- **IMPORTAR JOGO**: importa o data pack por SAF, pasta extraída ou
  arquivo zip, para `Android/data/org.nx2a.t010025d01221a000/files/`.
  Se já houver dados, ele avisa antes de sobrescrever.
- **CONFIGURAÇÃO**: só as chaves que o host realmente lê no boot —
  Docked/Handheld, contador de FPS, gamepad na tela, vibração e
  opacidade do gamepad (20–80%). Sem botões inertes: nada de Turnip,
  escala ou FSR, porque o host não lê essas chaves.
- **CONTROLES**: lista os controles de Switch e explica que mover,
  redimensionar e esconder botões se faz dentro do jogo, em
  pausa > Gamepad > Edit layout, com um botão para abrir o jogo direto
  para editar.
- **SOBRE**: pacote, versão, status dos dados (RomFS, shaders.dmsv,
  env.txt), botão **Log** (mostra `files/log.txt`), e links para o
  canal no YouTube, o grupo no Telegram, o nx2android (shirai91) e
  este repositório. A aba de drivers não existe: este host usa o
  Vulkan do sistema, sem Turnip.
- Botões reais, não imagem com botões transparentes por cima — foi
  refeito do zero depois que a primeira versão temática foi rejeitada
  por parecer "imagem travada".

### Botões do controle virtual (no jogo)

- O efeito de apertar um botão era azulado; agora é **laranja**.
  Causa: o sprite de "apertado" do tema do gamepad tinha preenchimento
  azul (98, 201, 254). O tema foi recolorido só para este port (o tema
  original não foi tocado): o preenchimento de apertado agora é laranja
  (254, 170, 97). Os botões parados continuam cinza translúcido com
  contorno branco, por desenho do tema.
- Nada mudou na posição, no tamanho ou na função dos botões, e o
  Hide/Show da alpha01 continua funcionando igual.

### Layout do menu interno (pausa, no jogo)

- Painel: antes era quase preto e opaco, com destaque rosa. Agora é
  **laranja translúcido** (dá para ver o jogo atrás), com **cantos bem
  mais arredondados**, e o destaque (abas, slider de opacidade, botão
  Resume, interruptores) virou **laranja** — a mesma cor do launcher.
- Texto refeito de verdade: antes era uma fonte bitmap 5x7 (quadradinhos,
  mesmo com a pena de borda da versão intermediária). Agora o menu usa
  uma fonte suave com anti-aliasing (DejaVu Sans Mono Bold renderizada
  grande e reduzida), na mesma posição e no mesmo tamanho de antes —
  as curvas ficam lisas em vez de pixeladas.
- Contador de FPS: antes era grande, branco e blocado no canto superior
  esquerdo. Agora é **menor** (de 3,5% para 2,2% da altura da tela) e
  **laranja**, na mesma fonte suave do menu.

## Importante — leia antes de instalar

- **APK funcional disponibilizado nesta release.** Gere o seu próprio pacote de dados
  com o porter do nx2android, a partir do seu próprio NSP e das suas
  próprias chaves, e copie o conteúdo solto para
  `Android/data/org.nx2a.t010025d01221a000/files/` (RomFS, mods,
  `shaders.dmsv`, `env.txt`, `nx2a-data.json`) — ou use o botão
  Importar jogo do launcher. Veja o mini tutorial no README.
- **Desinstalar apaga `files/`** (dados e saves). Instale por cima
  quando houver atualização com a mesma assinatura.
- **Experimental**: perfil provisório, sem heap check, SDK 10_4_1 do
  jogo contra host SDK 16, Unity 2019.4.15f1 IL2CPP. O log fica em
  `files/log.txt` — pegue antes de reabrir o jogo, senão vira
  `log.prev.txt` (o botão Log do launcher mostra o log atual).
- Este repositório e esta release **não** contêm NSP, RomFS, shaders,
  módulos patchados, data pack, chaves ou saves. Não distribua arquivos
  do jogo nem chaves.
- O menu interno de pausa do jogo já tem Export save / Import save
  (o host copia o save para `files/saves/`). O launcher desta versão
  ainda não tem esses botões — é uma adição rápida, avaliada à parte.

## Créditos

- nx2android (shirai91).
- Alex Kidd in Miracle World DX © SEGA; Jankenteam / Merge Games.
