---
title: Carga masiva de datos en tablas en una publicación de mezcla | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- TSQL
helpviewer_keywords:
- bulk load [SQL Server replication]
- merge replication bulk loading [SQL Server replication]
- sp_addtabletocontents
ms.assetid: 16e6498a-b449-4051-aec4-ea814a2ad993
caps.latest.revision: 33
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ae19f3f41aa81e3f1a2ef01e7b2b9383bd163e11
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="bulk-load-data-into-tables-in-a-merge-publication"></a>Carga masiva de datos en tablas en una publicación de mezcla
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Cuando los datos se cargan en las tablas utilizando [bcp Utility](../../tools/bcp-utility.md) o el comando [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) de forma predeterminada, los desencadenadores de replicación de mezcla que mantienen datos del seguimiento en la tabla del sistema [MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md) no se activan. Puede forzar a que se activen los desencadenadores de replicación de mezcla cuando se cargan los datos o puede insertar mediante programación los metadatos de la replicación generados después de la operación de copia masiva utilizando los procedimientos almacenados de replicación.  
  
### <a name="to-bulk-load-data-into-tables-published-by-merge-replication-using-the-bcp-utility"></a>Para realizar la carga masiva de datos en tablas publicadas mediante replicación de mezcla utilizando la utilidad bcp  
  
1.  En el publicador o suscriptor, ejecute [bcp Utility](../../tools/bcp-utility.md) o [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) para insertar los datos en una tabla publicada utilizando la replicación de mezcla.  
  
2.  Utilice uno de los métodos siguientes para asegurarse de que los metadatos de replicación se generan para los datos insertados.  
  
    -   Ejecute la copia masiva mediante la opción de FIRE_TRIGGERS.  
  
    -   En la base de datos en la que se insertaron los datos, ejecute [sp_addtabletocontents &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addtabletocontents-transact-sql.md). Especifique el nombre de tabla en el que los datos se insertaron para **@table_name**.  
  
  
