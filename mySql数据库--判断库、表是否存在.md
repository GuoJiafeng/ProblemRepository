方法一（在查询器?）：

DELIMITER $$
 
DROP FUNCTION IF EXISTS `func_check_db_exists`$$
 
CREATE FUNCTION `func_check_db_exists`(db_name varchar(64)) RETURNS varchar(20) CHARSET utf8
BEGIN
  if exists(select 1 from information_schema.schemata where schema_name=db_name) then
    return 'Exists!';
  else
    return 'Not exists!';
  end if;
END$$
 
DELIMITER ;


-------------------------------
方法二
drop database if exists test2;
create database if not exists test2;