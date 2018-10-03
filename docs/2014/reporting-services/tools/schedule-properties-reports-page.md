---
title: Propiedades de la programación (página Informes) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.scheduleproperties.reports.f1
ms.assetid: 7db728bd-4b08-43ef-a49a-e8dcdd37cf89
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 635a5428685feff5887b0800388a41f95a108c1a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48209235"
---
# <a name="schedule-properties-reports-page"></a>Propiedades de la programación (página Informes)
  Utilice esta página para ver una lista de todos los informes que utilizan esta programación compartida. Las programaciones pueden utilizarse para actualizar instantáneas de informe, generar un historial de informes, desencadenar una suscripción o hacer expirar una copia del informe almacenada en caché. Para averiguar cómo se usa la programación, vea la información de propiedad y suscripciones del informe.  
  
 Aunque esta página muestra cada informe que usa la programación compartida, no indica cuántas veces se usa la programación compartida dentro de ese informe único. Por ejemplo, supongamos que 20 diferentes suscriptores al informe Company Sales usan la misma programación compartida para desencadenar el procesamiento de suscripciones. En este caso, el informe Company Sales solamente aparecerá una vez en esta lista, aunque el informe tenga 20 referencias a la programación compartida.  
  
 Para abrir esta página, inicie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conectarse a un servidor de informes, abra el **programaciones compartidas** carpeta, haga clic en una programación compartida, seleccione **propiedades**y, a continuación, haga clic en **informes** .  
  
> [!NOTE]  
>  Esta característica no está disponible en todas las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Características compatibles con las ediciones de SQL Server 2012](http://go.microsoft.com/fwlink/?linkid=232473) (http://go.microsoft.com/fwlink/?linkid=232473).  
  
## <a name="options"></a>Opciones  
 **Carpeta**  
 Especifica la ruta de acceso del informe.  
  
 **Informe**  
 Especifica el nombre del informe que utiliza la programación.  
  
## <a name="see-also"></a>Vea también  
 [Crear, modificar y eliminar programaciones](../subscriptions/create-modify-and-delete-schedules.md)   
 [Programaciones](../subscriptions/schedules.md)   
 [Servidor de informes en Management Studio ayuda F1](report-server-in-management-studio-f1-help.md)   
 [Conectar con un servidor de informes en Management Studio](connect-to-a-report-server-in-management-studio.md)   
 [Configurar las propiedades generales de un informe &#40;el Administrador de informes&#41;](../configure-general-properties-for-a-report-report-manager.md)  
  
  
