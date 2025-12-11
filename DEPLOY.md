# 🚀 Guia de Deploy - Whis Diet

Este guia mostra como fazer o deploy da aplicação Whis Diet em diferentes plataformas.

## 📋 Pré-requisitos

1. Conta no GitHub (para versionamento)
2. Conta no Vercel/Netlify (gratuita)

---

## 🌐 Opção 1: Deploy no Vercel (Recomendado)

### Passo 1: Preparar o Projeto

1. Certifique-se de que o projeto está funcionando localmente:
```bash
npm run dev
```

2. Teste o build de produção:
```bash
npm run build
npm run preview
```

### Passo 2: Criar Repositório no GitHub

1. Crie um repositório no GitHub (se ainda não tiver)
2. No terminal, execute:

```bash
# Se ainda não inicializou o git
git init
git add .
git commit -m "Initial commit - Whis Diet"

# Adicione o repositório remoto (substitua SEU_USUARIO pelo seu usuário do GitHub)
git remote add origin https://github.com/SEU_USUARIO/whis-diet.git
git branch -M main
git push -u origin main
```

### Passo 3: Deploy no Vercel

#### Método A: Via Interface Web (Mais Fácil)

1. Acesse [vercel.com](https://vercel.com)
2. Faça login com sua conta GitHub
3. Clique em **"Add New Project"**
4. Importe o repositório do GitHub
5. Configure o projeto:
   - **Framework Preset**: Vite
   - **Root Directory**: `./` (raiz)
   - **Build Command**: `npm run build`
   - **Output Directory**: `dist`
   - **Install Command**: `npm install`
6. Clique em **"Deploy"**
7. Aguarde alguns minutos
8. Pronto! Você receberá uma URL como: `https://whis-diet.vercel.app`

#### Método B: Via CLI (Linha de Comando)

1. Instale o Vercel CLI:
```bash
npm install -g vercel
```

2. No diretório do projeto, execute:
```bash
vercel
```

3. Siga as instruções:
   - Faça login na sua conta Vercel
   - Confirme as configurações
   - Aguarde o deploy

4. Para fazer deploy em produção:
```bash
vercel --prod
```

### Passo 4: Configurar Domínio Personalizado (Opcional)

1. No dashboard do Vercel, vá em **Settings** > **Domains**
2. Adicione seu domínio personalizado
3. Siga as instruções de configuração DNS

---

## 🌐 Opção 2: Deploy no Netlify

### Passo 1: Preparar o Projeto

1. Crie um arquivo `netlify.toml` na raiz do projeto (já criado abaixo)

### Passo 2: Deploy no Netlify

#### Método A: Via Interface Web

1. Acesse [netlify.com](https://netlify.com)
2. Faça login com GitHub
3. Clique em **"Add new site"** > **"Import an existing project"**
4. Conecte seu repositório do GitHub
5. Configure:
   - **Build command**: `npm run build`
   - **Publish directory**: `dist`
6. Clique em **"Deploy site"**

#### Método B: Via CLI

```bash
# Instalar Netlify CLI
npm install -g netlify-cli

# Login
netlify login

# Deploy
netlify deploy --prod
```

---

## 🌐 Opção 3: Deploy no GitHub Pages

### Passo 1: Instalar Plugin do Vite

```bash
npm install --save-dev vite-plugin-gh-pages
```

### Passo 2: Configurar vite.config.js

Adicione a configuração do GitHub Pages no `vite.config.js`:

```javascript
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'
import ghPages from 'vite-plugin-gh-pages'

export default defineConfig({
  plugins: [react(), ghPages()],
  base: '/whis-diet/', // Substitua 'whis-diet' pelo nome do seu repositório
  // ... resto da configuração
})
```

### Passo 3: Deploy

```bash
npm run build
npm install -g gh-pages
gh-pages -d dist
```

### Passo 4: Configurar GitHub Pages

1. No GitHub, vá em **Settings** > **Pages**
2. Selecione a branch `gh-pages` como source
3. Salve

---

## ⚙️ Configurações Adicionais

### Arquivo vercel.json (Opcional)

Crie um arquivo `vercel.json` na raiz para configurações específicas:

```json
{
  "version": 2,
  "builds": [
    {
      "src": "package.json",
      "use": "@vercel/static-build",
      "config": {
        "distDir": "dist"
      }
    }
  ],
  "routes": [
    {
      "src": "/(.*)",
      "dest": "/index.html"
    }
  ],
  "headers": [
    {
      "source": "/manifest.json",
      "headers": [
        {
          "key": "Content-Type",
          "value": "application/manifest+json"
        }
      ]
    }
  ]
}
```

### Variáveis de Ambiente (Se necessário)

Se no futuro você precisar de variáveis de ambiente:

1. No Vercel: **Settings** > **Environment Variables**
2. No Netlify: **Site settings** > **Environment variables**

---

## 🔧 Troubleshooting

### Problema: Página em branco após deploy

**Solução**: Verifique se o `base` no `vite.config.js` está correto ou remova se não usar subdiretório.

### Problema: Assets não carregam

**Solução**: Certifique-se de que o `publicDir` está configurado corretamente no `vite.config.js`.

### Problema: Service Worker não funciona

**Solução**: Verifique se o `manifest.json` e `sw.js` estão na pasta `public/`.

---

## 📱 Testando o Deploy

Após o deploy, teste:

1. ✅ A aplicação carrega corretamente
2. ✅ Login/Registro funciona
3. ✅ Dados são salvos no localStorage
4. ✅ Notificações funcionam (precisa de HTTPS)
5. ✅ PWA funciona (instalação no mobile)
6. ✅ Service Worker está ativo

---

## 🎯 Recomendação

**Use o Vercel** - É a opção mais simples e rápida:
- ✅ Deploy automático a cada push no GitHub
- ✅ HTTPS gratuito
- ✅ CDN global
- ✅ Preview de cada PR
- ✅ Configuração mínima necessária

---

## 📞 Suporte

Se tiver problemas, verifique:
- Logs de build no dashboard da plataforma
- Console do navegador para erros
- Network tab para verificar carregamento de assets

