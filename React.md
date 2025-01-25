# 🚀 Iniciando um Projeto React com Vite

Este guia irá ajudá-lo a criar e configurar uma aplicação React usando o Vite e o ESLint com o padrão Airbnb.

---

## 📁 Passo 1: Criar e Configurar a Aplicação com Vite

1. Criar o diretório do projeto.
2. Instalar o React com Vite:
   ```bash
   npm create vite@latest
   ```
   **Nota:** Após criar o projeto, não instale as dependências ainda. Configure o ESLint antes.
3. Editar o arquivo `package.json` e alterar o script `dev`:
   ```json
   "scripts": {
     "dev": "vite --open",
     "build": "vite build"
   }
   ```

---

## 🛠️ Passo 2: Configurar o ESLint

1. Remover o arquivo de configuração padrão do Vite:
   ```bash
   rm .eslintrc.cjs
   ```

2. Remover as dependências padrão do ESLint criadas pelo Vite:
   ```bash
   npm remove @typescript-eslint/eslint-plugin @typescript-eslint/parser eslint-plugin-react-hooks eslint-plugin-react-refresh
   ```

3. Instalar o pacote de regras do ESLint com padrão Airbnb:
   ```bash
   npx install-peerdeps --dev eslint-config-airbnb
   ```

4. Remover `eslint.config.js` e Criar o arquivo `.eslintrc.json` com o seguinte conteúdo:
   ```json
   {
     "extends": ["airbnb", "airbnb/hooks", "plugin:@typescript-eslint/recommended"],
     "parser": "@typescript-eslint/parser",
     "plugins": ["@typescript-eslint"],
     "env": {
       "browser": true,
       "es2021": true
     },
     "rules": {
       "react/jsx-filename-extension": [1, { "extensions": [".jsx", ".tsx"] }],
       "import/no-extraneous-dependencies": ["error", { "devDependencies": true }]
     }
   }
   ```

5. Adicionar o script de lint no `package.json`:
   ```json
   "scripts": {
     ...
     "lint": "eslint . --ext .js,.jsx,.ts,.tsx"
     ...
   }
   ```

6. Criar o arquivo de configuração do VSCode em `.vscode/settings.json`:
   ```json
   {
     "editor.formatOnSave": true,
     "editor.codeActionsOnSave": {
       "source.fixAll.eslint": "explicit",
       "source.fixAll.stylelint": "explicit"
     },
     "extensions.ignoreRecommendations": false
   }
   ```

7. Rodar o ESLint para verificar:
   ```bash
   npm run lint
   ```

---

## 🚀 Finalizando

Agora você pode instalar as dependências e começar a desenvolver:
```bash
npm install
npm run dev
