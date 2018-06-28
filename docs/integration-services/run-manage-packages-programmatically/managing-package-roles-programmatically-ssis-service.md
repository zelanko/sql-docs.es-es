---
title: Administrar roles de paquete mediante programación (servicio SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
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
manager: craigg
ms.openlocfilehash: 79a5fe202e292e6684a75d8aceae3f9ab53e37db
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/12/2018
ms.locfileid: "35403907"
---
# <a name="managing-package-roles-programmatically-ssis-service"></a>Administrar roles de paquete mediante programación (servicio SSIS)
  Cuando trabaja mediante programación con paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], puede determinar qué roles están disponibles para aplicar a los paquetes o bien determinar o establecer los roles que se aplican a un paquete individual. La clase <xref:Microsoft.SqlServer.Dts.Runtime.Application> del espacio de nombres <xref:Microsoft.SqlServer.Dts.Runtime> proporciona diferentes métodos para satisfacer estos requisitos.  
  
 Los roles se aplican solo a paquetes almacenados en la base de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **msdb**. Para obtener más información acerca de los roles de paquete, consulte [Integration Services Roles &#40;SSIS Service&#41; (Roles de Integration Services &#40;servicio SSIS&#41;)](../../integration-services/security/integration-services-roles-ssis-service.md).  
  
 Todos los métodos descritos en este tema requieren que se haga una referencia al ensamblado **Microsoft.SqlServer.ManagedDTS**. Después de agregar la referencia en un proyecto nuevo, importe el espacio de nombres <xref:Microsoft.SqlServer.Dts.Runtime> mediante una instrucción **using** o **Imports**.  
  
> [!IMPORTANT]  
>  Los métodos de la clase <xref:Microsoft.SqlServer.Dts.Runtime.Application> para trabajar con el almacén de paquetes SSIS solamente admiten ".", localhost o el nombre del servidor local. No puede utilizar "(local)".  
  
## <a name="determining-which-roles-are-available"></a>Determinar los roles disponibles  
 Para determinar qué roles están disponibles para los paquetes almacenados en un servidor determinado, llame al método <xref:Microsoft.SqlServer.Dts.Runtime.Application.GetDtsServerRoles%2A> de la clase <xref:Microsoft.SqlServer.Dts.Runtime.Application>.  
  
## <a name="determining-which-roles-are-assigned"></a>Determinar los roles asignados  
 Para determinar qué roles se han asignado ya a un paquete determinado, llame al método <xref:Microsoft.SqlServer.Dts.Runtime.Application.GetPackageRoles%2A>. Para asignar roles a un paquete, llame al método <xref:Microsoft.SqlServer.Dts.Runtime.Application.SetPackageRoles%2A>.  
  
## <a name="see-also"></a>Ver también  
 [Roles de Integration Services &#40;servicio SSIS&#41;](../../integration-services/security/integration-services-roles-ssis-service.md)  
  
  
