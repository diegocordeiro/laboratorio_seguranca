# Prática Nmap: Varredura de Rede com Kali Linux  

---

## **Introdução ao Nmap**  
- **Nmap** (Network Mapper) é uma ferramenta de código aberto para **exploração de redes** e **auditoria de segurança**.  
- Usado para:  
  - Descobrir hosts e serviços em uma rede.  
  - Identificar portas abertas, sistemas operacionais e vulnerabilidades.  
- **Kali Linux** já inclui o Nmap por padrão.  

**Comando básico**:  
```bash
nmap [opções] [alvo]
```

---

## **Instalação e Verificação**  
- No Kali Linux, o Nmap já está instalado. Para verificar:  
  ```bash
  nmap --version
  ```  
- Caso precise instalar:  
  ```bash
  sudo apt update && sudo apt install nmap
  ```  

**Dica**: Sempre mantenha o Nmap atualizado para ter as últimas funcionalidades.  

---

## **Varredura de Hosts (Ping Scan)**  
- Identifica hosts ativos em uma rede sem escanear portas.  
  ```bash
  nmap -sn 192.168.1.0/24
  ```  
- **Exemplo de saída**:  
  ```  
  Host 192.168.1.1 is up.  
  Host 192.168.1.5 is up.  
  ```  
- **-sn**: Desativa a varredura de portas (somente ping).  

---

## **Varredura de Portas TCP**  
- Descobre portas abertas em um host específico.  
  ```bash
  nmap -sS 192.168.1.1
  ```  
- **-sS**: **TCP SYN Scan** (stealth scan) – rápido e discreto.  
- **Portas comuns**:  
  - **22 (SSH)**, **80 (HTTP)**, **443 (HTTPS)**.  

**Importante**: Varreduras agressivas podem ser detectadas por firewalls.  

---

## **Varredura de Portas UDP**  
- Serviços como DNS e DHCP usam UDP.  
  ```bash
  nmap -sU 192.168.1.1
  ```  
- **-sU**: Especifica varredura UDP.  
- **Mais lenta** que TCP devido à natureza do protocolo UDP.  

---

## **Detecção de Sistema Operacional**  
- Identifica o SO do host alvo.  
  ```bash
  nmap -O 192.168.1.1
  ```  
- **-O**: Ativa a detecção de OS.  
- **Precisa de permissões root** para maior precisão.  

**Exemplo de saída**:  
```  
Running: Linux 3.X  
OS details: Linux 3.2 - 4.9  
```  

---

## **Varredura de Serviços e Versões**  
- Identifica versões de serviços rodando nas portas.  
  ```bash
  nmap -sV 192.168.1.1
  ```  
- **-sV**: Ativa detecção de versão.  
- **Útil** para encontrar vulnerabilidades conhecidas.  

**Exemplo**:  
```  
80/tcp open  http    Apache 2.4.29  
```  

---

## **Varredura Agressiva**  
- Combina técnicas para um scan detalhado.  
  ```bash
  nmap -A 192.168.1.1
  ```  
- **-A**: Inclui detecção de OS, versão de serviços e scripts NSE.  
- **Cuidado**: Gera muito tráfego e pode ser detectado.  

---

## **Scripts NSE (Nmap Scripting Engine)**  
- Automatiza tarefas como exploração e coleta de informações.  
  ```bash
  nmap --script=http-title 192.168.1.1
  ```  
- **Exemplos de scripts**:  
  - **http-title**: Extrai o título da página web.  
  - **vulners**: Busca vulnerabilidades conhecidas.  

**Documentação**: [Nmap Scripting Engine Docs](https://nmap.org/book/nse.html)  

---

## **Conclusão e Boas Práticas**  
- **Resumo**:  
  - Nmap é **poderoso** para análise de redes.  
  - Use varreduras **leves** (-sS) para evitar detecção.  
  - Combine técnicas (-A) para relatórios detalhados.  
- **Boas práticas**:  
  - Sempre **obtenha permissão** antes de escanear redes.  
  - Use **--help** ou **man nmap** para explorar opções.  