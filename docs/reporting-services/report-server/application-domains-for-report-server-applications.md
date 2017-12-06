---
title: "Dominios de aplicación para las aplicaciones del servidor de informes | Microsoft Docs"
ms.custom: 
ms.date: 03/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-server
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- application domains [Reporting Services]
- recycling application domains
ms.assetid: a455e2e6-8764-493d-a1bc-abe80829f543
caps.latest.revision: "18"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: ce02d45295537bf9eef80816f7099a4697ddfd1c
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="application-domains-for-report-server-applications"></a>Dominios de aplicación para las aplicaciones del servidor de informes
  En [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], el servidor de informes se implementa como un servicio único que contiene el servicio web del servidor de informes, el Administrador de informes y una aplicación de procesamiento de fondo. Cada aplicación se ejecuta en su propio dominio de aplicación dentro del proceso del servidor de informes único. En su mayor parte, los dominios de aplicación se crean, configuran y administran internamente. Sin embargo, saber cómo se producen las operaciones de reciclaje para los dominios de aplicación del servidor de informes puede resultar útil si está investigando problemas de rendimiento o memoria, o resolviendo los problemas de las interrupciones del servicio.  
  
> [!NOTE]  
>  Si configura el acceso al Generador de informes en un servidor de informes que utiliza la autenticación básica, el Generador de informes se ejecutará en su propio dominio de aplicación. Este dominio de aplicación es diferente de otros dominios de aplicación que se ejecutan en el proceso de servidor. Es administrado por el Controlador del servicio y no está sujeto a las características de administración de memoria que vuelven a ajustar la asignación de memoria en respuesta a la presión de memoria en el servidor de informes.  
  
 En la lista siguiente se describen los eventos que producen las operaciones de reciclaje de dominio de aplicación para las aplicaciones de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] :  
  
-   Operaciones de reciclaje programadas que se producen en intervalos predefinidos  
  
-   Cambios de configuración en el servidor de informes  
  
-   [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] cambios de configuración.  
  
-   Errores de asignación de memoria  
  
 En la tabla siguiente se resume el comportamiento de reciclaje de dominio de aplicación en respuesta a estos eventos:  
  
|Evento|Descripción del evento|Se aplica a|Configurable|Descripción de la operación de reciclaje|  
|-----------|-----------------------|----------------|------------------|-----------------------------------|  
|Operaciones de reciclaje programadas que se producen en intervalos predefinidos|De forma predeterminada, los dominios de aplicación se reciclan cada 12 horas.<br /><br /> Las operaciones de reciclaje programadas son una práctica común para aplicaciones de [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] que consiguen mantener el buen estado general del proceso.|Servicio web del servidor de informes<br /><br /> Administrador de informes<br /><br /> Aplicación de procesamiento de fondo|Sí. El valor de configuración**RecycleTime** del archivo RSReportServer.config determina el intervalo de reciclaje.<br /><br /> **MaxAppDomainUnloadTime** establece el tiempo de espera durante el cual se puede completar el procesamiento de fondo.|[!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] administra la operación de reciclaje para el servicio web y el Administrador de informes.<br /><br /> Para la aplicación de procesamiento de fondo, el servidor de informes crea un nuevo dominio de aplicación para los nuevos trabajos que se inician desde las programaciones. Los trabajos ya en curso pueden completarse en el dominio de aplicación actual hasta que expire el tiempo de espera.|  
|Cambios de configuración en el servidor de informes|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] reciclará los dominios de aplicación en respuesta a los cambios del archivo RSReportServer.config.|Servicio web del servidor de informes<br /><br /> Administrador de informes<br /><br /> Aplicación de procesamiento de fondo|No.|No puede detener las operaciones de reciclaje. Sin embargo, las operaciones de reciclaje que se producen en respuesta a los cambios de configuración se controlan de la misma manera que las operaciones de reciclaje programadas. Los nuevos dominios de aplicación se crean para nuevas solicitudes mientras se completan los trabajos y las solicitudes actuales en el dominio de aplicación actual.|  
|[!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] cambios de configuración|[!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] reciclará los dominios de aplicación si se producen cambios en los archivos que supervisa (por ejemplo, los archivos machine.config y Web.config, y los archivos de programa de [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] ).|Servicio web del servidor de informes<br /><br /> Administrador de informes|No.|[!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] administra la operación.<br /><br /> Las operaciones de reciclaje que se inician a través de [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] no afectan al dominio de aplicación de procesamiento de fondo.|  
|Errores en la asignación de memoria y presión de memoria|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] reciclará inmediatamente los dominios de aplicación en caso de que se produzca un error de asignación de memoria o cuando el servidor se encuentre en situaciones de presión de memoria.|Servicio web del servidor de informes<br /><br /> Administrador de informes<br /><br /> Aplicación de procesamiento de fondo|No.|Con presión de memoria, el servidor de informes no aceptará las nuevas solicitudes en el dominio de aplicación actual. Durante el período en el que el servidor deniega nuevas solicitudes, se producen errores de HTTP 503. No se crearán nuevos dominios de aplicación hasta que se descargue el dominio de aplicación anterior. Esto significa que si realiza un cambio de archivo de configuración mientras el servidor se encuentra con alta presión de memoria, las solicitudes y los trabajos que se encuentran en curso podrían no iniciarse o completarse.<br /><br /> En caso de error de asignación de memoria, todos los dominios de aplicación se reinician inmediatamente. Se quitan los trabajos y solicitudes que se encuentran en curso. Debe reiniciar dichos trabajos y solicitudes manualmente.|  
  
