# Relatório — Atividade Prática: Sockets TCP

**Disciplina:** Computação distribuída
**Nome:** Leonardo de Olivera Klitzke
**Data:** 12/10/2026

---

## Nível 1 — Inspecionar o código

### 1.1 Servidor (`servidor.py`)

Descreva com suas palavras o que cada chamada abaixo faz e por que ela
é necessária:

| Chamada | O que ela faz? |
|---------|---------------|
| `socket.socket(AF_INET, SOCK_STREAM)` | Cria um socket TCP |
| `servidor_socket.bind((HOST, PORTA))` | Define IP e Porta do servidor |
| `servidor_socket.listen(5)` | Servidor escuta requisições, e cria uma fila de até 5 conexões pendentes |
| `servidor_socket.accept()` | Aceita a conexão de um cliente |
| `conn.recv(TAMANHO_BUFFER)` | Recebe dados do cliente de até o tamanho do buffer |
| `conn.sendall(resposta.encode("utf-8"))` | Envia uma resposta do cliente |
| `conn.close()` | Encerra a conexão |

### 1.2 Cliente (`cliente.py`)

| Chamada | O que ela faz? |
|---------|---------------|
| `socket.socket(AF_INET, SOCK_STREAM)` | Cria o soket TCP do cliente |
| `cliente_socket.connect((HOST_SERVIDOR, PORTA_SERVIDOR))` | Conexão com o socket do servidor na porta e ip indicados|
| `cliente_socket.sendall(mensagem.encode("utf-8"))` | Envia dados para o servidor |
| `cliente_socket.recv(TAMANHO_BUFFER)` | Recebe dados do servidor com tam. máximo de TAMANHO_BUFFER |

### 1.3 Rede e contêineres

Por que o cliente usa o hostname `"servidor"` em vez de `"localhost"`
para se conectar? O que aconteceria se usasse `"localhost"`?

> _Resposta:_
Por que servidor e cliente estão em containeres docker diferentes, ou seja, cada container docker tem seu próprio localhost

Se usasse localhost ele encontraria o próprio endereço e tentaria fazer conexão consigo mesmo, o que não faz sentido
---

## Nível 2 — Modificar o servidor

Descreva as mudanças que você fez no `servidor.py` para:

1. Devolver a mensagem **em maiúsculas**:

   > Para isso é necessário apenas modificar a resposta que o servidor dá, originalmente tínhamos: `resposta = mensagem`, que foi modificado para `resposta = mensagem.upper()`, pois o `.upper()` retorna a string mensagem maiúscula

2. Exibir no log o **contador de mensagens recebidas** acumulado:

   >   Apenas adicionado um `total_mensagens += 1` após o recebimento da mensagem, pensei em fazer uma verificação `if mensagem`, mas não se faz necessária, pois isso está dentro de `if dados`, ou seja, dados chegaram (a verificação desejada)

Após a modificação, você precisou rodar `docker compose up --build`.
Por que o `--build` é necessário aqui?

> _Resposta:_ o `--build` é necessário para reconstruir o container, sem essa flag o servidor continua executando a versão antiga

---

## Observações livres

Anote aqui qualquer comportamento inesperado que observaram, erros que
apareceram e como resolveram, ou dúvidas que ainda têm:

>

---

## Dúvida para a próxima aula

> sem dúvidas
