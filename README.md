# 💈 Sistema de Agendamento para Barbearias e Salões

## 📋 Sobre o Projeto

Sistema completo de agendamento online para barbearias e salões de beleza, com integração WhatsApp para confirmação automática de agendamentos.

### ✨ Funcionalidades

#### Site Principal (index.html):
- ✅ Catálogo de serviços com preços
- ✅ Formulário de agendamento online
- ✅ Design moderno e responsivo
- ✅ Animações suaves
- ✅ Salvamento automático no banco de dados

#### Painel Administrativo (admin.html):
- ✅ Dashboard com estatísticas em tempo real
- ✅ Visualização de agendamentos (grade ou lista)
- ✅ Filtros por data, status e profissional
- ✅ Confirmação via WhatsApp com 1 clique
- ✅ Gerenciamento de status (pendente, confirmado, concluído, cancelado)
- ✅ Detalhes completos de cada agendamento
- ✅ Envio de lembretes automáticos

### 🎯 Como Funciona o WhatsApp

O sistema usa a **Opção 1 - Link de WhatsApp** (100% gratuita):

1. Cliente faz o agendamento
2. Dados são salvos no Firebase
3. No painel admin, o funcionário vê o agendamento
4. Clica em "💬 Enviar Confirmação"
5. Abre o WhatsApp com mensagem pronta para o cliente
6. Funcionário só precisa clicar em "Enviar"

**Mensagem automática enviada:**
```
Olá *[Nome do Cliente]*! 😊

Confirmamos seu agendamento no *Studio Elegance*:

📋 *Serviço:* Corte Masculino - R$ 45,00
📅 *Data:* quinta-feira, 06 de fevereiro
⏰ *Horário:* 14:30
👨‍🎤 *Profissional:* Carlos

Estamos te esperando! 💈✨

Em caso de imprevisto, por favor nos avise com antecedência.
```

---

## 🚀 Como Configurar (Passo a Passo)

### 1️⃣ Criar Conta no Firebase (Banco de Dados Gratuito)

1. Acesse: https://firebase.google.com/
2. Clique em "Começar" ou "Get Started"
3. Faça login com sua conta Google
4. Clique em "Adicionar projeto" / "Add project"
5. Escolha um nome (ex: "barbearia-sistema")
6. Desabilite o Google Analytics (não é necessário)
7. Clique em "Criar projeto"

### 2️⃣ Configurar o Firestore Database

1. No menu lateral, clique em "Build" > "Firestore Database"
2. Clique em "Criar banco de dados" / "Create database"
3. Escolha "Iniciar no modo de teste" / "Start in test mode"
4. Selecione a localização: "southamerica-east1 (São Paulo)"
5. Clique em "Ativar" / "Enable"

### 3️⃣ Pegar as Credenciais do Firebase

1. No menu lateral, clique no ícone de engrenagem ⚙️ > "Configurações do projeto"
2. Role para baixo até "Seus aplicativos"
3. Clique no ícone `</>` (Web)
4. Digite um apelido (ex: "site-agendamento")
5. **NÃO** marque "Configure também o Firebase Hosting"
6. Clique em "Registrar app"
7. **COPIE** todo o código do `firebaseConfig` que aparece

Exemplo do que você vai copiar:
```javascript
const firebaseConfig = {
  apiKey: "AIzaSyB1234567890abcdefghijk",
  authDomain: "seu-projeto.firebaseapp.com",
  projectId: "seu-projeto-12345",
  storageBucket: "seu-projeto.appspot.com",
  messagingSenderId: "123456789012",
  appId: "1:123456789012:web:abc123def456"
};
```

### 4️⃣ Colar as Credenciais nos Arquivos

Você precisa colar essas credenciais em **2 arquivos**:

#### No arquivo `index.html`:
1. Abra o arquivo `index.html`
2. Procure por `// TODO: Substituir com suas credenciais do Firebase`
3. Substitua o bloco `firebaseConfig` inteiro pelas suas credenciais

#### No arquivo `admin.html`:
1. Abra o arquivo `admin.html`
2. Procure por `// TODO: Substituir com suas credenciais do Firebase`
3. Substitua o bloco `firebaseConfig` inteiro pelas suas credenciais

### 5️⃣ Configurar Regras de Segurança do Firebase

1. No Firebase Console, vá em "Firestore Database"
2. Clique na aba "Regras" / "Rules"
3. Substitua o conteúdo por:

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

4. Clique em "Publicar" / "Publish"

