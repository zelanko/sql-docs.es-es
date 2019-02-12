---
title: Configurar la memoria disponible para las aplicaciones del servidor de informes | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- memory [Reporting Services]
- memory thresholds [Reporting Services]
ms.assetid: ac7ab037-300c-499d-89d4-756f8d8e99f6
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: e3d07c9739a7c0b8989bb22f79c03f03e1f46681
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56027902"
---
# <a name="configure-available-memory-for-report-server-applications"></a>Configurar la memoria disponible para las aplicaciones del servidor de informes
  Aunque [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] puede usar toda la memoria disponible, puede invalidar el comportamiento predeterminado configurando un límite superior en la cantidad total de los recursos de memoria asignados a las aplicaciones de servidor [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] . También puede establecer umbrales que hacen que el servidor de informes cambie la manera de asignar prioridades y procesa las solicitudes dependiendo de si la presión de memoria es baja, media o alta. En niveles bajos de presión de memoria, el servidor de informes responde concediendo una prioridad ligeramente superior al procesamiento de informes a petición o interactivo. En los niveles altos de presión de memoria, el servidor de informes usa varias técnicas para seguir siendo operativo usando los recursos limitados que están disponibles para él.  
  
 En este tema se describe la configuración que puede especificar y la manera en la que el servidor responde cuando la presión de memoria se convierte en un factor en las solicitudes de procesamiento.  
  
## <a name="memory-management-policies"></a>Directivas de administración de memoria  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] responde a las restricciones de recursos del sistema ajustando la cantidad de memoria que se asigna a aplicaciones concretas y tipos de solicitudes de procesamiento. Entre las aplicaciones que se ejecutan en el servicio del servidor de informes y que están sujetas a la administración de memoria se incluyen:  
  
-   El Administrador de informes, que es una aplicación front-end web para el servidor de informes.  
  
-   El servicio web del servidor de informes, que se usa para el procesamiento de informes interactivo y las solicitudes a petición.  
  
-   Una aplicación de procesamiento en segundo plano, que se usa para el procesamiento programado de informes, la entrega de suscripciones y el mantenimiento de bases de datos.  
  
 Las directivas de administración de memoria se aplican al servicio del servidor de informes en su conjunto y no a las aplicaciones individuales que se ejecutan dentro del proceso.  
  
 Si no hay presión de memoria en el sistema, cada aplicación de servidor solicita memoria al inicio, anticipándose a la recepción de solicitudes, para ofrecer un rendimiento óptimo cuando las solicitudes se reciban a la larga. Conforme se genera la presión de memoria, el servidor de informes ajusta su modelo de proceso como se describe en la tabla siguiente.  
  
|Presión de memoria|Respuesta del servidor|  
|---------------------|---------------------|  
|Baja|Las solicitudes actuales continúan en proceso. Casi siempre se aceptan las nuevas solicitudes. A las solicitudes que se dirigen a la aplicación de procesamiento de fondo se les proporciona una prioridad menor que a las solicitudes dirigidas al servicio web del servidor de informes.|  
|Media|Las solicitudes actuales continúan en proceso. Se podrían aceptar las nuevas solicitudes. A las solicitudes que se dirigen a la aplicación de procesamiento de fondo se les proporciona una prioridad menor que a las solicitudes dirigidas al servicio web del servidor de informes. Se reducen las asignaciones de memoria para las tres aplicaciones de servidor, con reducciones relativamente mayores al procesamiento de fondo para liberar más memoria para solicitudes de servicio web.|  
|Alta|Se reduce aún más la asignación de memoria. Se deniegan las aplicaciones de servidor que solicitan más memoria. Las solicitudes actuales disminuyen y tardan más tiempo en completarse. No se aceptan nuevas solicitudes. El servidor de informes intercambia archivos de datos en memoria al disco.<br /><br /> Si las restricciones de memoria se vuelven graves y no hay ninguna memoria disponible para controlar las nuevas solicitudes, el servidor de informes devolverá un error no disponible de servidor HTTP 503 mientras se completan las solicitudes actuales. En algunos casos, los dominios de aplicación se podrían reciclar para reducir la presión de memoria inmediatamente.|  
  
 Aunque no puede personalizar las respuestas del servidor de informes a los diferentes escenarios de presión de memoria, puede especificar la configuración que define los límites que separan las respuestas de presión de memoria alta, media y baja.  
  
