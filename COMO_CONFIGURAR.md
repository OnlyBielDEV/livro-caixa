# Como ativar a sincronização entre aparelhos

Isso leva uns 5 minutos e é 100% gratuito. Você vai criar um projeto no
Firebase (do Google), que vai guardar seus dados na nuvem com login por
e-mail e senha.

## Passo 1 — Criar o projeto

1. Acesse **console.firebase.google.com** e entre com sua conta Google
2. Clique em **"Criar projeto"**, dê um nome (ex: "livro-caixa") e siga o assistente (pode desativar o Google Analytics, não é necessário)

## Passo 2 — Ativar o login por e-mail/senha

1. No menu lateral, vá em **Build > Authentication**
2. Clique em **"Vamos começar"**
3. Escolha **"E-mail/senha"** na lista de provedores e ative (toggle) a primeira opção
4. Salve

## Passo 3 — Criar o banco de dados

1. No menu lateral, vá em **Build > Firestore Database**
2. Clique em **"Criar banco de dados"**
3. Escolha a localização mais próxima (ex: `southamerica-east1` — São Paulo)
4. Comece em **modo de produção**
5. Depois de criado, vá na aba **"Regras"** e substitua tudo pelo texto abaixo, depois clique em **"Publicar"**:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
  }
}
```

Isso garante que cada pessoa só acessa os próprios dados.

## Passo 4 — Pegar as chaves de configuração

1. No menu lateral, clique na engrenagem ⚙️ ao lado de "Visão geral do projeto" → **"Configurações do projeto"**
2. Desça até **"Seus aplicativos"** e clique no ícone **`</>`** (Web)
3. Dê um apelido (ex: "livro-caixa-web") e clique em **"Registrar app"**
4. Vai aparecer um bloco de código com `const firebaseConfig = { ... }` — copie esse objeto inteiro

## Passo 5 — Colar no arquivo

1. Abra o `index.html` (pode ser num editor de texto simples, tipo Bloco de Notas/TextEdit)
2. Procure por `firebaseConfig` perto do topo do arquivo
3. Substitua o bloco `{ apiKey: "COLE_AQUI", ... }` pelo que você copiou do Firebase
4. Salve o arquivo

Pronto — é só hospedar (veja abaixo) e usar. Na primeira vez, clique em
**"Criar conta"** com um e-mail e senha. Use o mesmo login em qualquer
outro aparelho para ver os mesmos dados, sincronizados em tempo real.
