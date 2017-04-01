---
title: "Instalar Reporting Services e Internet Information Services en paralelo (modo nativo de SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "01/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "implementar [Reporting Services], IIS"
ms.assetid: 9b651fa5-f582-4f18-a77d-0dde95d9d211
caps.latest.revision: 40
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# Instalar Reporting Services e Internet Information Services en paralelo (modo nativo de SSRS)
  Puede instalar y ejecutar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (SSRS) e Internet Information Services (IIS) en el mismo equipo. La versión de IIS que utilice determinará los problemas de interoperabilidad que debe tratar.  
  
||  
|-|  
|[!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en modo nativo|  
  
|Versión de IIS|Problemas|Descripción|  
|-----------------|------------|-----------------|  
|8.0, 8.5|Las solicitudes destinadas a una aplicación las acepta una aplicación diferente.<br /><br /> HTTP.SYS exige reglas de prioridad para las reservas de direcciones URL. Puede que las solicitudes que se envían a aplicaciones con el mismo nombre de directorio virtual y que supervisan de manera conjunta el puerto 80, no alcancen el destino deseado si la reserva de direcciones URL es débil en relación con la reserva de direcciones URL de otra aplicación.|En determinadas condiciones, un extremo registrado que reemplaza otro extremo de dirección URL en el esquema de reserva de direcciones URL podría recibir solicitudes HTTP pensadas para la otra aplicación.<br /><br /> El uso de nombres de directorio virtual únicos para el servicio web del servidor de informes y el [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] ayuda a evitar este conflicto.<br /><br /> En este tema se proporciona información detallada acerca de este escenario.|  
  
## Reglas de prioridad para las reservas de direcciones URL  
 Para poder resolver problemas de interoperabilidad entre IIS y [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], debe entender las reglas de prioridad de reserva de direcciones URL. Las reglas de prioridad se pueden generalizar en la instrucción siguiente: una reserva de direcciones URL que tiene valores definidos de forma más explícita se encuentra en la primera posición para recibir solicitudes que coinciden con la dirección URL.  
  
-   Una reserva de direcciones URL que especifica un directorio virtual es más explícita que una que omite un directorio virtual.  
  
-   Una reserva de direcciones URL que especifica una dirección única (mediante una dirección IP, un nombre de dominio completo, un nombre de equipo de red o un nombre de host) es más explícita que un carácter comodín.  
  
-   Una reserva de direcciones URL que especifica un carácter comodín fuerte es más explícita que un carácter comodín débil.  
  
 Los ejemplos siguientes muestran un intervalo de reservas de direcciones URL, ordenado de más a menos explícito:  
  
|Ejemplo|Solicitud|  
|-------------|-------------|  
|http://123.234.345.456:80/reports|Recibe todas las solicitudes que se envían a http://123.234.345.456/reports o http://\<nombreDeEquipo>/reports si un servicio de nombre de dominio puede resolver la dirección IP a dicho nombre de host.|  
|http://+:80/reports|Recibe las solicitudes enviadas a cualquier dirección IP o nombre de host válido para dicho equipo siempre que la dirección URL contenga el nombre de directorio virtual "reports".|  
|http://123.234.345.456:80|Recibe cualquier solicitud que especifica http://123.234.345.456 o http://\<nombreDeEquipo> si un servicio de nombre de dominio puede resolver la dirección IP en dicho nombre de host.|  
|http://+:80|Recibe solicitudes que aún no se han recibido por otras aplicaciones, para cualquier extremo de aplicación asignado a **Todas asignadas**.|  
|http://*:80|Recibe solicitudes que aún no se han recibido por otras aplicaciones, para cualquier extremo de aplicación asignado a **Todas sin asignar**.|  
  
 Una indicación de que hay un conflicto en el puerto es que verá el siguiente mensaje de error: 'System.IO.FileLoadException: El proceso no puede tener acceso al archivo porque está siendo utilizado en otro proceso. (Excepción de HRESULT: 0x80070020).'.  
  
## Reservas de direcciones URL para IIS 8.0 y 8.5 con [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Reporting Services  
 Dadas las reglas de prioridad descritas en la sección anterior, puede empezar a entender cómo las reservas de direcciones URL definidas para Reporting Services e IIS promueven la interoperabilidad. Reporting Services recibe las solicitudes que especifican explícitamente los nombres de directorio virtual para sus aplicaciones; IIS recibe todas las solicitudes restantes, que se pueden dirigir a continuación a las aplicaciones que se ejecutan dentro del modelo de proceso de IIS.  
  
|Aplicación|Reserva de direcciones URL|Descripción|Confirmación de solicitud|  
|-----------------|---------------------|-----------------|---------------------|  
|Servidor de informes|http://+:80/ReportServer|Carácter comodín fuerte en el puerto 80, con directorio virtual del servidor de informes.|Recibe todas las solicitudes del puerto 80 que especifican el directorio virtual del servidor de informes. El servicio web del servidor de informes recibe todas las solicitudes para http://\<nombreDeEquipo>/reportserver.|  
|Portal web|http://+:80/Reports|Carácter comodín fuerte en el puerto 80, con directorio virtual Reports.|Recibe todas las solicitudes del puerto 80 que especifican el directorio virtual de informes. El [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] recibe todas las solicitudes para http://\<nombreDeEquipo>/reports.|  
|IIS|http://*:80/|Carácter comodín débil en el puerto 80.|Recibe las solicitudes restantes del puerto 80 que no recibe ninguna otra aplicación.|  
  
## Implementaciones en paralelo de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y SQL Server 2016 Reporting Services en IIS 8.0 y 8.5  
 Los problemas de interoperabilidad entre IIS y Reporting Services se producen cuando los sitios web de IIS tienen nombres de directorio virtual idénticos a los usados por Reporting Services. Por ejemplo, supongamos que tiene la siguiente configuración:  
  
-   Un sitio web en IIS asignado al puerto 80 y un directorio virtual denominado "Reports".  
  
-   Una instancia del servidor de informes de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] instalada en la configuración predeterminada, donde la reserva de direcciones URL también especifica el puerto 80 y la aplicación [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] también usa "Reports" como nombre del directorio virtual.  
  
 Dada esta configuración, el [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] recibirá una solicitud que se envía a http://\<nombreDeEquipo>:80/reports. La aplicación a la que se tiene acceso a través del directorio virtual Reports en IIS ya no recibirá solicitudes una vez instalada la instancia del servidor de informes de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
 Si ejecuta implementaciones simultáneas de versiones anteriores y más recientes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], es probable que encuentre el problema de enrutamiento que acabamos de describir. Esto se debe a que todas las versiones de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usan "ReportServer" y "Reports" como nombres de directorio virtual para las aplicaciones del servidor de informes y del [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] , lo que aumenta la probabilidad de que tenga los directorios virtuales "reports" y "reportserver" en IIS.  
  
 Para asegurarse de que todas las aplicaciones reciben solicitudes, siga estas directrices:  
  
-   Para las instalaciones de Reporting Services, use nombres de directorios virtuales que no haya usado previamente ningún sitio web de IIS en el mismo puerto que Reporting Services. Si se produce un conflicto, instale Reporting Services en el modo "solo archivos" (mediante la opción "Instalar, pero no configurar el servidor de informes" del Asistente para la instalación), de manera que pueda configurar los directorios virtuales una vez finalizada la instalación. Una indicación de que hay un conflicto en la configuración es que verá el siguiente mensaje de error: System.IO.FileLoadException: El proceso no puede tener acceso al archivo porque está siendo utilizado en otro proceso. (Excepción de HRESULT: 0x80070020).  
  
-   Para las instalaciones que configure manualmente, adopte las convenciones de nomenclatura predeterminadas en las direcciones URL que configure. Si instala [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] como una instancia con nombre, incluya el nombre de la instancia al crear un directorio virtual.  
  
## Vea también  
 [Configurar las direcciones URL del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
 [Configurar una dirección URL &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)   
 [Instalar el servidor de informes en modo nativo de Reporting Services](../../reporting-services/install-windows/install-reporting-services-native-mode-report-server.md)  
  
  