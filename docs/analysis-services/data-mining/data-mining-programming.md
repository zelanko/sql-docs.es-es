---
title: Programación de minería de datos de Analysis Services | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1b4068d012b64cb4fc5352ed11c8576a38d6d6c4
ms.sourcegitcommit: 603d5ef9b45c2f111d36d11864dc032917e4a321
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/08/2019
ms.locfileid: "65450124"
---
# <a name="data-mining-programming"></a>Programación de minería de datos
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]

  Si los visores y las herramientas integrados en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no cumplen sus requisitos, puede extender la capacidad de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] codificando sus propias extensiones. En este enfoque, tiene dos opciones:  
  
-   **XMLA**  
  
     [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] admite XML for Analysis (XMLA) como protocolo de comunicación con aplicaciones cliente. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] admite comandos adicionales que amplían la especificación XML for Analysis.  
  
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
 [OLE DB para minería de datos](data-mining-programming-ole-db.md)  
 Describe las adiciones realizadas en la especificación para admitir la minería de datos y los datos multidimensionales: nuevas columnas y nuevos conjuntos de filas de esquema y el lenguaje DMX (Extensiones de minería de datos) para crear y administrar las estructuras de minería de datos.  
  
## <a name="related-reference"></a>Referencia relacionada  
 [Desarrollo con ADOMD.NET](https://docs.microsoft.com/bi-reference/adomd/developing-with-adomd-net)  
 Presenta el cliente ADOMD.NET y objetos de programación de servidor.  
  
 [Desarrollar con Objetos de administración de análisis &#40;AMO&#41;](https://docs.microsoft.com/bi-reference/amo/developing-with-analysis-management-objects-amo)  
 Presenta la biblioteca de programación de AMO.  
  
 [Desarrollar aplicaciones con Analysis Services Scripting Language &#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla)  
 Presenta XML for Analysis (XMLA) y sus extensiones.  
  
## <a name="see-also"></a>Vea también  
 [Guía del desarrollador (Analysis Services)](../analysis-services-developer-documentation.md)   
 [Referencia de Extensiones de minería de datos &#40;DMX&#41;](../../dmx/data-mining-extensions-dmx-reference.md)  
  
  
