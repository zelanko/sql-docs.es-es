---
title: Establecer la configuración regional de un informe o un cuadro de texto (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- locales [Reporting Services]
ms.assetid: df115b01-184b-47f0-b5ec-0ad965ff9bee
caps.latest.revision: 43
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: d2fdbe4d44dd16d4f3094725c7032379ab163902
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36105767"
---
# <a name="set-the-locale-for-a-report-or-text-box-reporting-services"></a>Establecer la configuración regional de un informe o un cuadro de texto (Reporting Services)
  La propiedad **Language** de un informe o un cuadro de texto contiene la configuración regional, que determina los formatos predeterminados para mostrar los datos de informe que difieren según el idioma y la región, como por ejemplo, la fecha, la moneda o los valores numéricos. La propiedad **Language** de un cuadro de texto invalida la propiedad **Language** del informe. Si no se especifica ningún valor para **Language**, Reporting Services usa la configuración regional del sistema operativo del servidor de informes para los informes publicados o la del equipo en que se crea el informe para la vista previa del informe.  
  
 Para los informes HTML, puede invalidar el valor de **Language** predeterminado y usar el idioma especificado por el encabezado HTTP del cliente de explorador usando el campo integrado User!Language en una expresión para la propiedad **Language** de un informe o un cuadro de texto.  
  
 También puede especificar la propiedad **Language** para un informe en una dirección URL. Para obtener más información, consulte [establecer el idioma para los parámetros de informe en una dirección URL](../set-the-language-for-report-parameters-in-a-url.md).  
  
### <a name="to-set-the-locale-for-a-report"></a>Para establecer la configuración regional de un informe  
  
1.  En la vista Diseño, haga clic fuera de la superficie de diseño del informe para seleccionar el informe.  
  
2.  En el panel Propiedades, en la propiedad **Language** , escriba o seleccione el idioma que desea usar para el informe.  
  
### <a name="to-set-the-locale-for-a-text-box"></a>Para establecer la configuración regional de un cuadro de texto  
  
1.  En la vista Diseño, seleccione el cuadro de texto al que desea aplicar la configuración regional.  
  
2.  En el panel Propiedades, haga lo siguiente:  
  
    -   En la propiedad **Calendar** , escriba o seleccione el calendario que desea usar para las fechas.  
  
    -   En la propiedad **Direction** , escriba o seleccione la dirección en que se escribe el texto.  
  
    -   En la propiedad **Language** , escriba o seleccione el idioma que desea usar para el cuadro de texto. Este valor invalida la propiedad **Language** para el informe.  
  
    -   En la propiedad **NumeralLanguage** , escriba o seleccione el formato que desea utilizar para los números del cuadro de texto.  
  
    -   En la propiedad **NumeralVariant** , escriba o seleccione la variante de formato que desea usar para los números del cuadro de texto.  
  
    -   En la propiedad **UnicodeBiDi** , seleccione el nivel de incrustación bidireccional que se va a usar en el cuadro de texto.  
  
## <a name="see-also"></a>Vea también  
 [Expresión que se utiliza en los informes &#40;el generador de informes SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)  
  
  