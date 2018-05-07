---
title: Archivos y números de versión | Documentos de Microsoft
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: smo
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, versions
- components [SMO]
- files [SMO], components
- SMO [SQL Server], versions
- versions [SMO]
ms.assetid: 510907b6-e7a9-41bd-b892-d6d99a5118e1
caps.latest.revision: 34
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 10e11076ce023a3d969b4ba95a30c15de43eafa6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="files-and-version-numbers"></a>Archivos y números de versión
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  Todas las necesarias componentes de objeto de administración de SQL Server (SMO) se incluyen en el paquete de Microsoft.SqlServer.SqlManagementObjects NuGet. SMO se implementa en varios ensamblados administrados. Puede desarrollar aplicaciones SMO en un cliente o un servidor.  

>>[!Important]
La versión del archivo de los ensamblados SMO se muestra como principal. **0**. Build.Revision. Pero la versión de ensamblado integrada es principal. **100**. Build.Revision. Esto se hace para conservar la versión de SMO que se usan en cada aplicación independiente para las actualizaciones en uno no afecta a los demás.
>>
>>Por este motivo, debe **no** instala estas versiones de los ensamblados a la caché de ensamblados Global (GAC). Si lo hace, podría hacer que otras aplicaciones, como [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Studio, se interrumpa. 
  
|Archivo|Description|  
|-----------|-----------------|  
|Microsoft.SqlServer.ConnectionInfo.dll|Contiene compatibilidad para conectar a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|Microsoft.SqlServer.ServiceBrokerEnum.dll|Contiene compatibilidad para programar [!INCLUDE[msCoName](../../includes/msconame-md.md)] Service Broker. Solo se requiere en programas que tienen acceso a Service Broker.|  
|Microsoft.SqlServer.Smo.dll|Contiene la mayoría de las clases SMO.|  
|Microsoft.SqlServer.SmoExtended.dll<br /><br /> Microsoft.SqlServer.Management.Sdk.Sfc.dll<br /><br /> Microsoft.SqlServer.SqlEnum.dll|Contiene compatibilidad para las clases SMO.|  
|Microsoft.SqlServer.WmiEnum.dll|Contiene las clases de proveedor de Instrumental de administración de Windows (WMI). Solo se requiere en los programas que utilizan las clases del proveedor WMI.|  
|Microsoft.SqlServer.RegSvrEnum.dll|Contiene las clases de servidor registrado. Solo se requiere en los programas que utilizan las clases de servidor registrado.|  
  
  
