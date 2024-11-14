<h1>Atendimento Laboratorial - CoraçãoLab</h1>

Este Dashboard criado é de uma empresa que faz atendimentos laboratóriais, em específico cardiovasculares.
Todos os dados presentes nesse projeto foram modificados a fim de respeitar as políticas de privacidade e da Lei Geral de Proteção de Dados Pessoais (LGPD)

<br>

<h2><a href="https://app.powerbi.com/groups/me/reports/37f68f19-977d-42c7-8f7a-00a6159c193d/e6c7e54d0faf25d2cbf4?experience=power-bi" target="_blank">Acesse o Projeto</a></h2>

<hr>
<br>
<br>

<h2>Base de Dados</h2>

As fontes de dados utilizados nesse peojeto foram quatro arquivos em excel.

<br>

A primeira fonte se chama <b>"d_convenios"</b>, e contém duas colunas:

<b>"ID Convênio"</b>: Exibe os identificadores dos convênios

<B>"Convênio"</b>: Exibe o nome do convênio

<br>

![01](https://github.com/user-attachments/assets/a62ab6f7-b140-4237-90ca-8274f4da7d2b)

<br>
<br>

A segundo fonte se chama <b>"d_procedimento"</b>, contendo duas colunas:

<b>"ID Procedimento"</b>: Exibe os indentificadores dos procedimentos

<b>Procedimento</b>: Exibe o nome dos procedimentos realizados

<br>

![02](https://github.com/user-attachments/assets/246ee14e-cba0-433a-a756-ed78cf55b9a0)

<br>
<br>

A terceira fonte se chama <b>"d_recepcionista</b> contendo também duas colunas:

<b>"ID Recepcionista"</b>: Exibe os identificadores dos recepcionistas

<b>"Recepcionista</b>: Exibe o nome dos recepcionistas

<br>

![03](https://github.com/user-attachments/assets/9d28688e-6894-4b16-b46f-87632efb84b3)

<br>
<br>

E por fim, a quarta e última fonte se chama <b>"f_atendimento"</b> e contém nove colunas:

<b>"Data</b>: Exibe a data do atendimento 

<b>"Hora</b>: Exibe a hora do atendimento

<b>ID Atendimento</b>: Identificador do atendimento

<b>"ID Paciente</b>: Identificador do paciente

<b>"Qtde Item"</b>: Quantidade de atendimentos por paciente

<b>"Valor"</b>: Valor da consulta

<b>"ID Convênio</b> FK da tabela de <b>"d_convênio"</b>

<b>"ID Procedimento"</b> FK da tabela <b>"d_procedimento"</b>

<b>"ID Recepcionista"</b> FK da tabela <b>"d_recepcionista"</b>

<br>

![image](https://github.com/user-attachments/assets/f949e120-3d37-4e11-acb6-4d67aad00c7d)

<hr>
<br>
<br>

<h2>Tratamento de Dados - ETL</h2>

O primeiro processo de tratamento que irei fazer será na tabela <b>"f_atendimento"</b>, mais especificamente na coluna <b>"Data/Hora"</b>, que está mal formatada.

Irei fazer uma quebra nos dados das linhas que estão com o formato mal configurado, para assim conseguir colocar a coluna no formato de <b>Data</b>.

Para separar a coluna em duas colunas vou utilizar a opção de Dividir Coluna com base no Delimitador.

O delimitador passado como argumento foi o espaço em branco, " ".

Após o processo eu faço a renomeação das colunas criadas para <b>"Data"</b> e <b>"Hora"</b>. E faço a mudança do tipo de dado para <b>"Data"</b> e <b>"Hora"</b>.

<br>

![01](https://github.com/user-attachments/assets/d9f7868d-dd1f-4a03-8f58-0261a6752c77)

<br>
<br>

Agora preciso criar uma tabela de inteligência de tempo, justamente para termos dados relacionados a data presentes na tabela.

Essa tabela é muito útil para análises do tipo "Qual horário tenho mais atendimento?", "Qual dia da semana tenho mais atendimentos?", entre outras análises envolvendo Data.

Criarei duas tabelas, uma se chamará <b>"dCalendario"</b> e a outra <b>"dHoras"</b>.

<br>

Para criar a tabela <b>"dCalendario"</b> utilizarei um Script para otimizar essa criação usando linhas de código com a linguagem <b>M</b> do PowerQuery.

A única coisa que preciso modificar no Script é o nome da tabela e a coluna de data.

A tabela é a <b>"f_atendimento"</b> e a coluna é a <b>"Data"</b>.

<br>

![03](https://github.com/user-attachments/assets/82ceb434-e98f-433a-8c07-f1d7639e7705)

<br>

Pronto! Agora minha tabela <b>"dCalendario"</b> está criada com todas as informações que preciso de data.

<br>

![04](https://github.com/user-attachments/assets/be8ab151-3d84-4aac-a9dc-ac36d29045e7)

<br>
<br>

Agora vou para a criação da minha tabela <b>"dHoras"</b>, onde também irei utilizar um Script para criá-la com linha de código utilizando a linguagem <b>M</b> do PowerQuery.

Agora basta eu colocar o Script que deu muito trabalho para resolver os erros do código, no painel de Editor Avançado.

![05](https://github.com/user-attachments/assets/defe9490-bab3-442c-a430-fdb840e74c83)

<br>

A tabela criada <b>"dHoras"</b> ficou da seguinte forma:

<br>

![06](https://github.com/user-attachments/assets/c26de890-fcea-46ce-b270-3c373f2d5ab7)

<hr>
<br>
<br>

<h2>Relacionamentos</h2>

Agora irei criar os relacionamentos das tabelas criadas <b>"dCalendario"</b> e <b>"dHoras"</b> com suas respectivas cardinalidades.

A tabela <b>"dCalendario"</b> vou relacionar utilizando a coluna <b>"Data"</b> com a coluna <b>"Data"</b> da tabela <b>"f_atendimento"</b>.

A tebela <b>"dHoras"</b> vou relacionar utilizando a coluna <b>"Hora"</b> com a coluna <b>"Hora"</b> da tabela <b>"f_atendimento"</b>.

Ambas as relações têm cardinalidade <b>"1,*"</b> <b>(Um para Muitos)</b>.

<br>

![07](https://github.com/user-attachments/assets/5fdfa711-78c7-4d2e-b57e-6209db59983c)

<hr>
<br>
<br>

<h2>Medidas em DAX</h2>

Criarei agora as medidas em DAX que irei utilizar ao longo do projeto, utilizando a linguagem <b>DAX (Data Analysis Expressions)</b> do PowerBI.

<br>

Para começar a criação das minhas medidas na linguagem DAX, primeiramente vou criar uma tabela com o nome de <b>"Medidas"</b>, essa tabela terá como única e exclusiva função servir como repositório para as medidas criadas, assim elas ficam organizadas e mais fácil de acessar.

<br>

![01](https://github.com/user-attachments/assets/4dd9edcb-72e3-4c03-8faf-6023ac47f176)

<br>
<br>

A primeira medida criada será a <b>"Atendimentos"</b> e sua função será fazer o cálculo da quantidade de atendimentos realizados.

Explicando a medida, eu utilizo a função DISTINCTCOUNT para fazer a contagem distinta linha a linha da tabela da coluna <b>"ID Atendimento"</b> da tabela <b>"f_atendimento"</b>.

<br>

![02](https://github.com/user-attachments/assets/f38fe0d1-5e2a-46e3-9952-f28340d57ab2)

<br>
<br>

Agora vou criar uma medida chamada <b>"Faturamento"</b> para buscar o faturamento da empresa.

Explicando a medida eu trago a função SUM para fazer a soma dos valores de toda a coluna de <b>"Valor"</b> da tabela <b>"f_atendimento"</b>.

<br>

![03](https://github.com/user-attachments/assets/877029b7-9b45-46ab-bc73-c244441e04ba)

<br>
<br>

Irei criar uma medida para exibir a meta para atendimentos e a meta de faturamento.

Ambas as metas é o valor posterior fixo mensalmente.

A medida é bem simples:

Meta Atendimento = 3000

Meta Faturamento = 500000

<br>
<br>

A proxima medida que criarei se chamará <b>"Atingimento de Meta"</b>, e sua função será exibir a % (porcentagem) que falta para atingir a meta no ano.

Explicando a medida, uso a função DIVIDE para fazer a divisão das medidas <b>"Faturamento"</b> com <b>"Meta Faturamento"</b> e faço depois a multiplicação (*) por 12 (meses do ano).

<br>

![05](https://github.com/user-attachments/assets/49d7dbe8-d1b8-4a8a-80a8-1a270beccd54)

<br>
<br>

Agora para auxiliar na medida de <b>"Atingimento de Meta"</b> criado anteriormente, irei criar uma medida chamada <b>"Atendimento Meta Comp."</b>. Ele servirá para mostrar o total do atingimento de meta, ou seja, o 100%.

Explicação da medida, eu apenas faço a subtração de 1 (100%) pela medida de <b>"Atingimento de Meta"</b>.

<br>

![06](https://github.com/user-attachments/assets/cf19fb02-2a89-4d02-b043-1d6637f84e76)

<br>
<br>

Criarei uma Medida chamada <b>"Qtd Meses"</b> para me mostrar apenas os meses que tiveram faturamento na empresa.

Explicando a medida:

Uso a função calculate para buscar os dados da tabela <b>"f_atendimento"</b> com seus respectivos filtros, depois uso a função DISTINCTCOUNT para buscar todos os valores distintos da coluna <b>"MesAno"</b> da tabela <b>"dCalendario"</b>.

<br>

![07](https://github.com/user-attachments/assets/37aef043-4109-44cb-b1f1-55d0c58ee2ad)

<br>
<br>

Criarei uma medida chamada <b>"Atingimento de Meta Até Mês Atual"</b>, como o próprio nome sugere, essa medida terá como função mostrar o faturamento até o mês atual.

Explicando a medida:

Criei uma variável chamada <b>"vQtdMeses"</b>, onde rece basicamente o código da medida de <b>"Atingimento de meta"</b>.

E me retornará como resultado a função DIVIDE fazendo a divisão da medida <b>"Faturamento"</b> pela variável criada <b>"vQtdMeses"</b> e depois multiplico pela medida <b>"Meta Faturamento"</b>.

Crio uma variável chamada de <b>"vPercentual"</b> para me mostrar o valor percentual da meta

Dentro do RETURN (Retorna o Valor) crio uma função IF para mostrar os valores abaixo e acima da média.

Se o vPercentua l(Valor % da Meta) for "<" abaixo de "0" mostra o texto abaixo da meta atual com o valor que está abaixo da meta.

Se não, o valor está acima da meta, e mostra a frase "acima da meta até o mês atual" com o valor que está acima da meta

<br>

![08](https://github.com/user-attachments/assets/b711cd84-78c8-439a-bbdb-e41a2de2ed0b)

<br>
<br>

Agora faço a criação da medida <b>"Meta Até o Mês Atual"</b>, que exibirá o tamanho da meta até o meu mês atual.

Reaproveito apenas o código da medida criada anteriormente.

E retorno o valor da variável criada multiplicada pela medida de <b>"Meta Faturamento"</b>.

<br>

![09](https://github.com/user-attachments/assets/5a48d696-4892-4da1-9f08-afc259887c48)

<hr>
<br>
<br>

<h2>Criação da Página Desempenho de Atendimento</h2>

Antes da criação de qualquer gráfico no Dashboard, eu fiz a criação do Background da página no aplicativo <b>Figma</b>

Farei a aplicação da tela de fundo na página. Isso me auxilia na hora de montar meu Dashboard, pois já fica a marcação de onde colocar os gráficos, e isso me auxilia e facilita muito o processo de criação.

<br>

![01](https://github.com/user-attachments/assets/c5031358-101e-4a64-a282-46c71d864f5d)

<br>
<br>

A página ficou com esse seguinte aspecto.  

<br>

![02](https://github.com/user-attachments/assets/a2c2732e-5794-4b6e-8b48-528130c08c66)


<br>
<br>

Para facilitar a estilização dos gráficos que serão criados, vou personalizar um estilo o tornando como padrão em todos para todos os gráficos, e assim, otimizar mais ainda meu tempo de criação do Dashboard.

<br>

![3](https://github.com/user-attachments/assets/62ffd63f-73fe-4b58-aac2-66a3c335b0d1)


<br>
<br>

O primeiro gráfico que irei criar será o <b>Cartão de Linha Múltipla</b>, ele servirá para exibir o valor total de faturamento.

Adicionei os seguintes dados:

Na aba de Campos, adicionei a medida <b>"Faturamento"</b>.

<br>

![04](https://github.com/user-attachments/assets/de4587fb-cdb8-4087-9ff7-b3e051af6e8e)

<br>
<br>

Agora criarei um gráfico de <b>Segmentação de Dados</b> para poder fazer o filtro da página pelos anos.

Adicionei os seguintes dados:

No aba Campo, adicionei a coluna <b>"Ano"</b> da tabela <b>"dCalendario"</b>.

Ativei neste gráfico a opção de escolha única, e mudei o estilo para suspenso.

<br>

![Segmentação](https://github.com/user-attachments/assets/293843f8-d320-4ea5-88bb-d2077624b6c5)

<br>
<br>

Vou fazer a criação de um gráfico de <b>Velocímetro</b>, para me mostrar o total da meta atingido e o total de meta que ainda falta para atingir.

Adicionei os seguintes dados:

No campo de Valor, adicionei a medida <b>"Atingimento Meta"</b>.

<br>

![06](https://github.com/user-attachments/assets/b27167f0-2308-4c8f-adeb-6effd6e9f07e)

<br>
<br>

Agora criarei um <b>Gráfico de Colunas Empilhadas</b>, esse gráfico me mostrará informações sobre o Faturamento por Mês e Ano.

Adicionei os seguintes dados:

No <b>"Eixo X"</b>, adicionei a coluna <b>"MesAno"</b> da tabela auxiliar <b>"dCalendario"</b>

No <b>"Eixo Y"</b>, adicionei a medida <b>"Faturamento"</b>.

<br>

![07](https://github.com/user-attachments/assets/353cc21d-5e9f-4ed4-bda8-5f1eb7419906)

<br>
<br>

Agora criarei um gráfico <b>Cartão de Linha Múltipla</b>, para exibir a quantidade da meta até o mês atual.

Adiciono os seguintes dados:

Na aba Campos, adiciono a medida <b>"Meta Até o Mês Atual"</b>.

<br>

![08](https://github.com/user-attachments/assets/f09d852c-94bb-4b46-bed9-bb2b94cbc1e7)


<br>
<br>

Crio agora um <b>Gráfico de Colunas Empilhadas</b>, para me mostrar a quantidade de atendimentos por mês e ano, e uma linha de tendência me mostrando a meta de atendimentos.

Adicionei os seguintes dados:

No <b>"Eixo X"</b>, adicionei a coluna <b>"MesAno"</b> da tabela <b>"dCalendario"</b>

No <b>"Eixo Y"</b> adicionei a medida <b>"Qtd Atendimentos"</b>

Na parte de Análises do Visual, adicionei uma linha constante passando como parâmetro a medida criada <b>"Meta Atendimento"</b>.

<br>

![09](https://github.com/user-attachments/assets/0cc3f46c-636e-4b73-a3b8-0c74a25f1c5c)

<br>
<br>

Agora quero nesse gráfico criado anteriormente, pintar o pedaço da barra que está acima da meta de uma cor diferente da que está abaixo da meta. Para conseguir tal resultado tenho que criar duas medidas utilizando a linguagem DAX.

A primeira medida será para a parte da barra que se localiza abaixo da meta .

Crio a medida chamada de <b>"Até a Meta"</b>

Começo usando a função IF (se) referenciando a medida de <b>"Qtd Atendimentos"</b> <b>">" (maior)</b> que a meta de atendimento presente na medida <b>"Meta Atendimento"</b> vai chamar a medida <b>"Meta de Atendimento"</b> (vai fixar o valor).

Se não vai colocar o valor da Quantidade de atendimentos presente na medida <b>"Qtd Atendimentos"</b>.

<br>

![10](https://github.com/user-attachments/assets/0c8e1bd3-3918-4633-b8de-c440930ec3b5)

<br>
<br>

Agora farei a criação da segunda medida para pintar a parte da barra acima da meta de atendimentos.

A medida se chamará <b>"Acima da Média"</b>.

Utilizo a função IF para mostrar se a quantidade de atendimentos presentes na medida <b>"Qtd Atendimentos"</b> é <b>">" (maior)</b> que a meta de atendimentos presente na medida <b>"Meta Atendimento"</b>.

Logo após faço a subtração de <b>"Qtd Atendimentos"</b> menos <b>"Meta Atendimento"</b>.

<br>

![11](https://github.com/user-attachments/assets/cee9128e-fa7c-40ff-b8fe-b6dd0323c2be)

<br>
<br>

Agora para ter o resultado que eu quero no meu Gráfico de Colunas Empilhada, basta eu adicionar as medida <b>"Acima da Meta"</b> e <b>"Até da Meta"</b> no <b>"Eixo Y"</b>

![12](https://github.com/user-attachments/assets/01695345-012c-4710-abb6-9a915b087454)

<br>
<br>

Agora farei  a criação de um gráfico <b>Matriz</b> para exibir os atendimentos filtrados por hora, dias da semana e outras datas.

Adicionei os seguintes dados:

No campo Linhas, adiciono a coluna <b>"Faixa Hora"</b> da tabela <b>"dHoras"</b> - renomeio para <b>"Hora"</b>

No campo Colunas, adiciono a coluna <B>"NomeDia"</b> da tabela <b>"dCalendario"</b> 

No campo Valores, adiciono a medida <b>"Qtd Atendimentos"</b> - renomeio para <b>"Atendimentos"</b>.

<br>

![13](https://github.com/user-attachments/assets/eaa007c5-dbb0-4608-ae87-641fe08bba09)

<br>
<br>

Agora vou fazer algumas estilizações para deixa a Matriz mais elegante.

Vou fazer uma formatação condicional para estilizar o fundo da célula e o valor dela.

![14](https://github.com/user-attachments/assets/23644f64-915c-42ea-adb7-fdd4770ff418)

<br>
<br>

Por fim minha matriz está com a formatação da forma que eu queria, para lê esse gráfico é a mesma coisa que lê um gráfico de <b>Mapa de Calor</b>, cores mais quentes e intensas significam mais dados, cores mais frias e menos intensas significam menos dados.

<br>

![15](https://github.com/user-attachments/assets/ce594bcd-aed5-4e33-a3bd-6dbccada6702)

<br>
<br>

Por fim, terminei meu projeto, a página de Desempenho de Atendimento ficou assim:

<br>

![Fim](https://github.com/user-attachments/assets/da6207c8-c6d7-4600-b2a3-80a71931bb43)


































