# O Jogo do Bicho Misterioso

**Roteiro de aula — parte prática**
*Revisão de Python a serviço do pensamento computacional em IA — Aula 01*

> Inteligência Artificial e Aprendizagem de Máquina · FECAP · 2026/02

---

## Objetivo da aula

Preparar o raciocínio exigido pela disciplina — representar conhecimento, organizar dados e tomar decisões a partir de atributos — usando a revisão de Python como veículo, não como fim em si.

Ao final, o aluno terá construído, célula por célula, um sistema de perguntas e respostas que descobre um animal por eliminação, e terá percebido — sem que isso precise ser dito explicitamente — que esse sistema é equivalente aos exemplos de "IA baseada em regras" já vistos nos tópicos 1.2 e 1.3.

## Por que "O Jogo do Bicho Misterioso"

Dar um nome à atividade ajuda a reconhecê-la ao longo do semestre: o mesmo conjunto de animais e atributos volta nas Aulas 2 (Pandas), 3 (visualização), 4-5 (regressão/classificação) e 7 (clustering) — o aluno aprende técnica nova sem precisar entender um domínio novo a cada aula.

- Atributos booleanos simples (voa, nada, tem pelos, é doméstico, bota ovos) — sem exigir conhecimento prévio de nenhuma área específica.
- Evita ambiguidades comuns de personagens fictícios ou pessoas reais.
- Permite construir filtros progressivos de forma intuitiva, sem jargão técnico.

## Antes de começar (pré-requisitos da aula)

Esta parte prática pressupõe que os alunos já têm uma conta Google ativa e sabem, no mínimo, abrir um notebook em branco no Colab (coberto na etapa de configuração de ambiente da Aula 01). Não é necessário nenhum conhecimento prévio de Python.

## Visão geral dos blocos

| Duração | Bloco | Pergunta condutora | Conceito Python |
|---|---|---|---|
| 8 min | 0. Abertura — jogo humano (sem código) | Como vocês descobrem o animal um do outro, só com perguntas? | — |
| 8 min | 1. Representar um animal | Como representar um animal dentro do computador? | Dicionário (`dict`) |
| 6 min | 2. Representar vários animais | Como representar vários animais ao mesmo tempo? | Lista de dicionários |
| 6 min | 3. Percorrer a coleção | Como olhar, um por um, todos os animais da lista? | Laço `for` |
| 10 min | 4. Eliminar por um critério | Como eliminar quem não atende uma característica? | `if` + filtro |
| 8 min | 5. Combinar dois critérios | Como perguntar duas coisas ao mesmo tempo? | `and` / `or` |
| 10 min | 6. Virar função reutilizável | Como reaproveitar essa lógica pra qualquer pergunta? | Função (`def`) |
| 8 min | 7. Desafio rápido | Consegue adicionar um animal e escrever seu próprio filtro? | Prática livre |
| 6 min | 8. Fechamento e ponte | Quem escolheu as perguntas hoje? E se fosse o computador? | Conexão com 1.2/1.3 |

*Tempo total estimado: ~70 minutos. Ajuste os blocos 5 e 7 conforme o ritmo da turma — são os mais elásticos.*

---

## Detalhamento bloco a bloco

### 0. Abertura — o jogo humano (sem código)

Antes de abrir o Colab, jogue a versão humana com a turma: pense em um animal e deixe os alunos fazerem perguntas de sim/não até descobrirem qual é. Depois, inverta — um aluno pensa, a turma pergunta.

Feche esse bloco com a pergunta-ponte:

> *"Vocês acabaram de fazer, na cabeça, exatamente o que vamos ensinar o computador a fazer agora."*

### 1. Como representar um animal?

Introduza o dicionário como a forma natural de representar um conjunto de atributos nomeados.

```python
cachorro = {
    "nome": "Cachorro",
    "voa": False,
    "nada": True,
    "tem_pelos": True,
    "e_domestico": True,
    "bota_ovos": False,
}
```

Pergunte à turma: "que outro atributo vocês adicionariam?" — deixa a estrutura ser co-construída, não só ditada.

### 2. Como representar vários animais?

