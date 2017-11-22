---
title: MSSQLSERVER_1904 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 1904 (Database Engine error)
ms.assetid: 2a35d57d-74e2-45a2-8f67-3f2e51d69712
caps.latest.revision: "9"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4f2267a8410f134aafad64634e9682e05b2ed466
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver1904"></a>MSSQLSERVER_1904
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|1904|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|KEYCOUNT|  
|Texto del mensaje|%S_MSG '%.*ls' en la tabla '%.\*ls' tiene %d nombres de columna en la lista de claves %S_MSG. El límite máximo para la lista de columnas de clave de índice o estadísticas es %d.|  
  
## <a name="explanation"></a>Explicación  
La lista de columnas de clave para el índice o estadística especificados supera el número máximo permitido de columnas.  
  
## <a name="user-action"></a>Acción del usuario  
Modifique la lista de columnas de clave para que no incluya más columnas del número máximo especificado.  
  
Con los índices no clúster, considere utilizar la cláusula INCLUDE en la instrucción CREATE INDEX para agregar columnas al índice como columnas sin clave. Este método impide superar la limitación de tamaño de índice actual de 16 columnas de clave como máximo. Para más información, consulte [Create Indexes with Included Columns](~/relational-databases/indexes/create-indexes-with-included-columns.md).  
  
## <a name="see-also"></a>Vea también  
[CREATE INDEX &#40;Transact-SQL&#41;](~/t-sql/statements/create-index-transact-sql.md)  
[CREATE STATISTICS &#40;Transact-SQL&#41;](~/t-sql/statements/create-statistics-transact-sql.md)  
  
