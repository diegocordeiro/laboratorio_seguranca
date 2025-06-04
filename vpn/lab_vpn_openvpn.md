# 🔍 Testando Acesso Seguro com Wireshark (Antes e Depois da VPN)

## 🎯 Objetivo

Capturar pacotes de rede para **comparar o tráfego sem VPN (não criptografado)** com o **tráfego criptografado com VPN**, utilizando o Wireshark no Kali Linux.

---

## ⚙️ Pré-requisitos

- Kali Linux com Wireshark instalado:

```bash
  sudo apt install wireshark -y
````

* Conexão com a internet (via Wi-Fi ou Ethernet).
* VPN funcional com OpenVPN (cliente configurado).
* Acesso a um site (ex: [http://www.ifsul.edu.br/](http://www.ifsul.edu.br/)).

---

## 🧪 Etapa 1: Captura de Tráfego Sem VPN

1. Abrir o Wireshark:

   ```bash
   sudo wireshark &
   ```

2. Selecionar a interface de rede usada para a internet (ex: `eth0` ou `wlan0`).

3. Iniciar a captura.

4. Em outro terminal, gerar tráfego HTTP simples:

   ```bash
   curl http://www.ifsul.edu.br/
   ```

5. Parar a captura no Wireshark.

6. Aplicar filtro para visualizar pacotes HTTP:

   ```
   http
   ```

   ou

   ```
   ip.addr == [SEU IP]
   ```

7. Analisar:

   * O conteúdo da requisição HTTP está visível.
   * Cabeçalhos e dados trafegam em texto claro.

---

## 🔐 Etapa 2: Captura de Tráfego com VPN Ativa

1. Conectar-se à VPN:

   ```bash
   sudo openvpn --config cliente1.ovpn
   ```

2. Verificar conexão (mensagem: `Initialization Sequence Completed`).

3. Voltar ao Wireshark e iniciar nova captura na mesma interface (`eth0` ou `wlan0`).

4. Gerar o mesmo tráfego:

   ```bash
   curl http://www.ifsul.edu.br/
   ```

5. Parar a captura.

6. Aplicar filtros para tráfego VPN:

   ```
   udp.port == 1194
   ```

   ou

   ```
   ip.addr == [IP_DO_SERVIDOR_VPN]
   ```

7. Analisar:

   * O tráfego HTTP não é visível.
   * Pacotes são encapsulados em UDP com conteúdo criptografado.
   * Dados da aplicação aparecem como binário (ilegível).

---

## 📸 Resultado Esperado

| Situação        | Visível no Wireshark?                                |
| --------------- | ---------------------------------------------------- |
| Sem VPN         | ✅ Sim – dados HTTP em texto claro                    |
| Com VPN (ativa) | 🔒 Não – apenas pacotes criptografados (UDP/OpenVPN) |

---

## 📚 Dica Extra: Mostrar Encapsulamento

* Clique em um pacote UDP da VPN no Wireshark.
* Observe:

  * Camada de transporte: UDP
  * Camada de aplicação: dados criptografados
  * Nenhum conteúdo HTTP visível

