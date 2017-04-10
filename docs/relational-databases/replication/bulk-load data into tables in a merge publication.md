---
title: "Realizar una carga masiva de datos en tablas de una publicaci&#243;n de mezcla (programaci&#243;n de la replicaci&#243;n con Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "carga masiva [replicación de SQL Server]"
  - "carga masiva de la replicación de mezcla [replicación de SQL Server]"
  - "sp_addtabletocontents"
ms.assetid: 16e6498a-b449-4051-aec4-ea814a2ad993
caps.latest.revision: 33
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Realizar una carga masiva de datos en tablas de una publicaci&#243;n de mezcla (programaci&#243;n de la replicaci&#243;n con Transact-SQL)
  Cuando los datos se cargan en las tablas mediante el [utilidad bcp](../../tools/bcp-utility.md) o [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) de comandos, de forma predeterminada, los desencadenadores de replicación de mezcla que mantienen los datos de seguimiento de la [MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md) tabla del sistema no se activan. Puede forzar a que se activen los desencadenadores de replicación de mezcla cuando se cargan los datos o puede insertar mediante programación los metadatos de la replicación generados después de la operación de copia masiva utilizando los procedimientos almacenados de replicación.  
  
### Para realizar la carga masiva de datos en tablas publicadas mediante replicación de mezcla utilizando la utilidad bcp  
  
1.  En el publicador o suscriptor, ejecute [bcp Utility](../../tools/bcp-utility.md) o [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) para insertar los datos en una tabla publicada utilizando la replicación de mezcla.  
  
2.  Utilice uno de los métodos siguientes para asegurarse de que los metadatos de replicación se generan para los datos insertados.  
  
    -   Ejecute la copia masiva mediante la opción de FIRE_TRIGGERS.  
  
    -   En la base de datos en la que se insertaron los datos, ejecute [sp_addtabletocontents & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addtabletocontents-transact-sql.md). Especifique el nombre de tabla en la que se insertan los datos de **@table_name**.  
  
  