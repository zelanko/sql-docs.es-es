---
title: Conceder permisos de administrador del servidor (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- administrator rights [Analysis Services]
- server-wide administrative permissions [Analysis Services]
ms.assetid: 20d1234b-a457-4a84-ae08-fe356870c466
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8df7e950f300028b2246450bf29ed0e8776f2cd4
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/26/2018
ms.locfileid: "50145300"
---
# <a name="grant-server-administrator-permissions-analysis-services"></a>Conceder permisos de administrador de servidor (Analysis Services)
  Los miembros del rol de administrador de servidor dentro de una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tienen acceso no restringido a todos los datos y objetos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de dicha instancia. Un usuario debe ser miembro del rol de administrador de servidor para poder realizar cualquier tarea en el servidor, como crear o procesar una base de datos, modificar las propiedades del servidor o iniciar un seguimiento (que no sea para procesar eventos).  
  
 La pertenencia al rol se establece al instalar [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . El usuario que ejecuta el programa de instalación puede agregarse a sí mismo al rol, o agregar otros usuarios, al aprovisionar el servidor. Es posible modificar la pertenencia al rol como una tarea posterior a la instalación mediante el procedimiento siguiente.  
  
## <a name="modify-server-role-membership"></a>Modificar la pertenencia al rol de servidor  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conéctese a la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], haga clic con el botón derecho en el nombre de la instancia en el Explorador de objetos y, después, haga clic en **Propiedades**.  
  
2.  Haga clic en **Seguridad** en el panel **Seleccionar una página** y, a continuación, haga clic en clic **Agregar** en la parte inferior de la página para agregar uno o más usuarios o grupos de Windows al rol de servidor.  
  
     ![Cuadro de diálogo Agregar usuarios en management studio](../media/ssas-serveradminadd.png "cuadro de diálogo Agregar usuarios en management studio")  
  
 Durante la instalación, el programa de instalación de SQL Server le pide que especifique al menos una cuenta de usuario como administrador del sistema de Analysis Services.  
  
 De forma predeterminada, a los miembros del grupo local Administradores también se les conceden derechos administrativos en Analysis Server. Aunque no se concede explícitamente al grupo local la pertenencia al rol de administrador del servidor de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , los administradores locales pueden crear bases de datos, agregar usuarios y permisos, y realizar cualquier otra tarea permitida a los administradores del sistema. Este comportamiento se puede configurar. Viene determinado por la `BuiltinAdminsAreServerAdmins` propiedad del servidor, que se establece en **true** de forma predeterminada. Puede cambiar esta propiedad en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para más información, consulte [Security Properties](../server-properties/security-properties.md).  
  
 También se pueden administrar roles de servidor mediante Objetos de administración de análisis (AMO). Para obtener más información, vea [Desarrollar con Objetos de administración de análisis &#40;AMO&#41;](https://docs.microsoft.com/bi-reference/amo/developing-with-analysis-management-objects-amo).  
  
## <a name="see-also"></a>Vea también  
 [Cómo autorizar el acceso a objetos y operaciones &#40;Analysis Services&#41;](../multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)   
 [Roles de seguridad &#40;Analysis Services - Datos multidimensionales&#41;](../multidimensional-models/olap-logical/security-roles-analysis-services-multidimensional-data.md)  
  
  
