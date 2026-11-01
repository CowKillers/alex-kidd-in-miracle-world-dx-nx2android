# Alex Kidd in Miracle World DX — Release alpha01 (rascunho)

> **Rascunho para auditoria — release ainda NÃO publicada.**

## O que é

Primeiro alpha público do port experimental de Alex Kidd in Miracle
World DX (Switch, versão 1.4.0) para Android, feito com o nx2android.
O jogo abre, chega ao menu principal e ao início da gameplay a 60 FPS
no Galaxy S23, nos modos retrô e DX — provado pelas capturas no README.
**Não é um teste do jogo completo.**

## Asset

- `AlexKiddInMiracleWorldDx-hide.apk`
- 1.896.894 bytes
- SHA-256:
  `5b2a76f5984d33732f0e8d9b2e37b0f462e03e767bac199ce7d3d4b27eccd2ed`
- Pacote: `org.nx2a.t010025d01221a000`
- versionCode 2 / versionName 1.4.0
- Única permissão: VIBRATE
- Signer: nx2a probe,
  SHA-256 `2551deaa93bb03dcdafb689f1efab76afd8e29538814c770048aba30d88697a0`

## Novidade desta versão

- **Hide/Show no editor de layout**: no menu de pausa → Gamepad →
  Edit layout, a barra tem Hide (toggle do botão selecionado) e Show
  all. Todos os botões começam visíveis; quem escolhe o que esconder é
  você. O botão do menu nunca pode ser escondido; Reset restaura tudo;
  o escondido persiste em `settings.txt` como
  `hidden=<layout>,<controle>`. O patch está em `patches/hide.patch`
  neste repositório.

## Importante — leia antes de instalar

- **O APK sozinho não é o jogo.** Gere o seu próprio pacote de dados
  com o porter do nx2android, a partir do seu próprio NSP e das suas
  próprias chaves, e copie o conteúdo solto para
  `Android/data/org.nx2a.t010025d01221a000/files/` (RomFS, mods,
  `shaders.dmsv`, `env.txt`, `nx2a-data.json`). Veja o mini tutorial no
  README.
- **Desinstalar apaga `files/`** (dados e saves). Instale por cima
  quando houver atualização com a mesma assinatura.
- **Experimental**: perfil provisório, sem heap check, SDK 10_4_1 do
  jogo contra host SDK 16, Unity 2019.4.15f1 IL2CPP. O log fica em
  `files/log.txt` — pegue antes de reabrir o jogo, senão vira
  `log.prev.txt`.
- Este repositório e esta release **não** contêm NSP, RomFS, shaders,
  módulos patchados, data pack, chaves ou saves. Não distribua arquivos
  do jogo nem chaves.

## Créditos

- nx2android (shirai91).
- Alex Kidd in Miracle World DX © SEGA; Jankenteam / Merge Games.
