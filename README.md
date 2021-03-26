## Core Java Character

Este módulo contém artigos sobre Java Character Class

# 1. Visão Geral
Neste tutorial, começaremos passando rapidamente por alguns tipos de categorias gerais para cada ponto de código Unicode definido ou intervalo de caracteres para entender a diferença entre letras e caracteres alfabéticos.

Além disso, veremos os métodos isAlphabetic() e isLetter() da classe Character em Java. Finalmente, vamos cobrir as semelhanças e distinções entre esses métodos.

# 2. Tipos de categorias gerais de caracteres Unicode
O Unicode Character Set (UCS) contém 1.114.112 pontos de código: U + 0000 — U + 10FFFF. Caracteres e intervalos de pontos de código são agrupados por categorias.

A classe Character fornece duas versões sobrecarregadas do método getType() que retorna um valor que indica o tipo de categoria geral do personagem.

Vejamos a assinatura do primeiro método:

```
public static int getType(char ch)
```

Este método não pode lidar com caracteres suplementares. Para lidar com todos os caracteres Unicode, incluindo caracteres suplementares, a classe Character do Java fornece um método getType sobrecarregado que possui a seguinte assinatura:

```
public static int getType(int codePoint)
```

A seguir, vamos começar a examinar alguns tipos de categorias gerais.

### 2.1. LETRA MAIÚSCULA
O tipo de categoria geral UPPERCASE_LETTER representa letras maiúsculas.

Quando chamamos o método Character # getType em uma letra maiúscula, por exemplo, 'U', o método retorna o valor 1, que é equivalente ao valor UPPERCASE_LETTER enum:

```
assertEquals(Character.UPPERCASE_LETTER, Character.getType('U'));
```

### 2.2. LETRA MINÚSCULA

O tipo de categoria geral LOWERCASE_LETTER está associado a letras minúsculas.

Ao chamar o método Character # getType em uma letra minúscula, por exemplo, 'u', o método retornará o valor 2, que é o mesmo que o valor enum de LOWERCASE_LETTER:

```
assertEquals(Character.LOWERCASE_LETTER, Character.getType('u'));
```

### 2.3. TITLECASE_LETTER
Em seguida, a categoria geral TITLECASE_LETTER representa os caracteres iniciais em maiúsculas.

Alguns caracteres parecem pares de letras latinas. Quando chamamos o método Character # getType em tais caracteres Unicode, isso retornará o valor 3, que é igual ao valor de enum TITLECASE_LETTER:

```
assertEquals(Character.TITLECASE_LETTER, Character.getType('\u01f2'));
```

Aqui, o caractere Unicode '\u01f2' representa a letra latina maiúscula 'D' seguida por um pequeno 'Z' com um caron.

### 2.4. MODIFIER_LETTER
Uma letra modificadora, no padrão Unicode, é “uma letra ou símbolo tipicamente escrito ao lado de outra letra que ele modifica de alguma forma”.

O tipo de categoria geral MODIFIER_LETTER representa essas letras modificadoras.

Por exemplo, a letra modificadora H minúsculo, 'ʰ', quando passada para o método Character # getType retorna o valor de 4, que é o mesmo que o valor enum de MODIFIER_LETTER:

```
assertEquals(Character.MODIFIER_LETTER, Character.getType('\u02b0'));
```

O caractere Unicode '\u020b' representa a letra modificadora H.

### 2.5. OTHER_LETTER

O tipo de categoria geral OTHER_LETTER representa um ideograma ou uma letra em um alfabeto unicase. Um ideograma é um símbolo gráfico que representa uma ideia ou um conceito, independente de qualquer linguagem específica.

Um alfabeto unicase tem apenas uma caixa para suas letras. Por exemplo, o hebraico é um sistema de escrita unicase.

Vejamos um exemplo de uma letra hebraica Alef, 'א', quando a passamos para o método Character # getType, ela retorna o valor de 5, que é igual ao valor enum de OTHER_LETTER:

```
assertEquals(Character.OTHER_LETTER, Character.getType('\u05d0'));
```

O caractere Unicode '\u05d0' representa a letra hebraica Alef.

### 2.6. LETTER_NUMBER
Finalmente, a categoria LETTER_NUMBER está associada a numerais compostos de letras ou símbolos semelhantes a letras.

Por exemplo, os algarismos romanos vêm na categoria geral LETTER_NUMBER. Quando chamamos o método Character # getType com numeral romano cinco, 'Ⅴ ', ele retorna o valor 10, que é igual ao valor enum LETTER_NUMBER:

```
assertEquals(Character.LETTER_NUMBER, Character.getType('\u2164'));
```

