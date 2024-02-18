# Comparação de strings no processamento de dados
<p align="center"> 
<a href="https://www.r-project.org" target="_blank" rel="noreferrer" title="Esse documento possui códigos em R"> <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/r/r-original.svg" alt="R" width="40" height="40"/> </a>
 <a href="https://www.python.org" target="_blank" rel="noreferrer" title="Esse documento possui códigos em Python">
    <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/python/python-original.svg" alt="python" width="40" height="40"/>
</a>
</p>

Um dos pontos mais interessantes da ciência de dados é que a informação pode vir de formas variadas, seja por textos, cartas, PDFs, fotos… De forma resumida, a análise de dados via bases numéricas é algo crucial, porém a base não numérica pode conter muita relevância e por vezes ser a fonte primordial.

Nesse artigo você vai conferir a necessidade de comprar strings e casos reais onde a ciência de dados pode atuar para gerar ganho em tomadas de decisões cruciais, mas antes de mais nada:

# Porque comparar de Strings?

Para fomentar a importância dessa análise eu vou citar dois exemplos:

No primeiro caso vamos supor que você trabalha numa grande empresa de dados com várias tabelas distintas criadas por pessoas em diferentes níveis de conhecimento sobre dados. Aqui você precisa identificar o fluxo de valores de uma empresa, nem todos os bancos possuem a melhor chave primária e a melhor forma de identificar o faturamento é validando o nome da empresa. Como o mundo real é uma caixinha de surpresas, o nome da empresa na tabela de cadastro (muitas vezes chamada de dimensão) é algo como *Sousa de Oliveira Distribuidora de Alimentos*. A tabela contendo as movimentações (comumente chamada de fato) possui dados da mesma empresa, mas seu nome aparece como *Sousa de Oliveira Distr. de Alimentos*. 

No segundo caso, você trabalha na própria *Sousa de Oliveira Distribuidora de Alimentos* e está realizando o contrato de novos clientes, dentre eles a *Araújo-Guimarães Panificadora*. Pra verificar a idoneidade do cliente, você busca os dados de movimentações antes de entrar na sua empresa. Porém, em outras distribuidoras de alimentos, o cliente só tinha registros com um nome de *Araujo de Guimarães Panificadora*. Os dados parecem realmente ser condizentes com o novo cliente, mas não existem registros na receita com o nome novo.

# A distância de Jaro-Winkler

# Distância de Jaro-Winkler

A distância de Jaro-Winkler, proposta por William E. Winkler em 1990 como uma extensão da distância de Jaro introduzida por Matthew A. Jaro em 1989, fornece uma medida mais robusta de similaridade entre strings. Essa métrica é comumente utilizada em tarefas de comparação de strings, como deduplicação de dados, verificação ortográfica e reconhecimento de padrões, especialmente em situações onde há erros tipográficos ou variações ortográficas.

## Formulação Matemática

A fórmula para calcular a distância de Jaro-Winkler entre duas strings \( s_1 \) e \( s_2 \) é dada por:

\[
\text{Jaro-Winkler}(s_1, s_2) = J(s_1, s_2) + P \cdot L \cdot (1 - J(s_1, s_2))
\]

onde:
- \( J(s_1, s_2) \) é a distância de Jaro entre as strings \( s_1 \) e \( s_2 \).
- \( P \) é um fator de ajuste, geralmente configurado entre 0 e 0.25.
- \( L \) é o comprimento do prefixo comum mais longo entre as duas strings, limitado a um máximo de 4.

## Propriedades

- **Simetria**: A distância de Jaro-Winkler entre \( s_1 \) e \( s_2 \) é igual à distância entre \( s_2 \) e \( s_1 \).
- **Valores**: A distância de Jaro-Winkler varia de 0 (strings totalmente diferentes) a 1 (strings idênticas).
- **Sensibilidade ao Prefixo**: A métrica dá peso extra aos caracteres idênticos no início das strings, o que a torna útil para comparar strings com variações ortográficas ou pequenas diferenças.

# Outras métricas interessantes - Fala GPT!!!
Pedi ajuda ao meu querido amigo GPT pra me auxiliar em tópicos extras, o que será que ele considera como alternativas para medir a semelhança entre strings?

<p align="center">      
  <a href="https://openai.com/chatgpt" target="_blank" rel="noreferrer" title="Este Conteúdo foi gerado por IA"> <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/4/4d/OpenAI_Logo.svg/512px-OpenAI_Logo.svg.png" alt="ChatGPT" width="100" height="30"/> 
  </p>

__Distância de Levenshtein (ou edição):__

Imagine que você está comparando duas palavras e quer saber quantas mudanças você precisa fazer em uma para que ela se torne igual à outra. Essas mudanças podem ser adicionar, remover ou trocar letras. Quanto menor o número de mudanças, mais parecidas as palavras são.

__Distância de Hamming:__

Vamos dizer que você tem duas sequências de caracteres com o mesmo tamanho. A distância de Hamming é basicamente contar quantos caracteres são diferentes em posições correspondentes nas duas sequências.

__Distância de Damerau-Levenshtein:__

É como a distância de Levenshtein, mas também leva em conta o fato de que algumas vezes as letras podem estar fora de ordem ou trocadas. Então, se você trocar duas letras adjacentes em uma palavra, isso conta como uma única mudança.

__Coeficiente de similaridade de Jaccard:__

Imagine que você tem dois grupos de palavras. O coeficiente de Jaccard mede a similaridade entre esses grupos, olhando para a quantidade de palavras que eles têm em comum e dividindo pelo total de palavras que eles têm juntos.

## Em Python

```python
import textdistance

def calcular_distancia_jaro_winkler(string1, string2):
    distancia = textdistance.jaro_winkler(string1, string2)
    return distancia

# Exemplo de uso
string1 = "gato"
string2 = "cão"
distancia = calcular_distancia_jaro_winkler(string1, string2)
print("Distância de Jaro-Winkler entre '{}' e '{}': {}".format(string1, string2, distancia))
```

## Em R

``` R
# Instalar e carregar o pacote stringdist se ainda não estiver instalado
if (!requireNamespace("stringdist", quietly = TRUE)) {
  install.packages("stringdist")
}
library(stringdist)

# Função para calcular a distância de Jaro-Winkler
calcular_distancia_jaro_winkler <- function(string1, string2) {
  distancia <- stringdist(string1, string2, method = "jw")
  return(distancia)
}

# Exemplo de uso
string1 <- "cachorro"
string2 <- "carro"
distancia <- calcular_distancia_jaro_winkler(string1, string2)
print(paste("A distância de Jaro-Winkler entre", string1, "e", string2, "é:", distancia))

```

# E o algoritmo de análise exploratória de dados?

Se você veio aqui pelo algoritmo que desenvolvi [neste](https://github.com/jose-de-oliveira/algoritmo_AED)
 repositório, já deve ter entendido bem o contexto do primeiro problema e como é possível incorporar a comparação de strings em cenários pouco prováveis mas bastante relevantes da análise de dados!
