# Criando um Dashboard corporativo com integração com MySQL e Azure

1.	Verifique os cabeçalhos e tipos de dados
```
use azure_company;

desc employee;
desc department;
desc dependent;
desc dept_locations;
desc project;
desc works_on;
```

2.	Modifique os valores monetários para o tipo double preciso
```
use azure_company

alter table employee
modify column Salary DOUBLE
```

3.	Verifique a existência dos nulos e analise a remoção
```

```

4.	Os employees com nulos em Super_ssn podem ser os gerentes. Verifique se há algum colaborador sem gerente

5.	Verifique se há algum departamento sem gerente

6.	Se houver departamento sem gerente, suponha que você possui os dados e preencha as lacunas

7.	Verifique o número de horas dos projetos

8.	Separar colunas complexas

9.	Mesclar consultas employee e departament para criar uma tabela employee com o nome dos departamentos associados aos colaboradores. A mescla terá como base a

10.	tabela employee. Fique atento, essa informação influencia no tipo de junção

11.	Neste processo elimine as colunas desnecessárias. 

12.	Realize a junção dos colaboradores e respectivos nomes dos gerentes . Isso pode ser feito com consulta SQL ou pela mescla de tabelas com Power BI. Caso utilize

13.	SQL, especifique no README a query utilizada no processo.

14.	Mescle as colunas de Nome e Sobrenome para ter apenas uma coluna definindo os nomes dos colaboradores

15.	Mescle os nomes de departamentos e localização. Isso fará que cada combinação departamento-local seja único. Isso irá auxiliar na criação do modelo estrela em um módulo futuro.

14.	Agrupe os dados a fim de saber quantos colaboradores existem por gerente

15.	Elimine as colunas desnecessárias, que não serão usadas no relatório, de cada tabela

