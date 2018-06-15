---
title: Bases de datos de modelo multidimensional (SSAS) | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1ec839c9638b3baf79cba0148cc932ead7820f7b
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34022068"
---
# <a name="multidimensional-model-databases-ssas"></a>Bases de datos de modelos multidimensionales (SSAS)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] es una colección del orígenes de datos, vistas del origen de datos, cubos, dimensiones y roles. Una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] también puede incluir estructuras de minería de datos y ensamblados personalizados que proporcionan un método para agregar funciones definidas por el usuario a la base de datos.  
  
 Los cubos son los objetos de consulta fundamentales de Analysis Services. Cuando se conecta con una base de datos de Analysis Services a través de una aplicación cliente, se está conectando con un cubo de esa base de datos. Una base de datos puede contener varios cubos si se reutilizan dimensiones, ensamblados, roles o estructuras de minería de datos en varios contextos.  
  
 Puede crear y modificar una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] mediante programación o mediante uno de estos métodos interactivos:  
  
-   Implementar un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] a una instancia designada de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Este proceso crea una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] si no hay ninguna con ese nombre en la instancia. A continuación, crea instancias de los objetos designados en la base de datos recién creada. Al trabajar con una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], los cambios que se hacen en los objetos del proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] solo surten efecto cuando el proyecto se implementa en una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
-   Para crear una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] vacía en una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], use [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]y, después, conéctese directamente a esa base de datos con [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] y cree objetos en esta (en lugar de crearlos en un proyecto). Al trabajar así con una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , los cambios que se hacen en los objetos surten efecto en la base de datos a la que se está conectando cuando se guarda el objeto modificado.  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] usa la integración con software de control de código fuente para permitir que varios desarrolladores de software trabajen con objetos distintos de un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] a la vez. Un programador también puede interactuar con una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] directamente, en lugar de hacerlo a través de un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , pero entonces existe el riesgo de que los objetos de una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dejen de estar sincronizados con el proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utilizado para su implementación. Después de la implementación, una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] se administra con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Hay algunos cambios que se pueden hacer en una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], por ejemplo en particiones y roles, que pueden hacer que los objetos de una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dejen de estar sincronizados con el proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usado para su implementación.  
  
## <a name="related-tasks"></a>Tareas relacionadas  
 [Adjuntar y separar bases de datos de Analysis Services](../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)  
  
 [Realizar una copia de seguridad y restaurar las bases de datos de Analysis Services](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
 [Documentar y crear scripts de una base de datos de Analysis Services](../../analysis-services/multidimensional-models/document-and-script-an-analysis-services-database.md)  
  
 [Modificar o eliminar una base de datos de Analysis Services](../../analysis-services/multidimensional-models/modify-or-delete-an-analysis-services-database.md)  
  
 [Mover una base de datos de Analysis Services](../../analysis-services/multidimensional-models/move-an-analysis-services-database.md)  
  
 [Cambie el nombre de una base de datos multidimensional &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/rename-a-multidimensional-database-analysis-services.md)  
  
 [Nivel de compatibilidad de una base de datos multidimensional &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md)  
  
 [Establecer propiedades de bases de datos multidimensionales &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/set-multidimensional-database-properties-analysis-services.md)  
  
 [Sincronizar bases de datos de Analysis Services](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md)  
  
 [Cambiar una base de datos de Analysis Services entre los modos ReadOnly y ReadWrite](../../analysis-services/multidimensional-models/switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md)  
  
## <a name="see-also"></a>Vea también  
 [Conectar con una base de datos de Analysis Services en modo en línea](../../analysis-services/multidimensional-models/connect-in-online-mode-to-an-analysis-services-database.md)   
 [Crear un proyecto de Analysis Services &#40;SSDT&#41;](../../analysis-services/multidimensional-models/create-an-analysis-services-project-ssdt.md)   
 [Consulta de datos multidimensionales con MDX](../../analysis-services/multidimensional-models/mdx/querying-multidimensional-data-with-mdx.md)  
  
  
