---
title: Modelo de objetos SMO | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
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
- SMO [SQL Server], object model
- SQL Server Management Objects, object model
ms.assetid: bd6e59b6-ca46-42c0-adb2-c9d64cf6e00b
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: e3bc9ec53d5550f8671b7ac9bb786ae9d631f6df
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="smo-object-model"></a>Modelo de objetos SMO
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  El modelo de objetos SMO se compone de una jerarquía de objetos. El objeto <xref:Microsoft.SqlServer.Management.Smo.Server> es el objeto de nivel superior y todos los objetos de clase de instancia se encuentran debajo del objeto <xref:Microsoft.SqlServer.Management.Smo.Server>.  
  
 La clase <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer> es una clase de nivel superior con una jerarquía de objeto independiente. El <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer> objeto representa [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servicios y la configuración de red disponible a través del proveedor de WMI.  
  
 Además de los objetos <xref:Microsoft.SqlServer.Management.Smo.Server> y <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer>, hay varias clases de utilidad que representan tareas u operaciones, como <xref:Microsoft.SqlServer.Management.Smo.Transfer>, <xref:Microsoft.SqlServer.Management.Smo.Backup> o <xref:Microsoft.SqlServer.Management.Smo.Restore>  
  
 El modelo de objetos SMO se compone de varios espacios de nombres. Para más información, vea [Espacios de nombres SMO](../../relational-databases/server-management-objects-smo/smo-object-model-namespaces.md).  
  
## <a name="see-also"></a>Vea también  
 [Diagrama del modelo de objetos de SMO](../../relational-databases/server-management-objects-smo/smo-object-model-diagram.md)   
 [Espacios de nombres SMO](../../relational-databases/server-management-objects-smo/smo-object-model-namespaces.md)   
 [Conceptos del proveedor WMI de administración de configuración](../../relational-databases/wmi-provider-configuration/wmi-provider-for-configuration-management.md)  
  
  
