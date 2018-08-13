---
title: Espacios de nombres SMO | Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: smo
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- object models [SMO]
- SMO [SQL Server], namespaces
- namespaces [SMO]
- SQL Server Management Objects, namespaces
ms.assetid: 7bfabe4d-9f4c-4bc9-b998-93bd2b50ee8a
caps.latest.revision: 39
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 9688b97d469e9ec3687c9d005d776987785ebc5d
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39550395"
---
# <a name="smo-object-model-namespaces"></a>Espacios de nombres del modelo de objetos de SMO
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Los objetos de administración (SMO) tienen varios espacios de nombres. Los diferentes espacios de nombres representan áreas de funcionalidad diferentes dentro de los SMO.  
  
 En [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], los ensamblados SMO se encuentran en la carpeta C:\Program Files\Microsoft SQL Server\130\SDK\Assemblies\.  
  
## <a name="namespaces"></a>Espacios de nombres  
 Los espacios de nombres de SMO son los siguientes:  
  
|Clase|Función|  
|-----------|--------------|  
|<xref:Microsoft.SqlServer.Management.Smo>|Contiene clases de instancia, las clases de utilidad y enumeraciones que se utilizan para manipular mediante programación [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|<xref:Microsoft.SqlServer.Management.Common>|Contiene las clases que son comunes a Replication Management Objects (RMO) y SMO, como clases de conexión.|  
|<xref:Microsoft.SqlServer.Management.Smo.Agent>|Contiene clases que representan el Agente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|<xref:Microsoft.SqlServer.Management.Smo.Wmi>|Contiene clases que representan el proveedor WMI.|  
|<xref:Microsoft.SqlServer.Management.Smo.RegisteredServers>|Contiene clases que representan el servidor registrado.|  
|<xref:Microsoft.SqlServer.Management.Smo.Mail>|Contiene clases que representan el correo electrónico de base de datos.|  
|<xref:Microsoft.SqlServer.Management.Smo.Broker>|Contiene clases que representan el [!INCLUDE[ssSB](../../includes/sssb-md.md)].|  
  
  
