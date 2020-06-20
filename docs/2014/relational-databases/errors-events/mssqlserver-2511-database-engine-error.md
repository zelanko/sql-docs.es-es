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
ms.openlocfilehash: 23e91b0d64140329639cf57f3a336cd2eab8e4e8
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85034514"
---
# <a name="mssqlserver_2511"></a>MSSQLSERVER_2511
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|2511|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBCC_KEYS_OUT_OF_ORDER|  
|Texto del mensaje|Error de tabla: id. de objeto %d, id. de índice %d, id. de partición %I64d, id. de unidad de asignación %I64d (tipo %.*ls). Las claves no están ordenadas en la página %S_PGID, zonas %d y %d.|  
  
## <a name="explanation"></a>Explicación  
 Se detectaron claves desordenadas en el índice especificado. La página en la que están las claves puede estar dañada.  
  
## <a name="user-action"></a>Acción del usuario  
 Vuelva a generar el índice especificado usando la instrucción ALTER INDEX REBUILD.  
  
  
