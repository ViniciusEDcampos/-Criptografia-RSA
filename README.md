# 🔐 Criptografia RSA: Princípios e Funcionamento

Este repositório contém uma explicação sobre os princípios matemáticos, funcionamento e aplicações práticas do algoritmo de Criptografia RSA.

## 1. O que é o RSA?

O RSA (Rivest-Shamir-Adleman) é um algoritmo de **criptografia de chave pública** (ou assimétrica), desenvolvido em 1977. Ele é um dos pilares da segurança digital moderna.

Sua principal característica é o uso de um par de chaves:

* **Chave Pública ($N, e$):** Usada para criptografar a mensagem. Pode ser compartilhada abertamente.
* **Chave Privada ($N, d$):** Usada para descriptografar a mensagem. Deve ser mantida em absoluto segredo.

O RSA resolve o problema clássico da criptografia: a necessidade de compartilhar uma chave secreta de forma segura antes de iniciar a comunicação.

## 2. 📐 Fundamentos Matemáticos

A robustez do RSA reside na dificuldade computacional de problemas da Teoria dos Números.

### 2.1. Números Primos e Fatoração

A segurança do RSA baseia-se na **dificuldade de fatorar números inteiros grandes**.

1.  **Geração do Módulo:** O algoritmo escolhe dois números primos grandes e distintos, $p$ e $q$.
2.  **Cálculo de N:** O módulo $N$ é o produto desses primos: $N = p \times q$.
3.  **O Problema:** Mesmo que $N$ seja público, é computacionalmente inviável para um atacante encontrar $p$ e $q$ se $N$ for grande o suficiente. Se $N$ for fatorado, o sistema é quebrado.

### 2.2. Aritmética Modular e Teorema de Euler

A codificação e decodificação usam a congruência modular.

* **Função Totiente de Euler ($\phi(N)$):** Essencial para gerar a chave privada. Ela calcula a quantidade de números positivos menores que $N$ que são coprimos com $N$. Para $N = p \times q$, a fórmula é:
    > $\phi(N) = (p-1)(q-1)$

* **Expoente Privado ($d$):** O expoente $d$ é o inverso multiplicativo do expoente público $e$ módulo $\phi(N)$. Ele é encontrado resolvendo a congruência:
    > $e \times d \equiv 1 \pmod{\phi(N)}$

O **Teorema de Euler** garante que o processo é reversível, ou seja, que a mensagem criptografada pode ser descriptografada de volta ao seu original.

## 3. ⚙️ O Algoritmo Passo-a-Passo

O processo do RSA é dividido em três fases:

### Fase 1: Geração de Chaves

1.  **Escolher Primos:** Selecionar dois primos grandes e aleatórios, $p$ e $q$.
2.  **Calcular $N$ e $\phi(N)$:**
    * $N = p \times q$ (Módulo público)
    * $\phi(N) = (p-1)(q-1)$ (Valor secreto)
3.  **Escolher $e$ (Expoente Público):** Selecionar $e$ tal que $1 < e < \phi(N)$ e $mdc(e, \phi(N)) = 1$. (Um valor comum e eficiente é $e = 65537$).
4.  **Calcular $d$ (Expoente Privado):** Calcular $d$ tal que $e \times d \equiv 1 \pmod{\phi(N)}$ (usando o Algoritmo Euclidiano Estendido).

**Resultado:**
* **Chave Pública:** $(N, e)$
* **Chave Privada:** $(N, d)$

---

### Fase 2: Criptografia (Codificação)

Para criptografar uma mensagem $M$ (onde $M$ é um número $M < N$) usando a **Chave Pública ($N, e$)**:

> $C \equiv M^e \pmod{N}$

O resultado $C$ é o texto cifrado.

---

### Fase 3: Descriptografia (Decodificação)

Para decodificar o texto cifrado $C$ usando a **Chave Privada ($N, d$)**:

> $M \equiv C^d \pmod{N}$

O resultado $M$ é a mensagem original.

## 4. 🛡️ Segurança e Aplicações Práticas

### 4.1. Tamanho da Chave

A segurança depende da inviabilidade de fatorar $N$.
* Chaves curtas (ex: 768 bits) já foram quebradas.
* **Recomendação Atual:** O comprimento mínimo de chave recomendado é de **2048 bits**. Chaves de 4096 bits são usadas para segurança de longo prazo.

### 4.2. Aplicações

O RSA é mais lento que algoritmos simétricos (como o AES). Por isso, ele é mais usado em **sistemas híbridos**.

* **Comunicações Seguras (HTTPS, SSH, VPNs):** O RSA é usado para criptografar e trocar de forma segura uma "chave de sessão" (uma chave simétrica). O restante da comunicação é criptografado com a chave simétrica (AES), que é muito mais rápida.
* **Assinaturas Digitais:** O RSA é ideal para autenticação. Para assinar, o remetente criptografa o *hash* da mensagem com sua **chave privada**. O destinatário usa a **chave pública** do remetente para descriptografar o hash e verificar a autenticidade e integridade da mensagem.

### 4.3. Limitações

* **Performance:** Lento para criptografar grandes volumes de dados.
* **Computação Quântica:** O RSA é vulnerável ao **Algoritmo de Shor**, que pode fatorar números grandes em tempo polinomial. Isso exigirá uma futura migração para a criptografia pós-quântica.

---

## 📚 Fonte Principal

Este conteúdo é baseado em dissertações e artigos que abordam a Criptografia RSA, Teoria dos Números e Aritmética Modular, como a tese de mestrado de Daniele Helena Bonfim (2017) e o TCC de Camila Cecilia Castro (2019).
