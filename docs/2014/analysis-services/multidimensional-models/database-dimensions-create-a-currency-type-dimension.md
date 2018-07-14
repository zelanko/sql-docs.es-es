---
title: Crear una dimensión de tipo moneda | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- dimensions [Analysis Services], currency
- currency [Analysis Services]
- converting currency
- currency dimensions [Analysis Services]
ms.assetid: b1f037d1-ce47-4e47-a1c2-5ec9e781cff6
caps.latest.revision: 16
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7b9eb36a77501a7195c18138eab0d767fc7aed63
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37232025"
---
# <a name="create-a-currency-type-dimension"></a>Crear una dimensión de tipo moneda
  En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], una dimensión de tipo moneda es aquella cuyos atributos representan una lista de monedas para la elaboración de informes financieros.  
  
 Una dimensión de moneda permite agregar funciones de conversión de moneda a un cubo en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para agregar conversión de moneda a un cubo, se utiliza el Asistente de Business Intelligence para definir un script de expresiones multidimensionales (MDX) que convierte medidas de moneda en valores adecuados a la configuración regional de la aplicación cliente. Para crear el script MDX, el Asistente de Business Intelligence necesita la siguiente información:  
  
-   Una dimensión de moneda que representa las monedas de origen. (Esta dimensión es la dimensión de moneda de origen.)  
  
-   Se utilizará un grupo de medida que representa las tasas de cambio.  
  
 A partir de esta información, el Asistente de Business Intelligence diseña un proceso de conversión de moneda que identifica la dimensión de moneda de destino adecuada (la dimensión de moneda que representa las monedas de destino). En función del número de conversiones de moneda que necesite la solución de Business Intelligence, el Asistente de Business Intelligence puede definir varias dimensiones de moneda de destino. Para más información sobre cómo definir conversiones de moneda, vea [Conversiones de moneda &#40;Analysis Services&#41;](../currency-conversions-analysis-services.md).  
  
 Para identificar una dimensión como dimensión de moneda, establezca el `Type` propiedad de la dimensión a `Currency`.  
  
## <a name="dimension-structure"></a>Estructura de dimensión  
 Una dimensión de moneda contiene como mínimo un atributo clave que identifica monedas específicas en la tabla de dimensión para la dimensión de moneda. El valor del atributo clave es diferente en las dimensiones de moneda de origen y de destino:  
  
-   Para identificar un atributo como atributo clave de una dimensión de moneda de origen, establezca la propiedad `Type` del atributo en `CurrencySource`.  
  
-   Para identificar un atributo como la dimensión de moneda de destino, establezca la `Type` propiedad del atributo en `CurrencyDestination`.  
  
 Para fines de elaboración de informes, tanto las dimensiones de moneda de origen como de destino pueden incluir también los siguientes atributos:  
  
-   Un atributo de nombre de moneda  
  
     Para identificar un atributo como atributo de nombre de moneda, establezca la propiedad `Type` del atributo en `CurrencyName`.  
  
-   Un atributo de origen de moneda  
  
     Para identificar un atributo como atributo de origen de moneda, establezca la propiedad `Type` del atributo en `CurrencySource`.  
  
-   Un código de moneda ISO (International Standards Organization)  
  
     Para identificar un atributo como atributo de código ISO de moneda, establezca el `Type` propiedad del atributo en `CurrencyIsoCode`.  
  
 Para más información sobre tipos de atributo, vea [Configurar tipos de atributos](attribute-properties-configure-attribute-types.md).  
  
## <a name="defining-account-intelligence-with-the-business-intelligence-wizard"></a>Definir la inteligencia de cuentas mediante el Asistente de Business Intelligence  
 Tras definir una dimensión de cuenta y agregar dicha dimensión a un cubo, puede utilizar el Asistente de Business Intelligence para agregar a la dimensión características de inteligencia de cuentas, como la identificación y asignación de tipos de cuentas. Para más información, vea [Agregar inteligencia de cuentas a una dimensión](bi-wizard-add-account-intelligence-to-a-dimension.md).  
  
## <a name="see-also"></a>Vea también  
 [Atributos y jerarquías de atributo](../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [Asistente de Business Intelligence F1 Ayuda](../business-intelligence-wizard-f1-help.md)   
 [Tipos de dimensiones](../multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)  
  
  
