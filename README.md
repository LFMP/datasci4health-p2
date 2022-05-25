# Relatório Final de Projeto P2

## Predição de prognóstico de morte para pacientes que dão entrada em internamentos ou emergência

## Prediction of death prognosis for patients admitted to inpatient or emergency room

## Apresentação

O presente projeto foi originado no contexto das atividades da disciplina de pós-graduação [Ciência e Visualização de Dados em Saúde](https://ds4h.org/), oferecida no primeiro semestre de 2022, na Unicamp. Equipe responsável:

| **Nome**  | **RA**  | **Especialização**  |
|:--------: |:------: |:------------------: |
|Leonardo Rodrigues da Costa|146895|Física|
|Luiz Fellipe Machi Pereira|203532|Computação|

## Contextualização da Proposta

Médicos são frequentemente solicitados a fazer previsões sobre os resultados futuros de saúde de seus pacientes pois é nisso que eles baseiam as decisões de tratamento. Uma dessas previsões é sobre o tempo de vida restante que um paciente tem. Embora as previsões clínicas de sobrevida sejam frequentemente imprecisas e excessivamente otimistas, dada a sua dificuldade, elas ainda estão muito bem correlacionadas com a sobrevida real e, portanto, ainda são recomendadas para uso na prática clínica de rotina [\[1\]](https://spcare.bmj.com/content/early/2019/05/10/bmjspcare-2018-001761).

Nossa proposta é construir um preditor do prognóstico de mortalidade para os pacientes que dão entrada em um encontro de internação ou emergência. A resposta deste preditor é uma escala, que indica se o paciente irá morrer em um intervalo que vai de uma a quatro semanas. Para construção do preditor foram utilizados dados gerados pelo banco de dados sintético Synthea [\[2\]](https://github.com/synthetichealth/synthea).

A escala proposta possuí 5 valores possíveis, sendo eles:

* 0: para quando não risco de morte em até 1 mês,
* 1: para risco de morte em até 1 semana
* 2: para risco de morte em entre 1 e 2 semanas
* 3: para risco de morte em entre 2 e 3 semanas
* 4: para risco de morte em entre 3 e 4 semanas

## Ferramentas

Nosso código foi feito em linguagem Python e executado exclusivamente pelo Google Collaboratory. As bibliotecas utilizadas foram:

* Numpy
* Pandas
* ZipFile
* dateutil
* Matplotlib
* Scikit-Learn

Também foi feita uma implementação de modelos via workflow, utilizando o programa Orange Workflow.

## Metodologia

Após elaborar nossa pergunta de pesquisa, foi realizada uma análise de dados de a construção e validação de um modelo de predição. Os detalhes de cada etapa, bem como os resultados obtidos e discussões, podem ser encontrados juntamente com o código Python, disponível no [arquivo notebook](notebooks/P2.ipynb).

## Problemas desta abordagem

* O limite de uso da memória RAM do Google Collaboratory e o longo tempo de construção de cada feature vector  e preditor foram fatores limitantes da nossa análise, principalmente com a inclusão do cenário 04;
* Como algumas condições (como câncer) eram descritas por múltiplos códigos SNOMED, achamos que seria muito custoso incluí-las em nossa análise:
* Inicialmente, estávamos observando os pacientes de ambulatório, emergência e internação, mas como a grande maioria dos encontros ocorre no ambulatório, seria muito custoso manter esse tipo de encontro. Por isso escolhemos apenas encontros críticos como ‘Emergency’ e ‘Inpatient’.
* Apesar de tentarmos embasar a nossa escolha de atributos para o vetor de características em condições associadas ao aumento de mortalidade nos quatro cenários, não testamos outras composições do vetor de características ou incluímos outros atributos referentes às demais condições ou propriedades dos outros arquivos.

## Conclusão

Observando os resultados, vemos que todos os preditores tiveram um viés “otimista” colocando a maior parte dos pacientes na categoria 0 onde não há risco de morte. Esse tipo resultado vai de acordo com o que vimos na literatura  [\[1\]](https://spcare.bmj.com/content/early/2019/05/10/bmjspcare-2018-001761), e mostra a dificuldade de montar um preditor de mortalidade acurado. Analisando as distribuições de risco e de idade, e também os ranks de mortalidade, podemos constatar que há uma grande variação das características da população de cada cenário, o que pode ter diminuído o desempenho dos preditores. Previsivelmente, os preditores treinados no cenário 4 tiveram o melhor desempenho, ao passo que os preditores treinados no cenário 2 tiveram o pior. O algoritmo SVM que montamos com o Scikit-Learn também realizou predições mais acuradas que os algoritmos de aprendizado nativos do Orange Workflow.
