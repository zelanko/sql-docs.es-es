---
title: MSSQLSERVER_7916 | Microsoft Docs
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
helpviewer_keywords: 7916 (Database Engine error)
ms.assetid: 9bac3536-de14-4e98-84c2-bde9a59ba0d1
caps.latest.revision: "16"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 623e22492ef6cc668f1ddacdfa2d3a4974fc1336
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver7916"></a>MSSQLSERVER_7916
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|7916|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBCC2_REPAIR_RECORD|  
|Texto del mensaje|Reparación: se ha eliminado el registro para el Id. de objeto O_ID, Id. de índice I_ID, Id. de partición PN_ID, Id. de unidad de asignación A_ID (tipo TYPE), en la página P_ID, ranura S_ID. Se volverán a generar los índices.|  
  
## <a name="explanation"></a>Explicación  
Este es un mensaje informativo de REPAIR que indica que el registro especificado se eliminó de la página.  
  
## <a name="user-action"></a>Acción del usuario  
Ninguno  
  
