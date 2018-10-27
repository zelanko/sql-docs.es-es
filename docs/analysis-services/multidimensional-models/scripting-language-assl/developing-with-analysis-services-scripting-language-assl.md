---
title: Desarrollar aplicaciones con Analysis Services Scripting Language (ASSL) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c113e07099ed96abdb0eb5f62c8517ee422d3cc7
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/26/2018
ms.locfileid: "50145810"
---
# <a name="developing-with-analysis-services-scripting-language-assl"></a>Desarrollar aplicaciones con Analysis Services Scripting Language (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  El lenguaje de scripting de Analysis Services (ASSL) es una extensión de XMLA que agrega un lenguaje de definición de objetos y un lenguaje de comandos para crear y administrar estructuras Analysis Services directamente en el servidor. Puede utilizar ASSL en la aplicación personalizada para comunicarse con Analysis Services a través del protocolo XMLA. ASSL consta de dos partes:  
  
-   Un lenguaje de definición de datos (DDL), o lenguaje de definición de objetos, que define y describe una instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], así como las bases de datos y los objetos de base de datos que la instancia contiene.  
  
-   Un lenguaje de comandos que envía comandos de acción, como **crear**, **Alter**, o **proceso**, a una instancia de Analysis Services. Este lenguaje de comandos se describe en el [XML for Analysis &#40;XMLA&#41; referencia](https://docs.microsoft.com/bi-reference/xmla/xml-for-analysis-xmla-reference).  
  
 Para ver el ASSL que describe una solución multidimensional en [!INCLUDE[ssBIDevStudio](../../../includes/ssbidevstudio-md.md)], puede utilizar el comando Ver código en el nivel de proyecto. También puede crear o modificar el script de ASSL en [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] utilizando el editor de consultas XMLA. Los scripts que cree pueden usarse para administrar objetos o ejecutar comandos en el servidor.  
  
## <a name="see-also"></a>Vea también  
 [ASSL y características de objetos](../../../analysis-services/multidimensional-models/scripting-language-assl/assl-objects-and-object-characteristics.md)   
 [Convenciones XML de ASSL](../../../analysis-services/multidimensional-models/scripting-language-assl/assl-xml-conventions.md)   
 [Orígenes de datos y enlaces &#40;SSAS multidimensional&#41;](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)  
  
  
