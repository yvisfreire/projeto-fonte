# Projeto - Fonte de Tensão Ajustável
Este projeto, desenvolvido para a disciplina SSC0180 - Eletrônica para Computação, consiste numa fonte de tensão ajustável entre 3V a 12V com capacidade para 100mA.

## Componentes do Circuito
| Nome | Especificação | Justificativa | Preço |
| --- | --- | --- | --- |
| Fonte de Alimentação A/C | Entrada de 127V | Prover energia para o circuito | - |
| Transformador | Transformador Trafo 12V+12V 500mA | Transformar a tensão de entrada em 24V | R$32,86 |
| Ponte de Diodos | 10A/1000V | Faz com que a corrente percorra todo o circuito uniformemente no mesmo sentido | R$3,67 |
| Capacitor | Capacitor Eletrolítico 270uF / 35V | Filtragem, previne a oscilação da carga | R$1,56 |
| Transistor | Transistor NPN 2N3904 | Regula a tensão no circuito | R$0,36 |
| Diodo Zener | Diodo Zener BZX55C [13V/0.5W] | Corta a tensão de saída do capacitor abaixo da oscilação (ripple) | R$0,09 |
| Resistor (1) | Resistor de 2.7K | Responsável por limitar a corrente que flui ao Diodo Zener garantindo a segurança do mesmo | R$0,06 |
| Resistor (2) | Resistor de 2.2K | Responsável por limitar a resistência do potenciômetro de forma que a tensão final seja no mínimo aproximadamente 3V | R$0,06 |
| Potenciômetro | Potenciômetro Linear de 5KΩ | Ajusta a tensão de saída | R$1,99 |

