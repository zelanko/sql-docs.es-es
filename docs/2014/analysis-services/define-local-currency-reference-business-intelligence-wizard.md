---
title: Definir la referencia de moneda Local (Asistente de Business Intelligence) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.biwizard.currencyconversion.localcurrency.f1
ms.assetid: 74993b0d-dfca-476b-acba-d66c593680a5
caps.latest.revision: 24
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 10810e19ec00aa77a14cb5a21789dfee1f9ae09a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36103669"
---
# <a name="define-local-currency-reference-business-intelligence-wizard"></a>Definir la referencia de moneda local (Asistente de Business Intelligence)
  Use la página **Definir la referencia de moneda local** para definir las monedas locales en la funcionalidad de conversión de monedas que incluye los tipos de conversión varios a varios o varios a uno especificados en la página **Seleccionar el tipo de conversión** . La moneda local es la moneda en que se almacenan las transacciones de medidas seleccionadas en la página **Seleccionar medidas** .  
  
> [!NOTE]  
>  Esta página no aparece si se ha iniciado el Asistente de Business Intelligence desde el Diseñador de dimensiones o al hacer clic con el botón derecho en una dimensión del Explorador de soluciones de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Tampoco aparece si se ha seleccionado **Uno a varios** en la página **Seleccionar el tipo de conversión** .  
  
## <a name="options"></a>Opciones  
 **Identificadores de la tabla de hechos**  
 Seleccione esta opción para especificar un atributo que proporcione los identificadores de moneda para las monedas locales en una dimensión de moneda a la que hace referencia la tabla de hechos que contiene las medidas seleccionadas en la página **Seleccionar medidas** . (Una dimensión de moneda uno cuyo `Type` propiedad está establecida en *moneda*.)  
  
 Use esta opción si la propia transacción determina la moneda local para la transacción. Por ejemplo, en la base de datos de ejemplo [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] de[!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)], el grupo de medida Internet Sales tiene una relación de dimensión normal con la dimensión Currency. La tabla de hechos de ese grupo de medida contiene una columna de clave externa que hace referencia a los identificadores de moneda de la tabla de dimensiones de esa dimensión.  
  
 **Dimensión de moneda y el atributo hace referencia a los datos de hechos**  
 Seleccione el atributo de moneda en una dimensión de moneda cuyos miembros representen los identificadores de moneda para las monedas locales. (Un atributo de moneda es aquel cuyo `Type` propiedad está establecida en *moneda*.)  
  
> [!NOTE]  
>  Esta opción no estará disponible si no se selecciona la opción **Identificadores de la tabla de hechos** .  
  
 **Atributos de la tabla de dimensiones**  
 Seleccione esta opción para especificar un atributo de una dimensión relacionada con el grupo de medida que contiene los identificadores de moneda para las monedas locales.  
  
 Use esta opción si la relación entre una transacción y otra entidad comercial, como la ubicación, determina la moneda local para la transacción. Por ejemplo, en la base de datos de ejemplo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] de[!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)], el grupo de medida Financial Reporting tiene una relación de dimensión referenciada con la dimensión Currency a través de la dimensión Organization. Es decir, la tabla de hechos para el grupo de medida Financial Reporting contiene una columna de clave externa que hace referencia a miembros de la tabla de dimensiones para la dimensión Organization. A su vez, la tabla de dimensiones de la dimensión Organization contiene una columna de clave externa que hace referencia a los identificadores de moneda de la tabla de dimensiones de la dimensión Currency.  
  
 **Atributo de dimensión que hace referencia a moneda**  
 Seleccione el atributo de una dimensión cuyos miembros hacen referencia a los identificadores de moneda para las monedas locales.  
  
> [!NOTE]  
>  Esta opción no estará disponible si no se selecciona la opción **Atributos de la tabla de dimensiones** .  
  
## <a name="see-also"></a>Vea también  
 [Ayuda de F1 de Asistente de Business Intelligence](business-intelligence-wizard-f1-help.md)   
 [Diseñador de cubos &#40;Analysis Services - datos multidimensionales&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [Diseñador de dimensiones &#40;Analysis Services - datos multidimensionales&#41;](dimension-designer-analysis-services-multidimensional-data.md)  
  
  