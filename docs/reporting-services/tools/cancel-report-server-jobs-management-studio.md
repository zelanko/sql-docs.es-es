---
title: Cancelar trabajos del servidor de informes (Management Studio) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: tools
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.reportserver.cancelreportserverjobs.f1
ms.assetid: 1c5b4975-49e9-4d0b-b298-2638e81edbfd
caps.latest.revision: "14"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d0ea49d4e9d399f5027f235bce8b895d063ed4e7
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2018
---
# <a name="cancel-report-server-jobs-management-studio"></a>Cancelar trabajos del servidor de informes (Management Studio)
  Use el cuadro de diálogo **Cancelar trabajos del Servidor de informes** para ver o cancelar los informes en curso. Este cuadro de diálogo muestra todos los trabajos que se están ejecutando actualmente en el servidor de informes. Aunque no puede pausar o reiniciar trabajos que se están procesando actualmente, puede cancelar todos los trabajos o los trabajos individuales si están tardando demasiado tiempo en completarse.  
  
 Se pueden cancelar trabajos de usuario y del sistema.  
  
-   Un trabajo de usuario es cualquier trabajo que haya iniciado un usuario individual; por ejemplo, ejecutar un informe a petición, crear manualmente una instantánea del historial de informes o crear manualmente una instantánea de ejecución de informe. Una suscripción estándar en curso es también un trabajo de usuario.  
  
-   Un trabajo del sistema es un trabajo iniciado por el servidor de informes; Los trabajos del sistema incluyen el procesamiento de informes programados.  
  
 Para abrir esta página, inicie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conéctese a un servidor de informes, haga clic con el botón derecho en **Trabajos**y, después, haga clic en **Cancelar todos los trabajos**. También puede abrir **Trabajos**, hacer clic con el botón derecho en un trabajo que se está ejecutando en el servidor de informes y seleccionar **Cancelar trabajos**.  
  
 Antes de cancelar un trabajo, puede ver sus propiedades para determinar cuándo se inició el trabajo. Para obtener más información, vea [Propiedades del trabajo &#40;Management Studio&#41;](../../reporting-services/tools/job-properties-management-studio.md).  
  
> [!NOTE]  
>  Esta característica no se admite en [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] con Advanced Services. La página no aparece cuando se ejecuta [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)].  
  
## <a name="options"></a>.  
 **Nombre**  
 Muestra el nombre del informe. Las suscripciones se identifican con su descripción.  
  
 **Tipo**  
 Los valores válidos son **Usuario** y **Sistema**.  
  
 **Start Time**  
 Muestra cuándo se inició el trabajo.  
  
 **Nombre de usuario**  
 Para los trabajos iniciados por un usuario, esta columna muestra el nombre del usuario.  
  
 **Estado**  
 Muestra el estado del trabajo. Los valores válidos son **Nuevo** y **En ejecución**. Estado siempre es **Nuevo** cuando comienza el trabajo. Después de 60 segundos, el estado cambia a **En ejecución**. Debe actualizar la página para que se refleje el cambio.  
  
 **Aceptar**  
 Cancele un trabajo único o varios trabajos. Los trabajos se cancelan inmediatamente y no se pueden reanudar. Si cancela un trabajo por error, debe solicitar de nuevo el informe o la suscripción para iniciar un nuevo trabajo.  
  
## <a name="see-also"></a>Ver también  
 [Servidor de informes en Management Studio ayuda F1](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
 [Conectar con un servidor de informes en Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [Administrar un proceso en ejecución](../../reporting-services/subscriptions/manage-a-running-process.md)  
  
  
