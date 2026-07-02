# 🎟️ Rifa_Machine — Sistema Operacional de Alocação e Auditoria de Ativos Sorteáveis

Um MVP utilitário de engenharia de software desenvolvido em Python e Tkinter para automatizar a triagem, alocação segura, rastreabilidade e sorteio auditável de cotas numeradas (ledger de 1 a 100 ativos).

---

## 📄 O Problema de Negócio (Data Storytelling)

Em campanhas institucionais, ações beneficentes ou distribuições corporativas de prêmios, o controle manual de planilhas físicas ou de papel apresenta alto risco operacional. Os gargalos mais comuns incluem a venda duplicada do mesmo número (dupla alocação), fraudes por alteração indevida de dados e falta de transparência no momento do sorteio. 

O **Rifa_Machine** resolve essa dor eliminando falhas humanas na governança do processo. Ele atua como um livro-razão local (*ledger*) que assegura a unicidade de cada cota, gerencia a mutabilidade de posse dos ativos (transferências) e garante um sorteio transacional perfeitamente aleatório, transparente e auditável.

---

## 🎯 Funcionalidades de Negócios & Entrega de Valor

A aplicação foi estruturada dividindo as responsabilidades de conformidade operacional em quatro módulos principais:

* 📥 **Módulo de Ingestão e Higienização de Dados:** Interface de cadastro equipada com um pipeline de tratamento de strings. O motor higieniza as entradas, remove espaços em branco, descarta caracteres inválidos e impede duplicidades síncronas antes de submeter os números ao banco de dados em memória.
* 🔍 **Módulo de Consulta e Auditoria:** Tela de exibição que consolida o status atual do livro-razão. Agrupa os números por comprador de forma ordenada (alfabética e numérica), calculando o balanço de liquidez das vendas em tempo real (ex: "X de 100 ativos alocados").
* ⚙️ **Componente de Mutabilidade e Transferência:** Ferramenta dedicada a garantir o compliance de pós-venda. Permite a edição em lote de nomes ou a transferência pontual e segura da propriedade de um número específico entre compradores, sem corromper o histórico de dados.
* 🎰 **Motor Transacional de Sorteio Automático:** Algoritmo estatístico que processa as chaves do ledger (`random.choice`) para determinar o ganhador. O sistema possui trava de segurança nativa: impede a realização de sorteios caso a liquidez de vendas seja igual a zero, mitigando execuções em falso.

---

## 🛠️ Engenharia de Software & Integridade de Estado

O grande diferencial deste utilitário reside no rigor da validação e na blindagem de dados aplicada diretamente na camada lógica da interface gráfica:

### 🛡️ Higienização Síncrona e Tratamento de Duplicações
Para evitar colisões de dados ou travamentos caso o operador insira números repetidos na mesma linha, o sistema utiliza compressão de dados por conjuntos (*set comprehension*) em tempo de execução para higienizar e deduzir a intenção do usuário de forma atômica:

```python
# Pipeline de validação e desduplicação em tempo real
try:
    numeros_escolhidos = [int(x) for x in {p.strip() for p in entrada.split(',')} if x != ""]
except ValueError:
    messagebox.showerror("Erro", "Números inválidos. Use apenas inteiros separados por vírgula.")
```
### 🧵 Sincronização de Estado Multi-Janelas

A arquitetura do software gerencia a consistência de dados em múltiplas camadas de visualização (`tk.Toplevel`). Sempre que uma transação de compra é consolidada com sucesso, o sistema dispara rotinas reativas que atualizam dinamicamente os contadores e os rótulos de status na janela principal e nos buffers de texto secundários, eliminando divergências visuais para o operador.

---

## 🔍 Visualização da Interface

*(Insira aqui capturas de tela das janelas do menu principal, tela de cadastro com lista de números disponíveis e o pop-up de celebração do ganhador sorteado)*

---

## 🚀 Como Executar o Projeto

### Requisitos do Sistema
* Python 3 instalado no ambiente global.
* Interface gráfica nativa (Tkinter já vem embutido por padrão no instalador oficial do Python).

### Execução
1.  Salve o arquivo principal da aplicação como `rifa_gui.py`.
2.  Execute o comando diretamente no seu terminal de preferência:

```bash
python rifa_gui.py

```

## 🗺️ Roadmap de Evolução Arquitetural

- [ ] Implementar camada de persistência definitiva utilizando banco de dados relacional leve (`SQLite3`).
- [ ] Desenvolver exportador de relatórios e recibos de transações em formato PDF para os compradores.
- [ ] Integrar sementes criptográficas (*cryptographic seeds*) na função de sorteio para implementar o conceito de *Provably Fair* (Sorteio Comprovadamente Justo).

---

## 💼 Atuação Consultiva e Aplicação Prática

Esta prova de conceito (*Proof of Concept*) demonstra de forma prática minha capacidade de estruturar sistemas de validação rígida, gerenciamento estável de estados locais e automação de regras de negócio de ponta a ponta. Aplico essa visão orientada a processos na criação de soluções utilitárias que mitiguem erros em rotinas operacionais e logísticas de empresas.

---

## 📬 Contatos e Links Úteis

* 📧 **Contato para Projetos Corporativos:** fcoliveirasilva@gmail.com
* 🗂️ **Voltar ao Portfólio Central:** [Mapeamento de Habilidades](https://github.com/fernandocosilva/inventario-de-habilidades)