## <a name="when-to-customize-memory-management-settings"></a>Cuándo personalizar la configuración de administración de memoria  
 La configuración predeterminada especifica los intervalos desiguales para presión de memoria baja, media y alta. De forma predeterminada, la zona de presión de memoria baja es mayor que las zonas para la presión de memoria media y alta. Esta configuración es óptima para las cargas de procesamiento que se distribuyen uniformemente o que crecen o se rechazan de manera incremental. En este escenario, la transición entre las zonas es gradual y el servidor de informes tiene el tiempo de ajustar su respuesta.  
  
 La modificación de la configuración predeterminada resulta útil si el modelo de carga incluye picos. Cuando hay picos repentinos en la carga de procesamiento, el servidor de informes puede pasar de no tener presión de memoria a presentar errores de asignación de memoria muy rápidamente. Esto puede producirse si tiene varias instancias simultáneas de un informe que usa mucha memoria que empiezan al mismo tiempo. Para controlar este tipo de carga de procesamiento, desea que el servidor de informes pase a una respuesta de presión de memoria media o alta lo antes posible de manera que pueda reducir el procesamiento. Esto permite que se completen más solicitudes. Para ello, debería disminuir el valor para `MemorySafetyMargin` para hacer la zona de presión de memoria baja menor en relación con las demás zonas. Si se hace, dará lugar a que las respuestas para presión de memoria media o alta se produzcan antes.  
  
## <a name="configuration-settings-for-memory-management"></a>Valores de configuración para la administración de memoria  
 Entre los valores de configuración que controlan la asignación de memoria para el servidor de informes se incluyen `WorkingSetMaximum`, `WorkingSetMinimum`, `MemorySafetyMargin` y `MemoryThreshold`.  
  
-   `WorkingSetMaximum` y `WorkingSetMinimum` definen el intervalo de memoria disponible. Puede configurar estos valores para establecer un intervalo de memoria disponible para las aplicaciones del servidor de informes. Esto puede resultar útil si está hospedando varias aplicaciones en el mismo equipo y determina que el servidor de informes está usando una cantidad desproporcionada de recursos del sistema en relación con otras aplicaciones del mismo equipo.  
  
-   `MemorySafetyMargin` y `MemoryThreshold` establecen los límites para los niveles bajo, medio, y alto de presión de memoria. Para cada estado, [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] adopta acciones correctoras para asegurarse de que el procesamiento de informe y otras solicitudes se controlan adecuadamente en relación con la cantidad de memoria disponible en el equipo. Puede especificar los valores de configuración que determinan la delineación entre los niveles de presión bajo, alto y medio.  
  
     Aunque puede cambiar los valores de configuración, al hacerlo no se mejorará el rendimiento del procesamiento de informes. El cambio de los valores de configuración solamente resulta útil si se quitan las solicitudes antes de completarlas. La mejor manera de mejorar el rendimiento del servidor es implementar el servidor de informes o las aplicaciones del servidor de informes individuales en equipos dedicados.  
  
 La ilustración siguiente muestra cómo se usa la configuración en conjunto para distinguir entre los niveles bajo, medio y alto de presión de memoria:  
  
 ![Valores de configuración para el estado de la memoria](../media/rs-memoryconfigurationzones.gif "Valores de configuración para el estado de la memoria")  
  
 En la tabla siguiente se describen las configuraciones `WorkingSetMaximum`, `WorkingSetMinimum`, `MemorySafetyMargin` y `MemoryThreshold`. Los valores de configuración se especifican en el archivo [RSReportServer.config](rsreportserver-config-configuration-file.md).  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|`WorkingSetMaximum`|Especifica un umbral de memoria después de que no se conceda ninguna nueva solicitud de asignación de memoria a las aplicaciones del servidor de informes.<br /><br /> De forma predeterminada, el servidor de informes establece `WorkingSetMaximum` en la cantidad de memoria disponible en el equipo. Este valor se detecta cuando se inicia el servicio.<br /><br /> Este valor no aparece en el archivo RSReportServer.config a menos que lo agregue manualmente. Si desea que el servidor de informes use menos memoria, puede modificar el archivo RSReportServer.config y agregar el elemento y el valor. El intervalo de valores válidos es de 0 al entero máximo. Este valor se expresa en kilobytes.<br /><br /> Cuando se alcanza el valor de `WorkingSetMaximum`, el servidor de informes no acepta nuevas solicitudes. Las solicitudes que se encuentran en curso actualmente podrán completarse. Las nuevas solicitudes se aceptan solo cuando el uso de memoria cae por debajo del valor especificado mediante `WorkingSetMaximum`.<br /><br /> Si las solicitudes existentes continúan consumiendo memoria adicional después de que se ha alcanzado el valor `WorkingSetMaximum`, se reciclarán todos los dominios de aplicación de servidor. Para obtener más información, vea [Application Domains for Report Server Applications](application-domains-for-report-server-applications.md).|  
