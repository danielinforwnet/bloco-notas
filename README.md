# 📝 NoteFlow – Bloco de Notas Inteligente

> Aplicação moderna de notas com sincronização em tempo real via Firebase, hospedável no GitHub Pages.

![NoteFlow Preview](https://img.shields.io/badge/Status-Pronto%20para%20uso-6366f1?style=for-the-badge)
![Firebase](https://img.shields.io/badge/Firebase-10.x-orange?style=for-the-badge&logo=firebase)
![Vanilla JS](https://img.shields.io/badge/Vanilla%20JS-ES6+-yellow?style=for-the-badge&logo=javascript)

---

## ✨ Funcionalidades

- 🔐 **Autenticação** – E-mail/senha + Google OAuth
- 📝 **Editor Rico** – Negrito, itálico, listas, alinhamento, links, imagens
- 🏷️ **Categorias & Tags** – Organização flexível
- 🎨 **Cores personalizadas** – 8 cores por nota
- ⭐ **Favoritos** – Marque notas importantes
- 📦 **Arquivo & Lixeira** – Fluxo completo de ciclo de vida
- 🔍 **Pesquisa em tempo real** – Por título, conteúdo, categoria e tags
- 🌙 **Tema claro/escuro** – Com preferência salva
- 💾 **Auto salvamento** – A cada 2 segundos
- 📜 **Histórico** – Até 20 versões por nota
- 📄 **Exportar** – PDF e TXT
- ⌨️ **Atalhos** – Ctrl+N, Ctrl+K, Ctrl+S, etc.
- 📱 **Responsivo** – Desktop, tablet e mobile
- ⚡ **Tempo real** – Via `onSnapshot()` do Firestore

---

## 🚀 Como configurar

### 1. Criar projeto no Firebase

1. Acesse [console.firebase.google.com](https://console.firebase.google.com)
2. Clique em **"Adicionar projeto"**
3. Siga o assistente (Analytics é opcional)

### 2. Configurar Authentication

1. No menu lateral: **Authentication → Primeiros passos**
2. Ative o provedor **E-mail/senha**
3. Ative o provedor **Google**

### 3. Criar o Firestore

1. No menu lateral: **Firestore Database → Criar banco de dados**
2. Escolha **modo de produção** e selecione a região mais próxima

### 4. Configurar regras do Firestore

Vá em **Firestore → Regras** e cole:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /notes/{noteId} {
      allow read, write: if request.auth != null && request.auth.uid == resource.data.uid;
      allow create: if request.auth != null && request.auth.uid == request.resource.data.uid;
    }
    match /categories/{catId} {
      allow read, write: if request.auth != null && request.auth.uid == resource.data.uid;
      allow create: if request.auth != null && request.auth.uid == request.resource.data.uid;
    }
  }
}
```

### 5. Criar índices do Firestore

Vá em **Firestore → Índices** e crie os seguintes índices compostos:

| Coleção    | Campo 1        | Campo 2        |
|------------|----------------|----------------|
| notes      | uid (Asc)      | updatedAt (Desc) |
| categories | uid (Asc)      | name (Asc)     |

> Você também pode simplesmente rodar o app e clicar nos links de erro que o Firebase gera automaticamente para criar os índices.

### 6. Obter as credenciais do Firebase

1. Vá em **Configurações do projeto** (ícone de engrenagem)
2. Em **"Seus aplicativos"**, clique em **"Adicionar app"** → Web (`</>`)
3. Registre o app com um nome
4. Copie o objeto `firebaseConfig`

### 7. Atualizar o arquivo de configuração

Abra o arquivo `js/firebase-config.js` e substitua os valores:

```javascript
const firebaseConfig = {
  apiKey: "SUA_API_KEY_AQUI",
  authDomain: "seu-projeto.firebaseapp.com",
  projectId: "seu-projeto",
  storageBucket: "seu-projeto.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abc123def456"
};
```

### 8. Adicionar domínio autorizado (para Google Login)

1. **Authentication → Configurações → Domínios autorizados**
2. Adicione `SEU-USUARIO.github.io`

---

## 🌐 Deploy no GitHub Pages

```bash
# 1. Crie um repositório no GitHub (ex: noteflow)
# 2. Inicialize o Git na pasta do projeto
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/SEU-USUARIO/noteflow.git
git push -u origin main

# 3. Ative o GitHub Pages
# Settings → Pages → Branch: main → /(root) → Save
```

Sua aplicação estará disponível em:
`https://SEU-USUARIO.github.io/noteflow/`

---

## ⌨️ Atalhos de Teclado

| Atalho      | Ação              |
|-------------|-------------------|
| `Ctrl+N`    | Nova nota         |
| `Ctrl+K`    | Focar pesquisa    |
| `Ctrl+B`    | Toggle sidebar    |
| `Ctrl+D`    | Alternar tema     |
| `Ctrl+S`    | Salvar nota       |
| `Esc`       | Fechar editor     |
| `Ctrl+B`    | Negrito (editor)  |
| `Ctrl+I`    | Itálico (editor)  |
| `Ctrl+U`    | Sublinhado (editor)|

---

## 📁 Estrutura do Projeto

```
noteflow/
├── index.html              # Aplicação principal
├── css/
│   └── style.css           # Estilos (tema claro/escuro)
├── js/
│   ├── firebase-config.js  # ⚠️ Configure suas credenciais aqui
│   └── app.js              # Lógica completa da aplicação
└── README.md
```

---

## 🛠️ Tecnologias

- **HTML5** – Semântico e acessível
- **CSS3** – Custom properties, Grid, Flexbox, animações
- **JavaScript ES6+** – Módulos nativos, async/await
- **Firebase 10** – Auth, Firestore com `onSnapshot()`
- **Font Awesome 6** – Ícones
- **Google Fonts** – Inter

---

## 📜 Licença

MIT – Livre para uso pessoal e comercial.
