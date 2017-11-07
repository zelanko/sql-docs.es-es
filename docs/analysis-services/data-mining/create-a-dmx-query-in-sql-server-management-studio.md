---
title: Crear una consulta DMX en SQL Server Management Studio | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- templates [Analysis Services], queries
- SQL Server Management Studio [Analysis Services], DMX queries
- predictions [Analysis Services], DMX prediction queries
- predictions [DMX]
- prediction queries [DMX]
- queries [DMX], prediction queries
- mining models [Analysis Services], DMX
ms.assetid: 568ce40a-1f53-47eb-8c79-14347cdfde83
caps.latest.revision: 43
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 51a8ea188eb54adf0ac208225dd7c5fda417178c
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="create-a-dmx-query-in-sql-server-management-studio"></a>Crear una consulta DMX en SQL Server Management Studio
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona un conjunto de características para ayudarle a crear consultas de predicción, consultas de contenido y consultas de definición de datos en los modelos y estructuras de minería de datos.  
  
-   El Generador de consultas de predicción gráfico está disponible tanto en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] como en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], para simplificar el proceso de escritura de consultas de predicción y la asignación de conjuntos de datos a un modelo.  
  
-   Las plantillas de consulta que se proporcionan en el Explorador de plantillas agilizan la creación de muchos tipos de consultas DMX, incluidos muchos tipos de consultas de predicción. Se proporcionan plantillas para las consultas de contenido, las consultas que usan conjuntos de datos anidados, las consultas que devuelven casos de la estructura de minería de datos e, incluso, las consultas de definición de datos.  
  
-   El Explorador de metadatos en los paneles de consulta DMX y MDX proporciona una lista de los modelos disponibles y de las estructuras que se pueden arrastrar y colocar en el generador de consultas, junto con una lista de funciones DMX. Esta característica facilita la obtención de nombres de objeto directamente, sin necesidad de escribir.  
  
 En este tema se describe cómo crear una consulta DMX mediante el Explorador de metadatos y el editor de consultas DMX.  
  
##  <a name="BKMK_Templates"></a> Plantillas de consulta DMX  
 Las plantillas para crear consultas DMX básicas están disponibles en el Explorador de plantillas. La carpeta **DMX** contiene las plantillas de minería de datos, que se dividen en las categorías siguientes:  
  
-   **Contenido del modelo**  
  
-   **Administración del modelo**  
  
-   **Consultas de predicción**  
  
-   **Contenido de la estructura**  
  
 También puede crear plantillas personalizadas, para las consultas o los comandos que se ejecutan con frecuencia.  
  
## <a name="xmla-query-templates"></a>Plantillas de consulta XMLA  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] también proporciona plantillas para las consultas XMLA.  
  
 Hay cierta superposición entre los tipos de consultas que se pueden realizar mediante XMLA y DMX. Por ejemplo, puede crear algunas consultas de contenido de modelo con conjuntos de filas de esquema de minería de datos o DMX, pero los conjuntos de filas de esquema a veces contienen información que no se expone en las consultas de contenido DMX.  
  
 También hay algunas diferencias clave en la manera en que las operaciones se tratan en DMX y en XMLA. Por ejemplo, puede usar XMLA para realizar operaciones administrativas como la copia de seguridad de una base de datos completa de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Pero, si quiere realizar la copia de seguridad de un único modelo de minería de datos, DMX proporciona un sencillo comando, [EXPORT &#40;DMX&#41;](../../dmx/export-dmx.md), que es más adecuado para ese fin.  
  
##  <a name="BKMK_Building_Queries"></a> Generar y ejecutar una consulta DMX  
  
#### <a name="open-a-new-dmx-query-window"></a>Abrir una nueva ventana de consulta DMX  
  
1.  Haga clic en **Nueva consulta** en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]y, a continuación, seleccione **Consulta DMX de Analysis Server**.  
  
2.  Cuando aparezca el cuadro de diálogo **Conectar al servidor** , seleccione la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que contiene los modelos de minería de datos con los que desea trabajar.  
  
#### <a name="open-template-explorer"></a>Abrir el Explorador de plantillas  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], en el menú **Ver,** seleccione **Explorador de plantillas**.  
  
2.  Haga clic en **Analysis Server** para ver una vista de árbol de las plantillas que se aplican a [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
#### <a name="apply-a-template-to-build-a-query"></a>Aplicar una plantilla para crear una consulta  
  
-   Haga clic con el botón derecho en el tipo adecuado de consulta y seleccione **Abrir**.  
  
-   O bien, arrastre la plantilla en el editor de consultas.  
  
-   También puede completar los parámetros de la consulta con la opción **Especificar valores para parámetros**, en el menú **Consulta** .  
  
 Para obtener ejemplos sobre cómo utilizar tipos específicos de consultas a partir de plantillas, consulte los temas siguientes:  
  
 [Crear una consulta de predicción singleton desde una plantilla](../../analysis-services/data-mining/create-a-singleton-prediction-query-from-a-template.md)  
  
 [Crear una consulta de contenido en un modelo de minería de datos](../../analysis-services/data-mining/create-a-content-query-on-a-mining-model.md)  
  
## <a name="see-also"></a>Vea también  
 [Herramientas de consulta de minería de datos](../../analysis-services/data-mining/data-mining-query-tools.md)   
 [Referencia de Extensiones de minería de datos &#40;DMX&#41;](../../dmx/data-mining-extensions-dmx-reference.md)  
  
  

