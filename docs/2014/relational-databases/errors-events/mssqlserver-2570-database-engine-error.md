---
title: MSSQLSERVER_2570 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 2570 (Database Engine error)
ms.assetid: 29800aa9-81aa-4371-992c-487dbb617f46
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5169e030246b8f5a834e6a2526232907a7e22526
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62914434"
---
# <a name="mssqlserver2570"></a>MSSQLSERVER_2570
    
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
 Este error es irreparable. Actualice la columna con un valor que se encuentre dentro del intervalo del tipo de datos de la columna y vuelva a ejecutar el comando.  Para obtener más información, vea este artículo de KB [923247](https://support.microsoft.com/kb/923247).  
  
## <a name="see-also"></a>Vea también  
 [UPDATE &#40;Transact-SQL&#41;](/sql/t-sql/queries/update-transact-sql)   
 [Tipos de datos &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)  
  
  
