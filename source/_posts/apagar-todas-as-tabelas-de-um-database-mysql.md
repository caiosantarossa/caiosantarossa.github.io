title: "Apagar todas as tabelas de um database MySQL"
date: 2014-03-26 19:39:44 +0000
tags: ["MySQL"]
---

Script para apagar todas as tabelas de um database MySQL, altere 'dbName' para o nome do seu database:

	use 'dbName';
	SET FOREIGN_KEY_CHECKS = 0; 
	SET @tables = NULL;
	SET GROUP_CONCAT_MAX_LEN=32768;

	SELECT GROUP_CONCAT('`', table_schema, '`.`', table_name, '`') INTO @tables
	FROM   information_schema.tables 
	WHERE  table_schema = (SELECT DATABASE());
	SELECT IFNULL(@tables, '') INTO @tables;

	SET        @tables = CONCAT('DROP TABLE IF EXISTS ', @tables);
	PREPARE    stmt FROM @tables;
	EXECUTE    stmt;
	DEALLOCATE PREPARE stmt;
	SET        FOREIGN_KEY_CHECKS = 1;