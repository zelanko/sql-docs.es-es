---
title: MSSQLSERVER_2511 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 2511 (Database Engine error)
ms.assetid: 9a00c0ed-eb4b-4fae-8016-192396006c37
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1748e8b483eecee43da921bd268d419408924af3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62868972"
---
# <a name="mssqlserver2511"></a>MSSQLSERVER_2511
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|2511|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBCC_KEYS_OUT_OF_ORDER|  
|Texto del mensaje|Error de tabla: Id. %d de objeto, índice Id. %d, partición Id. % I64d, Id. de unidad de asignación % I64d (tipo %. * ls). Las claves no están ordenadas en la página %S_PGID, zonas %d y %d.|  
  
## <a name="explanation"></a>Explicación  
 Se detectaron claves desordenadas en el índice especificado. La página en la que están las claves puede estar dañada.  
  
## <a name="user-action"></a>Acción del usuario  
 Vuelva a generar el índice especificado usando la instrucción ALTER INDEX REBUILD.  
  
  
