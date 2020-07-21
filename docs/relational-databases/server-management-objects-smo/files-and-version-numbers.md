---
title: Archivos y números de versión | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, versions
- components [SMO]
- files [SMO], components
- SMO [SQL Server], versions
- versions [SMO]
ms.assetid: 510907b6-e7a9-41bd-b892-d6d99a5118e1
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6d682ca3d6768da16d43c3c09471a6c722561dd3
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "86008628"
---
# <a name="files-and-version-numbers"></a>Archivos y números de versión
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  Todos los componentes de objetos de administración de SQL Server (SMO) necesarios se incluyen en el paquete NuGet Microsoft. SqlServer. SqlManagementObjects. SMO se implementa en varios ensamblados administrados. Puede desarrollar aplicaciones SMO en un cliente o un servidor.  

> > [!Important]
> > La versión de archivo de los ensamblados SMO se muestra como principal. **0**. Compilación. revisión. Pero la versión del ensamblado incrustado es principal. **100**. Compilación. revisión. Esto se hace para mantener la versión de SMO usada en cada aplicación independiente, de modo que las actualizaciones a una no afecten a ninguna otra.
> > 
> > Debido a esto, **no** debe instalar estas versiones de los ensamblados en la caché de ensamblados global (GAC). Esto podría hacer que otras aplicaciones, como [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Studio, se interrumpan. 
  
|Archivo|Descripción|  
|-----------|-----------------|  
|Microsoft.SqlServer.ConnectionInfo.dll|Contiene compatibilidad para conectar a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|Microsoft.SqlServer.ServiceBrokerEnum.dll|Contiene compatibilidad para programar [!INCLUDE[msCoName](../../includes/msconame-md.md)] Service Broker. Solo se requiere en programas que tienen acceso a Service Broker.|  
|Microsoft.SqlServer.Smo.dll|Contiene la mayoría de las clases SMO.|  
|Microsoft.SqlServer.SmoExtended.dll<br /><br /> Microsoft.SqlServer.Management.Sdk.Sfc.dll<br /><br /> Microsoft.SqlServer.SqlEnum.dll|Contiene compatibilidad para las clases SMO.|  
|Microsoft.SqlServer.WmiEnum.dll|Contiene las clases de proveedor de Instrumental de administración de Windows (WMI). Solo se requiere en los programas que utilizan las clases del proveedor WMI.|  
|Microsoft.SqlServer.RegSvrEnum.dll|Contiene las clases de servidor registrado. Solo se requiere en los programas que utilizan las clases de servidor registrado.|  
  
  
