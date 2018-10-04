---
title: Programación de minería de datos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- data mining [Analysis Services], developer's guide
ms.assetid: 9fd77b16-0b89-44ce-bcf1-7c04b62499da
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8aa16d708683a33281ee0836321e11f0a16e3211
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48047705"
---
# <a name="data-mining-programming"></a>Programación de minería de datos
  Si los visores y las herramientas integrados en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no cumplen sus requisitos, puede extender la capacidad de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] codificando sus propias extensiones. En este enfoque, tiene dos opciones:  
  
-   **XMLA**  
  
     [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)] admite XML for Analysis (XMLA) como protocolo de comunicación con aplicaciones cliente. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] admite comandos adicionales que amplían la especificación XML for Analysis.  
  
     Dado que [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utiliza XMLA para la compatibilidad con la definición, la manipulación y el control de los datos, puede crear estructuras y modelos de minería de datos mediante las herramientas visuales proporcionadas por [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] y extender, a continuación, los objetos de minería de datos que haya creado mediante scripts DMX (Extensiones de minería de datos) y ASSL (Analysis Services Scripting Language).  
  
     Puede crear y modificar objetos de minería de datos íntegramente en scripts XMLA, además de ejecutar mediante programación consultas de predicción en los modelos desde sus propias aplicaciones.  
  
-   **Objetos de administración de análisis (AMO)**  
  
     [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] también proporciona un marco completo que permite a los demás proveedores de minería de datos integrar los objetos de minería de datos en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
     Es posible crear estructuras y modelos de minería de datos mediante AMO. Vea los ejemplos siguientes de CodePlex:  
  
    -   Explorador de AMO  
  
         Se conecta a la instancia de SSAS especificada y muestra todos los objetos de servidor y sus propiedades, incluidos la estructura y los modelos de minería de datos.  
  
    -   Ejemplo simple de AMO  
  
         El ejemplo simple de AS abarca el acceso mediante programación a la mayoría de los objetos principales, y muestra la exploración de los metadatos y el acceso a los valores de los objetos.  
  
         En el ejemplo también se muestra cómo crear y procesar una estructura y un modelo de minería de datos, y cómo examinar un modelo de minería de datos existente.  
  
-   **DMX**  
  
     Puede usar DMX para encapsular instrucciones de comandos, consultas de predicción y consultas de metadatos, y devolver resultados en formato tabular, suponiendo que se haya creado una conexión con un servidor de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
## <a name="in-this-section"></a>En esta sección  
 [OLE DB para minería de datos](../../../2014/analysis-services/dev-guide/ole-db-for-data-mining.md)  
 Describe las adiciones realizadas en la especificación para admitir la minería de datos y los datos multidimensionales: nuevas columnas y nuevos conjuntos de filas de esquema y el lenguaje DMX (Extensiones de minería de datos) para crear y administrar las estructuras de minería de datos.  
  
## <a name="related-reference"></a>Referencia relacionada  
 [Desarrollo con ADOMD.NET](../multidimensional-models/adomd-net/developing-with-adomd-net.md)  
 Presenta el cliente ADOMD.NET y objetos de programación de servidor.  
  
 [Desarrollar con objetos de administración de análisis &#40;AMO&#41;](../multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md)  
 Presenta la biblioteca de programación de AMO.  
  
 [Desarrollar aplicaciones con Analysis Services Scripting Language &#40;ASSL&#41;](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)  
 Presenta XML for Analysis (XMLA) y sus extensiones.  
  
## <a name="see-also"></a>Vea también  
 [Guía del desarrollador &#40;Analysis Services&#41;](../analysis-services-developer-documentation.md)   
 [Extensiones de minería de datos &#40;DMX&#41; referencia](/sql/dmx/data-mining-extensions-dmx-reference)  
  
  