**⚠️ IMPORTANTE:** Essas regras permitem acesso total. Para produção, você deve adicionar autenticação!

---

## 🎨 Personalização para Cada Cliente

### Alterar Nome e Informações do Salão

**No arquivo `index.html`:**

1. **Nome do estabelecimento** (linha ~19-21):
```html
<h1 class="logo">Studio Elegance</h1>
<p class="tagline">Barbearia & Salão de Beleza</p>
```

2. **Título da página Hero** (linha ~36-38):
```html
<h2 class="hero-title">Seu estilo,<br>nossa expertise</h2>
<p class="hero-subtitle">Transformando cada visita em uma experiência única</p>
```

3. **Informações de contato no rodapé** (linha ~223-230):
```html
<h4>Contato</h4>
<p>📱 WhatsApp: (51) 99999-9999</p>
<p>📍 Rua Exemplo, 123 - Porto Alegre/RS</p>
<p>✉️ contato@studioelegance.com.br</p>
```

### Alterar Serviços e Preços

**No arquivo `index.html`** (seção de serviços, linha ~50-120):

```html
<div class="service-card">
    <div class="service-icon">✂️</div>
    <h3 class="service-name">Corte Masculino</h3>
    <p class="service-description">Corte personalizado com acabamento impecável</p>
    <div class="service-price">R$ 45,00</div>
    <div class="service-duration">⏱️ 40 min</div>
</div>
```

Também altere no **select do formulário** (linha ~165-172):
```html
<option value="Corte Masculino - R$ 45,00">Corte Masculino - R$ 45,00</option>
```

### Alterar Profissionais

**No arquivo `index.html`** (linha ~177-182):
```html
<select id="professionalSelect">
    <option value="Sem preferência">Sem preferência</option>
    <option value="Carlos">Carlos</option>
    <option value="Marina">Marina</option>
    <!-- Adicione mais profissionais aqui -->
</select>
```

**No arquivo `admin.html`** (linha ~60-66):
```html
<select id="filterProfessional" class="filter-input">
    <option value="todos">Todos</option>
    <option value="Carlos">Carlos</option>
    <option value="Marina">Marina</option>
    <!-- Adicione os mesmos profissionais -->
</select>
```

### Alterar Horários Disponíveis

**No arquivo `index.html`** (linha ~192-210):
```html
<select id="bookingTime" required>
    <option value="">Selecione o horário</option>
    <option value="09:00">09:00</option>
    <option value="09:30">09:30</option>
    <!-- Adicione ou remova horários conforme necessário -->
</select>
```

### Alterar Cores do Site

**No arquivo `styles.css` e `admin-styles.css`** (linha ~1-10):
```css
:root {
    --primary: #1a1a1a;        /* Cor principal (preto) */
    --secondary: #d4af37;      /* Cor secundária (dourado) */
    --accent: #8b7355;         /* Cor de destaque (marrom) */
    /* Altere essas cores conforme a identidade visual do cliente */
}
```

**Sugestões de paletas:**
- **Moderno:** primary: #2c3e50, secondary: #e74c3c
- **Elegante:** primary: #1a1a2e, secondary: #16213e
- **Vibrante:** primary: #ff6b6b, secondary: #4ecdc4

---

## 📱 Testando o Sistema

### Teste Local (no seu computador):

1. **Opção 1 - Servidor Python:**
```bash
python -m http.server 8000
```
Acesse: `http://localhost:8000`

2. **Opção 2 - Servidor PHP:**
```bash
php -S localhost:8000
```
Acesse: `http://localhost:8000`

3. **Opção 3 - Live Server (VS Code):**
- Instale a extensão "Live Server"
- Clique com botão direito no `index.html`
- Selecione "Open with Live Server"

### Teste de Agendamento:

1. Acesse a página principal
2. Role até "Agende seu Horário"
3. Preencha o formulário
4. Clique em "Confirmar Agendamento"
5. Veja a mensagem de sucesso

### Teste do Painel Admin:

1. Acesse `http://localhost:8000/admin.html`
2. Veja o agendamento que você criou
3. Clique em "💬 Enviar Confirmação"
4. O WhatsApp deve abrir com a mensagem pronta

---

## 🌐 Colocando Online (Hospedagem Gratuita)

### Opção 1: Firebase Hosting (Recomendado)

1. Instale o Firebase CLI:
```bash
npm install -g firebase-tools
```

2. Faça login:
```bash
firebase login
```

3. Inicialize o projeto:
```bash
firebase init hosting
```

