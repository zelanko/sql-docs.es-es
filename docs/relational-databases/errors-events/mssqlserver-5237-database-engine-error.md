---
title: MSSQLSERVER_5237 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 5237 (Database Engine error)
ms.assetid: 9ff28935-d1eb-47ee-99b3-1a65cb948ce7
caps.latest.revision: "17"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: eafae8fdc25989aaec7ea987d5e72ed7a9221e93
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver5237"></a>MSSQLSERVER_5237
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|5237|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBCC4_INDEXED_VIEW_CHECK_QUERY_FAILED_NO_ERRORCODE|  
|Texto del mensaje|Error de comprobación del conjunto de filas cruzadas de DBCC para el objeto 'NAME' (Id. de objeto O_ID) debido a un error de consulta interno.|  
  
## <a name="explanation"></a>Explicación  
Un error interno ha provocado que DBCC no pueda ejecutar la consulta para comprobar las vistas indizadas.  
  
## <a name="user-action"></a>Acción del usuario  
Vuelva a ejecutar el comando DBCC.  
  
