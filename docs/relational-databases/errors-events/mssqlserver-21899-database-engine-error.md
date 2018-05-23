---
title: MSSQLSERVER_21899 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 21899 (Database Engine error)
ms.assetid: 32b87a7c-5380-4638-b147-dd78618f6625
caps.latest.revision: 6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: eef2d234f855441e5a7d1465105c2b30aedbec74
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2018
---
# <a name="mssqlserver21899"></a>MSSQLSERVER_21899
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|21899|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SQLErrorNum21899|  
|Texto del mensaje|La consulta en el publicador redireccionado '%s' para determinar si hay entradas de sysserver para los suscriptores del publicador original '%s' no se ha realizado por el error '%d', mensaje de error '%s.|  
  
## <a name="explanation"></a>Explicación  
**sp_validate_redirected_publisher** consulta a las tablas de metadatos de suscripción de la base de datos del publicador en el servidor remoto para determinar sus suscriptores asociados. Se devuelve el error 21899 si no se puede realizar esta consulta. La consulta de validación requiere acceso a la base de datos publicada en el publicador redirigido. Si el inicio de sesión especificado cuando se llama a **sp_adddistpublisher** para el publicador original no está autorizado a acceder a la base de datos publicada en el publicador redirigido, se devuelve el error 21899.  
  
## <a name="user-action"></a>Acción del usuario  
Revise el mensaje de error citado para determinar la causa del error y llevar a cabo una acción correctora adecuada  
  
