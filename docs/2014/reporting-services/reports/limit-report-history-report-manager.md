---
title: Limitar el historial de informe (Administrador de informes) | Microsoft Docs
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
- viewing report history
- report history [Reporting Services], viewing history
- report history [Reporting Services], configuring history
- historical data [Reporting Services]
- displaying report history
ms.assetid: 8e255792-d9ef-496f-a26c-9e969c1209a0
caps.latest.revision: 35
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 91bb20ac70caf7d7d3e863c975415205badbc063
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36108269"
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
  
4.  Seleccione las opciones para el informe y haga clic en **Aplicar**. Para más información sobre cada opción, vea [Página de propiedades de opciones de instantánea &#40;Administrador de informes&#41;](../snapshot-options-properties-page-report-manager.md).  
  
## <a name="see-also"></a>Vea también  
 [Agregar una instantánea al historial del informe &#40;el Administrador de informes&#41;](../report-server/add-a-snapshot-to-report-history-report-manager.md)   
 [Administrador de informes &#40;Modo nativo de SSRS&#41;](../report-manager-ssrs-native-mode.md)  
  
  