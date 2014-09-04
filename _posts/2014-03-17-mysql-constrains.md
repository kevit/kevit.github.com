---
layout: post
title: "Mysql foreign keys"
description: ""
category: 
tags: [ mysql , constraints]
---

В данном случае это внешний ключ. Бывают ещё первичные ключи. Плюс,
посмотрите ещё в сторону уникальных индексов - UNIQUE INDEX.
Русскоязычной информации по этом дофига.
UPDATE:
FK_issue_project - название внешнего ключа. Обратите внимание на
общепринятый префикс FK - Foreign Key (внешний ключ). Используют также
PK - Primary Key (первичный ключ), UQ - Unique Index (уникальный
индекс), IX - Index (индекс).
ON DELETE CASCADE - означает, что при удалении записи в таблице, на
которую идёт ссылка (tbl_project), записи в таблице, которые ссылаются
(tbl_issue) будут удалены. По смыслу из названий таблиц: Все дефекты,
привязанные к проекту, будут удалены.
ON UPDATE RESTRICT - означает, что при изменении значения ключа, на
который идёт ссылка (tbl_project.id), будет выдана ошибка и изменение не
пройдёт.
Ещё бывает SET NULL (установить значение в NULL) и NO ACTION (ничего не
делать).


es, a foreign key is a type of constraint. MySQL has uneven support for
constraints:
•PRIMARY KEY: yes as table constraint and column constraint.
•FOREIGN KEY: yes as table constraint, but only with InnoDB and BDB
storage engines; otherwise parsed but ignored.
•CHECK: parsed but ignored in all storage engines.
•UNIQUE: yes as table constraint and column constraint.
•NOT NULL: yes as column constraintsraint.
•DEFERRABLE and other constraint attributes: no support.
The CONSTRAINT clause allows you to name the constraint explicitly,
either to make metadata more readable or else to use the name when you
want to drop the constraint. The SQL standard requires that the
CONSTRAINT clause is optional. If you leave it out, the RDBMS creates a
name automatically, and the name is up to the implementation.

http://stackoverflow.com/questions/310561/mysql-terminology-constraints-vs-foreign-keys-difference
