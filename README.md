# Guia de Workflow Colaborativo: Fork & Pull Request

Este documento descreve o fluxo de trabalho "Padrão Ouro" para colaboração em projetos com Git e GitHub (Forking Workflow). Ele garante que você possa desenvolver novas funcionalidades de forma isolada, mantendo seu repositório local sempre sincronizado com as atualizações do projeto original.

---

## 🛠️ 1. Preparação do Ambiente
### 1.1 Criar de contas e autorização
* Entrar no site https://github.com/ e criar uma conta caso ainda não possuam
* Escolher um nome de usuário

### 1.2 Instalação e Integração (Windows + VS Code)
*   Baixe e instale o [Git for Windows](https://gitforwindows.org).
*   No **VS Code**, pressione `Ctrl + Shift + X`, procure pela extensão **"GitHub Pull Requests and Issues"** e instale.
*   Para integrar, abra o terminal do VS Code (`Ctrl + '`) e configure sua identidade:
    ```bash
    git config --global user.name "Seu Nome"
    git config --global user.email "seu-email@exemplo.com"
    ```
### 1.3 Criar ou fazer fork
* No site do github você pode ir em repositórios e criar um novo; ou
* Você pode acessar o link de um repositório que já existe e fazer o fork para sua própria conta, vamos usar essa abordagem:
** Acessem https://github.com/dieison-depra-fiap/2026-engsoft-webdev
** Garantam que estejam logados na sua conta do github
** Cliquem no botão fork
** Escolham seu próprio nome para o repositório
** Pegue a URL do REPO (vou chamar de URL_REPO_ORIGINAL)

## ⚙️ 2. Configuração Inicial (Definindo o Upstream)

### 2.1 Criar uma pasta de trabalho na máquina local:
```bash
mkdir -p workspaces/fiap/
git clone URL_REPO_ORIGINAL
 (ex: https://github.com/dieison-depra/2026-engsoft-webdev.git)

cd 2026-engsoft-webdev
```

### 2.2 Vincular ao repositório original (Upstream)
Após fazer o *fork* do projeto no GitHub e cloná-lo para a sua máquina, seu repositório local estará conectado apenas à sua cópia privada (`origin`). O primeiro passo é conectá-lo ao repositório original (`upstream`).

Abra o terminal no VS Code e execute:

```bash
# Adiciona o repositório original como "upstream"
git remote add upstream https://github.com/dieison-depra-fiap/2026-engsoft-webdev.git

# Verifica se os remotes foram configurados corretamente (deve listar origin e upstream)
git remote -v
```

## 🌿 3. Criando uma Branch e Desenvolvendo
Nunca trabalhe diretamente na branch main. Crie um ambiente isolado para a sua nova feature.

```bash
# Cria uma nova branch e muda para ela imediatamente
git checkout -b minha-nova-feature
```

Faça suas alterações no código pelo VS Code. Quando terminar, salve o trabalho no seu repositório remoto (origin):

```bash
# Adiciona os arquivos modificados ao stage
git add .

# Cria o commit com uma mensagem descritiva do que foi feito
git commit -m "feat: adiciona nova funcionalidade X"

# Envia a branch para o seu GitHub (origin)
git push origin minha-nova-feature
```

## 🔄 4. Buscando Atualizações do Repositório Original
Enquanto você trabalhava, o repositório original (upstream) pode ter recebido atualizações. Precisamos trazer essas novidades para a sua máquina local.

```bash
# Volte para a branch main local
git checkout main

# Busque as informações de atualização do repositório original
git fetch upstream

# Aplique as novidades na sua main local
git merge upstream/main
```

Dica: Opcionalmente, você pode atualizar a main do seu próprio GitHub rodando um git push origin main logo após esse passo.

## 🧩 5. Integrando as Novidades na sua Branch (Merge)
Sua main agora está atualizada, mas a sua branch minha-nova-feature ainda não possui essas novidades. Vamos integrá-las para evitar problemas futuros.

```bash
# Volte para a sua branch de desenvolvimento
git checkout minha-nova-feature

# Traga as atualizações da main para dentro dela
git merge main
```

### 5.1 Resolução de Conflitos:
Se houver conflitos (código editado no mesmo lugar em ambas as versões), o VS Code irá destacá-los.

Abra os arquivos conflitantes.

Use os botões do VS Code (Accept Current, Accept Incoming, etc.) para escolher qual código manter.

Salve o arquivo.

Conclua o merge com um novo commit:

```bash
git add .
git commit -m "chore: resolve conflitos de merge com a main atualizada"
```

## 📤 6. Publicação Final e Pull Request
Sua branch agora contém o seu trabalho e está totalmente sincronizada com o projeto original. Chegou a hora de preparar o envio.

```bash
# Envia a versão final e sincronizada da branch para o seu GitHub
git push origin minha-nova-feature
```

Próximo e último passo: Acesse o seu repositório no GitHub pelo navegador. Você verá um aviso e um botão verde sugerindo a criação de um Pull Request. Clique nele, descreva suas alterações e envie sua contribuição para o repositório original!

## 🚀 7: Da branch para a main e Publicando
Agora que sua branch está testada e atualizada, é hora de levar as suas alterações para a oficial!

```bash
# Primeiro, mude para a branch que vai RECEBER as alterações (a main)
git checkout main

# Puxe o código da sua branch para dentro da main
git merge minha-nova-feature
```

Sua main local agora tem tudo! O último passo é mandar essa versão atualizada para a nuvem.

```bash
# Envia a main atualizada para o GitHub
git push origin main
```

Dica de Limpeza: Como a sua feature já está na main, você pode deletar a branch antiga para manter a casa limpa: git branch -d minha-nova-feature.