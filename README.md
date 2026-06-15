# Rede de Lideranças — Mulheres que Transformam

Site da iniciativa **Mulheres que Transformam** (MGI): apresenta o método em
6 passos para ampliar a liderança feminina, traz um guia em PDF e um
formulário de avaliação das oficinas (via Netlify Forms).

🔗 **No ar:** https://rede-lideres.netlify.app

## Sobre o projeto

- `index.html` — página única do site (conteúdo, método em 6 passos, gerador
  de plano em PDF e formulário de avaliação).
- `forms.html` — cópia oculta do formulário para garantir a detecção pelo
  Netlify Forms.
- `guia-rede-de-lideranca.pdf` — guia da Rede de Lideranças.

É um site **estático** (HTML/CSS/JS puro), sem etapa de build.

## Como rodar localmente

Basta abrir o `index.html` no navegador. Para testar como servidor:

```bash
# Python
python -m http.server 8000
# depois acesse http://localhost:8000
```

## Deploy

Hospedado no **Netlify**, com deploy contínuo a partir deste repositório:
cada `git push` re-publica o site e re-executa a detecção do formulário.

- **Build command:** *(vazio — site estático)*
- **Publish directory:** `.`

## Software livre / Licença

Este é um projeto de **software livre** com licenciamento duplo:

- **Código-fonte** (HTML, CSS, JS, configs) → [Licença MIT](LICENSE)
- **Conteúdo editorial** (textos, método, imagens, PDF) →
  [Creative Commons Atribuição 4.0 (CC BY 4.0)](LICENSE-CONTENT)

Você pode usar, modificar e compartilhar livremente, mantendo o crédito a
**Carla Figueiredo — Mulheres que Transformam / MGI**.

## Contribuições

Sugestões, correções e melhorias são bem-vindas! Abra uma *issue* ou envie
um *pull request*.
