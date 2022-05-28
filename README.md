<h1>Momento - Atividade de banco de dados </h1>

<h2>1 - Inclua suas próprias informações no departamento de tecnologia da empresa.</h2>

<b>QUERY EM SQL</b><br>

<code>INSERT INTO funcionarios (primeiro_nome, sobrenome, email, telefone, dataContratacao, ocupacao_id, salario, departamento_id)
VALUES ('Diego', 'Santos', 'santos.diego@momento.org', '365 598 545 478', '2022-06-07', 
(SELECT ocupacao_id FROM ocupacoes WHERE ocupacao_title LIKE '%Desenvolvedor Web%'), 2500.00, (SELECT departamento_id FROM departamento WHERE departamento_name LIKE '%Tecnologia%'));</code><br>

<h2>2-A administração está sem funcionários. Inclua os outros elementos do seu grupo do demoday no departamento de administração.</h2>

<b>QUERY EM SQL</b>:<br>

<code>INSERT INTO funcionarios(primeiro_nome, sobrenome, email, telefone, dataContratacao, ocupacao_id, salario, departamento_id)
VALUES 
    ('Camily', 'Vitoria', 'Cami.vit@momento.org', '11 304343434', '2012-06-12', (SELECT ocupacao_id FROM ocupacoes WHERE ocupacao_title LIKE '%Vice-presidente de administração%'), 
15200.00, (SELECT departamento_id FROM departamento WHERE departamento_name LIKE '%Admnistração%')),('Giullia', 'Maria', 'Maria.Giullia@momento.org', '11 305563434', '2021-05-12', (SELECT ocupacao_id FROM ocupacoes WHERE ocupacao_title LIKE '%Assistente Administrativo%'), 
1200.00, (SELECT departamento_id FROM departamento WHERE departamento_name LIKE '%Admnistração%')),
('Pedro', 'Oliveira', 'Oliveira@momento.org', '11 98963434', '1998-09-20', (SELECT ocupacao_id FROM ocupacoes WHERE ocupacao_title LIKE '%Assistente Administrativo%'), 
1200.00, (SELECT departamento_id FROM departamento WHERE departamento_name LIKE '%Admnistração%'));</code><br>

<h2>3-Agora diga, quantos funcionários temos ao total na empresa?</h2>

<b>Resposta: </b> 44

<b>QUERY EM SQL</b>:<br>

<code>SELECT COUNT(*) FROM funcionarios</code><br>

<h2>4-Quantos funcionários temos no departamento de finanças?</h2>

<b>Resposta: </b> 6

<b>QUERY EM SQL</b>:<br>

<code>SELECT COUNT(funcionarios.primeiro_nome) FROM funcionarios INNER JOIN departamento WHERE departamento.departamento_name LIKE '%Finanças%' AND departamento.departamento_id = funcionarios.departamento_id;</code><br>

<h2>5 - Qual a média salarial do departamento de tecnologia?</h2>

<b>Resposta: </b> 5216.67

<b>QUERY EM SQL</b>:<br>

<code>SELECT ROUND(AVG(funcionarios.salario),2) FROM funcionarios INNER JOIN departamento WHERE departamento.departamento_name LIKE '%Tecnologia%' AND funcionarios.departamento_id = departamento.departamento_id;</code><br>

<h2>6 - Quanto o departamento de Transportes gasta em salários?</h2>

<b>Resposta: </b> 41200.00

<b>QUERY EM SQL</b>:<br>

<code>SELECT SUM(funcionarios.salario) FROM departamento INNER JOIN funcionarios WHERE departamento.departamento_name LIKE '%Transporte%' 
AND funcionarios.departamento_id = departamento.departamento_id;</code><br>

<h2>7 - Um novo departamento foi criado. O departamento de inovações. Ele será locado no Brasil. Por favor, adicione-o no banco de dados.</h2>

<b>QUERY EM SQL</b>:<br>

<code>INSERT INTO departamento (departamento_name, posicao_id) VALUES ('tristeza', (SELECT posicao_id FROM posicao WHERE pais_id LIKE '%BR%' AND cidade LIKE '%São Paulo%'));</code><br>

<h2>8 - Novos Funcionários!
Três novos funcionários foram contratados para o departamento de inovações. Por favor, adicione-os: William Ferreira, casado com Inara Ferreira, possui um filho chamado Gabriel que tem 4 anos e adora brincar com cachorros. Ele será programador.Já a Fernanda Lima, que é casada com o Rodrigo, não possui filhos. Ela vai ocupar a posição de desenvolvedora.  Por último, a Gerente do departamento será Fabiana Raulino. Casada, duas filhas (Maya e Laura). 

O salário de todos eles será a média salarial dos departamentos de administração e finanças.</h2>

<b>QUERY INSERINDO NA TABELA FUNCIONARIOS</b>:<br>

<code>INSERT INTO funcionarios(primeiro_nome, sobrenome, email, telefone, dataContratacao, ocupacao_id, salario, departamento_id)
VALUES ('William', 'Ferreira', 'ferreira.will@momento.org', '688 695 4949', '2022-05-28', (SELECT ocupacao_id FROM ocupacoes WHERE ocupacao_title LIKE '%Desenvolvedor Web%'), 
(SELECT * FROM media), 
        (SELECT departamento_id FROM departamento WHERE departamento_name LIKE '%tristeza%')),
        ('Fernanda', 'Lima', 'Lima.fern@momento.org', '788 695 658', '2022-05-28', (SELECT ocupacao_id FROM ocupacoes WHERE ocupacao_title LIKE '%Desenvolvedor Web%'), 
(SELECT * FROM media), 
        (SELECT departamento_id FROM departamento WHERE departamento_name LIKE '%tristeza%')),
        ('Fabiana', 'Raulino', 'fabi.Rau@momento.org', '688 695 4949', '2022-05-28', (SELECT ocupacao_id FROM ocupacoes WHERE ocupacao_title LIKE '%Gerente de Finanças%'), 
(SELECT * FROM media), 
        (SELECT departamento_id FROM departamento WHERE departamento_name LIKE '%tristeza%')); </code>


  <b>CRIAÇÃO VIEW PARA AUXILIAR A INSERÇÃO</b>:<br>

