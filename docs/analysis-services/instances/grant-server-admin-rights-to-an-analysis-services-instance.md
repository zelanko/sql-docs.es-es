---
title: Conceder derechos de administrador de servidor a una instancia de Analysis Services | Documentos de Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- administrator rights [Analysis Services]
- server-wide administrative permissions [Analysis Services]
ms.assetid: 20d1234b-a457-4a84-ae08-fe356870c466
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b7d564225ff95de938df836f1fd49b85892e8ba3
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="grant-server-admin-rights-to-an--analysis-services-instance"></a>Conceder permisos de administrador de servidor (Analysis Services)
  Los miembros del rol de administrador de servidor dentro de una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tienen acceso no restringido a todos los datos y objetos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de dicha instancia. Un usuario debe ser miembro del rol de administrador de servidor para poder realizar cualquier tarea en el servidor, como crear o procesar una base de datos, modificar las propiedades del servidor o iniciar un seguimiento (que no sea para procesar eventos).  
  
 La pertenencia al rol se establece al instalar [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . El usuario que ejecuta el programa de instalación puede agregarse a sí mismo al rol, o agregar otros usuarios. Debe especificar al menos un administrador para que el programa de instalación le permita continuar.  
  
 De forma predeterminada, a los miembros del grupo local Administradores también se les conceden derechos administrativos en Analysis Server. Aunque no se concede explícitamente al grupo local la pertenencia al rol de administrador del servidor de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , los administradores locales pueden crear bases de datos, agregar usuarios y permisos, y realizar cualquier otra tarea permitida a los administradores del sistema. La concesión implícita de permisos de administrador es configurable. Está determinado por la propiedad de servidor **BuiltinAdminsAreServerAdmins** , que se establece en **true** de forma predeterminada. Puede cambiar esta propiedad en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para más información, consulte [Security Properties](../../analysis-services/server-properties/security-properties.md).  
  
 Con posterioridad a la instalación, puede modificar la pertenencia a un rol para agregar usuarios adicionales que necesiten derechos completos para el servicio. También se pueden administrar roles de servidor mediante Objetos de administración de análisis (AMO). Para obtener más información, vea [Desarrollar con Objetos de administración de análisis &#40;AMO&#41;](../../analysis-services/multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]Proporciona una progresión de roles cada vez más granulares para el procesamiento y consulta en los niveles de servidor, base de datos y objeto. Para obtener instrucciones sobre cómo usar estos roles, vea [Roles y permisos &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/roles-and-permissions-analysis-services.md).  
  
## <a name="modify-server-role-membership"></a>Modificar la pertenencia al rol de servidor  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conéctese a la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], haga clic con el botón derecho en el nombre de la instancia en el Explorador de objetos y, después, haga clic en **Propiedades**.  
  
2.  Haga clic en **Seguridad** en el panel **Seleccionar una página** y, a continuación, haga clic en clic **Agregar** en la parte inferior de la página para agregar uno o más usuarios o grupos de Windows al rol de servidor.  
  
     ![Cuadro de diálogo Agregar usuarios en management studio](../../analysis-services/instances/media/ssas-serveradminadd.png "cuadro de diálogo Agregar usuarios en management studio")  
  
### <a name="add-computer-accounts"></a>Agregar cuentas de equipo  
 También puede utilizar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para convertir una cuenta de equipo en miembro del grupo de administradores de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
1.  En el cuadro de diálogo **Seleccionar usuarios o grupos** , haga clic en **Ubicaciones**.  
  
2.  Seleccione el dominio del que son miembros los equipos que quiere agregar o seleccione **Todo el directorio** y haga clic en **Aceptar**.  
  
3.  Haga clic en **Tipos de objeto**.  
  
4.  Seleccione **Equipos** y haga clic en **Aceptar**.  
  
     ![agregar cuentas de equipo como administradores de ssas](../../analysis-services/instances/media/ssas-in-ssms-computerobjects.png "agregar cuentas de equipo como administradores de ssas")  
  
5.  En el cuadro de texto **Escribir los nombres de objeto para seleccionar** , escriba el nombre del equipo y haga clic en **Comprobar nombres** para comprobar que la cuenta de equipo se encuentra en las ubicaciones actuales. Si no encuentra la cuenta de equipo, compruebe el nombre del equipo y que el dominio del que es miembro el equipo sea correcto.  
  
## <a name="nt-servicessastelemetry-account"></a>Cuenta de NT Service\SSASTelemetry  
 **Servicio NT/SSASTelemetry** es una cuenta de equipo con privilegios reducidos que se crea durante la instalación y se usa exclusivamente para ejecutar la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] del servicio Programa para la mejora de la experiencia del usuario (CEIP). Este servicio requiere derechos de administrador en la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para ejecutar varios comandos de detección. Vea [Customer Experience Improvement Program for SQL Server Data Tools](../../sql-server/customer-experience-improvement-program-for-sql-server-data-tools.md) y [Microsoft SQL Server Privacy Statement](http://msdn.microsoft.com/library/57769f4a-5689-49a1-8298-e3c0db5106f8) para obtener más información.  
  
## <a name="see-also"></a>Vea también  
 [Cómo autorizar el acceso a objetos y operaciones &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)   
 [Roles de seguridad &#40;Analysis Services - Datos multidimensionales&#41;](../../analysis-services/multidimensional-models/olap-logical/security-roles-analysis-services-multidimensional-data.md)  
  
  

