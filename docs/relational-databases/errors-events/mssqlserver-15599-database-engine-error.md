---
title: MSSQLSERVER_15599 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 15599 (Database Engine error)
ms.assetid: 97e427a9-8587-46ea-954b-974b5df9c223
caps.latest.revision: 8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 01ad3f136b948fc9d62d863a91c9c1b9a571edea
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver15599"></a>MSSQLSERVER_15599
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|15599|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SEC_LOCAL_TEMP_AUDIT_PERMISSIONS|  
|Texto del mensaje|No se pueden establecer permisos ni auditoría y en objetos temporales locales.|  
  
## <a name="explanation"></a>Explicación  
La auditoría y los permisos no tienen ningún efecto cuando se establecen en objetos locales o globales temporales. Las instrucciones no producen un error (las operaciones vuelven correctamente), pero no tienen ningún efecto.  
  
Este comportamiento no ha cambiado, pero a partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], este mensaje informativo alerta al usuario.  
  
## <a name="user-action"></a>Acción del usuario  
No es necesaria ninguna acción, pero considere la posibilidad de quitar las instrucciones que intentan establecer la auditoría o los permisos en objetos locales o globales temporales.  
  
