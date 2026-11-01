# Alex Kidd in Miracle World DX — Release launcher-0.1

## O que é

Primeira versão numerada do launcher do port experimental de Alex
Kidd in Miracle World DX (Switch, versão 1.4.0) para Android, feito
com o nx2android. É o launcher v16: o mesmo jogo da alpha02, com
duas implementações novas que a alpha02 não tinha — **saves no
launcher** e **drivers de GPU (Turnip)** — e todo o resto da alpha02
mantido. O jogo abre, chega ao menu principal e ao início da
gameplay a 60 FPS no Galaxy S23, nos modos retrô e DX — provado
pelas capturas no README. **Não é um teste do jogo completo.**

## Asset

- `AlexKiddInMiracleWorldDx-launcher-v16.apk`
- 7.944.152 bytes
- SHA-256:
  `964eefdc45898eebdb9fbde54854b401ac9f0c48b08be9086e79dcd939c3dc8e`
- Pacote: `org.nx2a.t010025d01221a000`
- versionCode 18 / versionName 1.4.0
- Única permissão: VIBRATE
- Signer: nx2a probe,
  SHA-256 `2551deaa93bb03dcdafb689f1efab76afd8e29538814c770048aba30d88697a0`
- Instala por cima da alpha02 (mesma assinatura, versionCode maior),
  sem apagar os dados nem os saves em `files/`.

## O que mudou em relação à alpha02

### Saves no launcher (novo)

A alpha02 dizia que o launcher ainda não tinha os botões de save.
Agora tem — e eles **saíram do menu interno do jogo**: a aba Game
da pausa não mostra mais Export/Import. Tudo vive em
**Configuração > Saves**, no launcher, com o jogo fechado:

- **Exportar save**: copia o save interno do jogo para
  `files/saves/<AAAA MMDD-HHMMSS>/` (mais o arquivo `.device`, se
  houver). Recusa se ainda não houver save.
- **Importar save**: lista os saves em `files/saves/`, do mais
  recente para o mais antigo; confirma e agenda a troca para o
  próximo Jogar (o host aplica no boot, com backup automático do
  save atual em `<stamp>-before-import`).
- **Importar save de fora**: escolhe uma pasta por SAF, copia para
  `files/saves/<nome>/` e oferece aplicar.

### Drivers de GPU — Turnip (novo)

Botão **DRIVERS** na tela principal do launcher. O host desta
versão usa o adrenotools (compilado do fonte, `bylaws/libadrenotools`,
com os 5 `.so`: libadrenotools, libhook_impl, libmain_hook,
libfile_redirect_hook, libgsl_alloc_hook) quando há um driver
selecionado, e volta para o driver do sistema quando não há — ou
quando o driver falha, sem travar o jogo.

- **Sistema (Qualcomm)**: o driver que já vem no celular, o padrão.
- **Turnip turnip-8g2 incluso**: Mesa Turnip v26.3.0, feito para o
  Adreno 740 (Snapdragon 8 Gen 2). Vem dentro do APK como asset e é
  extraído na primeira abertura do launcher para a pasta interna
  de drivers. Não é arquivo do jogo — é um driver Mesa open source.
- **Importar driver (zip)**: escolhe um zip de driver por SAF, um
  por vez, para testar outros drivers. O launcher valida (tem que
  ter um único `.so`, mais o `meta.json` se houver; rejeita
  caminhos `..`, zips acima de 64 MB e zips com mais de um `.so`,
  e apaga a pasta parcial se a importação falhar) e pergunta se
  quer selecionar na hora.
- **Trial com volta automática**: ao tocar em JOGAR com um driver
  próprio, o launcher anota a tentativa; na volta, ele lê a linha
  da GPU no log (`GPU Turnip ...`). Se o driver não carregou, ele
  volta sozinho para o Sistema e avisa. Um driver ruim nunca
  prende você fora do jogo: basta abrir o launcher e tocar em
  Sistema.
- **Provado no S23**: com o turnip-8g2 selecionado, o log mostra
  `GPU Turnip Adreno (TM) 740, Vulkan 1.4.363` (o sistema era
  1.3.128), com todas as extensões que o host usa, e o jogo a
  60 FPS. O Turnip aqui é teste/melhoria — o jogo já rodava a
  60 FPS no driver da Qualcomm.
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
