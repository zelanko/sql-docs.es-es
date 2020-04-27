---
title: Conceder permisos para estructuras y modelos de minería de datos (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.roledesignerdialog.miningmodels.f1
helpviewer_keywords:
- data mining [Analysis Services], security
- permissions [Analysis Services], mining models
- mining models [Analysis Services], security
- mining structures [Analysis Services], security
- permissions [Analysis Services], mining structures
- user access rights [Analysis Services], mining structures
- user access rights [Analysis Services], mining models
ms.assetid: a0008004-e2b7-47db-acad-5fe7e12b130f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 25eb8fe00c523d4a94b7f6f0325bfd2c1f55e7be
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66074942"
---
# <a name="grant-permissions-on-data-mining-structures-and-models-analysis-services"></a>Otorgar permisos para estructuras y modelos de minería de datos (Analysis Services)
  De forma predeterminada, solamente el administrador de servidor dispone de permisos para ver las estructuras de minería de datos o modelos de minería de datos en la base de datos. Siga las instrucciones de más abajo para conceder permisos a usuarios que no sean administradores.  
  
## <a name="set-permissions-to-access-a-mining-structure"></a>Establecer permisos para obtener acceso a una estructura de minería datos  
  
1.  En SSMS, conéctese a Analysis Services. Vea [Conectarse desde aplicaciones cliente &#40;Analysis Services&#41;](../instances/connect-from-client-applications-analysis-services.md) si necesita ayuda con los pasos.  
  
2.  Abra la carpeta **Bases de datos** y seleccione una base de datos en el Explorador de objetos.  
  
3.  Haga clic con el botón derecho en **Roles** y elija **Nuevo rol**.  
  
4.  En la página General, escriba un nombre y, si lo desea, una descripción. La página también contiene diversos permisos de base de datos, como Control total, Procesar base de datos y Leer definición. No se necesita ninguno de estos permisos para tener acceso a la minería de datos. Vea [Otorgar permisos de base de datos &#40;Analysis Services&#41;](grant-database-permissions-analysis-services.md) para obtener más información sobre los permisos de base de datos.  
  
5.  En el panel **Estructura de minería de datos** , seleccione **Lectura** o **Lectura y escritura**  para cada estructura de minería de datos.  
  
6.  En el panel **Pertenencia** , especifique las cuentas de usuario y grupo de Windows que se conectan a Analysis Services con este rol.  
  
7.  Haga clic en **Aceptar** para completar la creación del rol.  
  
## <a name="set-permissions-to-access-a-mining-model"></a>Establecer permisos para obtener acceso a un modelo de minería de datos  
 Para los modelos de minería de datos, los roles pueden tener permisos de **Lectura** o **Lectura y escritura** , así como permisos de **Obtención de detalles** y **Leer definición** que permiten ver y explorar los datos subyacentes.  
  
 **Nota** : Si habilita la obtención de detalles en la estructura de minería de datos y el modelo de minería, cualquier usuario que sea miembro de un rol que tenga los permisos de obtención de detalles en el modelo de minería y la estructura de minería de datos también podrá ver las columnas en la estructura de minería de datos, aun cuando esas columnas no estén incluidas en el modelo de minería. Por consiguiente, para proteger información confidencial, debería preparar la vista del origen de datos de forma que enmascare datos personales y solo permita el acceso para la obtención de detalles en la estructura de minería de datos cuando sea necesario.  
  
 Para conceder permisos de lectura y escritura a un rol de base de datos, un usuario debe ser miembro del rol de servidor de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o de un rol de base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] con permisos de Control total (Administrador).  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conéctese a la instancia [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]de, expanda **roles** para la base de datos adecuada en explorador de objetos y, a continuación, haga clic en un rol de base de datos (o cree un nuevo rol de base de datos).  
  
2.  En el panel **Estructura de minería de datos** , busque el modelo de minería de datos en la lista **Modelos de minería de datos** y, después, seleccione **Lectura**, **Lectura y escritura**, **Obtención de detalles**o **Examinar** para ese modelo de minería de datos.  
  
3.  En el panel **Pertenencia** , especifique las cuentas de usuario y grupo de Windows que se conectan a Analysis Services con este rol.  
  
4.  Haga clic en **Aceptar** para completar la creación del rol.  
  
 Para usar un origen de datos en una consulta de obtención de detalles que usa la cláusula (DMX) OPENQUERY de Extensiones de minería de datos (DMX), el rol de base de datos también requiere permiso de lectura y escritura sobre el objeto de origen de datos correspondiente. Para obtener más información, vea [Otorgar permisos para un objeto de origen de datos &#40;Analysis Services&#41;](grant-permissions-on-a-data-source-object-analysis-services.md) y [OPENQUERY &#40;DMX&#41;](/sql/dmx/source-data-query-openquery).  
  
> [!NOTE]  
>  De forma predeterminada, el envío de consultas DMX al usar OPENROWSET está deshabilitado.  
  
## <a name="see-also"></a>Consulte también  
 [Conceder permisos de administrador de servidor &#40;Analysis Services&#41;](../instances/grant-server-admin-rights-to-an-analysis-services-instance.md)   
 [Conceder permisos de cubo o de modelo &#40;Analysis Services&#41;](grant-cube-or-model-permissions-analysis-services.md)   
 [Conceder acceso personalizado a datos de dimensión &#40;Analysis Services&#41;](grant-custom-access-to-dimension-data-analysis-services.md)   
 [Otorgar acceso personalizado a los datos de las celdas &#40;Analysis Services&#41;](grant-custom-access-to-cell-data-analysis-services.md)  
  
  
