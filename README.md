# Rede de Lideranças — Mulheres que Transformam

Site da iniciativa **Mulheres que Transformam** (MGI): apresenta o método em
6 passos para ampliar a liderança feminina, traz um guia em PDF e um
formulário de avaliação das oficinas (via Netlify Forms).

🔗 **No ar:** https://rede-lideres.netlify.app

## Sobre o projeto

- `index.html` — página única do site (conteúdo, método em 6 passos, gerador
  de plano em PDF, diretório da turma, devolutiva ao vivo e avaliação).
- `forms.html` — cópia oculta do formulário para garantir a detecção pelo
  Netlify Forms.
- `guia-rede-de-lideranca.pdf` — guia da Rede de Lideranças.
- `img/`, `fonts/` — imagens (QR codes) e fontes extraídas do HTML (antes
  embutidas em base64; a extração reduziu o `index.html` de ~8 MB para ~2,3 MB).

É um site **estático** (HTML/CSS/JS puro), sem etapa de build. As funções de
rede usam **Supabase** (só o cliente no navegador; sem backend próprio).

## Funcionalidades de rede (pós-oficina)

Além do plano em PDF, o site tem quatro recursos que fazem a rede sobreviver ao
encontro:

1. **Lembrete de 90 dias (`.ics`)** — botão no plano gera um evento de
   calendário com a meta da participante.
2. **Acompanhamento por e-mail** — a participante deixa e-mail + consentimento;
   em ~90 dias recebe um lembrete automático (ver *Configuração* abaixo).
3. **Diretório da turma** — mini-perfil (nome, área, "posso apoiar", "busco")
   publicado e visível às participantes, ao vivo.
4. **Devolutiva agregada** — mostra, ao vivo, nota média, "senti-me parte de uma
   rede" e nuvens de palavras do que a turma respondeu.

Cada oficina pode ser separada pela URL: `?oficina=nome-da-turma` (sem o
parâmetro, tudo cai em `geral`).

### Backend (Supabase)

Projeto **alavanca** (`rwdiujiuryiwqfsviitf`). Tabelas com prefixo `rm_`:
`rm_perfis` (diretório), `rm_avaliacoes` (avaliação), `rm_planos` (follow-up).
Padrão de segurança: **INSERT anônimo com consentimento**; leitura pública só via
view `rm_perfis_publico` (sem dados protegidos) e RPC `rm_resultados` (agregado);
e-mails dos planos só são lidos pela edge function (service role). A chave
publicável no `index.html` é segura por causa do RLS.

### Configuração do follow-up de 90 dias (passo manual único)

O envio automático usa a edge function `rm-checkin-90d` + um `cron` diário (já
criados). Falta apenas colar 3 segredos no painel do Supabase →
*Edge Functions → rm-checkin-90d → Secrets*:

- `CRON_KEY` — a chave que o cron já usa (peça à pessoa que configurou / está no
  Vault do projeto, secret `rm_cron_key`).
- `RESEND_API_KEY` — chave da API do [Resend](https://resend.com) (free tier).
- `RESEND_FROM` — remetente verificado, ex.: `Rede de Lideranças <rede@seu-dominio>`.

Enquanto esses segredos não existirem, a função fica **trancada** (não envia
nada) — o resto do site funciona normalmente.

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
