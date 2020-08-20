---
description: Espacios de nombres del modelo de objetos de SMO
title: Espacios de nombres SMO | Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- object models [SMO]
- SMO [SQL Server], namespaces
- namespaces [SMO]
- SQL Server Management Objects, namespaces
ms.assetid: 7bfabe4d-9f4c-4bc9-b998-93bd2b50ee8a
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f5e2c5b4574e03ed8820f3d9bfe307fe5a5c6e55
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88464950"
---
# <a name="smo-object-model-namespaces"></a>Espacios de nombres del modelo de objetos de SMO
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Los objetos de administración (SMO) tienen varios espacios de nombres. Los diferentes espacios de nombres representan áreas de funcionalidad diferentes dentro de los SMO.  
  
 En [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , los ensamblados SMO se encuentran en la carpeta c:\Archivos de programa\Microsoft SQL Server\130\SDK\Assemblies  
  
## <a name="namespaces"></a>Espacios de nombres  
 Los espacios de nombres de SMO son los siguientes:  
  
|Clase|Función|  
|-----------|--------------|  
|<xref:Microsoft.SqlServer.Management.Smo>|Contiene clases de instancia, clases de utilidad y enumeraciones que se utilizan para manipular mediante programación [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|<xref:Microsoft.SqlServer.Management.Common>|Contiene las clases que son comunes a Replication Management Objects (RMO) y SMO, como clases de conexión.|  
|<xref:Microsoft.SqlServer.Management.Smo.Agent>|Contiene clases que representan el Agente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|<xref:Microsoft.SqlServer.Management.Smo.Wmi>|Contiene clases que representan el proveedor WMI.|  
|<xref:Microsoft.SqlServer.Management.Smo.RegisteredServers>|Contiene clases que representan el servidor registrado.|  
|<xref:Microsoft.SqlServer.Management.Smo.Mail>|Contiene clases que representan el correo electrónico de base de datos.|  
|<xref:Microsoft.SqlServer.Management.Smo.Broker>|Contiene clases que representan el [!INCLUDE[ssSB](../../includes/sssb-md.md)].|  
  
  
