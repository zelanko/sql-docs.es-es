---
title: MSSQLSERVER_2530 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
ms.assetid: 5d4be07a-38a5-4b25-819c-4dcb4636cc15
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8058c7c31c49935d244726bf9e8ea0ac6cfbe750
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62914576"
---
# <a name="mssqlserver_2530"></a>MSSQLSERVER_2530
    
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
 [Habilitar índices y restricciones](../indexes/enable-indexes-and-constraints.md)   
 [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)   
 [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)   
 [DBCC DBREINDEX &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-dbreindex-transact-sql)  
  
  
