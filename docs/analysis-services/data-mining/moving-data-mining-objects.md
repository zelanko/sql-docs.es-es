---
title: "Mover objetos de minería de datos | Documentos de Microsoft"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data mining [Analysis Services], models
- data mining editor [Analysis Services]
- mining models [Analysis Services], managing
- Data Mining Designer
- mining models [Analysis Services], modifying
ms.assetid: bc108407-2603-4387-b930-b5bb9df78069
caps.latest.revision: 45
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 198dd7792a24f0090aec82593704f0f2165b0d43
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="moving-data-mining-objects"></a>Mover objetos de minería de datos
  Los escenarios más frecuentes para mover objetos de minería de datos son implementar un modelo de un entorno de prueba o de análisis en un entorno de producción, o compartir modelos con otros usuarios.  
  
 En este tema se describe cómo usar las herramientas y los lenguajes de scripting que proporciona [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], para mover objetos de minería de datos.  
  
## <a name="moving-data-mining-objects-between-databases-or-servers"></a>Mover objetos de minería de datos entre bases de datos o servidores  
 Puede mover objetos de minería de datos entre bases de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o entre instancias de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de las siguientes formas:  
  
-   Volviendo a implementar la solución en una base de datos diferente.  
  
-   Generando scripting de objetos individuales.  
  
-   Haciendo una copia de seguridad y restaurando una copia de la base de datos.  
  
-   Exportando e importando estructuras y modelos.  
  
 En la siguiente sección se describen estas opciones con más detalle.  
  
### <a name="deploying"></a>Implementar  
 La implementación de la solución en otro servidor o base de datos requiere que tenga el archivo de solución creado con [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Para más información sobre cómo implementar soluciones de Analysis Services, vea [Implementar proyectos de Analysis Services &#40;SSDT&#41;](../../analysis-services/multidimensional-models/deploy-analysis-services-projects-ssdt.md).  
  
### <a name="scripting"></a>Scripting  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proporciona varios lenguajes que puede utilizar para crear scripts de objetos.  
  
-   **XMLA**: puede incluir objetos con XMLA si hace clic con el botón derecho en objetos de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para ejecutar el script, ábralo en una ventana de **Consulta XMLA** en el servidor de destino.  
  
-   **DMX**: puede crear scripts mediante plantillas o uno de los generadores de consultas que se proporcionan en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] y [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 Tenga en cuenta, no obstante, que existen diferencias en las tareas que puede realizar con cada lenguaje de scripting:  
  
-   Las propiedades, como la descripción y los enlaces de datos del objeto, solo se pueden crear o cambiar mediante lenguajes DDL de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y no utilizando DMX.  
  
-   Solo DMX admite la importación y exportación de objetos de minería de datos.  
  
-   Solo DMX admite la generación de PMML o la importación de definiciones de modelo PMML.  
  
-   Solo DMX admite el aprendizaje de un modelo con datos de la aplicación. Además, la instrucción DMX INSERT INTO admite el aprendizaje de un modelo sin proporcionar valores para una columna de clave.  
  
 Para más información, vea [Desarrollar aplicaciones con Analysis Services Scripting Language &#40;ASSL&#41;](../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md).  
  
### <a name="backup-and-restore"></a>Copias de seguridad y restauración  
 La copia de seguridad y restauración de una base de datos de Analysis Services completa es el mejor método si la solución de minería de datos se basa en objetos OLAP. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] proporciona una funcionalidad de copia de seguridad y restauración que realiza copias de seguridad de bases de datos con más rapidez y facilidad.  
  
 Para más información sobre las copias de seguridad, vea [Realizar una copia de seguridad y restaurar las bases de datos de Analysis Services](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md).  
  
### <a name="exporting-and-importing"></a>Exportación e importación  
 Exportar y volver a importar después modelos y estructuras de minería de datos utilizando instrucciones DMX es la forma más fácil de mover o hacer copias de seguridad de objetos de minería de datos relacionales individuales. Para obtener más información sobre la sintaxis DMX para estas operaciones, vea los temas siguientes:  
  
-   [EXPORT &#40;DMX&#41;](../../dmx/export-dmx.md)  
  
-   [IMPORT &#40;DMX&#41;](../../dmx/import-dmx.md)  
  
 Si especifica la opción INCLUDE DEPENDENCIES, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] también exportará la definición de las vistas del origen de datos necesarias y, al importar el modelo o la estructura, volverá a crear la vista del origen de datos en el servidor de destino. Cuando termine de importar el modelo, asegúrese de establecer los permisos de minería de datos necesarios en el objeto.  
  
> [!NOTE]  
>  No se pueden exportar e importar modelos OLAP utilizando DMX. Si el modelo de minería de datos se basa en un cubo OLAP, debe utilizar la funcionalidad proporcionada por [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para hacer una copia de seguridad y restaurar una base de datos completa, o vuelva a implementar el cubo y sus modelos.  
  
## <a name="see-also"></a>Vea también  
 [Administración de las soluciones y los objetos de minería de datos](../../analysis-services/data-mining/management-of-data-mining-solutions-and-objects.md)  
  
  

