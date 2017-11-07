---
title: Anotaciones de CSDL para Business Intelligence (CSDLBI) | Documentos de Microsoft
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: bf6f372a-bc67-45ea-a771-b2dc5b0527e5
caps.latest.revision: 21
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: fcb4818edc09599822670e2e379f89bbf35c6fbb
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="csdl-annotations-for-business-intelligence-csdlbi"></a>Anotaciones de CSDL para Business Intelligence (CSDLBI)

[!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)]

  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] admite la presentación de la definición de un modelo tabular en un formato XML denominado Lenguaje de definición de esquemas conceptuales con anotaciones Business Intelligence (CSDLBI). En este tema se proporciona información general sobre CSDLBI y su uso con los modelos de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
## <a name="understanding-the-role-of-csdl"></a>Descripción del propósito de CSDL  
 El Lenguaje de definición de esquemas conceptuales (CSDL) es un lenguaje basado en XML que describe las entidades, las relaciones y las funciones. CSDL forma parte de Entity Data Framework. Las anotaciones BI son una extensión diseñada para admitir el modelado de datos mediante [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Aunque CSDL es compatible con Entity Data Framework, no es necesario comprender el modelo entidad-relación ni tener ninguna herramienta especial para generar un modelo tabular o un informe basado en un modelo. Es posible generar modelos mediante herramientas cliente como [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] o una API como AMO, e implementarlos en un servidor. Los clientes se conectan con el modelo mediante un archivo de definición de modelo, que normalmente se publica en una biblioteca de SharePoint donde pueden utilizarlo los diseñadores de informes y los consumidores de informes. Para obtener más información, vea estos vínculos:  
  
-   [Soluciones de modelos tabulares &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/tabular-model-solutions-ssas-tabular.md)  
  
-   [Implementación de soluciones de modelos tabulares &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/tabular-model-solution-deployment-ssas-tabular.md)  
  
-   [Conexión del modelo semántico de BI de PowerPivot &#40;.bism&#41;](../../analysis-services/power-pivot-sharepoint/power-pivot-bi-semantic-model-connection-bism.md)  
  
 El esquema CSDLBI lo genera el servidor de Analysis Services en respuesta a una solicitud de una definición de modelo realizada por un cliente como [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]. La aplicación cliente envía una consulta XML al servidor de Analysis Services que hospeda los datos del modelo. En respuesta, el servidor envía un mensaje XML que contiene una definición de las entidades del modelo, utilizando las anotaciones CSDLBI. El cliente de informes usa la información para mostrar los campos, las agregaciones y las medidas disponibles en el modelo. Las anotaciones CSDLBI también proporcionan información sobre cómo agrupar, ordenar y dar formato a los datos.  
  
 Para obtener información general sobre CSDLBI, vea [conceptos de CSDLBI](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/csdlbi-concepts.md).  
  
### <a name="working-with-csdl"></a>Trabajar con CSDL  
 El conjunto de anotaciones CSDLBI que representa cualquier modelo tabular determinado es un documento XML que contiene una colección de entidades, tanto simples como complejas. Las entidades definen las tablas (o dimensiones), las columnas (atributos), las asociaciones (relaciones) y las fórmulas incluidas en las columnas calculadas, medidas o KPI.  
  
 No puede modificar estos objetos directamente, sino que debe utilizar las herramientas del cliente y las interfaces de programación de aplicaciones (API) proporcionadas para trabajar con modelos tabulares.  
  
 Puede obtener el CSDL para un modelo enviando una solicitud DISCOVER al servidor que hospeda el modelo. La solicitud se debe calificar especificando el servidor y el modelo y, opcionalmente, una vista o una perspectiva. El mensaje devuelto es una cadena XML. Algunos elementos dependen del lenguaje y pueden devolver valores diferentes en función del lenguaje de la conexión actual. Para obtener más información, consulte [conjunto de filas DISCOVER_CSDL_METADATA](../../analysis-services/schema-rowsets/xml/discover-csdl-metadata-rowset.md).  
  
### <a name="csdlbi-versions"></a>Versiones de CSDLBI  
 La especificación CSDL original (de Entity Data Framework) es suficiente para la mayor parte de las entidades y propiedades necesarias para el modelado. Las anotaciones BI admiten requisitos especiales de modelos tabulares, propiedades de informes requeridas por clientes como [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] y metadatos adicionales requeridos por modelos multidimensionales. En esta sección se describen las actualizaciones de cada versión.  
  
 **CSDLBI 1.0**  
  
 El conjunto inicial de adiciones al esquema CSDL para admitir los modelos tabulares de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] contenía anotaciones que permitían el uso del modelado de datos, los cálculos personalizados y las presentaciones mejoradas:  
  
-   Nuevos elementos y propiedades para admitir modelos tabulares. Por ejemplo, se agregó una propiedad para especificar el tipo de consulta de base de datos utilizada para rellenar el modelo.  
  
-   Nuevas propiedades y extensiones para las entidades existentes.  Por ejemplo, el elemento Association se extendió para admitir las relaciones.  
  
-   Propiedades de visualización y navegación. Por ejemplo, se agregaron propiedades para admitir campos de ordenación personalizados e imágenes predeterminadas.  
  
 **1.1 DE CSDLBI**  
  
 Esta versión del esquema CSDLBI incluye adiciones para admitir el uso de bases de datos multidimensionales (como los cubos OLAP). Los nuevos elementos y propiedades son los siguientes:  
  
-   Compatibilidad con las dimensiones como entidades.  
  
-   Compatibilidad con las jerarquías.  
  
-   Expone particiones ROLAP.  
  
-   Compatibilidad con las traducciones.  
  
-   Compatibilidad con las perspectivas.  
  
 Para obtener información detallada acerca de los elementos individuales de las anotaciones CSDLBI, vea [Technical Reference for anotaciones BI para CSDL](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/technical-reference-for-bi-annotations-to-csdl.md). Para obtener información sobre la especificación de CSDL del núcleo, consulte el [especificación de CSDL](http://go.microsoft.com/fwlink/?LinkId=205855) en MSDN.  
  
## <a name="see-also"></a>Vea también  
 [Descripción del modelo de objetos tabulares en compatibilidad 1050 1103 a través de niveles](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)   
 [Conceptos de CSDLBI](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/csdlbi-concepts.md)   
 [Descripción del modelo de objetos tabulares en compatibilidad 1050 1103 a través de niveles](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)  
  
  

