<h1>Atendimento Laboratorial - CoraçãoLab</h1>

Este Dashboard criado é de uma empresa que faz atendimentos laboratóriais, em específico cariovasculares.
Todos os dados presentes nesse projeto foram modificados a fim de respeitar as políticas de privacidade e da Lei Geral de Proteção de Dados Pessoais (LGPD)

<hr>
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
















