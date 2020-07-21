---
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
ms.openlocfilehash: 192e3b98e7091ba337fa1b0090c6add2a255a97a
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "86012279"
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
  
  
