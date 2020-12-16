---
title: Control del comportamiento de desencadenadores y restricciones en la sincronización
description: Conozca cómo evitar que se ejecuten los desencadenadores o que se apliquen restricciones durante la sincronización de una publicación de replicación de SQL Server.
ms.custom: seo-lt-2019
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
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
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: b27eea51556b052187cdaffca077f01e2c47dae8
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97484907"
---
# <a name="control-behavior-of-triggers-and-constraints-in-synchronization"></a>Control del comportamiento de los desencadenadores y las restricciones en la sincronización
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  Durante la sincronización, los agentes de replicación ejecutan las instrucciones [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md), [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md) y [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md) en las tablas replicadas, que pueden provocar que se ejecuten los desencadenadores del lenguaje de manipulación de datos (DML) en estas tablas. Hay casos en los que quizá necesite evitar que se activen estos desencadenadores o que se apliquen restricciones durante la sincronización. Este comportamiento depende de cómo se cree el desencadenador o la restricción.  
  
### <a name="to-prevent-triggers-from-executing-during-synchronization"></a>Para evitar que los desencadenadores se ejecuten durante la sincronización  
  
1.  Al crear un nuevo desencadenador, especifique la opción NOT FOR REPLICATION de [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md).  
  
2.  Para un desencadenador existente, especifique la opción NOT FOR REPLICATION de [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md).  
  
### <a name="to-prevent-constraints-from-being-enforced-during-synchronization"></a>Para evitar que se apliquen restricciones durante la sincronización  
  
1.  Al crear una nueva restricción CHECK o FOREIGN KEY, especifique la opción CHECK NOT FOR REPLICATION en la definición de restricción de [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md).  
  
## <a name="see-also"></a>Consulte también  
 [Crear tablas &#40;motor de base de datos&#41;](../../relational-databases/tables/create-tables-database-engine.md)  
  
  
