---
title: "Carga masiva de datos en tablas en una publicación de mezcla | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- TSQL
helpviewer_keywords:
- bulk load [SQL Server replication]
- merge replication bulk loading [SQL Server replication]
- sp_addtabletocontents
ms.assetid: 16e6498a-b449-4051-aec4-ea814a2ad993
caps.latest.revision: 33
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: cbcbfedbd5b2296da2cb266bf78ca3f7db9760ac
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="bulk-load-data-into-tables-in-a-merge-publication"></a>Carga masiva de datos en tablas en una publicación de mezcla
  Cuando los datos se cargan en las tablas utilizando [bcp Utility](../../tools/bcp-utility.md) o el comando [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) de forma predeterminada, los desencadenadores de replicación de mezcla que mantienen datos del seguimiento en la tabla del sistema [MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md) no se activan. Puede forzar a que se activen los desencadenadores de replicación de mezcla cuando se cargan los datos o puede insertar mediante programación los metadatos de la replicación generados después de la operación de copia masiva utilizando los procedimientos almacenados de replicación.  
  
### <a name="to-bulk-load-data-into-tables-published-by-merge-replication-using-the-bcp-utility"></a>Para realizar la carga masiva de datos en tablas publicadas mediante replicación de mezcla utilizando la utilidad bcp  
  
1.  En el publicador o suscriptor, ejecute [bcp Utility](../../tools/bcp-utility.md) o [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) para insertar los datos en una tabla publicada utilizando la replicación de mezcla.  
  
2.  Utilice uno de los métodos siguientes para asegurarse de que los metadatos de replicación se generan para los datos insertados.  
  
    -   Ejecute la copia masiva mediante la opción de FIRE_TRIGGERS.  
  
    -   En la base de datos en la que se insertaron los datos, ejecute [sp_addtabletocontents &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addtabletocontents-transact-sql.md). Especifique el nombre de tabla en el que los datos se insertaron para **@table_name**.  
  
  

