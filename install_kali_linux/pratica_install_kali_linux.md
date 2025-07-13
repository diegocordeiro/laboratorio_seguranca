# 🐧 Prática: Instalação do Kali Linux

---

## 🎯 Objetivo

Iniciaremos nossas práticas com as ferramentas necessárias para compreender os passos realizados em um ataque específico. Para esse fim, iremos instalar o sistema operacional **Kali Linux**.

---

## 🔍 O que é o Kali Linux?

- Distribuição Linux de **código aberto** e gratuito, baseada em Debian.
- Voltada para:
  - Segurança da informação
  - Teste de penetração (pentest)
  - Computação forense
  - Engenharia reversa
- Possui mais de **600 ferramentas de teste**, como:
  - `Nmap` (scanner de portas)
  - `Wireshark` (sniffer de pacotes)
  - `John the Ripper` (cracker de senhas)
  - `Aircrack-ng` (testes de segurança em redes Wi-Fi)
- Mantida pela **Offensive Security**.

---

## 🖥️ Configuração do Ambiente

### 1. Download da Distribuição

Realize o download do instalador do sistema:

🔗 https://www.kali.org/get-kali/#kali-platforms  

- Utilizaremos a versão **ISO** para processadores com arquitetura **x64** (compatível com os computadores do laboratório).

---

### 2. Configuração da Máquina Virtual (VM)

Utilizaremos o **VirtualBox** para criar uma máquina virtual com as seguintes especificações:

- Sistema: Linux - 64 bits
- RAM: 2 GB
- Armazenamento: 20 GB (alocação dinâmica)
- Selecione a ISO previamente baixada  

---

### 3. Instalação do Sistema

Durante a instalação, siga os passos:

1. Selecione: **Graphical Install**
2. Idioma: **Português do Brasil**
3. Localização: **Brasil**
4. Teclado: **Português do Brasil**  
5. Nome da máquina (hostname): `kali-vm`
6. Nome de domínio: **deixe em branco**
7. Nome do usuário: `kali`  
   Senha: `ifpi@2025`
8. Definição do fuso horário: **Piauí**
9. Particionamento do disco:
   - "Assistido - usar o disco inteiro"
   - Selecione o disco virtual
   - "Todos os arquivos em uma partição (para iniciantes)"
   - "Finalizar o particionamento e escrever as mudanças no disco"
10. Confirme as mudanças no disco: **Sim**
11. Mantenha a seleção de pacotes padrão e clique em **Continuar**
12. Ao final, **remova a ISO** do drive da VM e **reinicie** a máquina

✅ Agora o Kali Linux está instalado e pronto para uso!

📺 Vídeo de apoio:  
🔗 [Tutorial Passo a Passo](https://drive.google.com/file/d/1QRCNXkNmrvf3LLsO5VmYyVljcJtrB8pG/view?usp=share_link)

---

## 🧰 Ferramentas disponíveis no Kali Linux

- Aircrack-ng  
- John the Ripper  
- Kismet  
- Maltego  
- Metasploit Framework  
- Nmap  
- Nikto  
- Social Engineering Tools  
- Sqlmap  
- Wireshark  
- Nessus  
- Zenmap  
- Hydra

Essas ferramentas permitem, entre outras ações:

- Exploração de falhas em redes e aplicações
- Descoberta de computadores na rede
- Varredura de portas e serviços por IP

---

## 📚 Atividade

1. Realize a instalação do Kali Linux em uma máquina no laboratório.  
2. Pesquise as funcionalidades e objetivos das ferramentas:

   - 🔎 **Nmap**
   - 🔐 **Nessus**
   - 📡 **Aircrack-ng**
