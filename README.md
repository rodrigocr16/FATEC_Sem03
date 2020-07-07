# Projeto para a Disciplina de LAB03 do curso de Banco de Dados Turma do 1º semestre de 2020 - Fatec São José dos Campos

Este projeto foi feito com o intuito de auxiliar no treinamento de funcionários da Latecoere no processo de montagem de peças.
As partes utilizadas neste projeto foram fornecidas pelo professor da disciplina, Giuliano Araujo Bertoti.

O projeto foi feito através da ferramenta CodePen, utilizando HTML e JavaScript em conjunto com bibliotecas em A-FRAME.
O projeto em sua totalidade pode ser acessado no site através ![deste link](https://codepen.io/rodrigo_reis16/pen/PoPLYxO?editors=1010).

Este repositório armazena todos os modelos e texturas utilizados no projeto, além de informações sobre o mesmo e prévias de suas funcionalidades.
___
## Legendas dos Botões
![01_legendas](https://raw.githubusercontent.com/rodrigocr16/Projeto_Latecoere/master/01_Legendas.gif)

Ao passar o ponteiro sobre os botões, estes são destacados e exibem suas legendas.
Este efeito é atingido criando eventos do tipo "mouseenter" e "mouseleave" no objeto, conforme descrito abaixo:
```
<a-text id = "lbl1" value = "Estagio 1" geometry = "primitive:plane 0" opacity = "0.5" visible = "false"
        position = "-0.30 0.575 -1.7" rotation = "-20 0 0" scale = "0.3 0.3 0.3" align = "center">
</a-text>
<a-cylinder id = "btnEstagio1" color = "#0f2442"
            scale = "0.05 0.08 0.05" position = "-0.30 0.40 -1.675" rotation = "55 0 0"
            event-set__enter1 = "_event: mouseenter; color: #FFFFFF"
            event-set__leave1 = "_event: mouseleave; color: #0f2442"
            event-set__enter2 = "_event: mouseenter; _target: #lbl1; visible: true"
            event-set__leave2 = "_event: mouseleave; _target: #lbl1; visible: false"
            animation__click1 = "startEvents: click; property: position; to: -0.30 0.38 -1.7; dur: 200"
            animation__click2 = "startEvents: click; property: position; to: -0.30 0.40 -1.675; dur: 200; delay: 200">
</a-cylinder>
```
___
## Estagiamento da Peça
![02_estagiamento](https://raw.githubusercontent.com/rodrigocr16/Projeto_Latecoere/master/02_Estagiamento.gif)

Clicar nos botões de estagiamento tem dois resultados possíveis: Alterar para o estágio correspondente da montagem, ou exibir a peça inserida naquela etapa do processo. Ao clicar no botão pela primeira vez, muda-se o estagiamento. Ao clicar pela segunda vez consecutiva, restará apenas a peça pertinente.
O processo é feito com a função addEventListener("click"), tornando os objetos visíveis ou invisíveis, conforme exemplificado através deste trecho, em JavaScript:
```
var estP1 = document.querySelector("#estagiamentoPeca1");
var estP2 = document.querySelector("#estagiamentoPeca2");
var estP3 = document.querySelector("#estagiamentoPeca3");
var estP4 = document.querySelector("#estagiamentoPeca4");

var estado = 0;

document.querySelector("#btnEstagio2").addEventListener(
  "click", function() {
    if(estado == 2){
      estP1.object3D.visible = false;
      estP3.object3D.visible = false;
      estP4.object3D.visible = false;
      estado = 0;
    } else {
      estP1.object3D.visible = true;
      estP2.object3D.visible = true;
      estP3.object3D.visible = false;
      estP4.object3D.visible = false;
      estado = 2;
    }
  }
);
```
___
## Rotação da Peça
![03_rotacao](https://raw.githubusercontent.com/rodrigocr16/Projeto_Latecoere/master/03_Rotacao.gif)

Os botões (<) e (>) localizados abaixo dos botões de estagiamento rotacionam a peça quando clicados. Este efeito é aplicado em cada uma das partes (sejam elas visíveis ou não no momento do clique) para que as peças sempre estejam com o mesmo alinhamento, independente do estagiamento.
Isso é obtido através de um incremento ou decremento na propriedade ".rotation.y" de cada peça:
```
var rotacao = 0.3;

document.querySelector("#btnEsq").addEventListener(
  "click", function() {
    estP1.object3D.rotation.y -= rotacao; estP2.object3D.rotation.y -= rotacao;
    estP3.object3D.rotation.y -= rotacao; estP4.object3D.rotation.y -= rotacao;
  }
);
document.querySelector("#btnDir").addEventListener(
  "click", function() {
    estP1.object3D.rotation.y += rotacao; estP2.object3D.rotation.y += rotacao;
    estP3.object3D.rotation.y += rotacao; estP4.object3D.rotation.y += rotacao;
  }
);
```
___
## Modo ESTAGIAMENTO / Modo MONTAGEM
![04_modos](https://raw.githubusercontent.com/rodrigocr16/Projeto_Latecoere/master/04_Modos.gif)

Ao lado dos botões existe uma alavanca que alterna entre os modos de Estagiamento e Montagem.
Quando a alavanca é acionada ela altera o valor de uma variável de controle `estado` que auxilia nas demais funções do projeto.
```
01.    if(estado <5){
02.      haste.setAttribute('animation', 'property: rotation; dur: 200; to: 90 0 0; loop: 1');
03.      manopla.setAttribute('animation', 'property: position; dur: 200 ; to: -0.8 0.33 -1.45; loop: 1');
04.      spot.setAttribute('light', 'angle: 80');
05.      ambiente.setAttribute('light', 'intensity: 0.2');
06.      vidraca.setAttribute('position', '0 10 -2');
07.      caixavidro.setAttribute('position', '0 0.30 -1.7');
08.      estP1.object3D.visible = false; estP2.object3D.visible = false;
09.      estP3.object3D.visible = false; estP4.object3D.visible = false;
10.      estado = 5;
11.    } else {
12.      haste.setAttribute('animation', 'property: rotation; dur: 200; to: 0 0 0; loop: 1');
13.      manopla.setAttribute('animation', 'property: position; dur: 200 ; to: -0.8 0.5 -1.625; loop: 1');
14.      spot.setAttribute('light', 'angle: 25');
15.      ambiente.setAttribute('light', 'intensity: 0.03');
16.      vidraca.setAttribute('position', '0 2.5 -2');
17.      caixavidro.setAttribute('position', '0 10 0');
18.      btn1.setAttribute('color', '#0f2442'); btn2.setAttribute('color', '#0f2442');
19.      btn3.setAttribute('color', '#0f2442'); btn4.setAttribute('color', '#0f2442');
20.      reset1(); reset2(); reset3(); reset4();
21.      estado = 0;
22.    }
```
Note que a função realiza diversos procedimentos - alguns estéticos, e outros funcionais:
- Nas linhas 02-03 e 12-13 é feita a animação da manopla e da haste da alavanca, para que esta aparente ser acionada;
- Em 04-05 e 14-15 as luzes mudam de intensidade para que o usuário possa focar no que é importante em cada modo;
- Em 06-07 e 16-17 os objetos `vidraca` e `glassbox` são movidos para impedir que o usuário interaja com elementos incongruentes com o modo selecionado;
- Em 10 e 21 a variável `estado` tem seu valor alterado para auxiliar nos processos pertinentes ao modo recém habilitado.

Nas linhas 08-09 e 18-20 são executados procedimentos que preparam o ambiente para o estagiamento recém-habilitado.
08-09 preparam o ambiente para o modo de MONTAGEM, enquanto 18-20 preparam para o modo de ESTAGIAMENTO.

![07_reset](https://raw.githubusercontent.com/rodrigocr16/Projeto_Latecoere/master/07_Reset.gif)

- Em 08-09 todos os objetos de Estagiamento atualmente exibidos tornam-se invisíveis, a fim de não atrapalhar no processo de montagem.

- Em 18-19 os botões de estagiamento têm suas cores redefinidas
- Em 21 são chamadas todas as funções de `reset`, que devolvem as peças de Montagem para suas posições e rotações originais.
___
## Montagem
![05_montagem](https://raw.githubusercontent.com/rodrigocr16/Projeto_Latecoere/master/05_Montagem.gif)

Ao clicar em uma das peças no modo Montagem, caso seja a peça correta naquela etapa do processo, a peça selecionada será posicionada no centro da tela e o botão correspondente àquela etapa da montagem acenderá com uma luz verde, indicando o acerto.

No exemplo abaixo veremos o que acontece ao clicarmos na peça 02:
```
document.querySelector("#montagemPeca2").addEventListener(
  "click", function() {
    if(estado == 6){
      btn2.setAttribute('color', '#39ff14');
      this.emit('start');
      estado = 7;
    } else {
      error();
    }
  }
);
```
Como podemos observar, a primeira etapa é verificar se a variável de controle `estado` está no valor correto. O valor da variável indica o estado do processo, seja de montagem ou de estagiamento. Neste caso, `estado == 6` implica que a peça 01 do processo de montagem está no lugar certo, indicando que a próxima etapa é encaixar a peça 02.

Se o evento acima for um sucesso, ele acenderá o botão com a luz verde (hex `#39ff14`) e chamará o evento `start` definido na própria peça, como gatilho das animações que alterarão a posição e a rotação da peça:
```
<a-gltf-model id = "montagemPeca2" visible = "true" src = "#peca2"
              position = "4 -3.5 -11" rotation="0 -70 0" scale="2 2 2"
              animation__click1 = "startEvents: start; property: position; to: 0 -1.5 -7; dur: 500"
              animation__click2 = "startEvents: start; property: rotation; to: 0 -30 0; dur: 500">
</a-gltf-model>
```

Depois disso, a variável `estado` recebe o valor 7, o que indica que a peça 02 está no lugar correto e a próxima peça pode ser selecionada.

### Erro na Montagem
![06_erro](https://raw.githubusercontent.com/rodrigocr16/Projeto_Latecoere/master/05_Erros.gif)

No caso de a peça selecionada não ser a peça correta para a etapa seguinte da montagem - ou seja, se o valor da variável `estado` não for o valor exigido por aquela peça - será chamada uma função de erro `error()`:
```
function error(){
  if(estado == 5){ btn1.setAttribute('color', '#ff0000'); }
  if(estado == 6){ btn2.setAttribute('color', '#ff0000'); }
  if(estado == 7){ btn3.setAttribute('color', '#ff0000'); }
}
```

Esta função simplesmente altera a cor do botão correspondente ao estágio pendente a fim de simular a emissão de uma luz vermelha brilhante. Embora seja um efeito simples, é um indicativo claro de que o usuário escolheu a peça errada para aquela etapa da montagem.
