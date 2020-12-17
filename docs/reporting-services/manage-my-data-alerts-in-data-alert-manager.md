---
title: Administrar mis alertas de datos en el Administrador de alertas de datos | Microsoft Docs
description: Aprenda a ver una lista de las alertas de datos que se han creado e información sobre las alertas en el Administrador de alertas de datos.
ms.date: 08/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- managing, alerts
- managing, data alerts
ms.assetid: e0e4ffdf-bd4c-4ebd-872b-07486cbb47c2
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016'
ms.openlocfilehash: db36e1374b94c95691b73e97837aa025d4fb07d1
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97477106"
---
# <a name="manage-my-data-alerts-in-data-alert-manager"></a>Administrar mis alertas de datos en el Administrador de alertas de datos

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../includes/ssrs-appliesto-not-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

Los usuarios de SharePoint pueden ver una lista de las alertas de datos que han creado e información acerca de las alertas. También pueden eliminar sus alertas, abrir las definiciones de las alertas para modificarlas en el Diseñador de alertas de datos y ejecutar sus alertas. En la imagen siguiente se muestran las características disponibles en el Administrador de alertas de datos para los usuarios.

 ![Características del Administrador de alertas para los usuarios de SharePoint](../reporting-services/media/rs-alertmanageriw.gif "Características del Administrador de alertas para los usuarios de SharePoint")

> [!NOTE]
> La integración de Reporting Services con SharePoint ya no está disponible a partir de SQL Server 2016.

### <a name="to-view-a-list-of-your-alerts"></a>Para ver una lista de sus alertas  
  
1.  Vaya a la biblioteca de SharePoint donde guardó los informes para los que creó alertas de datos.  
  
2.  Haga clic en el icono para expandir el menú desplegable de un informe y haga clic en **Administrar alertas de datos**. La imagen siguiente muestra el menú desplegable.  
  
     ![Abrir el Administrador de alertas desde el menú contextual del informe](../reporting-services/media/rs-openalertmanager.gif "Abrir el Administrador de alertas desde el menú contextual del informe")  
  
     Se abre el Administrador de alertas de datos. De forma predeterminada, se muestran las alertas del informe que seleccionó en la biblioteca.  
  
3.  Haga clic en la flecha abajo que aparece junto a la lista **Ver las alertas del informe** y seleccione un informe para ver sus alertas, o haga clic en **Mostrar todas** para ver todas las alertas.  
  
    > [!NOTE]  
    >  Si el informe que seleccionó no tiene ninguna alerta, no tiene que volver a la biblioteca de SharePoint para buscar y seleccionar un informe que tenga alertas. En su lugar, haga clic en **Mostrar todas** para ver una lista de todas sus alertas.  
  
     Aparece una tabla con el nombre de la alerta, el nombre del informe, su nombre como creador de la alerta, el número de veces que se envió la alerta, la última vez que se modificó la definición de la alerta y el estado de la alerta. Si la alerta no se puede generar o enviar, la columna de estado contiene información sobre el error que le ayudará a solucionar el problema.  
  
### <a name="to-edit-an-alert-definition"></a>Para editar una definición de alerta  
  
-   Haga clic con el botón derecho en la alerta de datos cuya definición de alerta quiere modificar y haga clic en **Editar**.  
  
     La definición de alerta se abre en el Diseñador de alertas de datos. Para más información, vea [Modificar una alerta de datos en el Diseñador de alertas](../reporting-services/edit-a-data-alert-in-alert-designer.md) y [Diseñador de alertas de datos](../reporting-services/data-alert-designer.md).  
  
    > [!NOTE]  
    >  Solo el usuario que creó la definición de alerta de datos puede modificarla.  
  
    > [!NOTE]  
    >  Si el informe ha cambiado y las fuentes de distribución de datos generadas desde el informe han cambiado, la definición de la alerta podría no ser válida. Esto sucede cuando una columna a la que hacen referencia las reglas de la alerta se elimina del informe, su tipo de datos cambia, se incluye en otra fuente de distribución de datos o se elimina o mueve el informe. Puede abrir una definición de alerta que no sea válida, pero no puede volver a guardarla hasta que sea válida con arreglo a la versión actual de la fuente de distribución de datos del informe en la que se basa. Para más información sobre cómo se generan las fuentes de datos de informes, vea [Generar fuentes de distribución de datos a partir de informes &#40;Generador de informes y SSRS&#41;](../reporting-services/report-builder/generating-data-feeds-from-reports-report-builder-and-ssrs.md).  
  
### <a name="to-delete-an-alert-definition"></a>Para eliminar una definición de alerta  
  
-   Haga clic con el botón derecho en la alerta de datos que quiere eliminar y haga clic en **Eliminar**.  
  
     Después de eliminar la alerta, no se envían más mensajes de alerta.  
  
### <a name="to-run-an-alert"></a>Para ejecutar una alerta  
  
-   Haga clic con el botón derecho en la alerta de datos que quiere ejecutar y haga clic en **Ejecutar**.  
  
     Se crea la instancia de alerta y el mensaje de alerta de datos se envía inmediatamente, independientemente de las opciones de programación que haya especificado en el Diseñador de alertas de datos. Por ejemplo, se enviará una alerta configurada para su envío semanal y solo si cambian los resultados.  

## <a name="see-also"></a>Consulte también

[Administrador de alertas de datos para administradores de alertas](../reporting-services/data-alert-manager-for-alerting-administrators.md)   
[Alertas de datos de Reporting Services](../reporting-services/reporting-services-data-alerts.md)  

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231).
