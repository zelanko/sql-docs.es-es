---
title: "Administrar Roles de paquete mediante programación (servicio SSIS) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: run-manage-packages-programmatically
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Integration Services packages, roles
- roles [Integration Services]
- packages [Integration Services], roles
ms.assetid: 2e0ca0d5-d4f5-421d-b17d-a48b37b923e5
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: 7a7fb000389756caf0c2f2ea00cd0b80e75557d8
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="managing-package-roles-programmatically-ssis-service"></a>Administrar roles de paquete mediante programación (servicio SSIS)
  Cuando trabaja mediante programación con paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], puede determinar qué roles están disponibles para aplicar a los paquetes o bien determinar o establecer los roles que se aplican a un paquete individual. La clase <xref:Microsoft.SqlServer.Dts.Runtime.Application> del espacio de nombres <xref:Microsoft.SqlServer.Dts.Runtime> proporciona diferentes métodos para satisfacer estos requisitos.  
  
 Roles se aplican solo a paquetes almacenados en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **msdb** base de datos. Para obtener más información acerca de los roles de paquete, consulte [Roles de Integration Services &#40; Servicio SSIS &#41; ](../../integration-services/security/integration-services-roles-ssis-service.md).  
  
 Todos los métodos descritos en este tema requieren una referencia a la **Microsoft.SqlServer.ManagedDTS** ensamblado. Después de agregar la referencia en un proyecto nuevo, importe la <xref:Microsoft.SqlServer.Dts.Runtime> espacio de nombres mediante el uso de un **con** o **importaciones** instrucción.  
  
> [!IMPORTANT]  
>  Los métodos de la <xref:Microsoft.SqlServer.Dts.Runtime.Application> clase para trabajar con el almacén de paquetes SSIS solo admiten ".", localhost o el nombre del servidor local. No puede utilizar "(local)".  
  
## <a name="determining-which-roles-are-available"></a>Determinar los roles disponibles  
 Para determinar qué roles están disponibles para los paquetes almacenados en un servidor determinado, llame al método <xref:Microsoft.SqlServer.Dts.Runtime.Application.GetDtsServerRoles%2A> de la clase <xref:Microsoft.SqlServer.Dts.Runtime.Application>.  
  
## <a name="determining-which-roles-are-assigned"></a>Determinar los roles asignados  
 Para determinar qué roles se han asignado ya a un paquete determinado, llame al método <xref:Microsoft.SqlServer.Dts.Runtime.Application.GetPackageRoles%2A>. Para asignar roles a un paquete, llame al método <xref:Microsoft.SqlServer.Dts.Runtime.Application.SetPackageRoles%2A>.  
  
## <a name="see-also"></a>Vea también  
 [Integración de servicios de Roles &#40; Servicio SSIS &#41;](../../integration-services/security/integration-services-roles-ssis-service.md)  
  
  

