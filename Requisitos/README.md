# Projeto de controle de três elevadores

## Aluno: Alexandre Pedro Santana

### Levantamento de Requisitos

### Glossário

#### [G-010] Andar
É o pavimento do edifício onde ou o Elevador está, ou a Chamada é feita.

#### [G-020] Botão Externo
Botão de Chamada de Elevador existente em cada Andar.

#### [G-030] Botão Interno
Botão de seleção do Andar ao qual o Usuário deseja ir, existente dentro do Elevador.

#### [G-040] Chamada
Solicitação feita por um Usuário sob pressionamento de Botão Interno (Chamada Interna) ou Externo (Chamada Externa).

#### [G-050] Direção
É a direção do Elevador Livre em relação à Chamada.

* Se os Elevadores estão todos no Andar 0 e a Chamada for no Andar 2, então a Direção é Subir.
* Se os Elevadores estão todos no Andar 2 e a Chamada for no Andar 0, então a Direção é Descer.

#### [G-060] Elevador
Qualquer um dos três veículos de transporte de passageiros em questão.

#### [G-070] Livre
Elevador sem atendimento de Chamadas por Botão Interno.

#### [G-080] Número
Identificação do Elevador: 1 (Esquerdo), 2 (Central) ou 3 (Direito).

#### [G-090] Porta Externa
Porta de fechamento externo do Elevador, existente em cada Andar. Pode ser aberta ou fechada.
É trancada após o fechamento da Porta Interna e destrancada após a abertura da Porta Interna.

#### [G-100] Porta Interna
Porta de fechamento interno do Elevador. Pode ser aberta ou fechada.

#### [G-110] Preferência
É o Elevador que atende preferencialmente a uma Chamada Externa.

#### [G-120] Usuário
Pessoa que opera os Botões Interno ou Externo de Chamada do Elevador.

### Requisitos

#### [R-010]
Se não há nenhuma Chamada por Botão Externo ou Botão Interno, então todos os Elevadores estão Livres.

#### [R-020]
Se qualquer um dos Elevadores estiver no Andar da Chamada e uma nova Chamada é feita nesse Andar, seja pelo Botão Externo, seja pelo Botão Interno, então o(s) Elevador(es) em questão deve(m) ignorar essa nova Chamada.

#### [R-030]
Se o Elevador estiver fechando a Porta Interna e ocorre uma Chamada por Botão Externo ou Botão Interno no mesmo Andar que o Elevador estiver, então a Porta deverá ser aberta.

#### [R-040]
Se ocorrer bloqueio mecânico da Porta do Elevador ou se não for detectado o fechamento da Porta do Elevador tempo menor ou igual a 7 segundos, então a Porta deverá ser aberta.

#### [R-050]
A Porta Interna se mantém aberta por 7 segundos em um Andar sob atendimento de Chamada. Após esse período, a Porta Interna é fechada.

#### [R-060]
Se a Porta Externa for aberta antes do fechamento completo da Porta Interna, a Porta Interna é reaberta por mais 7 segundos.

#### [R-070]
Se algum Elevador estiver Livre, então o Elevador de Preferência é o Elevador conforme explicado abaixo:

* Se o Elevador Livre estiver no Andar 0 e os outros dois Elevadores estiverem subindo a partir do Andar 3, então o Elevador Livre deve atender à Chamada por Botão Externo no Andar 2.
* Se o Elevador Livre estiver no Andar 0 e um dos outros dois Elevadores estiver no Andar 3 e descendo, então o Elevador Livre deve permanecer no seu lugar e não atender à Chamada por Botão Externo no Andar 2 ( | 2 - 0 | >= | 2 - 3 |, Elevador não-Livre descendo ).
* Se o Elevador Livre estiver no Andar 15 e os outros dois Elevadores estiverem descendo a partir do andar 10, então o Elevador Livre deve atender à Chamada por Botão Externo no Andar 12.
* Se o Elevador Livre estiver no Andar 15 e um dos outros dois Elevadores estiver no Andar 10 e subindo, então o Elevador Livre deve permanecer no seu lugar e não atender à Chamada por Botão Externo no Andar 12 ( | 12 - 15 | >= | 12 - 10 |, Elevador não-Livre subindo ).

Caso haja empate de Preferência entre Elevadores Livres, o Elevador de Preferência será o de Número menor.

#### [R-080]
Se a Direção de um Elevador for Subir, ele deve ir nessa Direção até atender a Chamada no Andar mais alto, mas sempre ir atendendo gradativamente às Chamadas feitas por Botão Interno e Botão Externo. No caso do Botão Externo, ele deve ser o de Subir ou, no caso do Andar 15, o Botão de Descer.

#### [R-090]
Se a Direção de um Elevador for Descer, ele deve ir nessa Direção até atender a Chamada no Andar mais baixo, mas sempre ir atendendo gradativamente às Chamadas feitas por Botão Interno e Botão Externo. No caso do Botão Externo, ele deve ser o de Descer ou, no caso do Andar 0, o Botão de Subir. Os Botões Internos têm prioridade maior do que os Botões Externos.

#### [R-100]
Se dois ou mais Elevadores tiverem a Direção de Subir, o Elevador de Número maior deve ir até o Andar mais alto com solicitação de Chamada (vide R-080).

#### [R-110]
Se dois ou mais Elevadores tiverem a Direção de Descer, o Elevador de Número maior deve ir até o Andar mais baixo com solicitação de Chamada (vide R-090).