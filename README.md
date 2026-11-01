# Alex Kidd in Miracle World DX no Android (nx2android)

Port experimental de **Alex Kidd in Miracle World DX** (Switch) para Android,
feito com o [nx2android](https://github.com/shirai91/nx2android) —
recompilação estática do jogo para rodar nativamente no celular, sem
emulador.

> **Alpha01 — experimental.** O projeto está em fase de desenvolvimento.
> As capturas abaixo provam que o jogo **abre, chega ao menu principal e
> ao início da gameplay a 60 FPS no Galaxy S23**, nos modos retrô e DX.
> **Não é um teste do jogo completo**: nada além do menu e do início da
> gameplay foi testado até aqui. Áreas, chefes e modos posteriores podem
> ter shaders faltando, texturas faltando, loadings presos ou crashes
> ainda não vistos. Baixe sabendo que é um alpha, não uma versão final.

## Download

📦 **[Release alpha01](https://github.com/CowKillers/alex-kidd-in-miracle-world-dx-nx2android/releases/tag/alpha01)**
— arquivo `AlexKiddInMiracleWorldDx-hide.apk` (1,9 MB, pacote
`org.nx2a.t010025d01221a000`, versionCode 2 / versão do jogo 1.4.0,
única permissão VIBRATE).

O APK sozinho **não** é o jogo: ele é só o executável do port. Sem os
dados do jogo na pasta certa, ele não joga. Veja o tutorial abaixo.

## Capturas (Galaxy S23, 60 FPS)

![Gameplay no modo retrô](screenshots/01-retro-gameplay.jpg)

![Gameplay no modo DX, com diálogo](screenshots/02-dx-gameplay.jpg)

![Menu de pausa, aba Gamepad](screenshots/03-pause-gamepad.jpg)

![Menu de pausa, aba Game](screenshots/04-pause-game.jpg)

![Menu principal](screenshots/05-main-menu.jpg)

## Mini tutorial — como instalar

### Requisitos

- Android arm64, com Vulkan 1.2+ e timeline semaphores. Testado e
  funcionando no Galaxy S23 (Adreno 740, Vulkan 1.3), a 60 FPS nas
  capturas acima.
- Controle físico ou touch na tela.

### Passo 1 — Instale o APK

1. Baixe `AlexKiddInMiracleWorldDx-hide.apk` da
   [release alpha01](https://github.com/CowKillers/alex-kidd-in-miracle-world-dx-nx2android/releases/tag/alpha01).
2. Abra o arquivo no celular e permita "instalar apps desconhecidos"
   quando o Android pedir. O app aparece como
   **Alex Kidd in Miracle World DX**.

### Passo 2 — Coloque os dados do jogo no lugar certo

**Os dados NÃO vêm no APK e NÃO estão neste repositório.** Você precisa
gerar o seu próprio pacote de dados com o porter do nx2android, a partir
do **seu próprio dump do jogo (NSP) e das suas próprias chaves** — nunca
baixe nem compartilhe RomFS, NSP, shaders ou chaves de terceiros.

Depois de gerar o pacote, copie o conteúdo **solto** (sem pasta extra no
meio) para:

```
Android/data/org.nx2a.t010025d01221a000/files/
```

A pasta tem que ficar assim:

```
Android/data/org.nx2a.t010025d01221a000/files/
├── RomFS/
├── mods/
├── shaders.dmsv
├── env.txt
└── nx2a-data.json
```

Detalhes que quebram o jogo se estiverem errados:

- O arquivo de shaders tem que se chamar **exatamente `shaders.dmsv`**,
  na raiz de `files/` — qualquer outro nome é ignorado.
- Não crie uma pasta `AlexKiddInMiracleWorldDx-data` nem `games` no meio
  do caminho.
- Se você desinstalar o app, **o Android apaga essa pasta inteira**
  (dados e saves). Depois de reinstalar, copie os dados de novo.

### Passo 3 — Jogue

Abra o **Alex Kidd in Miracle World DX** e jogue. O log do jogo fica em
`Android/data/org.nx2a.t010025d01221a000/files/log.txt` — pegue esse
arquivo **antes de reabrir o jogo**, porque no boot seguinte ele vira
`log.prev.txt`. Se algo der errado, esse log é o que decide o próximo
passo.

## Hide/Show no editor de layout

Recurso próprio deste port, aplicado pelo patch em `patches/hide.patch`
(veja `patches/README.md`). Todos os botões começam **visíveis** — nada
vem pré-escondido, e quem escolhe o que esconder é você.

1. Abra o menu de pausa (botão de menu) → Gamepad → **Edit layout**.
2. A barra do editor tem `-`, `+`, **Hide**, **Show all**, Reset, Cancel
   e Save.
3. Toque no botão que você quer tirar e aperte **Hide**, depois **Save**:
   ele some do jogo e não responde mais ao toque onde estava.
4. Para trazer de volta: reabra o editor — o botão escondido aparece
   apagado (fantasma). Toque nele e aperte **Hide** de novo (o Hide é um
   toggle), ou aperte **Show all** para trazer todos de uma vez, depois
   **Save**.
5. O botão do menu do pause **nunca pode ser escondido** — sem ele não
   haveria como abrir o pause nem o editor.
6. **Reset** + Save restaura posições, tamanhos e escondidos ao padrão
   (saída de emergência).
7. O escondido persiste em `settings.txt` como
   `hidden=<layout>,<controle>` (por exemplo, `hidden=phone,y`), e é
   **por layout**: esconder no layout phone do celular em paisagem não
   esconde no layout tablet, se a proporção da janela mudar.

## Mini tutorial — como buildar

### Requisitos

- Android arm64 com Vulkan 1.2+ e timeline semaphores (para testar).
- Android NDK **27.2.12479018**, .NET SDK **10**, Python **3.12**.
- O porter do nx2android, versão **v0.2.0, HEAD `ba7499a`**
  (https://github.com/shirai91/nx2android).
- O seu próprio dump do jogo (NSP) e as suas próprias `prod.keys`.
  **Nunca use a chave de assinatura de terceiros**: um APK assinado com
  outra chave não instala por cima do anterior — exige desinstalação
  limpa, que apaga `files/` e os saves.

### Passo 1 — Clone o nx2android

```sh
git clone https://github.com/shirai91/nx2android
cd nx2android
```

Confirme que está em `ba7499a` (v0.2.0) antes de continuar.

### Passo 2 — Aplique o patch Hide

```sh
# copie patches/hide.patch deste repositório para dentro do clone e aplique:
cp /caminho/para/alex-kidd-in-miracle-world-dx-nx2android/patches/hide.patch .
git apply hide.patch
git status --porcelain
```

O `git status` deve mostrar **somente** estes 3 arquivos modificados:

```
 M nxnative/dm/android/front_android.c
 M nxnative/dm/android/gfx_vk_present.c
 M nxnative/dm/android/overlay_layout.h
```

Sem o patch, o APK builda normalmente, mas **sem o Hide** no editor.

### Passo 3 — Porte o jogo com o porter (perfil experimental)

Alex Kidd não tem perfil upstream no nx2android: o port é experimental
e o porter gera um perfil provisório a partir do survey do seu NSP.

```sh
python3 -m porter port <pasta-do-seu-jogo> --experimental
```

Use a sua própria pasta com o seu NSP e as suas próprias `prod.keys`
(configuradas com `porter config keys <caminho>`). O porter gera o APK
e o pacote de dados (`AlexKiddInMiracleWorldDx-data/`). A referência do
perfil Android gerado está em `profiles/android.tsv` deste repositório
(veja `profiles/README.md`).

### Passo 4 — (Opcional, para rebuildar só o host) Build + repack

Para rebuildar apenas o host com o Hide, sem refazer o port inteiro:

```sh
DM_GAME=010025D01221A000 DM_GAMES_DIR=<pasta-do-build>/profile DM_GAMES_FIRST=1 \
  python3 nxnative/dm/android/build.py --game 010025D01221A000 \
    --ndk <caminho-do-NDK-27.2.12479018> --lib --release
```

Depois reempacote o APK com `nxnative/dm/android/apk/mkapk.py`,
usando **o seu próprio signer**. Confira no APK final: mesmo pacote
(`org.nx2a.t010025d01221a000`), mesma assinatura do APK que já estava
instalado (para instalar por cima), e o `libdmhost.so` novo dentro do
APK.

## Estado atual

- O jogo abre, chega ao menu principal e ao início da gameplay a
  60 fps no S23, nos modos retrô e DX, com HUD, input e pausa
  funcionando — provado pelas 5 capturas acima.
- **Testado: menu + início da gameplay. Não testado: o resto do jogo.**
- Perfil **provisório** gerado pelo porter experimental, sem heap check
  (os valores de memória são palpites do survey, não medições de boot).
- Jogo em SDK **10_4_1** contra um host convertido para SDK 16: tamanhos
  NVN e layouts de serviço do SDK 10 ainda não estão todos provados.
- Engine: Unity **2019.4.15f1 IL2CPP**, com FMOD; **3.951 shaders**
  traduzidos sem falha no split, sem prewarm de pipelines (engasgos
  iniciais são esperados e não são, por si só, um defeito).
- 2 vídeos MP4 (intro/ending) via subsdk de filme — progresso além da
  intro ainda é ponto a observar no log.
- Hide/Show no editor: implementado e buildado, **não testado em
  aparelho** até a publicação deste alpha (o fluxo completo no S23 é
  o que falta validar: esconder, salvar, trazer de volta, persistir).

## O que este repositório NÃO contém

- Nenhum arquivo do jogo (NSP, XCI, NSZ, RomFS, shaders, dados
  extraídos, data pack ou zip de data pack).
- Nenhum módulo patchado (`mods/*.patched.bin`).
- Nenhuma chave (`prod.keys`, chave de assinatura ou qualquer arquivo
  de chave).
- Nenhum log, save ou `env.txt` de aparelho.
- O APK **não** está neste repositório: ele vai apenas como asset da
  release alpha01, depois de auditado.

Cada pessoa precisa do próprio dump do jogo e das próprias chaves. Não
distribua arquivos do jogo nem chaves.

## Créditos

- [nx2android](https://github.com/shirai91/nx2android) (shirai91) — a base
  de recompilação usada pelo port.
- Alex Kidd in Miracle World DX © SEGA; desenvolvido por Jankenteam,
  publicado por Merge Games.