<code> CREATE VIEW media AS SELECT ROUND(AVG(funcionarios.salario),2) FROM funcionarios INNER JOIN departamento
	WHERE departamento_name LIKE '%Admnistração%' OR departamento_name LIKE '%Finanças%' AND funcionarios.departamento_id = departamento.departamento_id ;</code><br>

<b>INSERÇÃO DEPENDENTES</b>:<br>

<code>INSERT INTO dependentes(primeiro_nome, sobrenome, parentesco, funcionario_id) VALUES ('Inara', 'Ferreira', 'esposa', (SELECT funcionario_id FROM funcionarios WHERE email LIKE '%ferreira.will@momento.org%')),
('Gabriel', 'Ferreira', 'filho', (SELECT funcionario_id FROM funcionarios WHERE email LIKE '%ferreira.will@momento.org%')), ('Rodrigo', 'Lima', 'Marido', (SELECT funcionario_id FROM funcionarios WHERE email LIKE '%Lima.fern@momento.org%')),
    ('Maya', 'Raulino', 'filho', (SELECT funcionario_id FROM funcionarios WHERE email LIKE '%fabi.Rau@momento.org%')), ('Laura', 'Raulino', 'filho', (SELECT funcionario_id FROM funcionarios WHERE email LIKE '%fabi.Rau@momento.org%'));</code><br>



<h2>9 - Informe todas as regiões em que a empresa atua acompanhadas de seus países.</h2>

<b>QUERY EM SQL</b>:<br>

<code>SELECT paises.pais_name AS Pais, regiao.regiao_name FROM paises INNER JOIN regiao WHERE paises.regiao_id = regiao.regiao_id;</code><br>



<h2>10 - Joe Sciarra é filho de quem?</h2>

<b>Resposta: </b> Ismael Sciarra

<b>QUERY EM SQL</b>:<br>

<code>SELECT funcionarios.primeiro_nome, funcionarios.sobrenome FROM dependentes INNER JOIN funcionarios WHERE dependentes.funcionario_id = funcionarios.funcionario_id 
	AND dependentes.primeiro_nome LIKE '%Joe%' AND dependentes.sobrenome LIKE '%Sciarra%';</code><br>



<h2>11 - Jose Manuel possui filhos?</h2>

<b>Resposta: </b> Não

<b>QUERY EM SQL</b>:<br>

<code>SELECT funcionarios.primeiro_nome, dependentes.primeiro_nome FROM dependentes INNER JOIN funcionarios WHERE dependentes.funcionario_id = funcionarios.funcionario_id 
AND dependentes.sobrenome LIKE '%Manuel%';</code><br>



<h2>12 - Qual região possui mais países?</h2>

<b>Resposta: </b> Europa

<b>QUERY EM SQL</b>:<br>

<code>SELECT regiao.regiao_name, COUNT(paises.regiao_id) FROM paises INNER JOIN regiao WHERE regiao.regiao_id = paises.regiao_id GROUP BY regiao.regiao_name;</code><br>



<h2>13 - Exiba o nome cada funcionário acompanhado de seus dependentes.</h2>

<b>QUERY EM SQL</b>:<br>

<code>SELECT funcionarios.primeiro_nome, dependentes.primeiro_nome FROM funcionarios INNER JOIN dependentes WHERE funcionarios.funcionario_id = dependentes.funcionario_id</code><br>

<h2>14 - Karen Partners possui um cônjuge?</h2>

<b>Resposta: </b> Sim, o Alec

<b>QUERY EM SQL</b>:<br>

<code>SELECT dependentes.primeiro_nome, dependentes.sobrenome FROM dependentes INNER JOIN funcionarios WHERE funcionarios.funcionario_id = dependentes.funcionario_id 
				AND dependentes.funcionario_id = (SELECT funcionario_id FROM funcionarios WHERE primeiro_nome LIKE '%Karen%' AND sobrenome
                 LIKE '%Partners%');</code><br>

<h2>15 - O ID da tabela de países não segue um padrão numérico. Na sua visão, qual o impacto disso no desenvolvimento do banco?</h2>

<b>Resposta: </b> Nenhum, pois o requisito para ser uma <b>Primary Key</b> é não ser nulo e ser unico.



<h2>16 - Escolha um país para se mudar. Qual seria esse país? Por que escolheria esse país? E o departamento. O que seria? Como seriam seus funcionários?</h2>

<b>Resposta: </b>Para a Argentina, eu gosto de churrasco e falam que o churrasco la é bom. Departamento de comidas, meus funcionarios iriam gostar de comida

<h2>17 - Atualize as informações na tabela para que seu departamento seja criado.</h2>

<b>QUERY EM SQL</b>:<br>

<code>INSERT INTO posicao (endereco, cidade, pais_id) VALUES ( 'Brandsen 805', 'Buenos Aires', 'AR';</code><br>

<code>INSERT INTO departamento (departamento_name, posicao_id) VALUES ('Comedores de churrasco', (SELECT posicao_id FROM posicao WHERE endereco LIKE '%Brandsen 805%'));</code><br>



