---
title: Bases de datos de modelos multidimensionales (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio [Analysis Services], databases
- SQL Server Analysis Services, databases
- SSAS, databases
- Analysis Services, databases
- databases [Analysis Services], designing
- Business Intelligence Development Studio, databases [Analysis Services]
- databases [Analysis Services]
ms.assetid: 78b2f22a-b7bd-4a2b-b6fc-0bff4d2b3168
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5da033881d2a993ea4be6674dcf8b228cad80bf8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66073516"
---
# <a name="multidimensional-model-databases-ssas"></a>Bases de datos de modelos multidimensionales (SSAS)
  Una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] es una colección del orígenes de datos, vistas del origen de datos, cubos, dimensiones y roles. Una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] también puede incluir estructuras de minería de datos y ensamblados personalizados que proporcionan un método para agregar funciones definidas por el usuario a la base de datos.  
  
 Los cubos son los objetos de consulta fundamentales de Analysis Services. Cuando se conecta con una base de datos de Analysis Services a través de una aplicación cliente, se está conectando con un cubo de esa base de datos. Una base de datos puede contener varios cubos si se reutilizan dimensiones, ensamblados, roles o estructuras de minería de datos en varios contextos.  
  
 Puede crear y modificar una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] mediante programación o mediante uno de estos métodos interactivos:  
  
-   Implementar un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] a una instancia designada de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Este proceso crea una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] si no hay ninguna con ese nombre en la instancia. A continuación, crea instancias de los objetos designados en la base de datos recién creada. Al trabajar con una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], los cambios que se hacen en los objetos del proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] solo surten efecto cuando el proyecto se implementa en una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
-   Para crear una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] vacía en una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], use [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]y, después, conéctese directamente a esa base de datos con [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] y cree objetos en esta (en lugar de crearlos en un proyecto). Al trabajar así con una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , los cambios que se hacen en los objetos surten efecto en la base de datos a la que se está conectando cuando se guarda el objeto modificado.  
  
 
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] usa la integración con software de control de código fuente para permitir que varios desarrolladores de software trabajen con objetos distintos de un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] a la vez. Un programador también puede interactuar con una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] directamente, en lugar de hacerlo a través de un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , pero entonces existe el riesgo de que los objetos de una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dejen de estar sincronizados con el proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utilizado para su implementación. Después de la implementación, una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] se administra con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Hay algunos cambios que se pueden hacer en una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], por ejemplo en particiones y roles, que pueden hacer que los objetos de una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dejen de estar sincronizados con el proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usado para su implementación.  
  
## <a name="related-tasks"></a>Related Tasks  
 [Adjuntar y separar bases de datos de Analysis Services](attach-and-detach-analysis-services-databases.md)  
  
 [Realizar una copia de seguridad y restaurar las bases de datos de Analysis Services](backup-and-restore-of-analysis-services-databases.md)  
  
 [Documentar y crear scripts en una base de datos de Analysis Services](document-and-script-an-analysis-services-database.md)  
  
 [Modificar o eliminar una base de datos de Analysis Services](modify-or-delete-an-analysis-services-database.md)  
  
 [Mover una base de datos de Analysis Services](move-an-analysis-services-database.md)  
  
 [Cambiar el nombre de una base de datos multidimensional &#40;Analysis Services&#41;](rename-a-multidimensional-database-analysis-services.md)  
  
 [Establecer el nivel de compatibilidad de una base de datos multidimensional &#40;Analysis Services&#41;](compatibility-level-of-a-multidimensional-database-analysis-services.md)  
  
 [Establecer propiedades de bases de datos multidimensionales &#40;Analysis Services&#41;](set-multidimensional-database-properties-analysis-services.md)  
  
 [Sincronizar bases de datos de Analysis Services](synchronize-analysis-services-databases.md)  
  
 [Cambiar entre los modos ReadOnly y ReadWrite en una base de datos de Analysis Services](switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md)  
  
## <a name="see-also"></a>Consulte también  
 [Conectar en modo en línea a una base de datos de Analysis Services](connect-in-online-mode-to-an-analysis-services-database.md)   
 [Cree un proyecto de Analysis Services &#40;SSDT&#41;](create-an-analysis-services-project-ssdt.md)   
 [Consultar datos multidimensionales con MDX](mdx/querying-multidimensional-data-with-mdx.md)  
  
  
