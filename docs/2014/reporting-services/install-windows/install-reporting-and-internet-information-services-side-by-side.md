---
title: Instalar Reporting Services y Internet Information Services en paralelo (modo nativo de SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- deploying [Reporting Services], IIS
ms.assetid: 9b651fa5-f582-4f18-a77d-0dde95d9d211
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 514774acc7255f2f499bfe7fdd6e731944ab67fe
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "67285054"
---
# <a name="install-reporting-services-and-internet-information-services-side-by-side-ssrs-native-mode"></a>Instalar Reporting Services e Internet Information Services en paralelo (modo nativo de SSRS)
  Puede instalar y ejecutar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (SSRs) y Internet Information Services (IIS) en el mismo equipo. La versión de IIS que utilice determinará los problemas de interoperabilidad que debe tratar.  
  
||  
|-|  
|[!INCLUDE[applies](../../includes/applies-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo nativo|  
  
|Versión de IIS|Issues|Descripción|  
|-----------------|------------|-----------------|  
|IIS 6.0, 7.0, 8.0, 8.5|Las solicitudes destinadas a una aplicación las acepta una aplicación diferente.<br /><br /> HTTP.SYS exige reglas de prioridad para las reservas de direcciones URL. Puede que las solicitudes que se envían a aplicaciones con el mismo nombre de directorio virtual y que supervisan de manera conjunta el puerto 80, no alcancen el destino deseado si la reserva de direcciones URL es débil en relación con la reserva de direcciones URL de otra aplicación.|En determinadas condiciones, un extremo registrado que reemplaza otro extremo de dirección URL en el esquema de reserva de direcciones URL podría recibir solicitudes HTTP pensadas para la otra aplicación.<br /><br /> El uso de nombres de directorio virtual únicos para el servicio web del servidor de informes y el Administrador de informes ayuda a evitar este conflicto.<br /><br /> En este tema se proporciona información detallada acerca de este escenario.|  
  
## <a name="precedence-rules-for-url-reservations"></a>Reglas de prioridad para las reservas de direcciones URL  
 Para poder resolver problemas de interoperabilidad entre IIS y [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], debe entender las reglas de prioridad de reserva de direcciones URL. Las reglas de prioridad se pueden generalizar en la instrucción siguiente: una reserva de direcciones URL que tiene valores definidos de forma más explícita se encuentra en la primera posición para recibir solicitudes que coinciden con la dirección URL.  
  
-   Una reserva de direcciones URL que especifica un directorio virtual es más explícita que una que omite un directorio virtual.  
  
-   Una reserva de direcciones URL que especifica una dirección única (mediante una dirección IP, un nombre de dominio completo, un nombre de equipo de red o un nombre de host) es más explícita que un carácter comodín.  
  
-   Una reserva de direcciones URL que especifica un carácter comodín fuerte es más explícita que un carácter comodín débil.  
  
 Los ejemplos siguientes muestran un intervalo de reservas de direcciones URL, ordenado de más a menos explícito:  
  
|Ejemplo|Solicitud|  
|-------------|-------------|  
|http:\//123.234.345.456:80/Reports|Recibe todas las solicitudes que se envían a http\/:/123.234.345.456/reports o\<http://COMPUTERNAME>/Reports si un servicio de nombres de dominio puede resolver la dirección IP para ese nombre de host.|  
|http://+:80/reports|Recibe las solicitudes enviadas a cualquier dirección IP o nombre de host válido para dicho equipo siempre que la dirección URL contenga el nombre de directorio virtual "reports".|  
|http:\//123.234.345.456:80|Recibe cualquier solicitud que especifique http:\//123.234.345.456 o http://\<COMPUTERNAME> si un servicio de nombres de dominio puede resolver la dirección IP para ese nombre de host.|  
|http://+:80|Recibe solicitudes que aún no se han recibido por otras aplicaciones, para cualquier extremo de aplicación asignado a **Todas asignadas**.|  
|http://*:80|Recibe solicitudes que aún no se han recibido por otras aplicaciones, para cualquier extremo de aplicación asignado a **Todas sin asignar**.|  
  
 Una indicación de que hay un conflicto en el puerto es que verá el siguiente mensaje de error: 'System.IO.FileLoadException: El proceso no puede tener acceso al archivo porque está siendo utilizado en otro proceso. (Excepción de HRESULT: 0x80070020).'.  
  
## <a name="url-reservations-for-iis-60-70-80-85-with-sssql14-reporting-services"></a>Reservas de direcciones URL para IIS 6.0, 7.0, 8.0 y 8.5 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Reporting Services  
 Dadas las reglas de prioridad descritas en la sección anterior, puede empezar a entender cómo las reservas de direcciones URL definidas para Reporting Services e IIS promueven la interoperabilidad. Reporting Services recibe las solicitudes que especifican explícitamente los nombres de directorio virtual para sus aplicaciones; IIS recibe todas las solicitudes restantes, que se pueden dirigir a continuación a las aplicaciones que se ejecutan dentro del modelo de proceso de IIS.  
  
|Application|Reserva de direcciones URL|Descripción|Confirmación de solicitud|  
|-----------------|---------------------|-----------------|---------------------|  
|Servidor de informes|http://+:80/ReportServer|Carácter comodín fuerte en el puerto 80, con directorio virtual del servidor de informes.|Recibe todas las solicitudes del puerto 80 que especifican el directorio virtual del servidor de informes. El servicio web del servidor de informes recibe todas las solicitudes para http://\<nombreDeEquipo>/reportserver.|  
|Administrador de informes|http://+:80/Reports|Carácter comodín fuerte en el puerto 80, con directorio virtual Reports.|Recibe todas las solicitudes del puerto 80 que especifican el directorio virtual de informes. Administrador de informes recibe todas las solicitudes a\<http://COMPUTERNAME>/Reports.|  
|IIS|http://*:80/|Carácter comodín débil en el puerto 80.|Recibe las solicitudes restantes del puerto 80 que no recibe ninguna otra aplicación.|  
  
## <a name="side-by-side-deployments-of-sscurrent-and-sql-server-2005-reporting-services-on-iis-60-70-80-85"></a>Implementaciones en paralelo de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y SQL Server 2005 Reporting Services en IIS 6.0, 7.0, 8.0 y 8.5  
 Los problemas de interoperabilidad entre IIS y Reporting Services se producen cuando los sitios web de IIS tienen nombres de directorio virtual idénticos a los usados por Reporting Services. Por ejemplo, supongamos que tiene la siguiente configuración:  
  
-   Un sitio web en IIS asignado al puerto 80 y un directorio virtual denominado "Reports".  
  
-   Una [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] instancia del servidor de informes de instalada en la configuración predeterminada, donde la reserva de direcciones URL también especifica el puerto 80 y la aplicación administrador de informes también usa "Reports" como nombre del directorio virtual.  
  
 Dada esta configuración, Administrador de informes recibirá una solicitud que se\<envía a http://COMPUTERNAME>:80/Reports. La aplicación a la que se tiene acceso a través del directorio virtual Reports en IIS ya no recibirá solicitudes una vez instalada la instancia del servidor de informes de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
 Si ejecuta implementaciones simultáneas de versiones anteriores y más recientes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], es probable que encuentre el problema de enrutamiento que acabamos de describir. Esto se debe a que todas las versiones de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usan "ReportServer" y "Reports" como nombres de directorio virtual para las aplicaciones del servidor de informes y el Administrador de informes, lo que aumenta la probabilidad de que tenga los directorios virtuales "reports" y "reportserver" en IIS.  
  
 Para asegurarse de que todas las aplicaciones reciben solicitudes, siga estas directrices:  
  
-   Para las instalaciones de Reporting Services, use nombres de directorios virtuales que no haya usado previamente ningún sitio web de IIS en el mismo puerto que Reporting Services. Si se produce un conflicto, instale Reporting Services en el modo "solo archivos" (mediante la opción "Instalar, pero no configurar el servidor de informes" del Asistente para la instalación), de manera que pueda configurar los directorios virtuales una vez finalizada la instalación. Una indicación de que hay un conflicto en la configuración es que verá el siguiente mensaje de error: System.IO.FileLoadException: El proceso no puede tener acceso al archivo porque está siendo utilizado en otro proceso. (Excepción de HRESULT: 0x80070020).  
  
-   Para las instalaciones que configure manualmente, adopte las convenciones de nomenclatura predeterminadas en las direcciones URL que configure. Si instala [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] como una instancia con nombre, incluya el nombre de la instancia al crear un directorio virtual.  
  
## <a name="see-also"></a>Consulte también  
 [Configurar las direcciones URL del servidor de informes &#40;Administrador de configuración de SSRS&#41;](configure-report-server-urls-ssrs-configuration-manager.md)   
 [Configurar una dirección URL &#40;SSRS Configuration Manager&#41;](configure-a-url-ssrs-configuration-manager.md)   
 [Instalar el servidor de informes en modo nativo de Reporting Services](install-reporting-services-native-mode-report-server.md)  
  
  
