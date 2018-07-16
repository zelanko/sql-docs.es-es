---
title: Administrar roles de paquete mediante programación (servicio SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- integration-services
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- Integration Services packages, roles
- roles [Integration Services]
- packages [Integration Services], roles
ms.assetid: 2e0ca0d5-d4f5-421d-b17d-a48b37b923e5
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: bd0ffb7426ddcf3a816fbad8a414c7c156c72aee
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37311985"
---
# <a name="managing-package-roles-programmatically-ssis-service"></a>Administrar roles de paquete mediante programación (servicio SSIS)
  Cuando trabaja mediante programación con paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], puede determinar qué roles están disponibles para aplicar a los paquetes o bien determinar o establecer los roles que se aplican a un paquete individual. La clase <xref:Microsoft.SqlServer.Dts.Runtime.Application> del espacio de nombres <xref:Microsoft.SqlServer.Dts.Runtime> proporciona diferentes métodos para satisfacer estos requisitos.  
  
 Los roles se aplican solo a paquetes almacenados en la base de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **msdb**. Para obtener más información acerca de los roles de paquete, consulte [Integration Services Roles &#40;SSIS Service&#41; (Roles de Integration Services &#40;servicio SSIS&#41;)](../security/integration-services-roles-ssis-service.md).  
  
 Todos los métodos descritos en este tema requieren una referencia al ensamblado `Microsoft.SqlServer.ManagedDTS`. Después de agregar la referencia en un proyecto nuevo, importe el espacio de nombres <xref:Microsoft.SqlServer.Dts.Runtime> mediante una instrucción `using` o `Imports`.  
  
> [!IMPORTANT]  
>  Los métodos de la clase <xref:Microsoft.SqlServer.Dts.Runtime.Application> para trabajar con el almacén de paquetes SSIS solamente admiten ".", localhost o el nombre del servidor local. No puede utilizar "(local)".  
  
## <a name="determining-which-roles-are-available"></a>Determinar los roles disponibles  
 Para determinar qué roles están disponibles para los paquetes almacenados en un servidor determinado, llame al método <xref:Microsoft.SqlServer.Dts.Runtime.Application.GetDtsServerRoles%2A> de la clase <xref:Microsoft.SqlServer.Dts.Runtime.Application>.  
  
## <a name="determining-which-roles-are-assigned"></a>Determinar los roles asignados  
 Para determinar qué roles se han asignado ya a un paquete determinado, llame al método <xref:Microsoft.SqlServer.Dts.Runtime.Application.GetPackageRoles%2A>. Para asignar roles a un paquete, llame al método <xref:Microsoft.SqlServer.Dts.Runtime.Application.SetPackageRoles%2A>.  
  
![Icono de Integration Services (pequeño)](../media/dts-16.gif "icono de Integration Services (pequeño)")**mantenerse actualizado con Integration Services  **<br /> Para obtener las descargas, artículos, ejemplos y vídeos más recientes de Microsoft, así como soluciones seleccionadas de la comunidad, visite la página de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en MSDN:<br /><br /> [Visite la página de Integration Services en MSDN](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para recibir notificaciones automáticas de estas actualizaciones, suscríbase a las fuentes RSS disponibles en la página.  
  
## <a name="see-also"></a>Vea también  
 [Roles de Integration Services &#40;servicio SSIS&#41;](../security/integration-services-roles-ssis-service.md)  
  
  
