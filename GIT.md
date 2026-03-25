# Git — Histórico Completo do Projeto UPIN

Documentação detalhada de todos os comandos e ações Git realizados no projeto do site institucional da ONG UPIN.

---

## 1. Inicialização do Repositório

O diretório do projeto já existia em `/home/vertigo/Documentos/claude/site/` com o arquivo `index.html` criado.
O repositório Git foi inicializado com o comando:

```bash
git init
```

**O que aconteceu:**
- Criou a pasta oculta `.git/` dentro do diretório do projeto
- Definiu a branch padrão como `master`
- O repositório estava vazio — sem nenhum commit ainda

**Saída do terminal:**
```
Repositório vazio Git inicializado em /home/vertigo/Documentos/claude/site/.git/
```

---

## 2. Adição do Arquivo ao Stage (Staging Area)

```bash
git add index.html
```

**O que aconteceu:**
- O arquivo `index.html` foi adicionado à **staging area** (área de preparação)
- Isso significa que o arquivo está pronto para ser incluído no próximo commit
- O Git passou a rastrear esse arquivo

**Verificação com `git status`:**
```
No ramo master

No commits yet

Mudanças a serem submetidas:
  new file: index.html
```

---

## 3. Primeiro Commit

```bash
git commit -m "feat: criação inicial do site UPIN

Site institucional completo para a ONG UPIN (Unindo Potencial,
Inspirando Novas histórias), voltada ao atendimento de crianças
e adolescentes de comunidades do Rio de Janeiro.

Inclui:
- Identidade visual criada do zero (cores, tipografia, logo)
- Hero section com gradiente animado e chamada principal
- Contadores de impacto com animação por scroll
- Seções: Sobre, Projetos, Como Ajudar, Voluntariado,
  Depoimentos, Doação e Footer
- Formulário de voluntariado com feedback visual
- Seção de doação via Pix
- Layout responsivo para mobile e desktop
- Animações e efeitos de scroll com Intersection Observer

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>"
```

**O que aconteceu:**
- Foi criado o **commit raiz** (root commit) do repositório
- Hash gerado: `3049cca`
- 1 arquivo alterado, 2.055 inserções
- A mensagem segue o padrão **Conventional Commits** (`feat:`)

**Saída do terminal:**
```
[master (root-commit) 3049cca] feat: criação inicial do site UPIN
 1 file changed, 2055 insertions(+)
 create mode 100644 index.html
```

---

## 4. Criação do Repositório Remoto no GitHub

Como o `gh` CLI não estava instalado, o repositório foi criado diretamente via **API REST do GitHub**:

```bash
curl -s -X POST https://api.github.com/user/repos \
  -H "Authorization: token <GITHUB_TOKEN>" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "upin-site",
    "description": "Site institucional da ONG UPIN - Unindo Potencial, Inspirando Novas histórias",
    "public": true,
    "auto_init": false
  }'
```

**O que aconteceu:**
- Repositório público criado em: `https://github.com/lmodesto/upin-site`
- `auto_init: false` — o repositório foi criado vazio, sem README automático, para evitar conflito com o histórico local

---

## 5. Adição do Remote Origin

```bash
git remote add origin https://<GITHUB_TOKEN>@github.com/lmodesto/upin-site.git
```

**O que aconteceu:**
- Registrou o repositório remoto do GitHub como `origin`
- O token foi embutido na URL para autenticação via HTTPS

**Verificação:**
```bash
git remote -v
# origin  https://github.com/lmodesto/upin-site.git (fetch)
# origin  https://github.com/lmodesto/upin-site.git (push)
```

---

## 6. Push para o GitHub

```bash
git push -u origin master
```

**O que aconteceu:**
- O commit local foi enviado para o GitHub
- A flag `-u` (upstream) vinculou a branch local `master` à branch remota `origin/master`
- A partir deste momento, `git push` e `git pull` funcionam sem precisar especificar o remote

**Saída do terminal:**
```
To https://github.com/lmodesto/upin-site.git
 * [new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'
```

---

## 7. Adição do GIT.md e Novo Commit

```bash
git add GIT.md
git commit -m "docs: adiciona documentação completa do fluxo Git"
git push
```

---

## Resumo dos Comandos Utilizados

| Comando | Descrição |
|---|---|
| `git init` | Inicializa o repositório local |
| `git add index.html` | Adiciona arquivo à staging area |
| `git commit -m "..."` | Cria o commit com mensagem descritiva |
| `git remote add origin <url>` | Conecta ao repositório remoto |
| `git push -u origin master` | Envia commits e vincula branch ao remote |
| `git status` | Verifica estado do repositório |
| `git remote -v` | Lista os remotes configurados |
| `git log --oneline` | Exibe histórico resumido de commits |

---

## Estado Final do Repositório

```
Branch:   master
Remote:   https://github.com/lmodesto/upin-site
Commits:  2
Arquivos: index.html, GIT.md
Status:   limpo (working tree clean)
```

---

## Conceitos Git Utilizados

### Working Directory
Onde os arquivos do projeto ficam. Qualquer alteração feita aqui não está salva no Git ainda.

### Staging Area (Index)
Área intermediária onde você prepara as mudanças antes do commit. O `git add` move arquivos do working directory para cá.

### Commit
Snapshot permanente do projeto. Cada commit tem um hash único (ex: `3049cca`), autor, data e mensagem.

### Remote
Repositório hospedado em um servidor externo (neste caso, o GitHub). O nome `origin` é a convenção padrão para o remote principal.

### Branch
Linha de desenvolvimento independente. A branch padrão criada foi `master`. Branches permitem trabalhar em funcionalidades separadas sem afetar o código principal.

### Push / Pull
- `push` — envia commits locais para o remote
- `pull` — baixa commits do remote para o local

---

*Documentação gerada em 24/03/2026 com auxílio do Claude Code (Anthropic).*
