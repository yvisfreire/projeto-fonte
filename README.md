# Projeto - Fonte de Tensão Ajustável
Este projeto, desenvolvido para a disciplina SSC0180 - Eletrônica para Computação, consiste numa fonte de tensão ajustável entre 3V a 12V com capacidade para 100mA.

## Componentes do Circuito
| Nome | Especificação | Justificativa | Preço |
| --- | --- | --- | --- |
| Fonte de Alimentação A/C | Entrada de 127V | Prover energia para o circuito | - |
| Transformador | Transformador Trafo 12V+12V 500mA | Transformar a tensão de entrada em 24V | R$32,86 |
| Ponte de Diodos | 10A/1000V | Faz com que a corrente percorra todo o circuito uniformemente no mesmo sentido | R$3,67 |
| Capacitor | Capacitor Eletrolítico 470uF / 35V | Filtragem, previne a oscilação da carga | R$0,77 |
| Transistor | Transistor NPN 2N3904 | Regula a tensão no circuito | R$0,36 |
| Diodo Zener | Diodo Zener BZX55C [13V/0.5W] | Corta a tensão de saída do capacitor abaixo da oscilação (ripple) | R$0,09 |
| Resistor (1) | Resistor de 2.7K | Responsável por limitar a corrente que flui ao Diodo Zener garantindo a segurança do mesmo | R$0,06 |
| Resistor (2) | Resistor de 2.2K | Responsável por limitar a resistência do potenciômetro de forma que a tensão final seja no mínimo aproximadamente 3V | R$0,06 |
| Potenciômetro | Potenciômetro Linear de 5KΩ | | Ajusta a tensão de saída | R$1,99 |

Todos os valores foram retirados da loja [Báu da Eletrônica](https://www.baudaeletronica.com.br/)

## Circuito Falstad

Com base nos componentes descritos acima, construímos o seguinte circuito na ferramenta Falstad:

<div align="center">
<p float="left">
  <img src="/circuito-falstad.png" width="900" />
</p>
</div>

[Link do Falstad para a simulação](https://tinyurl.com/circuito-falstad).

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
- Davi Fagundes Ferreira da Silva - 
- Henrico Lazuroz Moura de Almeida - 12543502
- Pedro Guilherme dos Reis Teixeira - 
- Yvis Freire Silva Santos - 
