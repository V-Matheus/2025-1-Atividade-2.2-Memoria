# S.O. 2025.1 - Atividade 2.02 - Gestão de memória

## Informações gerais

- **Objetivo do repositório**: Repositório para atividade avaliativa dos alunos
- **Assunto**: Gestão de memória
- **Público alvo**: alunos da disciplina de SO (Sistemas Operacionais) do curso de TADS (Superior em Tecnologia em Análise e Desenvolvimento de Sistemas) no CNAT-IFRN (Instituto Federal de Educação, Ciência e Tecnologia do Rio Grande do Norte - Campus Natal-Central).
- disciplina: **SO** [Sistemas Operacionais](https://github.com/sistemas-operacionais/)
- professor: [Leonardo A. Minora](https://github.com/leonardo-minora)
- Repositótio do aluno: FIXME

## Tarefas do aluno
1. Fork desse repositório e atualizar a linha 10 com o nome e link do github
2. Ler a descrição da atividade
3. Montar a resposta no final deste arqivo, no tópico **Resposta**

---

## 1. Descrição da atividade
### 1.1. Objetivo
Praticar os conceitos de alocação de memória (best-fit), memória virtual e desfragmentação em um sistema com memória limitada.

---

### 1.2. Contexto
Um computador possui apenas **64 KB de RAM** e um **disco rígido para memória virtual**. O sistema operacional deve gerenciar 5 processos com tamanhos diferentes, cuja soma ultrapassa a capacidade da RAM.

#### 1.2.1. Processos iniciais

| Processo | Tamanho (KB) |
|----------|-------------|
| P1       | 20          |
| P2       | 15          |
| P3       | 25          |
| P4       | 10          |
| P5       | 18          |
| **Total**| **88 KB**   |

- **Memória RAM**: 64 KB (contígua, inicialmente vazia).  
- **Memória Virtual (Disco)**: Espaço ilimitado para paginação.

#### 1.2.2. Alocação Inicial com Best-Fit
Os alunos devem simular a alocação dos processos na RAM usando o algoritmo **best-fit**.  
- A memória RAM será representada como um bloco contíguo (ex: `[0KB - 64KB]`).  
- Devem alocar os processos nos menores espaços livres que atendam ao seu tamanho.  

**Alocação inicial**:  
1. P1 (20 KB) → Ocupa [0-20].  
2. P2 (15 KB) → Ocupa [20-15].  
3. _continuar a partir daqui_

#### 1.2.3. Simular Memória Virtual (Paginação)
- Os processos não alocados na RAM devem ser "paginados" no disco.  
- Criar uma tabela de páginas indicando quais partes estão na RAM e quais estão no disco.  

#### 1.2.4. Desfragmentação da RAM
- Desfragmentar a RAM para liberar espaço contíguo.
- Após desfragmentação (compactação), verificar quais processos podem ser alocado.  

### 1.3. Questões para Reflexão
1. Best-fit foi mais eficiente que first-fit ou worst-fit neste cenário?  
2. Como a memória virtual evitou um deadlock?  
3. Qual o impacto da desfragmentação no desempenho do sistema?  

---

## Resposta

### 1. Alocação Inicial com Best-Fit

- **Processos e tamanhos:**  
  - P1: 20 KB  
  - P2: 15 KB  
  - P3: 25 KB  
  - P4: 10 KB  
  - P5: 18 KB  
- **RAM disponível:** 64 KB

**Alocação Best-Fit (simulação):**
- P1 (20 KB) → [0-20]
- P2 (15 KB) → [20-35]
- P4 (10 KB) → [35-45]
- P5 (18 KB) → [45-63] (sobra 1 KB livre)
- P3 (25 KB) → Não cabe na RAM

**Resumo:**  
P1, P2, P4 e P5 alocados na RAM. P3 fica fora.


### 2. Simular Memória Virtual (Paginação)

| Processo | RAM (KB) | Disco (KB) |
|----------|----------|------------|
| P1       | 20       | 0          |
| P2       | 15       | 0          |
| P3       | 0        | 25         |
| P4       | 10       | 0          |
| P5       | 18       | 0          |

---

### 3. Desfragmentação da RAM

Após desfragmentação, a RAM fica contígua, liberando 1 KB no final.  
Ainda não é possível alocar P3 (25 KB), pois não há espaço suficiente.

---

 ### 4. Questões para Reflexão

**Best-fit foi mais eficiente que first-fit ou worst-fit neste cenário?**  
Sim, pois minimizou fragmentação interna, permitindo alocar mais processos na RAM.

**Como a memória virtual evitou um deadlock?**  
Permitiu que processos excedentes fossem paginados para o disco, evitando bloqueio por falta de memória física.

**Qual o impacto da desfragmentação no desempenho do sistema?**  
Desfragmentação melhora o uso da RAM, reduz fragmentação e pode permitir alocação de novos processos, mas pode causar overhead temporário durante o processo.