## <a name="planned-and-unplanned-recycle-operations"></a>Operaciones de reciclaje planeadas e imprevistas  
 Las operaciones de reciclaje son planeadas o imprevistas dependiendo de las condiciones que provocan la operación:  
  
-   Las operaciones de reciclaje planeadas se producen en intervalos normales que se definen en el archivo RSReportServer.config. El valor predeterminado es cada 12 horas. Ésta es una práctica común para aplicaciones [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] que fomentan el mantenimiento del buen estado general del proceso. Para operaciones de reciclaje planeadas, el servidor de informes crea dominios de aplicación adicionales para las nuevas solicitudes. Las solicitudes que ya se encuentran en curso pueden completarse en el dominio de aplicación actual hasta que expire el tiempo de espera. Los valores de configuración que rigen las operaciones de reciclaje planeadas se establecen para el servidor en su conjunto. No puede configurar una programación de reciclaje o un umbral de memoria diferentes para cada aplicación.  
  
-   Las operaciones de reciclaje imprevistas se producen en momentos arbitrarios en respuesta a cambios de configuración, alta presión de memoria y errores de asignación de memoria:  
  
    -   Para los cambios de configuración, el servidor de informes intentará usar un reciclaje sin reinicio de dominios de aplicación que redirige las nuevas solicitudes a una nueva instancia del dominio de aplicación. Si se produce un error en el reciclaje sin reinicio de dominios de aplicación, el servidor inicia un reciclaje con reinicio de dominios de aplicación que cancela todas las solicitudes en curso, cierra los dominios de aplicación actuales y reinicia los dominios de aplicación.  
  
    -   Los errores de asignación de memoria indican que los recursos del sistema son insuficientes para la cantidad del procesamiento de informes realizado por el servidor. Se produce una operación de reciclaje con reinicio de dominios de aplicación para todos los dominios de aplicación en respuesta a un error de asignación de memoria. Se borran todas las colas de solicitudes. No se reinician las solicitudes canceladas. Los usuarios que estaban viendo un informe interactivamente deben actualizar o volver a abrir el informe. El procesamiento programado afectado por un error se cancelará y se realizará la próxima vez que se ejecute el procesamiento programado. Si el retraso es inaceptable, puede actualizar una instantánea de informe manualmente o modificar una programación de suscripción o una programación de instantánea de informe de manera que se ejecute inmediatamente.  
  
 Los dominios de aplicación para el servicio web del servidor de informes, el Administrador de informes y la aplicación de procesamiento de fondo se podrían reciclar de manera conjunta o individualmente, dependiendo de las circunstancias que hacen que se produzca el reciclaje:  
  
