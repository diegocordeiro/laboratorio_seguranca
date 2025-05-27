
# 🧪 Laboratório: Kali Linux + iptables para Treinar Bloqueio de Pacotes

## 🎯 Objetivo
- Configurar o `iptables` no Kali Linux para bloquear pacotes destinados ao IP `7.8.9.10`.
- Entender cada comando e operação.
- Testar conectividade com `ping` e `nc` (netcat).

---

## 🌐 Topologia Simulada

| Máquina              | IP                       | Função                                 |
|----------------------|--------------------------|----------------------------------------|
| Kali Linux (Firewall) | 192.168.56.101           | Servidor com `iptables` configurado.    |
| Destino Simulado     | 7.8.9.10 (via `lo`)       | IP simulado na interface de loopback.  |

---

## 🛠️ Passo a Passo Detalhado

### 1️⃣ Preparar o Kali Linux

```bash
sudo apt update
```
- Atualiza a lista de pacotes disponíveis.

```bash
sudo apt install iptables net-tools iproute2 iputils-ping netcat-traditional
```
- Instala ferramentas de rede necessárias:
  - `iptables`: firewall.
  - `net-tools`: utilitários clássicos (ex.: `ifconfig`).
  - `iproute2`: gerencia IPs (ex.: `ip a`).
  - `iputils-ping`: teste de conectividade ICMP.
  - `netcat-traditional`: testes de conexão TCP/UDP.

---

### 2️⃣ Descobrir o IP do Kali

```bash
ip a
```
- Exibe endereços IP das interfaces.

---

### 3️⃣ Simular o IP 7.8.9.10 no Kali

```bash
sudo ip addr add 7.8.9.10/32 dev lo
```
- Adiciona o IP `7.8.9.10` na interface `lo` (loopback).

Verificar:
```bash
ip a | grep 7.8
```
- Filtra a saída para ver o IP 7.8.9.10.

---

### 4️⃣ Testar conectividade sem bloqueios

Ping:
```bash
ping -c 4 7.8.9.10
```
- Envia 4 pacotes ICMP para o IP.

Netcat (terminal 1):
```bash
nc -lvp 8080
```
- Inicia um servidor TCP na porta 8080.
- `l`: Modo servidor (escutar).
- `v`: Verbose (detalhes).
- `p 8080`: Porta 8080.

Netcat (terminal 2):
```bash
nc 7.8.9.10 8080
```
- Conecta ao servidor no IP `7.8.9.10` e porta `8080`.

---

### 5️⃣ Criar a regra de bloqueio no iptables

```bash
sudo iptables -A INPUT -d 7.8.9.10 -j DROP
```
- `-A INPUT`: adiciona na cadeia INPUT.
- `-d 7.8.9.10`: aplica para pacotes com destino `7.8.9.10`.
- `-j DROP`: descarta os pacotes.

Verificar as regras:
```bash
sudo iptables -L -n --line-numbers
```
- `-L`: Lista as regras atuais.
- `- n`: Mostra endereços numéricos (não resolve nomes DNS).
- `--line-numbers`: Mostra o número de cada regra (útil para remoção).

---

### 6️⃣ Testar bloqueio com ping e netcat

Ping:
```bash
ping -c 4 7.8.9.10
```
- Espera-se que **não haja resposta**.

Netcat:
```bash
nc 7.8.9.10 8080
```
- A conexão não será estabelecida.

---

### 7️⃣ Remover a regra de bloqueio

```bash
sudo iptables -D INPUT 1
```
- Remove a **primeira** regra da cadeia INPUT.

Testar novamente `ping` e `nc` — agora devem funcionar.

---

## 📌 Conceitos Aprendidos

✅ `iptables` como firewall no Linux.  
✅ Bloqueio de pacotes baseado no **destino** (`-d`).  
✅ Testes práticos com `ping` e `nc`.  
✅ Gerenciamento de regras (`-A`, `-D`, `-L`).

---

## 🚀 Dica Extra

Quer praticar mais? Experimente:
- Bloquear pacotes **de origem** (`-s`).
- Bloquear portas específicas (`-p tcp --dport 80`).
- Criar um script para regras automáticas.
