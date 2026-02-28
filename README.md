# Guia de Workflow Colaborativo: Fork & Pull Request

Este documento descreve o fluxo de trabalho "Padrão Ouro" para colaboração em projetos com Git e GitHub (Forking Workflow). Ele garante que você possa desenvolver novas funcionalidades de forma isolada, mantendo seu repositório local sempre sincronizado com as atualizações do projeto original.

---

## 🚀 1. Preparação do Ambiente
### 1.1 Criar de contas e autorização
* Entrar no site https://github.com/ e criar uma conta ainda não possuam
* Escolher um nome de usuário
* Informar ao professor

### 1.2 Instalação e Integração (Windows + VS Code)
*   Baixe e instale o [Git for Windows](https://gitforwindows.org).
*   No **VS Code**, pressione `Ctrl + Shift + X`, procure pela extensão **"GitHub Pull Requests and Issues"** e instale.
*   Para integrar, abra o terminal do VS Code (`Ctrl + '`) e configure sua identidade:
    ```bash
    git config --global user.name "Seu Nome"
    git config --global user.email "seu-email@exemplo.com"
    ```

## 📂 2. Configuração Inicial (Definindo o Upstream)

### 2.1 Criar uma pasta de trabalho na máquina local:
```bash
mkdir -p workspaces/fiap/
git clone https://github.com/dieison-depra-fiap/2026-engsoft-webdev.git
```

### 2.2 Vincular ao repositório original (Upstream)
Após fazer o *fork* do projeto no GitHub e cloná-lo para a sua máquina, seu repositório local estará conectado apenas à sua cópia privada (`origin`). O primeiro passo é conectá-lo ao repositório original (`upstream`).

Abra o terminal no VS Code e execute:

```bash
# Adiciona o repositório original como "upstream"
git remote add upstream https://github.com/dieison-depra-fiap/2026-engsoft-webdev

# Verifica se os remotes foram configurados corretamente (deve listar origin e upstream)
git remote -v
```

## 🔄 3. Fluxo de Alterações e Sincronização
### 3.1 Alterar, Comitar e Subir (Push)
* Faça as alterações nos arquivos pelo VS Code.
* Commit: Salva as alterações localmente.

```bash
git add .
git commit -m "Minha alteração incrível"

```
* Push: Envia para o seu repositório no GitHub.
```bash
git push origin main
```

## 3. Criando uma Branch e Desenvolvendo
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