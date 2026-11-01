# Alex Kidd in Miracle World DX — Release launcher-0.2

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

## O que mudou nesta versão

- Saves no launcher (Configuração > Saves).
- Drivers de GPU com Turnip incluso e importação de driver em zip.
- Janela de carregamento na importação, no tema do launcher.

Agora roda em mais dispositivos por causa do Turnip: dá para
trocar o driver de vídeo no launcher.

## Importante

- Gere o seu próprio pacote de dados com o porter do nx2android,
  a partir do seu próprio NSP e das suas próprias chaves.
- **Desinstalar apaga `files/`** (dados e saves).
- Este repositório e esta release **não** contêm NSP, RomFS, shaders,
  módulos patchados, data pack, chaves ou saves.
