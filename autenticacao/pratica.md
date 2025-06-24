
# 🔐 Prática: Assinatura Digital e Verificação de Integridade com Hash no Kali Linux

## 🎯 Objetivos

- Compreender os conceitos de **assinatura digital** e **função hash**.
- Criar um par de chaves criptográficas.
- Gerar o **hash** de um documento e usar a **chave privada** para assinar digitalmente.
- Usar a **chave pública** para verificar a assinatura.
- Identificar alterações no conteúdo via verificação de integridade.

---

## 🧠 Conceitos Fundamentais

### 🔢 Função Hash

- Uma função hash transforma qualquer entrada (como um texto) em uma sequência de tamanho fixo (ex: 256 bits).
- Pequenas mudanças no conteúdo resultam em hashes completamente diferentes.
- Exemplo: SHA-256 é uma função de hash amplamente utilizada.

### ✍️ Assinatura Digital

- A assinatura digital é criada **assinando o hash** de uma mensagem com a **chave privada**.
- Quem possui a **chave pública** pode verificar a autenticidade e integridade da mensagem.
- Isso garante:
  - **Autenticidade:** só o dono da chave privada poderia assinar.
  - **Integridade:** qualquer alteração na mensagem invalida a assinatura.
  - **Não repúdio:** o autor não pode negar que assinou a mensagem.

---

## 🧰 Pré-requisitos

- Kali Linux.
- Acesso ao terminal.
- Comandos `openssl`, `sha256sum` disponíveis.

---

## 🧪 Etapas da Prática

### 📁 1. Criar o Documento a Ser Assinado

```bash
echo "Documento oficial de teste - Prática de Assinatura Digital" > documento.txt
````

---

### 🔑 2. Gerar Par de Chaves Criptográficas

```bash
# Chave privada
openssl genpkey -algorithm RSA -out chave_privada.pem -pkeyopt rsa_keygen_bits:2048

# Chave pública
openssl rsa -pubout -in chave_privada.pem -out chave_publica.pem
```

---

### 🧾 3. Gerar o Hash do Documento

```bash
sha256sum documento.txt > hash_documento.txt
cat hash_documento.txt
```

> Observe o hash gerado e salve para futura comparação.

---

### ✍️ 4. Assinar o Documento Digitalmente

```bash
openssl dgst -sha256 -sign chave_privada.pem -out assinatura.bin documento.txt
```

---

### 🔍 5. Verificar a Assinatura com a Chave Pública

```bash
openssl dgst -sha256 -verify chave_publica.pem -signature assinatura.bin documento.txt
```

> **Saída esperada:**
>
> ```
> Verified OK
> ```

---

### 🔁 6. Alterar o Documento e Testar a Integridade

```bash
echo "Tentando alterar o documento..." >> documento.txt
```

#### Recalcular o Hash:

```bash
sha256sum documento.txt
```

> Compare com o hash original salvo em `hash_documento.txt`.

#### Tentar Verificar a Assinatura Novamente:

```bash
openssl dgst -sha256 -verify chave_publica.pem -signature assinatura.bin documento.txt
```

> **Saída esperada:**
>
> ```
> Verification Failure
> ```

---

## 🗂 Estrutura Final de Arquivos

```
documento.txt           → Documento original/modificado
chave_privada.pem       → Chave usada para assinar
chave_publica.pem       → Chave usada para verificar
assinatura.bin          → Assinatura digital (do hash do documento)
hash_documento.txt      → Hash SHA-256 original do documento
```

---

## 🧠 Reflexão e Discussão

1. Por que uma pequena modificação no arquivo invalida a assinatura?
2. Qual o papel da função hash na assinatura digital?
3. Por que usamos a chave privada para assinar e a pública para verificar?
4. Como garantir que a chave pública recebida é realmente do remetente?
5. Como garantimos a confidencialidade da mensagem?

---

## ✅ Conclusão

Você testou os principais conceitos por trás da **assinatura digital** e da **verificação de integridade** usando funções de **hash criptográfico** e **criptografia de chave pública** com `openssl`.
