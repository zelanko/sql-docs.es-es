---
title: Seleccionar el tipo de conversión (Asistente de Business Intelligence) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.biwizard.currencyconversion.conversiontype.f1
ms.assetid: 2c664138-e8a1-4c47-8e7d-ee01c57e4692
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ab618eaa2d8d54b08e3d01fa238d19451084eff8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66069618"
---
# <a name="select-conversion-type-business-intelligence-wizard"></a>Seleccionar el tipo de conversión (Asistente de Business Intelligence)
  Use la página **Seleccionar el tipo de conversión** para definir la relación entre las monedas locales y las monedas del informe en las transacciones almacenadas en varias monedas. La moneda local es la moneda en que se almacenan las transacciones de medidas seleccionadas en la página **Seleccionar medidas** . La moneda del informe es la moneda en que se convierten las transacciones seleccionadas en la página **Seleccionar medidas** .  
  
> [!NOTE]  
>  Esta página no aparece si se ha iniciado el Asistente de Business Intelligence desde el Diseñador de dimensiones o al hacer clic con el botón derecho en una dimensión del Explorador de soluciones de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
## <a name="options"></a>Opciones  
 **Varios a varios**  
 Almacena transacciones utilizando las monedas locales. La funcionalidad de conversión de moneda convierte estas transacciones en la moneda dinámica especificada en la página **Establecer las opciones de conversión de moneda** y, a continuación, en una o varias de las otras monedas del informe.  
  
 Por ejemplo, la moneda dinámica puede definirse como dólares norteamericanos (USD) y la tabla de hechos puede almacenar las transacciones en euros (EUR), dólares australianos (AUD) y pesos mexicanos (MXN). Al seleccionar esta opción se convierten estas transacciones de las monedas locales especificadas en la moneda dinámica y, a continuación, las transacciones convertidas se convierten de nuevo de la moneda dinámica a las monedas del informe especificadas. El resultado es que las transacciones se pueden almacenar en las monedas locales especificadas y verse en la moneda dinámica especificada o en cualquiera de las monedas del informe especificadas en la página **Especificar monedas del informe** .  
  
 **Varios a uno**  
 Almacena transacciones utilizando las monedas locales. La funcionalidad de conversión de moneda convierte estas transacciones en la moneda dinámica especificada en la página **Establecer las opciones de conversión de moneda** . La moneda dinámica funciona como la única moneda del informe especificada.  
  
> [!NOTE]  
>  Si esta opción está seleccionada, no aparece la página **Especificar monedas del informe** .  
  
 Por ejemplo, la moneda dinámica puede definirse como dólares norteamericanos (USD) y la tabla de hechos puede almacenar las transacciones en euros (EUR), dólares australianos (AUD) y pesos mexicanos (MXN). Al seleccionar esta opción se convierten estas transacciones de las monedas locales especificadas a la moneda dinámica. El resultado es que las transacciones se pueden almacenar en las monedas locales especificadas y verse en la moneda dinámica especificada.  
  
 **Uno a varios**  
 Almacene transacciones con la moneda dinámica especificada en la página **Establecer las opciones de conversión de moneda** y, después, en una o varias de las otras monedas del informe.  
  
> [!NOTE]  
>  Si esta opción está seleccionada, no aparece la página **Definir la referencia de moneda local** .  
  
 Por ejemplo, la moneda dinámica puede definirse como dólares norteamericanos (USD) y la tabla de hechos puede almacenar las transacciones en USD. Al seleccionar esta opción se convierten estas transacciones de la moneda dinámica en las monedas del informe especificadas. El resultado es que las transacciones se pueden almacenar en la moneda dinámica y verse en la moneda dinámica especificada o en cualquiera de las monedas del informe especificadas en la página **Especificar monedas del informe** .  
  
## <a name="see-also"></a>Consulte también  
 [Asistente de Business Intelligence (ayuda F1)](business-intelligence-wizard-f1-help.md)   
 [Diseñador de cubos &#40;Analysis Services de datos multidimensionales&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [Diseñador de dimensiones &#40;Analysis Services de datos multidimensionales&#41;](dimension-designer-analysis-services-multidimensional-data.md)  
  
  