-   Las operaciones de reciclaje iniciadas por [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] solamente afectan a las aplicaciones de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] : el servicio web del servidor de informes y el Administrador de informes. [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] reciclará los dominios de aplicación basándose en si hay cambios en los archivos que supervisa. Las operaciones de reciclaje que se inician a través de [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] normalmente son independientes de las operaciones de reciclaje para la aplicación de procesamiento de fondo.  
  
-   Las operaciones de reciclaje iniciadas por el servidor de informes afectan normalmente al servicio web del servidor de informes, al Administrador de informes y a la aplicación de procesamiento de fondo. Las operaciones de reciclaje se producen en respuesta a los cambios a los valores de configuración y se reinicia el servicio.  
  
## <a name="rsreportserver-configuration-settings-for-application-domains"></a>Valores de configuración de RSReportServer para dominios de aplicación  
 Los valores de configuración se especifican en el archivo [RSReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md). El ejemplo siguiente muestra los valores de configuración predeterminados para el comportamiento de reciclaje del dominio de aplicación.  
  
 `<RecycleTime>720</RecycleTime>`  
  
 `<MaxAppDomainUnloadTime>30</MaxAppDomainUnloadTime>`  
  
 Estos elementos se describen en la siguiente tabla.  
  
|Elemento|Se aplica a|Definición|  
|-------------|----------------|----------------|  
|**RecycleTime**|Los tres dominios de aplicación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|Especifica la frecuencia con la que se reciclan los dominios de aplicación. La programación de reciclaje predeterminada se ajusta al patrón de 12 horas, seguido normalmente del reciclaje de dominio de aplicación de [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] . A la hora programada, todas las solicitudes nuevas se reenvían a una nueva instancia del dominio de aplicación. Las solicitudes que se encuentran actualmente en curso en la instancia original pueden completarse. Una vez que se completan todos los procesos, se elimina la instancia original y la nueva instancia pasa a ser la única instancia de dominio de aplicación activa<br /><br /> El valor predeterminado es de 720 minutos.|  
|**MaxAppDomainUnloadTime**|Solo dominio de aplicación de procesamiento de fondo|De manera predeterminada, un servidor de informes asigna un tiempo de espera de 30 minutos, durante el cual el dominio de aplicación puede cerrarse mientras se produce una operación de reciclaje. Si los trabajos que están actualmente en curso no se pueden completar durante el tiempo asignado (o si un trabajo tarda más de lo que permite el tiempo de espera), la instancia del dominio de aplicación se reinicia inmediatamente. Todos los trabajos incompletos finalizan.<br /><br /> Para más información sobre cómo ver el estado o cancelar trabajos que se ejecutan en el servidor de informes, vea [Cancelar trabajos del servidor de informes &#40;Management Studio&#41;](../../reporting-services/tools/cancel-report-server-jobs-management-studio.md).|  
  
> [!NOTE]  
>  Aunque el servicio web del servidor de informes y el Administrador de informes son aplicaciones [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] , ninguna aplicación responde al reciclaje de dominio de aplicación programado que se podría especificar en machine.config para aplicaciones [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] hospedadas en IIS.  
  
## <a name="see-also"></a>Vea también  
 [El archivo de configuración RSReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [Modificar un archivo de configuración de Reporting Services &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)   
 [Configuración de la memoria disponible para las aplicaciones del servidor de informes](../../reporting-services/report-server/configure-available-memory-for-report-server-applications.md)  
  
  
