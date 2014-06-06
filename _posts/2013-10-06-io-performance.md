---
title: "IO Performance and RAID"
date: Sun Oct 06 16:12:50 +0800 2013
layout: post
published: true
categories: raid linux
---

http://www.dbasquare.com/2012/04/18/analyzing-io-performance/
http://perumal.org/analyzing-database-server-io-bottlenecks-using-iostat/

##RAID stripe calculation
правильный размер блока - средний размер операции ввода-вывода делённый на количество дисков с данными
т.е. для минимального RAID10 - avgrq-sz / 2

