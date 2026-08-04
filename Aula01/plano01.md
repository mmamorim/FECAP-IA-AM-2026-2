# Aula 1 — Inteligência Artificial e Aprendizado de Máquina

## Preparação do Ambiente e Revisão de Python

---

# Objetivo da Aula

Embora esta seja apresentada como uma aula de revisão de Python, seu verdadeiro objetivo é preparar os estudantes para o restante da disciplina.

Ao invés de revisar comandos isolados da linguagem, toda a aula será construída em torno de um único problema:

> **Como ensinar um computador a descobrir um animal fazendo perguntas?**

Python será apenas a ferramenta utilizada para resolver esse problema.

Ao longo do semestre, esse mesmo problema será reutilizado para introduzir Pandas, NumPy, algoritmos de classificação, árvores de decisão e outros conceitos de Machine Learning.

---

# Parte 1 — O problema

## Pergunta

> Pense em um animal.

(Não diga qual é.)

Pergunta para a turma:

> Como um computador poderia descobrir qual animal você pensou?

Após ouvir algumas respostas, concluir:

> Antes de aprender Inteligência Artificial, precisamos aprender a representar informações.

---

# Parte 2 — Google Colab

## Objetivo

Apresentar rapidamente o ambiente que será utilizado durante todo o semestre.

Mostrar apenas:

- criar notebook;
- executar células;
- criar células Markdown;
- salvar no Google Drive;
- diferença entre texto e código.

---

# Notebook

## Bloco 1 — Primeiro contato

```python
print("Bem-vindos à disciplina de IA e Aprendizado de Máquina!")
```

---

## Bloco 2 — Nosso problema

```python
print("Como um computador poderia descobrir um animal?")
```

Explicar que um computador não conhece animais.

Ele conhece apenas dados.

---

# Como representar um animal?

## Bloco 3

```python
cachorro = {
    "nome": "Cachorro",
    "voa": False,
    "nada": False,
    "pelos": True,
    "domestico": True
}

cachorro
```

Explicar:

- dicionário;
- chave;
- valor;
- atributos.

---

# Mais animais

## Bloco 4

```python
gato = {
    "nome": "Gato",
    "voa": False,
    "nada": False,
    "pelos": True,
    "domestico": True
}

aguia = {
    "nome": "Águia",
    "voa": True,
    "nada": False,
    "pelos": False,
    "domestico": False
}

pato = {
    "nome": "Pato",
    "voa": True,
    "nada": True,
    "pelos": False,
    "domestico": True
}
```

---

# Como representar vários animais?

## Bloco 5

```python
animais = [
    cachorro,
    gato,
    aguia,
    pato
]

animais
```

Introduzir listas.

---

# Como percorrer todos?

## Bloco 6

```python
for animal in animais:
    print(animal["nome"])
```

Revisar:

- for
- identação
- acesso ao dicionário

---

# Primeira pergunta

## O animal voa?

## Bloco 7

```python
for animal in animais:
    if animal["voa"]:
        print(animal["nome"])
```

Resultado esperado:

```
Águia
Pato
```

Explicar:

> Estamos eliminando candidatos.

---

# Segunda pergunta

## O animal nada?

## Bloco 8

```python
for animal in animais:
    if animal["nada"]:
        print(animal["nome"])
```

Resultado esperado:

```
Pato
```

---

# Observação importante

Perguntar para a turma:

> O que vocês perceberam?

Resposta esperada:

> O código é praticamente igual.

Apenas muda o atributo.

---

# Vamos reutilizar código

## Bloco 9

```python
def filtrar(animais, atributo):

    for animal in animais:

        if animal[atributo]:

            print(animal["nome"])
```

Explicar:

- parâmetros;
- reutilização;
- abstração.

---

# Testando

## Bloco 10

```python
filtrar(animais, "voa")
```

---

## Bloco 11

```python
filtrar(animais, "nada")
```

---

## Bloco 12

```python
filtrar(animais, "domestico")
```

---

# Podemos melhorar?

Perguntar:

> Como guardar o resultado ao invés de apenas imprimir?

---

## Bloco 13

```python
def filtrar(animais, atributo):

    resultado = []

    for animal in animais:

        if animal[atributo]:

            resultado.append(animal)

    return resultado
```

Explicar:

- listas;
- append();
- return.

---

## Bloco 14

```python
voadores = filtrar(animais, "voa")

voadores
```

---

## Bloco 15

```python
domesticos = filtrar(voadores, "domestico")

domesticos
```

Resultado esperado:

```python
[
    {
        "nome":"Pato",
        ...
    }
]
```

Mostrar que agora conseguimos combinar filtros.

---

# Exercício

Adicionar um novo animal.

Exemplo:

```python
tubarao = {
    "nome":"Tubarão",
    "voa":False,
    "nada":True,
    "pelos":False,
    "domestico":False
}

animais.append(tubarao)
```

Depois responder:

- Quais animais voam?
- Quais nadam?
- Quais são domésticos?

---

# Encerramento

Mostrar que hoje fomos nós que decidimos quais perguntas fazer.

Perguntar:

> Será que o computador consegue aprender sozinho quais perguntas são melhores?

Essa será exatamente a missão das próximas aulas.

---

# Conclusão

Nesta aula revisamos naturalmente:

- execução de código;
- Google Colab;
- variáveis;
- valores booleanos;
- dicionários;
- listas;
- estruturas de repetição (`for`);
- estruturas condicionais (`if`);
- funções;
- parâmetros;
- retorno de funções;
- manipulação de listas.

Sem apresentar esses tópicos como conteúdos isolados.

Todos surgiram como ferramentas necessárias para resolver um único problema: ensinar um computador a descobrir um animal.