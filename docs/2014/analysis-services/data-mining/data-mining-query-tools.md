---
title: Interfaces de consultas de minería de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- predictions [Analysis Services], DMX prediction queries
- predictions [DMX]
- DMX [Analysis Services], prediction queries
- prediction queries [DMX]
- predictions [Analysis Services]
- queries [DMX], prediction queries
- mining models [Analysis Services], DMX
ms.assetid: a8952427-fd8c-4300-8f62-25f57ac1be0c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7c59d3a18c1fd36f82e8ea60e42d1b9f6e2f34c2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66084981"
---
# <a name="data-mining-query-interfaces"></a>Interfaces de consultas de minería de datos
  Las consultas de minería de datos se basan en el lenguaje DMX (Extensiones de minería de datos). DMX se usa para todas las tareas de predicción y modelado, incluida la clasificación, el análisis de riesgos, la generación de recomendaciones y la regresión lineal. También puede recuperar los patrones y estadísticas que se generaron al procesar el modelo.  
  
 La sintaxis para una consulta de predicción usando DMX es similar a la sintaxis para una consulta de [!INCLUDE[tsql](../../includes/tsql-md.md)]. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] proporcionan herramientas que le ayudarán a generar las consultas de predicción DMX.  
  
 En este tema se describen las interfaces que puede usar para crear y ejecutar consultas de minería de datos con DMX.  
  
 [Herramientas de consulta](#bkmk_Tools)  
  
-   [Generador de consultas de predicción](#bkmk_Builder)  
  
-   [Editor de consultas](#bkmk_QueryEditor)  
  
-   [Plantillas DMX](#bkmk_Templates)  
  
-   [Integration Services](#bkmk_SSIS)  
  
 [Interfaces de programación de aplicaciones](#bkmk_API)  
  
##  <a name="bkmk_Tools"></a> Herramientas de consulta de minería de datos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dispone de las siguientes herramientas que puede utilizar para compilar consultas de predicción, consultas de contenido y consultas de definición de datos en objetos de minería de datos:  
  
-   Generador de consultas de predicción  
  
-   Editor de consultas  
  
-   Plantillas DMX  
  
-   Componentes de minería de datos de Integration Services  
  
###  <a name="bkmk_Builder"></a> Generador de consultas de predicción  
 El Generador de consultas de predicción se incluye en la pestaña **Predicción de modelo de minería de datos** del Diseñador de minería de datos, el cual está disponible en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]y en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Si utiliza el generador de consultas, puede utilizar las herramientas gráficas para seleccionar un modelo de minería de datos, agregar nuevos datos del caso y agregar funciones de predicción. El generador de consultas de predicción incluye un editor de texto que puede usar para modificar la consulta manualmente y una sencilla **resultados** panel para ver los resultados de la consulta.  
  
###  <a name="bkmk_QueryEditor"></a> Editor de consultas  
 El Editor de consultas en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] proporciona herramientas que puede usar para compilar y ejecutar consultas DMX. Puede conectar a una instancia de SQL Server Analysis Services y, a continuación, seleccionar una base de datos, columnas de estructura de minería de datos y un modelo de minería de datos. El **Explorador de metadatos** contiene una lista de funciones de predicción que puede examinar.  
  
###  <a name="bkmk_Templates"></a> Plantillas DMX  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] proporciona plantillas de consulta DMX interactivas que puede usar para compilar consultas DMX. Si no ve la lista de plantillas, haga clic en **Ver** en la barra de herramientas y seleccione **Explorador de plantillas**. Para ver todas las plantillas de Analysis Services, incluidas las plantillas para DMX, MDX y XMLA, haga clic en el icono de cubo.  
  
 Para compilar una consulta mediante una plantilla, puede arrastrar la plantilla a una ventana de consulta abierta, o puede hacer doble clic en la plantilla para abrir una nueva conexión y un nuevo panel de consulta.  
  
 Para consultar un ejemplo de cómo crear una consulta de predicción a partir de una plantilla, vea [Crear una consulta de predicción singleton desde una plantilla](create-a-singleton-prediction-query-from-a-template.md).  
  
> [!WARNING]  
>  El Complemento de minería de datos para Microsoft Office Excel también contiene varias plantillas, junto con un generador de consultas interactivo que puede ayudarle a crear instrucciones DMX complejas. Para utilizar las plantillas, haga clic en **Consulta**, y haga clic en **Avanzadas** en el Cliente de minería de datos.  
  
###  <a name="bkmk_SSIS"></a> Componentes de minería de datos de Integration Services  
 También puede incluir consultas de predicción como parte de un paquete de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Las siguientes tareas y transformaciones de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] admiten la creación y ejecución de consultas de predicción DMX e instrucciones DMX.  
  
|Componente|Descripción|  
|---------------|-----------------|  
|Tarea Consulta de minería de datos|Ejecuta consultas DMX y otras instrucciones DMX como parte de un flujo de control.<br /><br /> El editor de tareas incorpora el Generador de consultas de predicción y un cuadro de texto para modificar la consulta DMX manualmente. Sin embargo, el editor de tareas no puede validar la consulta con los objetos de una solución de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Por consiguiente, es mejor crear una consulta dentro de [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] y, a continuación, pegar el texto de la instrucción o consulta en el editor de tareas.|  
|Consulta de minería de datos, transformación|Ejecuta una consulta de predicción en un flujo de datos usando los datos proporcionados por un origen de flujo de datos.<br /><br /> El editor de tareas incorpora el Generador de consultas de predicción y un cuadro de texto para modificar la consulta DMX manualmente.<br /><br /> La transformación solo se puede utilizar para crear consultas que utilicen los datos del flujo de datos; es decir, consultas que utilicen la sintaxis de PREDICTION JOIN. Este componente no se puede utilizar para ejecutar consultas de contenido u otros tipos de instrucciones DMX.|  
  
##  <a name="bkmk_API"></a> Interfaces de programación de aplicaciones  
 Puede crear aplicaciones personalizadas que ejecuten consultas en modelos de minería de datos mediante distintos lenguajes de programación, junto con protocolos de servidor como OLE DB o el cliente ADOMD de Analysis Services. Para más información, vea [Programación de minería de datos](../dev-guide/data-mining-programming.md).  
  
 Sin embargo, XMLA constituye el formato del mensaje subyacente para todas las interacciones con un servidor de Analysis Services. En un mensaje XMLA, las consultas se representan de forma diferente dependiendo de si se envía una consulta de predicción basada en DMX, una consulta de contenido o una consulta que recupera metadatos del modelo mediante los conjuntos de filas de esquema de minería de datos.  
  
-   El texto de las **consultas de predicción** (y el resto de las instrucciones DMX) se envían en XMLA con el [método Execute &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute), con la consulta DMX colocada como texto en el [elemento Statement &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/statement-element-xmla) del [elemento Command &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/command-element-xmla).  
  
-   Para recuperar el **contenido del modelo** y los **metadatos del modelo**, como el número de clústeres, los atributos usados en los árboles de decisión, la fecha en que se procesó el modelo por última vez y los parámetros del algoritmo que se usaron al crear el modelo, puede usar el método [Discover &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover) y especificar uno de los conjuntos de filas del esquema de minería de datos en el encabezado del [elemento RequestType &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/type-element-xmla). Para restringir el ámbito de la consulta, escriba los criterios como restricciones en el [elemento RestrictionList &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/restrictionlist-element-xmla).  
  
## <a name="see-also"></a>Vea también  
 [Referencia de Extensiones de minería de datos &#40;DMX&#41;](/sql/dmx/data-mining-extensions-dmx-reference)   
 [Soluciones de minería de datos](data-mining-solutions.md)   
 [Descripción de la instrucción Select de DMX](/sql/dmx/understanding-the-dmx-select-statement)   
 [Estructura y uso de las consultas de predicción DMX](/sql/dmx/structure-and-usage-of-dmx-prediction-queries)   
 [Crear una consulta de predicción con el Generador de consultas de predicción](create-a-prediction-query-using-the-prediction-query-builder.md)   
 [Crear una consulta DMX en SQL Server Management Studio](create-a-dmx-query-in-sql-server-management-studio.md)  
  
  
