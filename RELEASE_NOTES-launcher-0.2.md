# Alex Kidd in Miracle World DX — Release launcher-0.2

## O que é

Segunda versão numerada do launcher do port experimental de Alex
Kidd in Miracle World DX (Switch, versão 1.4.0) para Android, feito
com o nx2android. É o launcher v18, byte a byte o mesmo APK
entregue no chat — nada foi alterado para esta release. (A release
launcher-0.1, com o launcher v16, foi apagada a pedido da autora;
esta release a substitui.) O jogo abre, chega ao menu principal e
ao início da gameplay a 60 FPS no Galaxy S23, nos modos retrô e
DX — provado pelas capturas no README. **Não é um teste do jogo
completo.**

## Asset

- `AlexKiddInMiracleWorldDx-launcher-v18.apk`
- 7.944.152 bytes
- SHA-256:
  `c5a7e80aef1fd2250c4774c6f1765ea4551c26b4ded4acda0fa82b59c2cf241f`
- Pacote: `org.nx2a.t010025d01221a000`
- versionCode 20 / versionName 1.4.0
- Única permissão: VIBRATE
- Signer: nx2a probe,
  SHA-256 `2551deaa93bb03dcdafb689f1efab76afd8e29538814c770048aba30d88697a0`
- Instala por cima da alpha02 (mesma assinatura, versionCode maior),
  sem apagar os dados nem os saves em `files/`.

## O que tem, em relação à alpha02

### Janela de carregamento na importação (nova)

- Ao escolher o zip do data pack (ou a pasta do jogo), abre na
  hora uma janela **"Importando..."** que fica até a cópia
  terminar ou falhar — antes disso a importação só mostrava
  Toasts curtos, e uma cópia de minutos parecia parada.
- A janela segue o tema do launcher: fundo marrom escuro
  arredondado, percentual grande em **laranja**, barra laranja
  sobre trilho marrom, detalhe "X MB de Y MB" em branco e arquivo
  atual em **bege**.
- Se a importação falhar, abre um diálogo com o motivo, em vez
  de um Toast que some. A lógica de cópia não mudou: mesmas 2
  passadas no zip, pasta-mãe, `.tmp` + rename, validação de
  RomFS/shaders/env e checagem de espaço.

### Saves no launcher

- Exportar/Importar save saíram do menu interno do jogo e vivem
  em **Configuração > Saves**, no launcher, com o jogo fechado:
  exportar copia o save interno para
  `files/saves/<AAAA MMDD-HHMMSS>/`; importar lista os saves, do
  mais recente para o mais antigo, e agenda a troca para o
  próximo Jogar (com backup automático do save atual); importar
  save de fora copia uma pasta por SAF para `files/saves/` e
  oferece aplicar.

### Drivers de GPU — Turnip

- Botão **DRIVERS** na tela principal. O host usa o adrenotools
  (compilado do fonte, `bylaws/libadrenotools`) quando há um
  driver selecionado, e volta para o driver do sistema quando
  não há — ou quando o driver falha, sem travar o jogo.
- **Sistema (Qualcomm)**: o padrão. **Turnip turnip-8g2 incluso**:
  Mesa Turnip v26.3.0, para o Adreno 740, dentro do APK como
  asset, extraído na primeira abertura. Não é arquivo do jogo.
- **Importar driver (zip)**: um zip por vez, por SAF, com
  validação (um único `.so`, `meta.json` se houver; rejeita
  `..`, acima de 64 MB e mais de um `.so`).
- **Trial com volta automática**: ao Jogar com um driver
  próprio, o launcher lê a linha da GPU no log; se o driver não
  carregou, volta sozinho para o Sistema e avisa. Provado no
  S23: `GPU Turnip Adreno (TM) 740, Vulkan 1.4.363`, jogo a
  60 FPS.
- **Atenção**: reimportar o jogo repõe o `env.txt` — depois de
  reimportar, selecione o driver de novo em DRIVERS.

### Mantido da alpha02

- Launcher no lugar do ícone do jogo (mesmo pacote, mesma
  assinatura), tela temática, JOGAR laranja com ✔️/✖️, botões bege
  com efeito ao tocar, trava de segurança do JOGAR sem dados,
  Importar jogo por SAF, Configuração só com as chaves que o host
  lê, Controles, Sobre com Log.
- Botões do controle virtual com efeito de apertado **laranja**.
- Menu interno de pausa com painel **laranja translúcido** de
  cantos arredondados, texto com fonte suave (anti-aliasing) e
  contador de FPS **menor e laranja**.
- Hide/Show da alpha01, igual: no editor de layout do jogo
  (pausa > Gamepad > Edit layout), com todos os botões visíveis
  por padrão.

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

## Créditos

- nx2android (shirai91).
- adrenotools (bylaws).
- Alex Kidd in Miracle World DX © SEGA; Jankenteam / Merge Games.
