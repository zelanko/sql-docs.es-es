---
title: Controlar el comportamiento de desencadenadores y restricciones durante la sincronización (programación de replicación Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
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
- identities [SQL Server replication]
- constraints [SQL Server], replication
- triggers [SQL Server], replication
- triggers [SQL Server replication]
- constraints [SQL Server replication]
- NOT FOR REPLICATION option
- NFR option
ms.assetid: 7c4e0f0e-cadc-4c99-98f4-69799b9b356b
caps.latest.revision: 35
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9ac9b8b012d8fcb10d0019518a2169c7f68dfdbb
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37272541"
---
# <a name="control-the-behavior-of-triggers-and-constraints-during-synchronization-replication-transact-sql-programming"></a>Controlar el comportamiento de desencadenadores y restricciones durante la sincronización (programación de la replicación con Transact-SQL)
  Durante la sincronización, los agentes de replicación ejecutan las instrucciones [INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/insert-transact-sql), [UPDATE &#40;Transact-SQL&#41;](/sql/t-sql/queries/update-transact-sql) y [DELETE &#40;Transact-SQL&#41;](/sql/t-sql/statements/delete-transact-sql) en las tablas replicadas, que pueden provocar que se ejecuten los desencadenadores del lenguaje de manipulación de datos (DML) en estas tablas. Hay casos en los que quizá necesite evitar que se activen estos desencadenadores o que se apliquen restricciones durante la sincronización. Este comportamiento depende de cómo se cree el desencadenador o la restricción.  
  
### <a name="to-prevent-triggers-from-executing-during-synchronization"></a>Para evitar que los desencadenadores se ejecuten durante la sincronización  
  
1.  Al crear un nuevo desencadenador, especifique la opción NOT FOR REPLICATION de [CREATE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql).  
  
2.  Para un desencadenador existente, especifique la opción NOT FOR REPLICATION de [ALTER TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-trigger-transact-sql).  
  
### <a name="to-prevent-constraints-from-being-enforced-during-synchronization"></a>Para evitar que se apliquen restricciones durante la sincronización  
  
1.  Al crear una nueva restricción CHECK o FOREIGN KEY, especifique la opción CHECK NOT FOR REPLICATION en la definición de restricción de [CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql).  
  
## <a name="see-also"></a>Vea también  
 [Crear tablas &#40;motor de base de datos&#41;](../tables/create-tables-database-engine.md)  
  
  
