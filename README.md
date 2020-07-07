# Projeto para a Disciplina de LAB03 do curso de Banco de Dados Turma do 1º semestre de 2020 - Fatec São José dos Campos

Este projeto foi feito com o intuito de auxiliar no treinamento de funcionários da Latecoere no processo de montagem de peças.
As partes utilizadas neste projeto foram fornecidas pelo professor da disciplina, Giuliano Araujo Bertoti.

Este repositório armazena todos os modelos e texturas utilizados no projeto, além de informações sobre o mesmo e prévias de suas funcionalidades.
___
# Legendas dos Botões
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
# Estagiamento da Peça
![02_estagiamento](https://raw.githubusercontent.com/rodrigocr16/Projeto_Latecoere/master/02_Estagiamento.gif)

Clicar nos botões de estagiamento tem dois resultados possíveis: Alterar para o estágio correspondente da montagem, ou exibir a peça inserida naquela etapa do processo. Ao clicar no botão pela primeira vez, muda-se o estagiamento. Ao clicar pela segunda vez consecutiva, restará apenas a peça pertinente.
O processo é exemplificado através deste trecho, em JavaScript:
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
</div>
