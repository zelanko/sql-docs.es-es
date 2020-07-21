---
title: Cancelar trabajos del servidor de informes (Management Studio) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
f1_keywords:
- sql13.swb.reportserver.cancelreportserverjobs.f1
ms.assetid: 1c5b4975-49e9-4d0b-b298-2638e81edbfd
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 8c433b8fcc0d768b3db48edf8bc56bed6440839a
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "65574219"
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
  
 **OK (CORRECTO)**  
 Cancele un trabajo único o varios trabajos. Los trabajos se cancelan inmediatamente y no se pueden reanudar. Si cancela un trabajo por error, debe solicitar de nuevo el informe o la suscripción para iniciar un nuevo trabajo.  
  
## <a name="see-also"></a>Consulte también  
 [Servidor de informes en Management Studio ayuda F1](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
 [Conectar con un servidor de informes en Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [Administración de un proceso en ejecución](../../reporting-services/subscriptions/manage-a-running-process.md)  
  
  
