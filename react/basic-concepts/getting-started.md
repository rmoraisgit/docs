---
title: Começando — Build & Rodar local
---

# 🚀 Começando — Build & Rodar local

Este guia explica como instalar dependências, rodar o servidor de desenvolvimento e gerar uma build de produção para um projeto React (ex.: Create React App ou Vite).

## 🔧 Requisitos

- Node.js (recomenda-se a versão LTS)
- npm (ou yarn/pnpm)
- npx (já incluso no npm)

## 🧭 Scripts comuns

- Instalar dependências: `npm install` (ou `yarn` / `pnpm install`)
- Rodar em desenvolvimento: `npm start` ou `npm run dev`
- Gerar build de produção: `npm run build`
- Servir build localmente: `npx serve -s build` ou `npm i -g serve && serve -s build -l 5000`

---

## ⚙️ Create React App (CRA)

1. Criar o projeto:

   ```bash
   npx create-react-app my-app
   cd my-app
   ```

2. Instalar dependências (se necessário):

   ```bash
   npm install
   ```

3. Rodar em desenvolvimento:

   ```bash
   npm start
   # abre em http://localhost:3000
   ```

4. Build de produção:

   ```bash
   npm run build
   # cria a pasta `build/`
   ```

5. Servir a build localmente (opcional):

   ```bash
   npx serve -s build
   ```

---

## ⚡ Vite

1. Criar o projeto:

   ```bash
   npm create vite@latest my-app
   cd my-app
   npm install
   ```

2. Rodar em desenvolvimento:

   ```bash
   npm run dev
   # geralmente em http://localhost:5173
   ```

3. Build de produção e preview:

   ```bash
   npm run build
   npm run preview
   ```

> Observação: o `npm run preview` do Vite já provê um servidor local para testar a build.

---

## 🧾 Variáveis de ambiente

- CRA: variáveis que começam com `REACT_APP_` são expostas ao app.
- Vite: variáveis devem começar com `VITE_`.
- Após editar `.env` reinicie o servidor de desenvolvimento.

## 🛠️ Dicas e resolução de problemas

- Porta em uso: mude a porta com `PORT=3001 npm start` (ou ajuste conforme sua shell/OS).
- Se algo falhar, tente `rm -rf node_modules && npm install` e reinicie.
- Confirme a versão do Node (`node -v`) se ocorrerem erros de compilação.
- No Windows, prefira PowerShell ou use `cross-env` para scripts multiplataforma.

---

## ✅ Resumo rápido

```bash
# instalar
npm install

# dev
npm start # ou npm run dev

# build
npm run build

# servir build
npx serve -s build
```