---
title: Almacenar en caché un informe (Administrador de informes) | Microsoft Docs
description: Aprenda a programar la expiración de un informe en caché en el Administrador de informes. El almacenamiento en caché de un informe acelera la visualización mientras permanece en la caché.
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- report execution properties [Reporting Services]
- cache [Reporting Services]
- cached reports [Reporting Services]
- schedules [Reporting Services], report expiration
- expiration [Reporting Services]
ms.assetid: 723d1cb0-c2e7-4763-8690-a6a7a8bbbb90
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 36bc03b94c42d8cf660039eb04c73ce88cf18223
ms.sourcegitcommit: fe59f8dc27fd633f5dfce54519d6f5dcea577f56
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/09/2020
ms.locfileid: "91934950"
---
# <a name="cache-a-report-report-manager"></a>Almacenar en caché un informe (Administrador de informes)
  Una manera de mejorar el rendimiento es configurar las propiedades de almacenamiento en caché para un informe. Cuando un informe se almacena en memoria caché, se guarda una copia del informe representado durante un breve período de tiempo. El primer usuario que solicita el informe debe esperar para que se complete todo el procesamiento antes de ver el informe. Los usuarios posteriores que soliciten el informe dentro del período de almacenamiento en caché pueden verlo de forma inmediata porque el procesamiento ya se ha producido.  
  
 Hay restricciones en los tipos de informes que puede almacenar en memoria caché. Por ejemplo, un informe no puede estar almacenado en memoria caché si el resultado del informe varía dependiendo de la identidad del usuario o si los datos se recuperan usando el token de seguridad del usuario que solicita el informe. Para más información, vea [Informes almacenados en caché &#40;SSRS&#41;](../../reporting-services/report-server/caching-reports-ssrs.md).  
  
### <a name="to-schedule-the-expiration-of-a-cached-report"></a>Para programar la expiración de un informe en caché  
  
1.  Inicie el [Administrador de informes &#40;Modo nativo de SSRS&#41;](../web-portal-ssrs-native-mode.md).  
  
2.  En el Administrador de informes, navegue hasta la página **Contenido** . Navegue hasta el informe para el que desea establecer propiedades de almacenando en memoria caché, mantenga el mouse sobre el elemento y haga clic en la flecha de lista desplegable.  
  
3.  En el menú desplegable, haga clic en **Administrar**.  
  
4.  En el marco izquierdo, haga clic en **Opciones de procesamiento**.  
  
5.  En la página, seleccione **Ejecutar este informe siempre con los datos más recientes**.  
  
6.  Seleccione una de las siguientes dos opciones de caché y configure la expiración como se indica a continuación:  
  
    -   Para configurar que una copia en caché expire después de un período determinado, haga clic en **Almacenar en caché una copia temporal del informe. La copia expirará después de un número determinado de minutos**. Escriba el número de minutos para la expiración del informe.  
  
    -   Para configurar que una copia en caché expire de acuerdo con una programación, haga clic en **Guardar en caché una copia temporal del informe. La copia del informe debe expirar según la siguiente programación.** Haga clic en **Configurar**, o seleccione una programación compartida para controlar la expiración del informe.  
  
7.  Haga clic en **Aplicar**.  
  
## <a name="see-also"></a>Consulte también  
 [Establecer las propiedades del procesamiento de informes](../../reporting-services/report-server/set-report-processing-properties.md)   
 [Informes almacenados en caché &#40;SSRS&#41;](../../reporting-services/report-server/caching-reports-ssrs.md)  
  
