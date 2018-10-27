---
title: Conceder permisos de administrador del servidor a una instancia de Analysis Services | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e437507d139959c21f723f8a674ca4879570339f
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/26/2018
ms.locfileid: "50145680"
---
# <a name="grant-server-admin-rights-to-an--analysis-services-instance"></a>Conceder permisos de administrador de servidor (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Los miembros del rol de administrador de servidor dentro de una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tienen acceso no restringido a todos los datos y objetos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de dicha instancia. Un usuario debe ser miembro del rol de administrador de servidor para poder realizar cualquier tarea en el servidor, como crear o procesar una base de datos, modificar las propiedades del servidor o iniciar un seguimiento (que no sea para procesar eventos).  
  
 La pertenencia al rol se establece al instalar [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . El usuario que ejecuta el programa de instalación puede agregarse a sí mismo al rol, o agregar otros usuarios. Debe especificar al menos un administrador para que el programa de instalación le permita continuar.  
  
 De forma predeterminada, a los miembros del grupo local Administradores también se les conceden derechos administrativos en Analysis Server. Aunque no se concede explícitamente al grupo local la pertenencia al rol de administrador del servidor de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , los administradores locales pueden crear bases de datos, agregar usuarios y permisos, y realizar cualquier otra tarea permitida a los administradores del sistema. La concesión implícita de permisos de administrador es configurable. Está determinado por la propiedad de servidor **BuiltinAdminsAreServerAdmins** , que se establece en **true** de forma predeterminada. Puede cambiar esta propiedad en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para más información, consulte [Security Properties](../../analysis-services/server-properties/security-properties.md).  
  
 Con posterioridad a la instalación, puede modificar la pertenencia a un rol para agregar usuarios adicionales que necesiten derechos completos para el servicio. También se pueden administrar roles de servidor mediante Objetos de administración de análisis (AMO). Para obtener más información, vea [Desarrollar con Objetos de administración de análisis &#40;AMO&#41;](https://docs.microsoft.com/bi-reference/amo/developing-with-analysis-management-objects-amo).  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proporciona una progresión de roles cada vez más granulares para el procesamiento y la consulta en los niveles de servidor, base de datos y objeto. Para obtener instrucciones sobre cómo usar estos roles, vea [Roles y permisos &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/roles-and-permissions-analysis-services.md).  
  
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
 **Servicio NT/SSASTelemetry** es una cuenta de equipo con privilegios reducidos que se crea durante la instalación y se usa exclusivamente para ejecutar la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] del servicio Programa para la mejora de la experiencia del usuario (CEIP). Este servicio requiere derechos de administrador en la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para ejecutar varios comandos de detección. Vea [Customer Experience Improvement Program for SQL Server Data Tools](../../sql-server/customer-experience-improvement-program-for-sql-server-data-tools.md) y [Microsoft SQL Server Privacy Statement](http://go.microsoft.com/fwlink/?LinkID=868444) para obtener más información.  
  
## <a name="see-also"></a>Vea también  
 [Cómo autorizar el acceso a objetos y operaciones &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)   
 [Roles de seguridad &#40;Analysis Services - Datos multidimensionales&#41;](../../analysis-services/multidimensional-models/olap-logical/security-roles-analysis-services-multidimensional-data.md)  
  
  
