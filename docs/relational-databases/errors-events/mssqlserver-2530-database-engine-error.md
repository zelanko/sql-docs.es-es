---
title: MSSQLSERVER_2530 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
ms.assetid: 5d4be07a-38a5-4b25-819c-4dcb4636cc15
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b51fb99c97447d630610be45dc3e3b681d90c40f
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "68085999"
---
# <a name="mssqlserver_2530"></a>MSSQLSERVER_2530
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|2530|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBCC_INDEX_IS_OFFLINE|  
|Texto del mensaje|El índice "%.*ls"" de la tabla "%.\*ls" está deshabilitado.|  
  
## <a name="explanation"></a>Explicación  
La instrucción DBCC no puede continuar porque el índice especificado está deshabilitado. Cuando se deshabilita un índice, sigue deshabilitado hasta que se vuelve a generar o se quita y se vuelve a crear.  
  
## <a name="user-action"></a>Acción del usuario  
  
1.  Habilite el índice deshabilitado utilizando uno de los métodos siguientes:  
  
    -   Instrucción ALTER INDEX con la cláusula REBUILD  
  
    -   CREATE INDEX con la cláusula DROP_EXISTING  
  
    -   DBCC DBREINDEX  
  
2.  Ejecute de nuevo la instrucción DBCC.  
  
## <a name="see-also"></a>Consulte también  
[Habilitar índices y restricciones](~/relational-databases/indexes/enable-indexes-and-constraints.md)  
[ALTER INDEX &#40;Transact-SQL&#41;](~/t-sql/statements/alter-index-transact-sql.md)  
[CREATE INDEX &#40;Transact-SQL&#41;](~/t-sql/statements/create-index-transact-sql.md)  
[DBCC DBREINDEX &#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-dbreindex-transact-sql.md)  
  
