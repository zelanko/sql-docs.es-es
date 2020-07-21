---
title: Ver eventos para el servicio de Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- events [Integration Services]
- service [Integration Services], events
- Integration Services service, events
ms.assetid: 37e23946-10d1-4116-8568-8fd24067102e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 57340afcbe1914b5e54ded06c8a7384ff33fd901
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85420142"
---
# <a name="view-events-for-the-integration-services-service"></a>Ver los eventos para el servicio Integration Services
  Hay dos herramientas en las que puede ver los eventos para el servicio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] :  
  
-   El cuadro de diálogo **Visor del archivo de registros** en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. El cuadro de diálogo **Visor del archivo de registros** incluye opciones para exportar, filtrar y buscar en el registro. Para obtener más información sobre las opciones del **Visor del archivo de registro**, vea [Ayuda F1 del Visor de archivos de registro](../relational-databases/logs/log-file-viewer-f1-help.md).  
  
-   El Visor de eventos de Windows.  
  
 Para obtener descripciones de los eventos registrados por el servicio de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , vea [Eventos registrados por el servicio Integration Services](service/events-logged-by-the-integration-services-service.md).  
  
### <a name="to-view-service-events-for-integration-services-in-sql-server-management-studio"></a>Para ver los eventos del servicio para Integration Services en SQL Server Management Studio  
  
1.  Abra [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
2.  En el menú **Archivo** , haga clic en **Conectar Explorador de objetos**.  
  
3.  En el cuadro de diálogo **Conectar al servidor** , seleccione el tipo de servidor [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , seleccione o localice el servidor al que desea conectarse y haga clic en **Conectar**.  
  
4.  En el Explorador de objetos, haga clic con el botón derecho en [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] y, después, haga clic en **Ver registros**.  
  
5.  Para ver los eventos de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , seleccione **SQL Server Integration Services**. La opción **Eventos NT** se selecciona automáticamente y se borra con la opción **SQL Server Integration Services** .  
  
### <a name="to-view-service-events-for-integration-services-in-windows-event-viewer"></a>Para ver los registros de eventos para Integration Services en el Visor de eventos de Windows  
  
1.  En el **Panel de control**, si utiliza la Vista clásica, haga clic en **Herramientas administrativas**o bien, si utiliza la Vista por categorías, haga clic en **Rendimiento y mantenimiento** y, a continuación, en **Herramientas administrativas**.  
  
2.  Haga clic en **Visor de eventos**.  
  
3.  En el cuadro de diálogo **Visor de eventos** , haga clic en **Aplicación**.  
  
4.  En el complemento **Aplicación** , localice una entrada en la columna **Origen** que contenga el valor **SQLISService**, haga clic con el botón derecho en la entrada y, después, haga clic en **Propiedades**.  
  
5.  O bien, haga clic en la flecha arriba o abajo para ver el evento anterior o el siguiente.  
  
6.  Si lo desea, puede hacer clic en el icono Copiar al Portapapeles para copiar la información del evento.  
  
7.  Elija si desea ver los datos del evento en bytes o en palabras.  
  
8.  Haga clic en **OK**.  
  
9. En el menú **Archivo** , haga clic en **Salir** para salir del cuadro de diálogo **Visor de eventos** .  
  
## <a name="see-also"></a>Consulte también  
 [Administrar el servicio de Integration Services](../../2014/integration-services/manage-the-integration-services-service.md)   
 [Agregar un registro para los contadores de rendimiento del flujo de datos](performance/performance-counters.md)  
  
  
