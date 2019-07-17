---
title: Iniciar o detener un Power Pivot para SharePoint Server | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4b53cc7730f962d790ebdb9a0373bf98e9bf32bf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208096"
---
# <a name="start-or-stop-a-power-pivot-for-sharepoint-server"></a>Iniciar o detener un servidor de Power Pivot para SharePoint
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] y una instancia de [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] operan conjuntamente en el mismo servidor de aplicaciones local para admitir el procesamiento de solicitudes y datos coordinado en una granja de servidores de SharePoint.  
  
 Este tema contiene las siguientes secciones:  
  
 [Dependencias de los servicios](#dependencies)  
  
 [Iniciar o detener los servicios](#startstop)  
  
 [Efectos de la detención de un servidor de Power Pivot](#effects)  
  
##  <a name="dependencies"></a> Dependencias de los servicios  
 El Servicio de sistema de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] depende de la instancia de servidor de Analysis Services local que se instala con él en el mismo servidor físico. Si detiene el Servicio de sistema de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , también debe detener manualmente la instancia de servidor de Analysis Services local. Si un servicio está en ejecución sin el otro, se producirán errores de asignación de solicitudes para el procesamiento de datos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
 El servidor de Analysis Services solo se debería ejecutar si va a diagnosticar o solucionar un problema. En todos los demás casos, el servidor requiere que el Servicio de sistema de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] se ejecute localmente en el mismo servidor.  
  
##  <a name="startstop"></a> Iniciar o detener los servicios  
 Use siempre Administración central para iniciar o detener el Servicio de sistema de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] o la instancia del servidor de Analysis Services. Administración central le permite iniciar o detener servicios juntos desde la misma página. Además, la Administración central usa un trabajo de temporizador denominado **Uno o más servicios se iniciaron o detuvieron inesperadamente** para reiniciar los servicios que cree que deberían estar en ejecución. Si detiene el Servicio de sistema de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] o Analysis Services mediante una herramienta que no es de SharePoint, los servicios se reiniciarán cuando se ejecute el trabajo de temporizador.  
  
 El inicio y la detención de los servicios son acciones que se aplican a una instancia de servicio física. Si tiene servidores de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint adicionales en la granja, los demás servidores dentro de la granja continuarán aceptando solicitudes de los datos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
 No puede iniciar o detener simultáneamente todos los servicios físicos en la granja. Debe seleccionar cada servidor y, a continuación, iniciar o detener un servicio determinado.  
  
 No puede iniciar, pausar ni detener un Servicio de sistema de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para una aplicación web específica, pero puede quitar un servicio de la lista de conexiones predeterminada para conseguir que no esté disponible. Para más información, vea [Conectar una aplicación de servicio PowerPivot a una aplicación web de SharePoint en Administración central de](../../analysis-services/power-pivot-sharepoint/connect-power-pivot-service-app-to-sharepoint-web-app-in-ca.md).  
  
1.  En Administración central, en **Configuración del sistema**, haga clic en **Administrar los servicios del servidor**.  
  
2.  En la parte superior de la página, en Servidor, haga clic en la flecha abajo y, a continuación, haga clic en **Cambiar el servidor**.  
  
3.  Seleccione el servidor de SharePoint que tiene el Servicio de sistema de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] o la instancia de [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] que desee iniciar o detener.  
  
4.  Seleccione el servicio y haga clic en la acción. Recuerde iniciar o detener los servicios como un par. Si inicia o detiene el Servicio de sistema de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , asegúrese de iniciar o detener también la instancia de servidor de Analysis Services que se ejecuta en el mismo equipo.  
  
##  <a name="effects"></a> Efectos de la detención de un servidor de Power Pivot  
 La tabla siguiente describe los efectos que tiene detener el servicio de Analysis Services y el Servicio de sistema de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en un servidor de SharePoint.  
  
|Efecto en|Descripción|  
|---------------|-----------------|  
|Consultas existentes|Las consultas que están en curso en un servidor de Analysis Services se detendrán inmediatamente. El usuario obtendrá un error que indica que los datos o que la conexión a un origen de datos no se han encontrado.|  
|Trabajos de actualización de datos que se están procesando actualmente|Los trabajos que están en curso en el servidor de Analysis Services actual se detendrán inmediatamente. Se producirá un error en la actualización de datos que se registrará en el historial de la actualización de datos.<br /><br /> Puede ver el estado de los trabajos actuales antes de detener el servicio mediante la página de comprobación del estado de los trabajos de Administración central de SharePoint.<br /><br /> Aunque es posible saber qué trabajos se están procesando actualmente, no hay ninguna manera de ver la propia cola para comprobar si otros trabajos están a punto de iniciarse.|  
|Solicitudes de actualización de datos existentes en la cola|Las solicitudes de actualización de datos programadas permanecerán en la cola de procesamiento durante un ciclo completo de la programación (es decir, se quedan en la cola hasta que tengan que volver a iniciarse). Si el Servicio de sistema de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no se reinicia a continuación, se quitará la solicitud de actualización de datos y se registrará un error.|  
|Nuevas solicitudes de consultas o actualización de datos|Si va a detener el único servidor de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint de la granja, las nuevas solicitudes de datos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no se controlarán y, en caso de que se produzca una solicitud de datos, se generará un error que indica que estos no se encuentran.<br /><br /> Si tiene más servidores de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint, la solicitud irá a uno de los servidores disponibles.|  
|Datos de uso|No se recopilarán datos de uso mientras se detienen los servicios.|  
  
## <a name="see-also"></a>Vea también  
 [Configurar las cuentas de servicio Power Pivot](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts.md)  
  
  
