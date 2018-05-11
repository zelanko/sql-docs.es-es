---
title: Desarrollar aplicaciones con Analysis Services Scripting Language (ASSL) | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 92e939c5ba180acdd0bd8509298ea1324a8414d7
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="developing-with-analysis-services-scripting-language-assl"></a>Desarrollar aplicaciones con Analysis Services Scripting Language (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  El lenguaje de scripting de Analysis Services (ASSL) es una extensión de XMLA que agrega un lenguaje de definición de objetos y un lenguaje de comandos para crear y administrar estructuras Analysis Services directamente en el servidor. Puede utilizar ASSL en la aplicación personalizada para comunicarse con Analysis Services a través del protocolo XMLA. ASSL consta de dos partes:  
  
-   Un lenguaje de definición de datos (DDL), o lenguaje de definición de objetos, que define y describe una instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], así como las bases de datos y los objetos de base de datos que la instancia contiene.  
  
-   Un lenguaje de comandos que envía comandos de acción, como **crear**, **Alter**, o **proceso**, a una instancia de Analysis Services. Este lenguaje de comandos se describe en el [XML for Analysis &#40;XMLA&#41; referencia](../../../analysis-services/xmla/xml-for-analysis-xmla-reference.md).  
  
 Para ver el ASSL que describe una solución multidimensional en [!INCLUDE[ssBIDevStudio](../../../includes/ssbidevstudio-md.md)], puede utilizar el comando Ver código en el nivel de proyecto. También puede crear o modificar el script de ASSL en [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] utilizando el editor de consultas XMLA. Los scripts que cree pueden usarse para administrar objetos o ejecutar comandos en el servidor.  
  
## <a name="see-also"></a>Vea también  
 [Objetos y características de objetos ASSL](../../../analysis-services/multidimensional-models/scripting-language-assl/assl-objects-and-object-characteristics.md)   
 [Convenciones XML de ASSL](../../../analysis-services/multidimensional-models/scripting-language-assl/assl-xml-conventions.md)   
 [Orígenes de datos y enlaces & #40; SSAS Multidimensional & #41;](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)  
  
  