Todos os valores foram retirados da loja [Báu da Eletrônica](https://www.baudaeletronica.com.br/)

## Transformação

Usamos um transformador de 127V AC para 24V AC, com o intuito de operar sobre uma tensão mais baixa, que fica adequada aos componentes da fonte. A corrente secundária de 24V é induzida pela oscilação da corrente primária de 127V. Com isso, obtemos um intervalo de oscilação de 127V a -127V para 24V a -24V.

Inicialmente, a tensão de pico da entrada equivale a 127V x √2 = 180V 

Foi escolhida a conversão de 127V para 24V com a mentalidade de que peças feitas para interagir com uma tensão de 24 volts são mais baratas e de mais fácil acessibilidade.

A fórmula feita para definir a razão de conversão transformador foi:

Ui / Uf = Ni / Nf

Sendo Ui e Uf respectivamente as tensões inicial e final, e Ni/Nf as suas razões.

Então: 127 / 24 = 1 / Nf 

<=> 

Nf = 0,1889

## Retificação

Nessa etapa, o objetivo é converter de uma corrente alternada de -24V a 24V para um corrente contínua que opere na faixa dos 24V. 

Para isso, usaremos uma ponte retificadora de diodos, cuja função é direcionar a corrente em apenas um lado. Isso ocorre por conta da própria característica dos diodos,
que permitem a passagem da correntes em apenas um sentido. Assim, os diodos são acionados sempre em pares. 

Por conseguinte, temos um corrente contínua, porém instável.

Cada Diodo consome 0,7V da tensão de entrada, logo:

Tensão de Pico (Vc) = 24V x √2 - 1,4V = 32,44V 

O esquema a baixo nos ajuda a compreender o papel da ponte retificadora de onda completa:

<div align="center">
<p float="left">
  <img src="/onda-completa.png" width="600" />
</p>
</div>

[Fonte](https://pt.m.wikipedia.org/wiki/Ficheiro:Rectified_waves.png)

## Filtragem

Como dito anteriormente, a corrente após a retificação é contínua, porém instável. Isso pode ser verificado pela instabilidade da tensão do circuito no falstad.

Para resolver isso, utilizamos um capacitor em paralelo com a saída, com o objetivo de reduzir essa oscilação a uma margem aceitável de operação.

Com a passagem da corrente, o capacitor carrega sua carga enquanto a tensão diminui. Em uma determinada tensão, o capacitor descarrega sua carga armazenada no circuito, fazendo com que a tensão retome ao patamar inicial. 

Para definir a capacitância ideal, precisamos definir um Ripple. No nosso caso, definimos um Ripple de, no máximo, 10%.
Logo:

Ripple = 10% x Vc = 0,1 x 32,44 = 3,24V

Com isso, definimos a capacitância através da seguinte fórmula:

C = I / f x Ripple

, onde:

I = corrente operando sobre o capacitor. No nosso caso, a corrente possui o valor em torno de 104mA.

f = frequência. Como estamos trabalhando com onda completa, a frequência utilizada será o dobro da frequência de entrada:
 
f = 60Hz x 2 = 120Hz

Logo,

C = 104mA . 10⁻3 / 120Hz . 3,24V = 0,268 . 10⁻3 = 268uF

Adotamos o capacitor de valor comercial mais próximo (270uF)

## Regulação

Agora, a parte de regulação funciona por conta de um diodo zener
que serve para cortar o ripple completamente, trabalhando com a tensão de saída do capacitor abaixo da oscilação do ripple. 

### Zener

O zener tem dois estados, ligado e desligado, quando ele está ligado é como um curto circuito, que corta a oscilação (ripple). Quando desligado, ele não serve de muito.

O diodo zener serve como um regulador de tensão porque a tensão resultante advém da subtração entre a tensão do capacitor e a tensão zener, o que corta o ripple de fato.

Importante ter esse resistor em cima do diodo zener para diminuir a corrente que passa por ele, senão ele queima. Para determinar essa resistência, utilizamos a seguinte fórmula:

R1 = (Vs - Vz) / Imax

, onde:

Vs = tensão do circuito. 24V de entrada - 1,4V dos diodos.
Vz = tensão zener. No nosso caso, escolhemos um zener que opera sobre 13V.
Imax = corrente máxima

Logo,

R1 = (22.6V - 13V) / 3mA

R1 = 2.7KΩ

A tensão da bateria sempre tem que estar maior que a zener para que ele esteja ligado.

### Potenciômetro

O potenciômetro funciona para, de fato, poder-se mudar a tensão resultante do circuito de 3v para 12v. 

O resistor abaixo dele permite que o mínimo chegue a 3v, senão ele estaria ligado no ground e, portanto, seria 0V a tensão mínima. Para determinar essa resistência, utilizamos a seguinte fórmula:

Vtransistor + Ripple / R2 + Rmin = Vzener / R2 + Rmax

4V / R2 + 25Ω = 13V / R2 + 4975Ω

R2 = 2.2KΩ

### Transistor

O transistor npn serve, também, para regular a tensão, embora transistores assim sejam utilizados para regular a corrente de uma dada parte do circuito. 

O transistor consome 0.7V da tensão, portanto o valor se aproxima bastante de 12v.

## Circuito Falstad

Com base nos componentes descritos acima, construímos o seguinte circuito na ferramenta Falstad:

<div align="center">
<p float="left">
  <img src="/circuito-falstad.jpg" width="900" />
</p>
</div>

[Link do Falstad para a simulação](https://tinyurl.com/ydsbskuw).

[Link para vídeo explicativo do circuito](https://drive.google.com/file/d/1KsUaTKmFKiEkLXKAnJEo1fPohyWpZy89/view?usp=sharing).

## Circuito EAGLE

<div align="center">
<p float="left">
  <img src="/circuito-eager.jpg" width="900" />
</p>
</div>

## Esquemático EAGLE

<div align="center">
<p float="left">
  <img src="/esquematico-eager.jpg" width="900" />
</p>
</div>

## Alunos:
- Davi Fagundes Ferreira da Silva - nº USP: 12544013
- Henrico Lazuroz Moura de Almeida - nº USP: 12543502
- Pedro Guilherme dos Reis Teixeira - nº USP: 12542477
- Yvis Freire Silva Santos - nº USP: 12608793
