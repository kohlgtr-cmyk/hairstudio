# ⚡ CONFIGURAÇÃO RÁPIDA - 5 MINUTOS

## PASSO 1: Criar projeto no Firebase
1. Acesse: https://console.firebase.google.com/
2. Clique "Adicionar projeto"
3. Nome: `meu-sistema-agendamento`
4. Desmarque Google Analytics
5. Criar projeto

## PASSO 2: Ativar Firestore
1. Menu lateral: Build > Firestore Database
2. Criar banco de dados
3. Modo de teste
4. Localização: southamerica-east1
5. Ativar

## PASSO 3: Pegar credenciais
1. Engrenagem ⚙️ > Configurações do projeto
2. Role até "Seus aplicativos"
3. Clique no ícone `</>`
4. Apelido: "site-agendamento"
5. Registrar app
6. COPIE o código firebaseConfig

## PASSO 4: Colar credenciais

### No index.html (linha ~239):
```javascript
const firebaseConfig = {
    apiKey: "COLE_AQUI",
    authDomain: "COLE_AQUI",
    projectId: "COLE_AQUI",
    storageBucket: "COLE_AQUI",
    messagingSenderId: "COLE_AQUI",
    appId: "COLE_AQUI"
};
```

### No admin.html (linha ~99):
```javascript
const firebaseConfig = {
    apiKey: "COLE_AQUI",
    authDomain: "COLE_AQUI",
    projectId: "COLE_AQUI",
    storageBucket: "COLE_AQUI",
    messagingSenderId: "COLE_AQUI",
    appId: "COLE_AQUI"
};
```

## PASSO 5: Configurar regras de segurança
1. Firestore Database > Regras
2. Cole isso:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /agendamentos/{document=**} {
      allow read, write: if true;
    }
  }
}
```

3. Publicar

## PASSO 6: Testar localmente

### Opção A - Python:
```bash
python -m http.server 8000
```

### Opção B - PHP:
```bash
php -S localhost:8000
```

### Opção C - Node.js:
```bash
npx http-server -p 8000
```

Acesse: http://localhost:8000

## PASSO 7: Fazer primeiro teste
1. Preencha o formulário de agendamento
2. Veja a confirmação
3. Abra admin.html
4. Veja o agendamento aparecer
5. Clique "Enviar Confirmação WhatsApp"
6. WhatsApp abre com mensagem pronta!

---

## ✅ CHECKLIST DE VERIFICAÇÃO

- [ ] Firebase criado
- [ ] Firestore ativado
- [ ] Credenciais copiadas
- [ ] Credenciais coladas em index.html
- [ ] Credenciais coladas em admin.html
- [ ] Regras de segurança configuradas
- [ ] Servidor local rodando
- [ ] Teste de agendamento funcionou
- [ ] WhatsApp abrindo corretamente

---

## 🚨 ERROS COMUNS

### "Firebase is not defined"
❌ Você não colou as credenciais
✅ Cole as credenciais nos 2 arquivos

### "Permission denied"
❌ Regras do Firestore incorretas
✅ Configure as regras conforme o Passo 5

### Página em branco
❌ Abrindo arquivo direto (file://)
✅ Use um servidor local (Python, PHP, etc)

### Agendamentos não aparecem
❌ Credenciais diferentes nos arquivos
✅ Use as MESMAS credenciais em index.html e admin.html

---

## 🎯 PRÓXIMO: PERSONALIZAR

Depois de testar, personalize para seu cliente:

1. **Nome** (index.html linha 19-21)
2. **Serviços** (index.html linha 50-120)
3. **Preços** (index.html linha 50-120)
4. **Profissionais** (index.html linha 177-182)
5. **Horários** (index.html linha 192-210)
6. **Contato** (index.html linha 223-230)
7. **Cores** (styles.css linha 1-10)

---

## 📱 COLOCAR ONLINE (GRÁTIS)

### Netlify (MAIS FÁCIL):
1. https://www.netlify.com/
2. Arraste a pasta do projeto
3. Pronto!

### Firebase Hosting:
```bash
npm install -g firebase-tools
firebase login
firebase init hosting
firebase deploy
```

---

Qualquer dúvida, consulte o README.md completo!
