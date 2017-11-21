---
title: MSSQLSERVER_1807 | Microsoft Docs
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
- 1807 (Database Engine error)
ms.assetid: 13c1b240-098b-4d9e-89aa-21599548e074
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: e7102630e638d891345c47ed8d9f92700fde39aa
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver1807"></a>MSSQLSERVER_1807
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|1807|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|CANNOT_EX_LOCK|  
|Texto del mensaje|No se puede obtener un bloqueo exclusivo en la base de datos '%.*ls'. Intente la operación en otro momento.|  
  
## <a name="explanation"></a>Explicación  
Una operación que necesita acceso exclusivo a la base de datos no pudo obtenerlo.  
  
## <a name="user-action"></a>Acción del usuario  
Desconecte todas las conexiones a esa base de datos o vuelva a intentar ejecutar la consulta en otro momento.  
  

