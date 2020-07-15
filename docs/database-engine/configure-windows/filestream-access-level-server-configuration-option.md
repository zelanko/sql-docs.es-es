---
title: filestream access level (opción de configuración del servidor) | Microsoft Docs
description: Familiarícese con la opción "filestream_access_level". Vea cómo cambia el nivel de acceso FILESTREAM para una instancia de SQL Server.
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], access level
- filestream access level
ms.assetid: b88f6ff2-795e-4730-bfb8-dbc6a958f2ad
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b891ba283acb1176a60bcc64105e126192aa8225
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85772461"
---
# <a name="filestream-access-level-server-configuration-option"></a>filestream access level (opción de configuración del servidor)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Utilice la opción filestream_access_level para cambiar el nivel de acceso de FILESTREAM para esta instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Antes de que esta opción tenga cualquier efecto, debe estar habilitada la configuración de administración de Windows para FILESTREAM. Puede habilitar esta configuración al instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o utilizando el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Value|Definición|  
|-----------|----------------|  
|0|Deshabilita la compatibilidad de FILESTREAM para esta instancia.|  
|1|Habilita FILESTREAM para el acceso a [!INCLUDE[tsql](../../includes/tsql-md.md)] .|  
|2|Habilita FILESTREAM para el acceso de transmisión por secuencias a [!INCLUDE[tsql](../../includes/tsql-md.md)] y Win32.|  
  
## <a name="see-also"></a>Consulte también  
 [Configuración del motor de base de datos - Secuencia de archivo](https://msdn.microsoft.com/library/641a10a1-ae52-4d26-8f1c-a032a4aeff02)   
 [Enable and Configure FILESTREAM](../../relational-databases/blob/enable-and-configure-filestream.md)  
  
  
