---
title: Roles y permisos (Analysis Services) | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- security [Analysis Services], about security
- security [Analysis Services - multidimensional data], about security
ms.assetid: bb885447-868b-4686-853c-8241f63d4370
caps.latest.revision: "21"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: c9205b1908bbb4be6678d752fa0808cb2676d5f1
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="roles-and-permissions-analysis-services"></a>Roles y permisos (Analysis Services)
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proporciona un modelo de autorización basada en roles que concede acceso a operaciones, objetos y datos. Todos los usuarios que acceden a una base de datos o a una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] deben hacerlo en el contexto de un rol.  
  
 Como administrador del sistema de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , se va a encargar de conceder la pertenencia al **rol de administrador del servidor** que proporciona acceso sin restricciones a las operaciones del servidor. Este rol tiene permisos fijos y no puede personalizarse. De forma predeterminada, los miembros del grupo local de administradores son automáticamente administradores del sistema de Analysis Services.  
  
 Los usuarios que no sean administradores y que realicen consultas o procesen datos se les concede acceso con los **roles de base de datos**. Los administradores del sistema y de base de datos deben crear roles que describan los diferentes niveles de acceso en una determinada base de datos y, a continuación, asignar la pertenencia a cada usuario que requiera acceso. Cada rol cuenta con un conjunto personalizado de permisos para obtener acceso a objetos y operaciones en una base de datos en particular. Puede asignar permisos en los siguientes niveles: base de datos, objetos interiores, como cubos y dimensiones (pero no perspectivas), y filas.  
  
 Una práctica habitual es crear roles y asignar miembros en operaciones independientes. A menudo, el diseñador del modelo agrega roles durante la fase de diseño. De este modo, todas las definiciones de roles se reflejan en los archivos de proyecto que definen el modelo. La asignación de pertenencia a los roles normalmente se lleva a cabo después, cuando la base de datos pasa a producción, y suelen hacerlo los administradores de bases de datos, que crean scripts que se pueden desarrollar, probar y ejecutar en una operación independiente.  
  
 Toda la autorización se basa en una identidad de Windows válida. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa la autenticación de Windows solamente para autenticar identidades de usuario. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no proporciona ningún método de autenticación de su propiedad. Vea [Metodologías de autenticación admitidas por Analysis Services](../../analysis-services/instances/authentication-methodologies-supported-by-analysis-services.md).  
  
> [!IMPORTANT]  
>  Los permisos se van sumando en cada usuario o grupo de Windows, en todos los roles de la base de datos. Si un rol impide que un permiso de usuario o grupo realice determinadas tareas o vea ciertos datos, pero hay otro rol que concede este mismo permiso a ese usuario o grupo, el usuario o grupo tendrá permiso para realizar la tarea o ver los datos.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Cómo autorizar el acceso a objetos y operaciones &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)  
  
-   [Otorgar permisos de base de datos &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-database-permissions-analysis-services.md)  
  
-   [Otorgar permisos para cubos o modelos &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md)  
  
-   [Otorgar permisos de procesamiento &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-process-permissions-analysis-services.md)  
  
-   [Otorgar permisos Leer definición en metadatos de objetos &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-read-definition-permissions-on-object-metadata-analysis-services.md)  
  
-   [Otorgar permisos para un objeto de origen de datos &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-permissions-on-a-data-source-object-analysis-services.md)  
  
-   [Otorgar permisos para estructuras y modelos de minería de datos &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-permissions-on-data-mining-structures-and-models-analysis-services.md)  
  
-   [Otorgar permisos para una dimensión &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-permissions-on-a-dimension-analysis-services.md)  
  
-   [Conceder acceso personalizado a datos de dimensión &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md)  
  
-   [Otorgar acceso personalizado a los datos de las celdas &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md)  
  
## <a name="see-also"></a>Vea también  
 [Crear y administrar roles &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/create-and-manage-roles-ssas-tabular.md)  
  
  
