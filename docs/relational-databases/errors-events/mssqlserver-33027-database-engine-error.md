---
title: MSSQLSERVER_33027 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 33027 (Database Engine error)
ms.assetid: bfdc626e-7958-4511-987d-3b687824e8af
caps.latest.revision: 11
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e7d9b03347fb6ca83827854f4af0b75e8accc131
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37190955"
---
# <a name="mssqlserver33027"></a>MSSQLSERVER_33027
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|33027|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SEC_CRYPTOPROV_CANTLOADDLL|  
|Texto del mensaje|No se pudo cargar el proveedor de servicios criptográficos '%.*ls' debido a una firma Authenticode o una ruta de archivo no válida. Revise los mensajes de otros errores anteriores.|  
  
## <a name="explanation"></a>Explicación  
SQL Server no ha podido utilizar el proveedor de servicios criptográficos enumerado en el mensaje de error porque SQL Server no ha podido cargar la DLL. O el nombre no es válido o la firma Authenticode no es válida.  
  
## <a name="user-action"></a>Acción del usuario  
Compruebe que el archivo está presente y SQL Server tiene permiso de acceso a esa ubicación. Compruebe el registro de errores para ver posibles mensajes relacionados adicionales. De lo contrario, póngase en contacto con el proveedor de servicios criptográficos para obtener más información.  
  