4. Escolha as opções:
   - Use um projeto existente: selecione seu projeto
   - Public directory: digite `.` (ponto)
   - Configure como SPA: `N` (não)
   - Sobrescrever index.html: `N` (não)

5. Faça o deploy:
```bash
firebase deploy
```

6. Seu site estará online em: `https://seu-projeto.web.app`

### Opção 2: Netlify (Mais Fácil)

1. Acesse: https://www.netlify.com/
2. Crie uma conta (grátis)
3. Arraste a pasta do projeto para o Netlify
4. Pronto! Seu site está online

### Opção 3: GitHub Pages

1. Crie um repositório no GitHub
2. Faça upload dos arquivos
3. Vá em Settings > Pages
4. Escolha a branch `main`
5. Salve e acesse seu site

---

## 💰 Monetização - Como Vender

### Estrutura de Preços Sugerida:

#### Pacote Básico - R$ 300 (pagamento único)
- ✅ Site completo personalizado
- ✅ Catálogo de serviços
- ✅ Formulário de agendamento
- ✅ Painel administrativo
- ✅ Integração WhatsApp (manual)
- ✅ Hospedagem grátis no Firebase
- ✅ 1 revisão de design
- ✅ Tutorial de uso

#### Pacote Premium - R$ 500 + R$ 50/mês
- ✅ Tudo do Pacote Básico
- ✅ Domínio personalizado (seusite.com.br)
- ✅ Automação completa WhatsApp*
- ✅ Lembretes automáticos
- ✅ Logo personalizada
- ✅ 3 revisões de design
- ✅ Suporte prioritário

*Requer integração com Evolution API ou similar

### Como Apresentar para Clientes:

1. **Crie uma apresentação mostrando:**
   - O problema atual (agendamentos por telefone são confusos)
   - A solução (sistema automatizado)
   - Benefícios (economia de tempo, menos erros, profissionalismo)

2. **Demonstração ao vivo:**
   - Mostre este template funcionando
   - Faça um agendamento de teste
   - Mostre como receber a confirmação no WhatsApp

3. **Argumentos de venda:**
   - "Seus clientes podem agendar 24/7"
   - "Reduza ligações telefônicas"
   - "Não perca mais clientes por falta de organização"
   - "Visual profissional aumenta credibilidade"
   - "Confirmação automática via WhatsApp"

---

## 🔧 Manutenção e Upgrades Futuros

### Melhorias que Você Pode Adicionar:

1. **Autenticação de Admin:**
   - Login com senha para acessar o painel

2. **Notificações por Email:**
   - Enviar emails além do WhatsApp

3. **Relatórios:**
   - Faturamento mensal
   - Serviços mais vendidos
   - Profissionais com mais agendamentos

4. **Integração com Calendário:**
   - Sincronizar com Google Calendar

5. **Pagamento Online:**
   - Aceitar pagamentos antecipados

6. **Sistema de Avaliações:**
   - Clientes podem avaliar o serviço

---

## 🆘 Problemas Comuns e Soluções

### Erro: "Firebase is not defined"
**Solução:** Verifique se colou as credenciais corretamente nos arquivos.

### Agendamentos não aparecem no painel
**Solução:** 
1. Verifique se as regras do Firestore estão corretas
2. Abra o Console do navegador (F12) e veja se há erros
3. Certifique-se de estar usando as mesmas credenciais em ambos os arquivos

### WhatsApp não abre
**Solução:**
1. Verifique se o número do cliente está correto (sem espaços ou caracteres especiais)
2. Teste em um dispositivo com WhatsApp instalado

### Site não funciona no celular
**Solução:** O site é responsivo, mas teste em um servidor real (não apenas abrindo o arquivo HTML).

---

## 📞 Suporte

Para dúvidas ou problemas:
1. Verifique este README novamente
2. Consulte a documentação do Firebase: https://firebase.google.com/docs
3. Revise o código comentado nos arquivos

---

## 📄 Licença

Este é um template para uso comercial. Você pode:
- ✅ Vender para clientes
- ✅ Personalizar à vontade
- ✅ Usar em múltiplos projetos
- ✅ Modificar o código

---

## 🎉 Próximos Passos

1. ✅ Configure o Firebase
2. ✅ Cole as credenciais
3. ✅ Teste localmente
4. ✅ Personalize para seu primeiro cliente
5. ✅ Faça o deploy
6. ✅ Apresente para o cliente
7. ✅ Receba o pagamento! 💰

**Boa sorte com suas vendas! 🚀**
# hairstudio
