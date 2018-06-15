---
title: Roles y permisos (Analysis Services) | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5e6b463fedda33d8b10fbe2d1e415f1ef248ae92
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34025792"
---
# <a name="roles-and-permissions-analysis-services"></a>Roles y permisos (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]Proporciona un modelo de autorización basada en roles que concede acceso a las operaciones, objetos y datos. Todos los usuarios que acceden a una base de datos o a una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] deben hacerlo en el contexto de un rol.  
  
 Como administrador del sistema de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , se va a encargar de conceder la pertenencia al **rol de administrador del servidor** que proporciona acceso sin restricciones a las operaciones del servidor. Este rol tiene permisos fijos y no puede personalizarse. De forma predeterminada, los miembros del grupo local de administradores son automáticamente administradores del sistema de Analysis Services.  
  
 Los usuarios que no sean administradores y que realicen consultas o procesen datos se les concede acceso con los **roles de base de datos**. Los administradores del sistema y de base de datos deben crear roles que describan los diferentes niveles de acceso en una determinada base de datos y, a continuación, asignar la pertenencia a cada usuario que requiera acceso. Cada rol cuenta con un conjunto personalizado de permisos para obtener acceso a objetos y operaciones en una base de datos en particular. Puede asignar permisos en los siguientes niveles: base de datos, objetos interiores, como cubos y dimensiones (pero no perspectivas), y filas.  
  
 Una práctica habitual es crear roles y asignar miembros en operaciones independientes. A menudo, el diseñador del modelo agrega roles durante la fase de diseño. De este modo, todas las definiciones de roles se reflejan en los archivos de proyecto que definen el modelo. La asignación de pertenencia a los roles normalmente se lleva a cabo después, cuando la base de datos pasa a producción, y suelen hacerlo los administradores de bases de datos, que crean scripts que se pueden desarrollar, probar y ejecutar en una operación independiente.  
  
 Toda la autorización se basa en una identidad de Windows válida. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa la autenticación de Windows solamente para autenticar identidades de usuario. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]no proporciona ningún método de autenticación propietario. Vea [metodologías de autenticación admitidas por Analysis Services](../../analysis-services/instances/authentication-methodologies-supported-by-analysis-services.md).  
  
> [!IMPORTANT]  
>  Los permisos se van sumando en cada usuario o grupo de Windows, en todos los roles de la base de datos. Si un rol impide que un permiso de usuario o grupo realice determinadas tareas o vea ciertos datos, pero hay otro rol que concede este mismo permiso a ese usuario o grupo, el usuario o grupo tendrá permiso para realizar la tarea o ver los datos.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Autorización de acceso a objetos y operaciones & #40; Analysis Services & #41;](../../analysis-services/multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)  
  
-   [Conceder permisos de base de datos & #40; Analysis Services & #41;](../../analysis-services/multidimensional-models/grant-database-permissions-analysis-services.md)  
  
-   [Conceder el cubo o modelo permisos & #40; Analysis Services & #41;](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md)  
  
-   [Otorgar permisos de procesamiento & #40; Analysis Services & #41;](../../analysis-services/multidimensional-models/grant-process-permissions-analysis-services.md)  
  
-   [Otorgar permisos Leer definición en metadatos de objetos & #40; Analysis Services & #41;](../../analysis-services/multidimensional-models/grant-read-definition-permissions-on-object-metadata-analysis-services.md)  
  
-   [Conceder permisos en un objeto de origen de datos & #40; Analysis Services & #41;](../../analysis-services/multidimensional-models/grant-permissions-on-a-data-source-object-analysis-services.md)  
  
-   [Conceder permisos en las estructuras de minería de datos y modelos de & #40; Analysis Services & #41;](../../analysis-services/multidimensional-models/grant-permissions-on-data-mining-structures-and-models-analysis-services.md)  
  
-   [Conceder permisos en una dimensión & #40; Analysis Services & #41;](../../analysis-services/multidimensional-models/grant-permissions-on-a-dimension-analysis-services.md)  
  
-   [Conceder acceso personalizado a la dimensión de datos & #40; Analysis Services & #41;](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md)  
  
-   [Conceder acceso personalizado a una celda de datos & #40; Analysis Services & #41;](../../analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md)  
  
## <a name="see-also"></a>Vea también  
 [Crear y administrar roles](../../analysis-services/tabular-models/create-and-manage-roles-ssas-tabular.md)  
  
  
