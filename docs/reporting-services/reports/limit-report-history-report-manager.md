---
title: Limitar el historial de informes (Administrador de informes) | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- viewing report history
- report history [Reporting Services], viewing history
- report history [Reporting Services], configuring history
- historical data [Reporting Services]
- displaying report history
ms.assetid: 8e255792-d9ef-496f-a26c-9e969c1209a0
caps.latest.revision: 36
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8e1925f7527202ea251a6949a18e2f03af4f5952
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="limit-report-history-report-manager"></a>Limitar el historial de informe (Administrador de informes)
  El historial de informes es un conjunto de instantáneas de informe que se crean a lo largo del tiempo. Puede crear el historial de informes a petición o programar la frecuencia con que una instantánea se crea y se agrega al historial de informes.  
  
 El historial de informes está almacenado en la base de datos del servidor de informes. Si las instantáneas de informes contienen una gran cantidad de datos, considere la posibilidad de limitar el historial de informes para minimizar el efecto de la retención de instantáneas en el tamaño de la base de datos.  
  
### <a name="to-configure-report-history-for-a-report-server"></a>Para configurar un historial del informe para un servidor de informes  
  
1.  En el Administrador de informes, haga clic en **Configuración del sitio** en la barra de herramientas global.  
  
2.  Seleccione **Conservar un número ilimitado de instantáneas en el historial de informe** si desea guardar todo el historial del informe indefinidamente. De lo contrario, seleccione **Limitar las copias del historial de informe** para especificar la cantidad máxima de instantáneas que se pueden guardar para un determinado informe.  
  
3.  Haga clic en **Aplicar**.  
  
### <a name="to-configure-report-history-for-a-specific-report"></a>Para configurar un historial de un informe específico  
  
1.  En el Administrador de informes, navegue al informe para el cual desea configurar el historial y, a continuación, haga clic en el informe para abrirlo.  
  
2.  Haga clic en la pestaña **Propiedades** .  
  
3.  Haga clic en la pestaña **Historial** .  
  
4.  Seleccione las opciones para el informe y haga clic en **Aplicar**. Para obtener más información sobre cada opción, vea [Página de propiedades de opciones de instantánea &#40;Administrador de informes&#41;](http://msdn.microsoft.com/library/f6641f59-5267-4f57-8957-63b93d1a9679).  
  
## <a name="see-also"></a>Vea también  
 [Agregar una instantánea para informar del historial &#40; El Administrador de informes &#41;](../../reporting-services/report-server/add-a-snapshot-to-report-history-report-manager.md)   
 [El Administrador de informes &#40; Modo nativo de SSRS &#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)  
  
  

