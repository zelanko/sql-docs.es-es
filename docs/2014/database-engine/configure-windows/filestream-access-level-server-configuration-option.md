---
title: filestream access level (opción de configuración del servidor) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], access level
- filestream access level
ms.assetid: b88f6ff2-795e-4730-bfb8-dbc6a958f2ad
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 90b4ec97a3ab31c93e92219b96724b75d7f86425
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62782260"
---
# <a name="filestream-access-level-server-configuration-option"></a>filestream access level (opción de configuración del servidor)
  Utilice la opción filestream_access_level para cambiar el nivel de acceso de FILESTREAM para esta instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Antes de que esta opción tenga cualquier efecto, debe estar habilitada la configuración de administración de Windows para FILESTREAM. Puede habilitar esta configuración al instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o utilizando el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Valor|Definición|  
|-----------|----------------|  
|0|Deshabilita la compatibilidad de FILESTREAM para esta instancia.|  
|1|Habilita FILESTREAM para el acceso a [!INCLUDE[tsql](../../includes/tsql-md.md)] .|  
|2|Habilita FILESTREAM para el acceso de transmisión por secuencias a [!INCLUDE[tsql](../../includes/tsql-md.md)] y Win32.|  
  
## <a name="see-also"></a>Vea también  
 [Configuración del motor de base de datos - Secuencia de archivo](../../sql-server/install/database-engine-configuration-filestream.md)   
 [Habilitar y configurar FILESTREAM](../../relational-databases/blob/enable-and-configure-filestream.md)  
  
  
