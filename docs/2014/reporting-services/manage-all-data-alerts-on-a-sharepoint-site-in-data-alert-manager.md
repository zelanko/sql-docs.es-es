---
title: Administrar todas las alertas de datos de un sitio de SharePoint en el Administrador de alertas de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- managing, alerts
- managing, data alerts
ms.assetid: 9c70b0f4-2db8-4c2e-acbf-96e2a55ddc48
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: debf7415a6364a358bb92066d53b840bcecd5930
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108340"
---
# <a name="manage-all-data-alerts-on-a-sharepoint-site-in-data-alert-manager"></a>Administrar todas las alertas de datos de un sitio de SharePoint en el Administrador de alertas de datos
  Los administradores de alertas de SharePoint pueden ver una lista de las alertas de datos creadas por los usuarios del sitio e información acerca de las alertas. Los administradores de alertas también pueden eliminar alertas. En la imagen siguiente se muestran las características disponibles para los administradores de alertas en el Administrador de alertas de datos.  
  
 ![Administrador de alertas para administradores de sitios de SharePoint](media/rs-alertmanagersite.gif "Administrador de alertas para administradores de sitios de SharePoint")  
  
### <a name="to-view-a-list-of-alerts-created-by-a-site-user"></a>Para ver una lista de las alertas creadas por un usuario del sitio  
  
1.  Vaya al sitio de SharePoint donde se guardan las definiciones de alertas de datos.  
  
2.  En la página Inicio, haga clic en **Acciones del sitio**.  
  
3.  Desplácese a la parte inferior de la lista y haga clic en **Configuración del sitio**.  
  
4.  En **Reporting Services**, haga clic en **Administrar alertas de datos**.  
  
5.  Haga clic en la flecha hacia abajo situada junta a la lista **Ver las alertas del usuario** y seleccione el usuario cuyas alertas desea ver.  
  
6.  Haga clic en la flecha hacia abajo que aparece junto a la lista **Ver las alertas del informe** y seleccione la alerta específica que desea ver, o haga clic en **Mostrar todas** para ver todas las alertas creadas por el usuario seleccionado.  
  
     En una tabla se muestra el nombre de la alerta, el nombre del informe, el nombre de la persona que creó la alerta de datos, el número de veces que se envió la alerta de datos, la última vez que se modificó la definición de la alerta de datos y el estado de la alerta de datos. Si la alerta de datos no se puede generar o enviar, la columna de estado contiene información sobre el error que le ayudará a solucionar el problema.  
  
### <a name="to-delete-an-alert-definition"></a>Para eliminar una definición de alerta  
  
-   Haga clic con el botón derecho en la alerta de datos que quiera eliminar y haga clic en **Eliminar**.  
  
    > [!NOTE]  
    >  Después de eliminar la alerta, no se envían más mensajes de alerta. Sin embargo, si consulta la base de datos de alertas puede que todavía exista la definición de la alerta. El servicio de alertas realiza limpiezas según una programación, y la definición de la alerta se eliminará definitivamente durante la limpieza siguiente. El intervalo de limpieza predeterminado es de 20 minutos. Este y otros intervalos de limpieza son configurables. Para obtener más información, vea [Alertas de datos de Reporting Services](../ssms/agent/alerts.md).  
  
## <a name="see-also"></a>Vea también  
 [Administrador de alertas de datos para administradores de alertas](../../2014/reporting-services/data-alert-manager-for-alerting-administrators.md)   
 [Alertas de datos de Reporting Services](../ssms/agent/alerts.md)  
  
  
