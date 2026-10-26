# Tour Vista Mar

Tour 3D interativo de um apartamento com vista para o mar. A cena é modelada e iluminada no Blender e exportada para a web como glTF com lightmaps pré-calculados para três períodos do dia (manhã, pôr do sol e noite).

## Stack

- Blender (modelagem, bake de iluminação, export glTF via Khronos glTF Blender I/O)
- glTF 2.0 / GLB, lightmaps em OpenEXR, céus em JPG
- Assets CC0 do [Poly Haven](https://polyhaven.com) (modelos, texturas e HDRIs)

## Arquivos de origem (.blend)

Os arquivos `.blend` do Blender **não ficam no repositório** por causa do tamanho. Eles são a fonte da cena: qualquer alteração na geometria, nos materiais ou na iluminação deve ser feita neles e reexportada para `web/`. Guarde-os fora do git (drive/backup) e mantenha a estrutura de `assets/` igual, porque os `.blend` apontam para esses caminhos.

## Estrutura

```
web/                       arquivos servidos pelo tour
  apartamento.glb          cena exportada (estrutura, objetos, vidros, guarda-corpo)
  ceu_<periodo>.jpg        fundo do céu por período
  lm_<periodo>.exr         lightmap geral
  lm_estrutura_<periodo>.exr  lightmap da estrutura (piso, paredes, teto)
  lm_objetos_<periodo>.exr    lightmap dos móveis e objetos
renders/                   renders estáticos de referência (<ambiente>_<periodo>.png)
assets/
  models/                  modelos glTF do Poly Haven (1k)
  tex/                     texturas PBR (diff, nor_gl, rough) em 1k
  hdri/                    HDRIs 2k usados na iluminação
  polyhaven/               metadados da API do Poly Haven (catálogo e lista de arquivos por asset)
```

Períodos: `manha`, `por_do_sol`, `noite`.

## Rodando localmente

Não há build. Os arquivos precisam ser servidos por HTTP (o navegador bloqueia glTF/EXR via `file://`):

```bash
python3 -m http.server 8000
```

Os arquivos ficam em `http://localhost:8000/web/`. Para inspecionar a cena, `web/apartamento.glb` abre em qualquer visualizador glTF (ex.: three.js editor, Blender).

Não há variáveis de ambiente.