|`WorkingSetMinimum`|Especifica un límite inferior para el consumo de recursos; el servidor de informes no liberará memoria si el uso de memoria total se encuentra por debajo de este límite.<br /><br /> De forma predeterminada, el valor se calcula al inicio del servicio. El cálculo es que la solicitud de asignación de memoria inicial es para el 60 por ciento de `WorkingSetMaximum`.<br /><br /> Este valor no aparece en el archivo RSReportServer.config a menos que lo agregue manualmente. Si desea personalizar este valor, debe agregar el elemento `WorkingSetMinimum` al archivo RSReportServer.config. El intervalo de valores válidos es de 0 al entero máximo. Este valor se expresa en kilobytes.|  
|`MemoryThreshold`|Especifica un porcentaje de `WorkingSetMaximum` que define el límite entre los escenarios de presión alta y media. Si el uso de memoria del servidor de informes alcanza este valor, el servidor de informes ralentiza el procesamiento de la solicitud y cambia la cantidad de memoria asignada a aplicaciones de servidor diferentes. El valor predeterminado es 90. Este valor debería ser mayor que el valor establecido para `MemorySafetyMargin`.|  
|`MemorySafetyMargin`|Especifica un porcentaje de `WorkingSetMaximum` que define el límite entre el los escenarios de presión media y baja. Este valor es el porcentaje de memoria disponible que se reserva para el sistema y no se puede usar para las operaciones del servidor de informes. El valor predeterminado es 80.|  
  
> [!NOTE]  
>  Los valores de configuración `MemoryLimit` y `MaximumMemoryLimit` están obsoletos en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y versiones posteriores. Si ha actualizado una instalación existente o está usando un archivo RSReportServer.config que incluye dicha configuración, el servidor de informes ya no leerá dichos valores.  
  
#### <a name="example-of-memory-configuration-settings"></a>Ejemplo de los valores de configuración de memoria  
 El ejemplo siguiente muestra los valores de configuración para un equipo del servidor de informes que usa valores de configuración de memoria personalizados. Si desea agregar `WorkingSetMaximum` o `WorkingSetMinimum`, debe escribir los elementos y los valores en el archivo RSReportServer.config. Ambos valores son enteros que expresan kilobytes de RAM que está asignando a las aplicaciones de servidor. El ejemplo siguiente especifica que la asignación de memoria total para las aplicaciones del servidor de informes no puede superar los 4 gigabytes. Si el valor predeterminado para `WorkingSetMinimum` (60% de `WorkingSetMaximum`) es aceptable, puede omitirlo y especificar únicamente `WorkingSetMaximum` en el archivo RSReportServer.config. Este ejemplo incluye `WorkingSetMinimum` para mostrar cómo aparecería si deseara agregarlo:  
  
```  
      <MemorySafetyMargin>80</MemorySafetyMargin>  
      <MemoryThreshold>90</MemoryThreshold>  
      <WorkingSetMaximum>4000000</WorkingSetMaximum>  
      <WorkingSetMinimum>2400000</WorkingSetMinimum>  
```  
  
#### <a name="about-aspnet-memory-configuration-settings"></a>Acerca de los valores de configuración de memoria de ASP.NET  
 Aunque el servicio web del servidor de informes y el Administrador de informes son aplicaciones de [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)], ninguna aplicación responde a los valores de configuración de memoria que especifica en la sección `processModel` de machine.config para aplicaciones de [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] que se ejecutan en el modo de compatibilidad de IIS 5.0. [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] lee solamente los valores de configuración de la memoria del archivo RSReportServer.config.  
  
## <a name="see-also"></a>Vea también  
 [Archivo de configuración RSReportServer](rsreportserver-config-configuration-file.md)   
 [Archivo de configuración RSReportServer](rsreportserver-config-configuration-file.md)   
 [Modificar un archivo de configuración de Reporting Services &#40;RSreportserver.config&#41;](modify-a-reporting-services-configuration-file-rsreportserver-config.md)   
 [Application Domains for Report Server Applications](application-domains-for-report-server-applications.md)  
  
  
