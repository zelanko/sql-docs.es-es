---
title: Establecer el idioma para los parámetros de informe en una dirección URL | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- overriding report language settings
- report servers [Reporting Services], language settings
- languages [Reporting Services]
- URL access [Reporting Services], language overrides
- international considerations [Reporting Services]
- global considerations [Reporting Services]
ms.assetid: e1ccf22f-80d6-45bc-aae0-f5f263275092
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 46b00567781ac2a87bb2d5ff48eaa9d7cd04058f
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2019
ms.locfileid: "59945521"
---
# <a name="set-the-language-for-report-parameters-in-a-url"></a>Establecer el idioma para los parámetros de informe en una dirección URL
  El parámetro de acceso URL *rs:ParameterLanguage* reduce un problema por el que los parámetros de informe sujetos a referencias culturales (como las fechas, horas, monedas y cifras) se interpretan con el idioma del explorador. Con *rs:ParameterLanguage*, la dirección URL se interpreta ahora independientemente del explorador. Por ejemplo, si el servidor de informes está establecido en la configuración regional de alemán, pero un usuario tiene acceso a un informe a través de una dirección URL mediante un explorador que está configurado en inglés de Estados Unidos, los valores de los parámetros que se pasen a un servidor de informes se interpretarán mal.  
  
 Considere la dirección URL siguiente para un informe:  
  
```  
http://myrshost/Reportserver?/SampleReports/Product+Line+Sales&rs:Command=Render&StartDate=4/10/2008&EndDate=11/10/2008  
```  
  
 En el caso anterior, el servidor, que se ejecuta con la referencia cultural "de-de", genera una dirección URL a través de una suscripción de correo electrónico o un hipervínculo. El hipervínculo indica que el informe debería parametrizarse con la fecha de inicio del 4 de octubre de 2008 y la fecha de fin del 11 de octubre de 2008, según los estándares de fecha y hora alemanas. Sin embargo, un usuario que tenga acceso a la dirección URL a través de un explorador establecido en "en-us" obliga al servidor a interpretar los valores como 10 de abril de 2008 y 10 de noviembre de 2008 con los estándares de fecha y hora de inglés de Estados Unidos. Para corregir el problema, se puede utilizar *rs:ParameterLanguage* con el objeto de invalidar el idioma del explorador para la interpretación de los parámetros:  
  
```  
http://myrshost/Reportserver?/SampleReports/Product+Line+Sales&rs:Command=Render&StartDate=4/10/2008&EndDate=11/10/2008&rs:ParameterLanguage=de-DE  
```  
  
 Además del valor **true** y **false** para el parámetro de acceso URL *rc:Parameters*, ahora puede pasar el valor **Collapsed**. Al usar *rc:Parameters*=**Collapsed** en una dirección URL, el área de mensajes de parámetros del Visor HTML se contrae fuera de la vista, pero el usuario todavía puede cambiarla. El valor **false** quita el área de mensajes de parámetros de la barra de herramientas del Visor HTML y hace que no esté disponible para el usuario final.  
  
## <a name="see-also"></a>Vea también  
 [Acceso URL &#40;SSRS&#41;](url-access-ssrs.md)   
 [Referencia de parámetros de acceso URL](url-access-parameter-reference.md)  
  
  
