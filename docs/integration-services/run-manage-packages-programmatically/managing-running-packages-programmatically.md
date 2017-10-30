---
title: "Administrar paquetes en ejecución mediante programación | Documentos de Microsoft"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- packages [Integration Services], managing
- running packages [Integration Services]
ms.assetid: 0e91f4ac-6f29-40d7-8c28-9b82e4802c35
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: 34f2c773e89c0162df5d13a16d27f01eb5d8f4df
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="managing-running-packages-programmatically"></a>Administrar los paquetes en ejecución mediante programación
  Cuando trabaja con paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] mediante programación, puede que desee determinar los paquetes que se están ejecutando en ese momento. La clase <xref:Microsoft.SqlServer.Dts.Runtime.Application> del espacio de nombres <xref:Microsoft.SqlServer.Dts.Runtime> proporciona métodos y clases para satisfacer estos requisitos.  
  
 Para obtener más información sobre cómo supervisar paquetes, vea [administración de paquetes &#40; Servicio SSIS &#41; ](../../integration-services/service/package-management-ssis-service.md).  
  
 Todos los métodos descritos en este tema requieren una referencia a la **Microsoft.SqlServer.ManagedDTS** ensamblado. Después de agregar la referencia en un proyecto nuevo, importe la <xref:Microsoft.SqlServer.Dts.Runtime> espacio de nombres con un **con** o **importaciones** instrucción.  
  
> [!IMPORTANT]  
>  Los métodos de la <xref:Microsoft.SqlServer.Dts.Runtime.Application> clase para trabajar con el almacén de paquetes SSIS solo admiten ".", localhost o el nombre del servidor local. No puede utilizar "(local)".  
  
## <a name="determining-which-packages-are-currently-running"></a>Determinar los paquetes que se están ejecutando  
 Para determinar qué paquetes se están ejecutando actualmente en el servidor especificado, llame al método <xref:Microsoft.SqlServer.Dts.Runtime.Application.GetRunningPackages%2A>. Este método devuelve una colección <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackages> de objetos <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage>.  
  
> [!NOTE]  
>  Los administradores ven todos los paquetes que se están ejecutando actualmente en el equipo; el resto de usuarios solamente ve los paquetes que han iniciado ellos mismos.  
  
## <a name="working-with-running-packages"></a>Trabajar con paquetes en ejecución  
 Una vez determinados los paquetes que se están ejecutando actualmente, puede recuperar información sobre los paquetes y solicitar que se detenga un paquete.  
  
### <a name="getting-information-about-a-running-package"></a>Obtener información sobre un paquete en ejecución  
 Al recorrer en iteración la colección <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackages>, puede utilizar las propiedades del objeto <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage> para buscar un paquete u obtener información adicional sobre los paquetes que se están ejecutando:  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.ExecutionDuration%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.ExecutionStartTime%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.InstanceID%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.PackageDescription%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.PackageID%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.PackageName%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.UserName%2A>  
  
### <a name="stopping-a-running-package"></a>Detener un paquete en ejecución  
 Puede llamar al método <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.Stop%2A> de un objeto <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage> para solicitar que se detenga el paquete. Es posible que se produzca un retraso entre el momento en el que se emite una solicitud de detención y el momento en el que realmente se detiene el paquete.  
  
## <a name="see-also"></a>Vea también  
 [Administración de paquetes &#40; Servicio SSIS &#41;](../../integration-services/service/package-management-ssis-service.md)   
 [Enumerar los paquetes disponibles mediante programación](../../integration-services/run-manage-packages-programmatically/enumerating-available-packages-programmatically.md)  
  
  

