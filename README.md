# 💬Chat do Marques

Um chat em tempo real minimalista construído com **Node.js**, **Express** e **Socket.IO** — com interface moderna em HTML/CSS puro.

---

## ✨ Funcionalidades

- Entrada com apelido único por sala (nomes duplicados são rejeitados)
- Mensagens em tempo real via WebSocket
- Diferenciação visual entre suas mensagens e as dos outros usuários
- Desconexão automática libera o nome na sala
- Validação server-side: apenas o dono do socket pode enviar mensagens em seu nome

---

## 🛠️ Tecnologias

| Camada     | Tecnologia                          |
|------------|-------------------------------------|
| Runtime    | Node.js                             |
| Servidor   | Express                             |
| WebSocket  | Socket.IO                           |
| Front-end  | HTML5 · CSS3 · JavaScript vanilla   |

---

## 🚀 Como rodar localmente

### Pré-requisitos

- [Node.js](https://nodejs.org/) v14 ou superior

### Instalação

```bash
# Clone o repositório
git clone https://github.com/seu-usuario/chat-do-marques.git
cd chat-do-marques

# Instale as dependências
npm install
```

### Execução

```bash
node index.js
```

Acesse no navegador: [http://localhost:3000](http://localhost:3000)

---

## 📁 Estrutura do projeto

```
chat-do-marques/
├── index.js       # Servidor Node.js + lógica de WebSocket
├── index.html     # Interface do chat
├── package.json
└── README.md
```

---

## ⚙️ Como funciona

### Fluxo de conexão

```
Cliente abre o chat
  └─► Modal pede apelido
        └─► Emite "new user" para o servidor
              ├─► Nome disponível → entra na sala ✅
              └─► Nome em uso    → erro no modal  ❌
```

### Eventos Socket.IO

| Evento          | Direção           | Descrição                                      |
|-----------------|-------------------|------------------------------------------------|
| `new user`      | cliente → servidor| Registra o apelido do usuário                  |
| `new user`      | servidor → cliente| Retorna `{ success: true/false }`              |
| `chat message`  | cliente → servidor| Envia `{ msg, nome }` para o servidor          |
| `chat message`  | servidor → todos  | Broadcast da mensagem para a sala              |
| `disconnect`    | automático        | Remove usuário e libera o apelido              |

### Segurança de identidade

O servidor valida que o `socket.id` de quem envia a mensagem corresponde ao nome declarado — impedindo que um cliente envie mensagens fingindo ser outro usuário.

---

## 📦 Dependências

```json
{
  "express": "^4.x",
  "socket.io": "^4.x"
}
```

Instale com:

```bash
npm install express socket.io
```

---

## 🔮 Melhorias futuras

- [ ] Suporte a múltiplas salas
- [ ] Histórico de mensagens com banco de dados
- [ ] Indicador de "digitando…"
- [ ] Autenticação com usuário e senha
- [ ] Deploy no Railway / Render / Fly.io

---

## 📄 Licença

MIT — sinta-se livre para usar, modificar e distribuir.
