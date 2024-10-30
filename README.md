# Criando um Dashboard corporativo com integração com MySQL e Azure

Inicialmente, selecionae o banco de dados <code>azure_company</code>:
```
use azure_company
```

1.	Verifique os cabeçalhos e tipos de dados
```
desc employee;
```

2.	Modifique os valores monetários para o tipo double preciso
```
alter table employee
modify column Salary DOUBLE
```

3.	Verifique a existência dos nulos e analise a remoção
```
select * from employee
where Fname IS NULL OR
      Minit IS NULL OR
      Lname IS NULL OR
      Ssn IS NULL OR
      Bdate IS NULL OR
      Address IS NULL OR
      Sex IS NULL OR
      Salary IS NULL OR
      Super_ssn IS NULL OR
      Dno IS NULL;
```

4.	Os employees com nulos em Super_ssn podem ser os gerentes. Verifique se há algum colaborador sem gerente
```
select Fname from employee
where Super_ssn is null;
```

5.	Verifique se há algum departamento sem gerente
```
select Dname from department
where Mgr_ssn is null;
```

6.	Se houver departamento sem gerente, suponha que você possui os dados e preencha as lacunas
```
update department 
set Mgr_ssn = 'Not Def'
where Mgr_ssn is null;
```

7.	Verifique o número de horas dos projetos
```
select sum(Hours) as Total_Horas 
from works_on;
```

8.	Separar colunas complexas
```
select Address,
	   substring_index(Address, '-', 1) as Number,
	   substring_index((substring_index(Address, '-', 2)), '-', -1) as Street,
	   substring_index(Address, '-', -1) as State 
from employee;
```

9.	Mesclar consultas employee e departament para criar uma tabela employee com o nome dos departamentos associados aos colaboradores. A mescla terá como base a tabela employee. Fique atento, essa informação influencia no tipo de junção
```
select e.*,
	   d.Dname as Department
from employee e 
inner join department d 
on e.Dno = d.Dnumber;
```

10.	Neste processo elimine as colunas desnecessárias. 
```
select concat(e.Fname, ' ', e.Lname) as Employee,
	   YEAR(CURDATE()) - YEAR(e.Bdate) - 
	   (DATE_FORMAT(CURDATE(), '%m%d') < DATE_FORMAT(e.Bdate, '%m%d')) as Age,
	   e.Sex,
	   d.Dname,
	   e.Salary,
	   concat(e2.Fname, ' ', e2.Lname) as Manager
from employee e
inner join department d 
on e.Dno = d.Dnumber
left join employee e2 
on e.Super_Ssn = e2.Ssn;
```

11.	Realize a junção dos colaboradores e respectivos nomes dos gerentes . Isso pode ser feito com consulta SQL ou pela mescla de tabelas com Power BI. Caso utilize SQL, especifique no README a query utilizada no processo.
```

```

12.	Mescle as colunas de Nome e Sobrenome para ter apenas uma coluna definindo os nomes dos colaboradores

13.	Mescle os nomes de departamentos e localização. Isso fará que cada combinação departamento-local seja único. Isso irá auxiliar na criação do modelo estrela em um módulo futuro.

15.	Agrupe os dados a fim de saber quantos colaboradores existem por gerente

16.	Elimine as colunas desnecessárias, que não serão usadas no relatório, de cada tabela