O caractere Unicode '\u2164' representa o numeral romano cinco.

A seguir, vamos examinar o método Character # isAlphabetic.

# 3. Character # isAlphabetic
Primeiro, vamos dar uma olhada na assinatura do método isAlphabetic:

```
public static boolean isAlphabetic(int codePoint)
```

Isso leva o ponto de código Unicode como o parâmetro de entrada e retorna verdadeiro se o ponto de código Unicode especificado for alfabético e falso caso contrário.

Um caractere é alfabético se seu tipo de categoria geral for qualquer um dos seguintes:

- LETRA MAIÚSCULA;
- LETRA MINÚSCULA;
- TITLECASE_LETTER;
- MODIFIER_LETTER;
- OTHER_LETTER;
- LETTER_NUMBER.

Além disso, um caractere é alfabético se tiver a propriedade contributiva Other_Alphabetic conforme definido pelo padrão Unicode.

Vejamos alguns exemplos de caracteres que são alfabetos:

```
assertTrue(Character.isAlphabetic('A'));
assertTrue(Character.isAlphabetic('\u01f2'));
```

Nos exemplos acima, passamos UPPERCASE_LETTER 'A' e TITLECASE_LETTER '\u01f2' que representa a letra latina maiúscula 'D' seguida por um pequeno 'Z' com um caron para o método isAlphabetic e retorna true.

# 4. Character # isLetter
A classe Character do Java fornece o método isLetter() para determinar se um caractere especificado é uma letra. Vejamos a assinatura do método:

```
public static boolean isLetter(char ch)
```

Leva um caractere como parâmetro de entrada e retorna verdadeiro se o caractere especificado for uma letra e falso caso contrário.

Um caractere é considerado uma letra se seu tipo de categoria geral, fornecido pelo método Character # getType, for qualquer um dos seguintes:

- LETRA MAIÚSCULA;
- LETRA MINÚSCULA;
- TITLECASE_LETTER;
- MODIFIER_LETTER;
- OTHER_LETTER.

No entanto, esse método não pode lidar com caracteres suplementares. Para lidar com todos os caracteres Unicode, incluindo caracteres suplementares, a classe Character do Java fornece uma versão sobrecarregada do método isLetter():

```
public static boolean isLetter(int codePoint)
```

Este método pode manipular todos os caracteres Unicode, pois leva um ponto de código Unicode como parâmetro de entrada. Além disso, retorna verdadeiro se o ponto de código Unicode especificado for uma letra, conforme definido anteriormente.

Vejamos alguns exemplos de caracteres que são letras:

```
assertTrue(Character.isAlphabetic('a'));
assertTrue(Character.isAlphabetic('\u02b0'));
```

Nos exemplos acima, inserimos LOWERCASE_LETTER 'a' e MODIFIER_LETTER '\u02b0' que representa a letra modificadora H pequeno para o método isLetter e retorna verdadeiro.

# 5. Compare e contraste
Finalmente, podemos ver que todas as letras são caracteres alfabéticos, mas nem todos os caracteres alfabéticos são letras.

Em outras palavras, o método isAlphabetic retorna true se um caractere for uma letra ou tiver a categoria geral LETTER_NUMBER. Além disso, também retorna verdadeiro se o caractere possuir a propriedade Other_Alphabetic definida pelo padrão Unicode.

Primeiro, vamos ver um exemplo de um caractere que é uma letra e também um alfabeto - caractere 'a':

```
assertTrue(Character.isLetter('a')); 
assertTrue(Character.isAlphabetic('a'));
```

O caractere 'a', quando passado para os métodos isLetter() e isAlphabetic() como um parâmetro de entrada, retorna verdadeiro.

A seguir, vamos ver um exemplo de um caractere que é um alfabeto, mas não uma letra. Nesse caso, usaremos o caractere Unicode '\u2164', que representa o numeral romano cinco:

```
assertFalse(Character.isLetter('\u2164'));
assertTrue(Character.isAlphabetic('\u2164'));
```

O caractere Unicode '\u2164' quando passado para o método isLetter() retorna falso. Por outro lado, quando passado para o método isAlphabetic(), retorna verdadeiro.

Certamente, para o idioma inglês, a distinção não faz diferença. Uma vez que todas as letras do idioma Inglês vêm sob a categoria de alfabetos. Por outro lado, alguns caracteres em outros idiomas podem ter uma distinção.

# 6. Conclusão
Neste artigo, aprendemos sobre as diferentes categorias gerais do ponto de código Unicode. Além disso, cobrimos as semelhanças e diferenças entre os métodos isAlphabetic() e isLetter().