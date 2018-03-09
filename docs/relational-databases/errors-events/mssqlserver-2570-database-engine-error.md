---
title: MSSQLSERVER_2570 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 2570 (Database Engine error)
ms.assetid: 29800aa9-81aa-4371-992c-487dbb617f46
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8ae42b008eba97f129510c641e748528dae26bdf
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver2570"></a>MSSQLSERVER_2570
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|2570|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBCC_COLUMN_VALUE_OUT_OF_RANGE|  
|Texto del mensaje|Página P_ID, zona S_ID en el Id. de objeto O_ID, Id. de índice I_ID, Id. de partición PN_ID, Id. de unidad de asignación A_ID (tipo TYPE). El valor de la columna COLUMN_NAME está fuera del intervalo del tipo de datos "DATATYPE". Actualice la columna de forma que contenga un valor válido.|  
  
## <a name="explanation"></a>Explicación  
El valor de columna incluido en la columna especificada está fuera del intervalo de valores posibles del tipo de datos de columna.  
  
## <a name="user-action"></a>Acción del usuario  
Este error es irreparable. Actualice la columna con un valor que se encuentre dentro del intervalo del tipo de datos de la columna y vuelva a ejecutar el comando.  Para obtener más información, vea este artículo de KB [923247](http://support.microsoft.com/kb/923247).  
  
## <a name="see-also"></a>Vea también  
[UPDATE &#40;Transact-SQL&#41;](~/t-sql/queries/update-transact-sql.md)  
[Tipos de datos &#40;Transact-SQL&#41;](~/t-sql/data-types/data-types-transact-sql.md)  
  
