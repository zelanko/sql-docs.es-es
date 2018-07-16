---
title: Cancelar trabajos del servidor de informes (Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.cancelreportserverjobs.f1
ms.assetid: 1c5b4975-49e9-4d0b-b298-2638e81edbfd
caps.latest.revision: 13
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 9995d9df8ee2a4a11dc43a36e1853bbf60667c54
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37248045"
---
# <a name="cancel-report-server-jobs-management-studio"></a>Cancelar trabajos del servidor de informes (Management Studio)
  Use el cuadro de diálogo **Cancelar trabajos del Servidor de informes** para ver o cancelar los informes en curso. Este cuadro de diálogo muestra todos los trabajos que se están ejecutando actualmente en el servidor de informes. Aunque no puede pausar o reiniciar trabajos que se están procesando actualmente, puede cancelar todos los trabajos o los trabajos individuales si están tardando demasiado tiempo en completarse.  
  
 Se pueden cancelar trabajos de usuario y del sistema.  
  
-   Un trabajo de usuario es cualquier trabajo que haya iniciado un usuario individual; por ejemplo, ejecutar un informe a petición, crear manualmente una instantánea del historial de informes o crear manualmente una instantánea de ejecución de informe. Una suscripción estándar en curso es también un trabajo de usuario.  
  
-   Un trabajo del sistema es un trabajo iniciado por el servidor de informes; Los trabajos del sistema incluyen el procesamiento de informes programados.  
  
 Para abrir esta página, inicie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conéctese a un servidor de informes, haga clic con el botón derecho en **Trabajos**y, después, haga clic en **Cancelar todos los trabajos**. También puede abrir **Trabajos**, hacer clic con el botón derecho en un trabajo que se está ejecutando en el servidor de informes y seleccionar **Cancelar trabajos**.  
  
 Antes de cancelar un trabajo, puede ver sus propiedades para determinar cuándo se inició el trabajo. Para obtener más información, vea [Propiedades del trabajo &#40;Management Studio&#41;](job-properties-management-studio.md).  
  
> [!NOTE]  
>  Esta característica no se admite en [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] con Advanced Services. La página no aparece cuando se ejecuta [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)].  
  
## <a name="options"></a>Opciones  
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
  
## <a name="see-also"></a>Vea también  
 [Servidor de informes en Management Studio ayuda F1](report-server-in-management-studio-f1-help.md)   
 [Conectar con un servidor de informes en Management Studio](connect-to-a-report-server-in-management-studio.md)   
 [Administrar un proceso en ejecución](../subscriptions/manage-a-running-process.md)  
  
  
