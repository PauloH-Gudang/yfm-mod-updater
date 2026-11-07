# Atualizador de mods — Yu-Gi-Oh! Forbidden Memories Recompiled

Atualiza mods feitos para a **v0.3.0** e a **v0.3.1-preview.2** (mod API 12) para a versão atual do
[FM Recompiled](https://github.com/Unchiga/Yu-Gi-Oh-Forbidden-Memories-Recompiled) (mod API 24),
e compila os mods em C para 32 bits e Windows 64 bits.

## Como usar

1. Abra o site (`index.html`, ou o GitHub Pages deste repositório) e envie a pasta ou o `.zip` do mod.
2. Baixe o mod corrigido e extraia a pasta dele em `mods/` deste repositório
   (ex.: `mods/meu-mod/mod.json`).
3. Faça commit e push. O workflow **build-mods** compila e publica em
   *Actions → (execução) → Artifacts → mods-compilados* um `.zip` por mod, pronto para o jogo,
   com `<library>.o` (32 bits) e `<library>.x86_64-windows.o` (Windows 64).
4. Extraia em `Documentos\My Games\YFM Re-Decomp\mods`, reinicie o jogo e ligue em F10 → Game → Mods.

O objeto do Android (`.aarch64-translated.o`) precisa do `memories-guest-ir`, que só vem no SDK do
release do jogo: use o `sdk/build-mod.bat` do release para gerá-lo.

## Para ativar o site no GitHub Pages

Settings → Pages → Source: **GitHub Actions**. A cada push na `main`, o `index.html` é publicado.

## O que tem aqui

| Pasta | O que é |
|---|---|
| `index.html` | o site (roda todo no navegador) |
| `mods/` | coloque aqui os mods a compilar |
| `tools/pc/` | `build_mod.py` oficial e os dois scripts que ele usa |
| `src.zip` | (extraído pelos workflows) só os headers do jogo (`.h`/`.inc`) e o SDK de C dos mods, sem o código-fonte do jogo |
| `.github/workflows/build-mods.yml` | compila os mods e publica o site |

Os arquivos de `tools/pc` e `src` vêm do repositório Unchiga/Yu-Gi-Oh-Forbidden-Memories-Recompiled
(commit `aceac37`). Para atualizar a uma versão nova do jogo, refaça o `src.zip` com os `.h`/`.inc` de `src/`,
`src/pc/mods/sdk/`, `src/pc/mods/mod_libc.c` e os três `.py`.

Compilar localmente: extraia o `src.zip` aqui e rode `python3 tools/pc/build_mod.py mods/meu-mod` (precisa de clang, ld.lld e llvm-objcopy).
