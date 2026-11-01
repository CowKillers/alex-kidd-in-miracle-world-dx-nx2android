# Patch Hide/Show do editor de layout

`hide.patch` é o diff exato das modificações locais do host nx2android
que acrescentam o Hide/Show ao editor de layout. Ele toca **somente**
estes 3 arquivos:

- `nxnative/dm/android/front_android.c`
- `nxnative/dm/android/gfx_vk_present.c`
- `nxnative/dm/android/overlay_layout.h`

## O que o patch faz

- Barra do editor ganha **Hide** (toggle do controle selecionado) e
  **Show all** (traz todos de volta).
- O botão do menu do pause nunca pode ser escondido.
- Controle escondido some do desenho e do toque no jogo, aparece como
  fantasma no editor, e persiste em `settings.txt` como
  `hidden=<layout>,<controle>`, por layout.
- **Reset** limpa posições, tamanhos e escondidos.

## Como aplicar

Na raiz do clone do nx2android (v0.2.0, HEAD `ba7499a`):

```sh
# copie hide.patch deste repositório para dentro do clone e aplique:
cp /caminho/para/alex-kidd-in-miracle-world-dx-nx2android/patches/hide.patch .
git apply hide.patch
git status --porcelain
```

O `git status` deve mostrar somente os 3 arquivos acima. Se aparecer
qualquer outro arquivo modificado, não continue — o patch não é esse.
O patch foi testado aplicando limpo (`git apply --check` + `git apply`)
num clone limpo em `ba7499a`, antes da publicação.

## Sem o patch

O APK builda normalmente a partir do nx2android limpo, mas **sem o
Hide**: o editor continua sendo só mover/redimensionar, e não há como
esconder um botão individual.
