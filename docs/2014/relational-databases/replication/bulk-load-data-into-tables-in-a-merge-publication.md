---
title: Carga masiva de datos en tablas en una publicación de mezcla (programación de replicación Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- bulk load [SQL Server replication]
- merge replication bulk loading [SQL Server replication]
- sp_addtabletocontents
ms.assetid: 16e6498a-b449-4051-aec4-ea814a2ad993
caps.latest.revision: 32
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5fe31b5f7720896c149af4463de3ef9a72cae23b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37166976"
---
# <a name="bulk-load-data-into-tables-in-a-merge-publication-replication-transact-sql-programming"></a>Realizar una carga masiva de datos en tablas de una publicación de mezcla (programación de la replicación con Transact-SQL)
  Cuando los datos se cargan en las tablas utilizando [bcp Utility](../../tools/bcp-utility.md) o el comando [BULK INSERT](/sql/t-sql/statements/bulk-insert-transact-sql) de forma predeterminada, los desencadenadores de replicación de mezcla que mantienen datos del seguimiento en la tabla del sistema [MSmerge_contents](/sql/relational-databases/system-tables/msmerge-contents-transact-sql) no se activan. Puede forzar a que se activen los desencadenadores de replicación de mezcla cuando se cargan los datos o puede insertar mediante programación los metadatos de la replicación generados después de la operación de copia masiva utilizando los procedimientos almacenados de replicación.  
  
### <a name="to-bulk-load-data-into-tables-published-by-merge-replication-using-the-bcp-utility"></a>Para realizar la carga masiva de datos en tablas publicadas mediante replicación de mezcla utilizando la utilidad bcp  
  
1.  En el publicador o suscriptor, ejecute [bcp Utility](../../tools/bcp-utility.md) o [BULK INSERT](/sql/t-sql/statements/bulk-insert-transact-sql) para insertar los datos en una tabla publicada utilizando la replicación de mezcla.  
  
2.  Utilice uno de los métodos siguientes para asegurarse de que los metadatos de replicación se generan para los datos insertados.  
  
    -   Ejecute la copia masiva mediante la opción de FIRE_TRIGGERS.  
  
    -   En la base de datos en la que se insertaron los datos, ejecute [sp_addtabletocontents &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addtabletocontents-transact-sql). Especifique el nombre de tabla en el que los datos se insertaron para **@table_name**.  
  
  
