---
title: Archivos y números de versión | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0a1b0b28afbb83028af8d71644af08ca660a0b36
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62753417"
---
# <a name="files-and-version-numbers"></a>Archivos y números de versión
  Todos los [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] componentes de objetos de administración (SMO) necesarios se instalan como parte [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de una instancia de cliente o servidor. SMO se implementa en varios ensamblados administrados. Puede desarrollar aplicaciones SMO en un cliente o un servidor.  
  
|Directory|Archivo|Descripción|  
|---------------|----------|-----------------|  
|[!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)]|Microsoft.SqlServer.ConnectionInfo.dll|Contiene compatibilidad para conectar a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)]|Microsoft.SqlServer.ServiceBrokerEnum.dll|Contiene compatibilidad para programar [!INCLUDE[msCoName](../../includes/msconame-md.md)] Service Broker. Solo se requiere en programas que tienen acceso a Service Broker.|  
|[!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)]|Microsoft.SqlServer.Smo.dll|Contiene la mayoría de las clases SMO.|  
|[!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)]|Microsoft.SqlServer.SmoExtended.dll<br /><br /> Microsoft.SqlServer.Management.Sdk.Sfc.dll<br /><br /> Microsoft.SqlServer.SqlEnum.dll|Contiene compatibilidad para las clases SMO.|  
|[!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)]|Microsoft.SqlServer.WmiEnum.dll|Contiene las clases de proveedor de Instrumental de administración de Windows (WMI). Solo se requiere en los programas que utilizan las clases del proveedor WMI.|  
|[!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)]|Microsoft.SqlServer.RegSvrEnum.dll|Contiene las clases de servidor registrado. Solo se requiere en los programas que utilizan las clases de servidor registrado.|  
  
  
