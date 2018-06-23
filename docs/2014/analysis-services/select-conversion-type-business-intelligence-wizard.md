---
title: Seleccione el tipo de conversión (Asistente de Business Intelligence) | Documentos de Microsoft
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
- sql12.asvs.biwizard.currencyconversion.conversiontype.f1
ms.assetid: 2c664138-e8a1-4c47-8e7d-ee01c57e4692
caps.latest.revision: 23
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: ba4018a6ce30e4e7de4e0ca3e79ae07007015650
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36203275"
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
  
## <a name="see-also"></a>Vea también  
 [Ayuda de F1 de Asistente de Business Intelligence](business-intelligence-wizard-f1-help.md)   
 [Diseñador de cubos &#40;Analysis Services - datos multidimensionales&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [Diseñador de dimensiones &#40;Analysis Services - datos multidimensionales&#41;](dimension-designer-analysis-services-multidimensional-data.md)  
  
  