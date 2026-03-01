# Guia de Workflow Colaborativo: Fork & Pull Request

**(Padrão Ouro para Contribuição em Projetos FIAP)**

Este fluxo segue o **Forking Workflow** — o padrão mais seguro e profissional para contribuir em repositórios que você não tem permissão de push direto (ex: repositório da disciplina).  
Ele mantém seu fork sempre sincronizado, evita conflitos desnecessários e facilita a revisão pelo professor/coordenador.

**Por que usar este fluxo?**  
- Isolamento: suas mudanças não afetam a main de ninguém  
- Sincronização fácil com o repositório oficial (upstream)  
- Code review via Pull Request  
- Histórico limpo e rastreável

---

## 🛠️ 1. Preparação do Ambiente

### 1.1 Conta e autenticação no GitHub
- Acesse https://github.com e crie uma conta (se ainda não tiver).  
- Escolha um username profissional (ex: dieison-silva-fiap).  
- **Dica**: Ative autenticação de dois fatores (2FA) — obrigatório para segurança.

### 1.2 Instalação e configuração (Windows + VS Code)
1. Baixe e instale o **Git for Windows** → https://git-scm.com/download/win  
2. No VS Code:  
   - Ctrl + Shift + X → busque e instale **GitHub Pull Requests and Issues**  
   - (Opcional, mas recomendado) Instale também **GitLens** para visualizar histórico e branches visualmente.
3. Configure sua identidade global (faça isso só uma vez):

```bash
git config --global user.name "Dieison Depra"
git config --global user.email "seu-email-real@exemplo.com"

#Verifique:
git config --global --list
```

## ⚙️ 2. Configuração Inicial (Fork + Upstream)
### 2.1 Faça o Fork do repositório oficial

* Acesse: https://github.com/dieison-depra-fiap/2026-engsoft-webdev
* Certifique-se de estar logado na sua conta
* Clique em Fork (canto superior direito)
* Escolha sua conta como destino → crie o fork
* Copie a URL HTTPS do seu fork (ex: https://github.com/SEU-USUARIO/2026-engsoft-webdev.git)

### 2.2 Clone localmente e adicione o upstream
Crie uma pasta organizada:
```bash
mkdir -p ~/workspaces/fiap/
cd ~/workspaces/fiap/
git clone https://github.com/SEU-USUARIO/2026-engsoft-webdev.git
cd 2026-engsoft-webdev

#Adicione o repositório oficial como upstream (faça isso só uma vez):
git remote add upstream https://github.com/dieison-depra-fiap/2026-engsoft-webdev.git

#Verifique (deve mostrar origin e upstream):
git remote -v
```

## 🌿 3. Criando uma Branch e Desenvolvendo
Regra de ouro: Nunca desenvolva diretamente na main!
```bash
# Sempre parta da main atualizada (faremos isso no passo 4)
git checkout main

# Crie e mude para uma branch com nome descritivo
git checkout -b feat/adiciona-filtro-preco-cardapio
# ou bugfix/corrige-botao-finalizar-mesa
# ou chore/atualiza-readme-aula-01
```

Faça suas alterações no VS Code.
Use Conventional Commits (padrão FIAP):
```bash
git add .
git commit -m "feat: adiciona filtro por preço no cardápio"
# ou "fix: corrige cálculo de desconto em pedidos acima de R$100"
# ou "docs: melhora explicação do README"

#Envie para o seu fork:
git push origin feat/adiciona-filtro-preco-cardapio
```

## 🔄 4. Sincronizando com o Upstream (antes de qualquer PR)
Sempre faça isso antes de começar uma nova feature ou antes de abrir PR:
```bash
git checkout main                # volte para main
git fetch upstream               # busca novidades sem mesclar
git merge upstream/main          # mescla as atualizações na sua main local

# (Opcional) Atualize também seu fork remoto
git push origin main
```

Dica anti-conflito: Faça isso frequentemente (ex: toda aula).

## 🧩 5. Integrando Atualizações na Sua Branch de Feature
Depois de atualizar a main, traga as novidades para sua branch:
```bash
git checkout feat/adiciona-filtro-preco-cardapio
git merge main
```

### 5.1 Resolvendo conflitos (acontece!)

* O VS Code destaca arquivos em conflito (vermelho no explorer).
* Abra o arquivo → use os botões: Accept Current Change / Accept Incoming / Accept Both
* Salve → marque como resolvido:

```bash
git add .
git commit -m "resolve: conflitos após merge com main atualizada"
```

📤 6. Criando o Pull Request (PR)
```bash
# Certifique-se de que tudo está enviado
git push origin feat/adiciona-filtro-preco-cardapio
```

- Vá ao seu fork no navegador
- Você verá um banner amarelo com Compare & pull request → clique
- Base repository: dieison-depra-fiap/2026-engsoft-webdev
- Compare: sua branch (feat/...)
- Escreva um bom título e descrição:
   - O que mudou?
   - Por quê?
   - Prints / gifs se ajudar
   - Referencie issues se existir (#numero)
- Clique Create pull request
Dica: Mantenha o PR pequeno e focado (1 feature por PR).

## 🚀 7. Finalizando: Merge na Sua Main Local e Limpeza
Após o PR ser aprovado e mesclado no upstream (ou se for só para seu portfólio):
```bash
git checkout main
git pull upstream main          # ou git pull origin main
git merge feat/adiciona-filtro-preco-cardapio   # (opcional se já mesclou via GitHub)

# Envie para seu fork
git push origin main

# Limpeza (muito importante!)
git branch -d feat/adiciona-filtro-preco-cardapio
git push origin --delete feat/adiciona-filtro-preco-cardapio
```

Dicas Finais e Anti-Erros Comuns (2026)

* Nunca force push (--force) em main ou branches compartilhadas
* Use git fetch upstream + git rebase upstream/main em vez de merge se quiser histórico linear (opcional, mais avançado)
* Sempre crie branches com prefixos: feat/, fix/, docs/, chore/
* Mantenha commits atômicos e mensagens claras
* Verifique o status do PR diariamente
* Se o upstream mudar muito: rebase sua branch em vez de merge (git rebase main)

Boa contribuição! 🚀
