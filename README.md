# Explorando Práticas de Teste

Neste exercício, vamos explorar práticas de teste em sistemas reais utilizando a ferramenta [TestMiner](https://andrehora.github.io/testminer).

O TestMiner permite visualizar e analisar testes de software em repositórios do GitHub, fornecendo dados sobre como os projetos organizam seus testes, como eles evoluem entre versões e quais bibliotecas de teste são utilizadas.
Explore a ferramenta antes de começar para se familiarizar com seu funcionamento.

---

## Passo 1: Selecionar um repositório

Escolha um repositório real que possua testes escritos na linguagem de sua preferência.
Abaixo estão alguns links para ajudá-lo a encontrar projetos interessantes:

- **Python:** https://github.com/topics/python?l=python
- **JavaScript:** https://github.com/topics/javascript?l=javascript
- **TypeScript:** https://github.com/topics/typescript?l=typescript
- **Java:** https://github.com/topics/java?l=java

## Passo 2: Explorar o repositório selecionado

Busque o repositório escolhido no [TestMiner](https://andrehora.github.io/testminer) e analise os dados de teste gerados pela ferramenta.

## Passo 3: Explicar uma prática de teste

Com base nos dados obtidos, selecione uma prática ou dado de teste relevante e explique-o com suas próprias palavras.

---

## Instruções de entrega

1. Faça um `fork` deste repositório (saiba mais sobre forks [aqui](https://docs.github.com/pt/pull-requests/collaborating-with-pull-requests/working-with-forks/fork-a-repo)).
2. Responda às questões abaixo diretamente neste arquivo `README.md` do seu fork. Pode adicionar imagens para enriquecer sua explicação.
3. No Moodle, submeta apenas a URL do seu fork.

---

## Respostas

**1. Repositório selecionado:** `https://github.com/psf/requests`

**2. Explicação:**

O repositório analisado foi o **requests**, uma das bibliotecas Python mais populares, usada para fazer requisições HTTP. Ao explorar os dados de teste no TestMiner, a prática que mais se destacou foi o uso de testes parametrizados com o decorator `@pytest.mark.parametrize` do pytest.

Testes parametrizados permitem executar a mesma função de teste com diferentes entradas sem duplicar código. Em vez de escrever um teste separado para cada cenário, define-se uma lista de parâmetros e o pytest cuida de executar o teste para cada combinação automaticamente.

```python
@pytest.mark.parametrize(
    "exception, url",
    (
        (MissingSchema, "hiwpefhipowhefopw"),
        (InvalidSchema, "localhost:3128"),
        (InvalidSchema, "localhost.localdomain:3128/"),
        (InvalidSchema, "10.122.1.1:3128/"),
        (InvalidURL, "http://"),
        (InvalidURL, "http://*"),
        (InvalidURL, "http://."),
    ),
)
def test_invalid_url(self, exception, url):
    with pytest.raises(exception):
        requests.get(url)
```

Nesse exemplo, `test_invalid_url` é executado 7 vezes, cada vez com uma URL inválida diferente e a exceção esperada. Sem parametrização, seriam necessárias 7 funções quase idênticas. A prática aparece por todo o repositório, cobrindo validação de URLs, métodos HTTP, headers e timeouts, o que mostra como ela ajuda a manter a suíte de testes abrangente sem aumentar a complexidade do código.
