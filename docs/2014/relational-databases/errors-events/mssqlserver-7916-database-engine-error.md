---
title: MSSQLSERVER_7916 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 7916 (Database Engine error)
ms.assetid: 9bac3536-de14-4e98-84c2-bde9a59ba0d1
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0eda0980b3b8ffbc748f15933ea397ae3d0b71e8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48134715"
---
# <a name="mssqlserver7916"></a>MSSQLSERVER_7916
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|7916|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBCC2_REPAIR_RECORD_DELETED|  
|Texto del mensaje|Reparación: se ha eliminado el registro para el Id. de objeto O_ID, Id. de índice I_ID, Id. de partición PN_ID, Id. de unidad de asignación A_ID (tipo TYPE), en la página P_ID, ranura S_ID. Se volverán a generar los índices.|  
  
## <a name="explanation"></a>Explicación  
 Este es un mensaje informativo de REPAIR que indica que el registro especificado se eliminó de la página.  
  
## <a name="user-action"></a>Acción del usuario  
 None  
  
  