Generalize o dicionário único para uma lista de dicionários — o "banco de dados" da turma.

```python
animais = [
    {"nome": "Cachorro", "voa": False, "nada": True,  "tem_pelos": True,  "e_domestico": True,  "bota_ovos": False},
    {"nome": "Aguia",    "voa": True,  "nada": False, "tem_pelos": False, "e_domestico": False, "bota_ovos": True},
    {"nome": "Pato",     "voa": True,  "nada": True,  "tem_pelos": False, "e_domestico": True,  "bota_ovos": True},
    {"nome": "Gato",     "voa": False, "nada": False, "tem_pelos": True,  "e_domestico": True,  "bota_ovos": False},
]
```

### 3. Como percorrer essa coleção?

Introduza o `for` para simplesmente imprimir os nomes — o primeiro contato com iteração, sem lógica de decisão ainda.

```python
for animal in animais:
    print(animal["nome"])
```

### 4. Como eliminar quem não atende a uma característica?

Combine `for` + `if` para filtrar. Esse é o coração conceitual da aula — a eliminação progressiva.

```python
candidatos = []
for animal in animais:
    if animal["voa"] == True:
        candidatos.append(animal)

print(f"Restam {len(candidatos)} candidatos")
for c in candidatos:
    print(c["nome"])
```

**Dica de condução:** depois de cada filtro aplicado, pergunte em voz alta "quantos animais ainda restam?". Sem precisar nomear o conceito, isso planta a intuição de ganho de informação — a mesma ideia por trás das árvores de decisão que aparecem na Aula 5.

### 5. Como combinar dois critérios ao mesmo tempo?

Introduza `and`/`or` para perguntas compostas — a mesma lógica que reaparece depois em filtros de Pandas e em nós de árvore de decisão.

```python
candidatos = []
for animal in animais:
    if animal["voa"] == True and animal["e_domestico"] == True:
        candidatos.append(animal)
```

### 6. Como transformar essa lógica em uma função reutilizável?

Encapsule o padrão de filtro em uma função genérica que recebe o critério como parâmetro.

```python
def filtrar(lista, atributo, valor):
    resultado = []
    for item in lista:
        if item[atributo] == valor:
            resultado.append(item)
    return resultado

candidatos = filtrar(animais, "nada", True)
```

### 7. Desafio rápido (prática livre, não avaliativa)

Peça que cada aluno (ou dupla) adicione 3 animais novos e 1 atributo novo ao dicionário, e escreva um filtro próprio usando a função `filtrar`. 3 a 5 minutos de mão na massa, seguido de 2-3 alunos compartilhando o que fizeram.

### 8. Fechamento e ponte para o restante da disciplina

Feche conectando explicitamente com o que já foi visto nos tópicos 1.2 e 1.3:

> *"Vocês acabaram de construir, na prática, o mesmo tipo de sistema dos anos 80 que vimos na linha do tempo — regras fixas, escritas por um humano. É IA, mas sem aprendizado."*

Encerre com a pergunta que abre caminho para a Aula 2 e para os tópicos de classificação:

> *"Hoje fomos nós que escolhemos as perguntas. Como fazer para que o próprio computador aprenda quais perguntas são melhores?"*

---

## O que o aluno leva desta aula

- Informações precisam ser representadas de forma estruturada (dicionários, listas).
- Decisões podem ser tomadas a partir de atributos (`if`, `and`, `or`).
- Um conjunto de objetos pode ser filtrado progressivamente conforme novas evidências surgem (`for` + `if`, função reutilizável).
- O sistema construído hoje ainda depende do programador para decidir quais perguntas fazer — o gancho natural para Aprendizado de Máquina.

## Material de apoio (entregar após a aula)

Como a aula é toda situacional — cada conceito aparece resolvendo um problema, não em uma lista isolada — vale disponibilizar um resumo de sintaxe para quem quiser revisar sozinho depois, cobrindo: dicionário, lista, `for`, `if`, `and`/`or`, e função (`def`). Este material não deve ser meta necessária de aula, só uma referência de apoio.

---

*Documento de apoio à Aula 01 — Inteligência Artificial e Aprendizagem de Máquina · FECAP · 2026/02*
