---
title: filestream access level (opción de configuración del servidor) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], access level
- filestream access level
ms.assetid: b88f6ff2-795e-4730-bfb8-dbc6a958f2ad
caps.latest.revision: 15
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c45a971793b03d30305adbb92d04e890f4dbc220
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="filestream-access-level-server-configuration-option"></a>filestream access level (opción de configuración del servidor)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Utilice la opción filestream_access_level para cambiar el nivel de acceso de FILESTREAM para esta instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Antes de que esta opción tenga cualquier efecto, debe estar habilitada la configuración de administración de Windows para FILESTREAM. Puede habilitar esta configuración al instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o utilizando el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Valor|Definición|  
|-----------|----------------|  
|0|Deshabilita la compatibilidad de FILESTREAM para esta instancia.|  
|1|Habilita FILESTREAM para el acceso a [!INCLUDE[tsql](../../includes/tsql-md.md)] .|  
|2|Habilita FILESTREAM para el acceso de transmisión por secuencias a [!INCLUDE[tsql](../../includes/tsql-md.md)] y Win32.|  
  
## <a name="see-also"></a>Ver también  
 [Configuración del motor de base de datos - Secuencia de archivo](http://msdn.microsoft.com/library/641a10a1-ae52-4d26-8f1c-a032a4aeff02)   
 [Enable and Configure FILESTREAM](../../relational-databases/blob/enable-and-configure-filestream.md)  
  
  
