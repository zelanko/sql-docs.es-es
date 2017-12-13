---
title: "Conceder permisos en las estructuras de minería de datos y modelos (Analysis Services) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.asvs.roledesignerdialog.miningmodels.f1
helpviewer_keywords:
- data mining [Analysis Services], security
- permissions [Analysis Services], mining models
- mining models [Analysis Services], security
- mining structures [Analysis Services], security
- permissions [Analysis Services], mining structures
- user access rights [Analysis Services], mining structures
- user access rights [Analysis Services], mining models
ms.assetid: a0008004-e2b7-47db-acad-5fe7e12b130f
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 44204be410e5d4e716f30f5f0775f8c62d152a55
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="grant-permissions-on-data-mining-structures-and-models-analysis-services"></a>Otorgar permisos para estructuras y modelos de minería de datos (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]De forma predeterminada, sólo un administrador del servidor de Analysis Services tiene permisos para ver las estructuras de minería de datos o modelos de minería de datos en la base de datos. Siga las instrucciones de más abajo para conceder permisos a usuarios que no sean administradores.  
  
## <a name="set-permissions-to-access-a-mining-structure"></a>Establecer permisos para obtener acceso a una estructura de minería datos  
  
1.  En SSMS, conéctese a Analysis Services. Vea [Conectarse desde aplicaciones cliente &#40;Analysis Services&#41;](../../analysis-services/instances/connect-from-client-applications-analysis-services.md) si necesita ayuda con los pasos.  
  
2.  Abra la carpeta **Bases de datos** y seleccione una base de datos en el Explorador de objetos.  
  
3.  Haga clic con el botón derecho en **Roles** y elija **Nuevo rol**.  
  
4.  En la página General, escriba un nombre y, si lo desea, una descripción. La página también contiene diversos permisos de base de datos, como Control total, Procesar base de datos y Leer definición. No se necesita ninguno de estos permisos para tener acceso a la minería de datos. Vea [Otorgar permisos de base de datos &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-database-permissions-analysis-services.md) para obtener más información sobre los permisos de base de datos.  
  
5.  En el panel **Estructura de minería de datos**, seleccione **Lectura** o **Lectura y escritura** para cada estructura de minería de datos.  
  
6.  En el panel **Pertenencia** , especifique las cuentas de usuario y grupo de Windows que se conectan a Analysis Services con este rol.  
  
7.  Haga clic en **Aceptar** para completar la creación del rol.  
  
## <a name="set-permissions-to-access-a-mining-model"></a>Establecer permisos para obtener acceso a un modelo de minería de datos  
 Para los modelos de minería de datos, los roles pueden tener permisos de **Lectura** o **Lectura y escritura** , así como permisos de **Obtención de detalles** y **Leer definición** que permiten ver y explorar los datos subyacentes.  
  
 **Nota** : Si habilita la obtención de detalles en la estructura de minería de datos y el modelo de minería, cualquier usuario que sea miembro de un rol que tenga los permisos de obtención de detalles en el modelo de minería y la estructura de minería de datos también podrá ver las columnas en la estructura de minería de datos, aun cuando esas columnas no estén incluidas en el modelo de minería. Por consiguiente, para proteger información confidencial, debería preparar la vista del origen de datos de forma que enmascare datos personales y solo permita el acceso para la obtención de detalles en la estructura de minería de datos cuando sea necesario.  
  
 Para conceder permisos de lectura y escritura a un rol de base de datos, un usuario debe ser miembro del rol de servidor de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o de un rol de base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] con permisos de Control total (Administrador).  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conéctese a la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], expanda **Roles** para la base de datos correspondiente en Explorador de objetos y, después, haga clic en un rol de base de datos (o cree un nuevo rol de base de datos).  
  
2.  En el panel **Estructura de minería de datos** , busque el modelo de minería de datos en la lista **Modelos de minería de datos** y, después, seleccione **Lectura**, **Lectura y escritura**, **Obtención de detalles**o **Examinar** para ese modelo de minería de datos.  
  
3.  En el panel **Pertenencia** , especifique las cuentas de usuario y grupo de Windows que se conectan a Analysis Services con este rol.  
  
4.  Haga clic en **Aceptar** para completar la creación del rol.  
  
 Para usar un origen de datos en una consulta de obtención de detalles que usa la cláusula (DMX) OPENQUERY de Extensiones de minería de datos (DMX), el rol de base de datos también requiere permiso de lectura y escritura sobre el objeto de origen de datos correspondiente. Para obtener más información, vea [Otorgar permisos para un objeto de origen de datos &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-permissions-on-a-data-source-object-analysis-services.md) y [OPENQUERY &#40;DMX&#41;](../../dmx/source-data-query-openquery.md).  
  
> [!NOTE]  
>  De forma predeterminada, el envío de consultas DMX al usar OPENROWSET está deshabilitado.  
  
## <a name="see-also"></a>Vea también  
 [Conceder permisos de administrador de servidor (Analysis Services)](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md)   
 [Otorgar permisos para cubos o modelos &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md)   
 [Conceder acceso personalizado a la dimensión de datos &#40; Analysis Services &#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md)   
 [Otorgar acceso personalizado a los datos de las celdas &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md)  
  
  
