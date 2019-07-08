---
title: 'Limitar el historial de informes: Reporting Services | Microsoft Docs'
ms.date: 06/26/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reports
ms.topic: conceptual
helpviewer_keywords:
- viewing report history
- report history [Reporting Services], viewing history
- report history [Reporting Services], configuring history
- historical data [Reporting Services]
- displaying report history
ms.assetid: 8e255792-d9ef-496f-a26c-9e969c1209a0
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 2dd66078363e281c2a73bfcc70ba685493bc3b88
ms.sourcegitcommit: c0e48b643385ce19c65ca6e348ce83b2d22b6514
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2019
ms.locfileid: "67492593"
---
# <a name="limit-report-history---reporting-services"></a>Limitar el historial de informes: Reporting Services
  El historial de informes es un conjunto de instantáneas de informe que se crean a lo largo del tiempo. Puede crear el historial de informes a petición o programar la frecuencia con que una instantánea se crea y se agrega al historial de informes.  
  
 El historial de informes está almacenado en la base de datos del servidor de informes. Si las instantáneas de informes contienen una gran cantidad de datos, considere la posibilidad de limitar el historial de informes para minimizar el efecto de la retención de instantáneas en el tamaño de la base de datos.  

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
  
## <a name="to-configure-report-history-for-a-report-server"></a>Para configurar un historial del informe para un servidor de informes  
  
1.  En el Administrador de informes, haga clic en **Configuración del sitio** en la barra de herramientas global.  
  
2.  Seleccione **Conservar un número ilimitado de instantáneas en el historial de informe** si desea guardar todo el historial del informe indefinidamente. De lo contrario, seleccione **Limitar las copias del historial de informe** para especificar la cantidad máxima de instantáneas que se pueden guardar para un determinado informe.  
  
3.  Haga clic en **Aplicar**.  
  
## <a name="to-configure-report-history-for-a-specific-report"></a>Para configurar un historial de un informe específico  
  
1.  En el Administrador de informes, navegue al informe para el cual desea configurar el historial y, a continuación, haga clic en el informe para abrirlo.  
  
2.  Haga clic en la pestaña **Propiedades** .  
  
3.  Haga clic en la pestaña **Historial** .  
  
4.  Seleccione las opciones para el informe y haga clic en **Aplicar**. Para más información sobre cada opción, vea [Página de propiedades de opciones de instantánea &#40;Administrador de informes&#41;](https://msdn.microsoft.com/library/f6641f59-5267-4f57-8957-63b93d1a9679).  
  
## <a name="see-also"></a>Consulte también  
 [Agregar una instantánea al historial de informes &#40;Administrador de informes&#41;](../../reporting-services/report-server/add-a-snapshot-to-report-history-report-manager.md)   
 [Administrador de informes &#40;Modo nativo de SSRS&#41;](https://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)  

::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"

## <a name="to-configure-report-history-for-a-report-server"></a>Para configurar un historial del informe para un servidor de informes  
  
1.  En el portal web, haga clic en **Configuración del sitio**en la barra de herramientas global.  
  
2.  Seleccione **Conservar un número ilimitado de instantáneas en el historial de informe** si desea guardar todo el historial del informe indefinidamente. De lo contrario, seleccione **Limitar las copias del historial de informe** para especificar la cantidad máxima de instantáneas que se pueden guardar para un determinado informe.  
  
3.  Haga clic en **Aplicar**.  
  
## <a name="to-configure-report-history-for-a-specific-report"></a>Para configurar un historial de un informe específico  
  
1.  En el portal web, navegue al informe para el cual desea configurar el historial y, a continuación, haga clic en el informe para abrirlo.  
  
2.  Haga clic en la pestaña **Propiedades** .  
  
3.  Haga clic en la pestaña **Historial** .  
  
4.  Seleccione las opciones para el informe y haga clic en **Aplicar**. Para más información sobre cada opción, vea [Página de propiedades de opciones de instantánea](https://msdn.microsoft.com/library/f6641f59-5267-4f57-8957-63b93d1a9679).  
  
## <a name="see-also"></a>Consulte también  
 [Incorporación de una instantánea al historial de informes](../../reporting-services/report-server/add-a-snapshot-to-report-history-report-manager.md)   

::: moniker-end
  
