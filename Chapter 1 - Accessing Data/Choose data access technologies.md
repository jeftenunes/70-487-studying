=> ADO.NET é uma das tecnologias de acesso a dados mais antigas do .NET
=> O ADO.NET foi construído para suportar grandes cargas e se destacar em securança, escalabilidade, flexibilidade e confiabilidade.
=> A segurança, escalabilidade, performance em geral é devido ao fato de o ADO.NET ter um viés direcionado a um ~disconnected model~
    Quando vamos executar um comando SQL (Insert, update e delete), simplesmente abrimos uma conexao, executamos o comando e fechamos a conexao o mais rapido possível, 
    quando executamos uma consulta SQL, abrimos a conexao, recuperamos os dados com os quais precisamos trabalhar e fechamos a conexao o mais rápido possível.

=> Razoes pelas quais é importante considerar o uso do disconnected model:
    1. Conexoes de dados sao caras para o SGDB manter: elas consomem processamento e recursos de rede, além do que os SGBDs só podem manter um número limitado de conexoes 
    de uma vez só.

    2. Conexoes de dados podem gerar locks, causando assim problemas de concorrência.

    Para mitigar esse problema, o ADO.NET utiliza uma tecnica de otimizaçao chamada ~connection pooling~
    Como o connection pooling functiona?

    => Na pratica, a maioria das aplicaçoes usa apenas uma ou algumas poucas configuraçoes de conexoes. Isso significa que durante a execuçao da aplicaçao, muitas conexoes 
    identicas serao abertas e fechadas diversas vezes, o que gera grande custo para o SGBD. Utilizando connection pooling, o ADO.NET reduz o número de novas conexoes novas 
    a serem abertas. O pooler mantém-se 'dono' da conexao física e gerencia as conexoes, mantendo funcionais alguns conjuntos de conexoes para cada configuracao. Quando o
    usuário chama o méetodo Open(), o pooler procura alguma conexao pronta para a configuraçao demandada no pool. Se o pooler encontrar alguma conexao disponivel, a retorna 
    em vez de abrir uma nova. Quando a aplicaçao chama o método Close(), o pooler a manda de volta ao conjunto de conexoes ativas em vez de fechá-la realmente.

=> Apenas conexoes de mesma configuraçao podem estar num pool.
=> O ADO.NET cria vários pools de conexao, um para cada configuracao.
=> As conexoes sao dividas nos pools por string de conexao e pelo Windows Identity, quando a integrated security é usada.
=> Por default, o ADO.NET utiliza connection pooling. Para que o ADO.NET pare de utilizar connection pooling, deve-se desabilitá-lo.

=> Outro ponto forte do ADO.NET é a compatibilidade cross-platform. ADO.NET contém o namespace System.Data, que contém muitas das classes bases utilizadas, independentemente de tecnologia de bancos de dados. Existem muitas libs específicas no mercado (System.Data.SqlClient, System.Data.OracleClient) mas também há as mais genéricas (System.Data.Ole, System.Data.Odbc), que permite acessar os SGBDs compatíveis com OleDb e ODBC.

