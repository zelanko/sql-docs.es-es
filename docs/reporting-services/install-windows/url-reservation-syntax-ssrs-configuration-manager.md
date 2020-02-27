---
title: Sintaxis de reserva de direcciones URL (Configuration Manager) | Microsoft Docs
ms.date: 05/18/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- URL reservations
ms.assetid: 30e4be2e-e65d-462c-895a-5a0a636d042f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: f2738eed803691eb8d18bb9affeee6e423ae5bae
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "77082228"
---
# <a name="url-reservation-syntax--ssrs-configuration-manager"></a>Sintaxis de reserva de direcciones URL (Administrador de configuración de SSRS)
  En este tema se describen los componentes de las cadenas de direcciones URL para el servicio web del servidor de informes y el Administrador de informes. La cadena de las direcciones URL que se almacena internamente tiene una estructura diferente de una dirección URL que se escribe en la barra de direcciones de una ventana del explorador. La cadena de reserva de direcciones URL aparece en la ventana Resultados de la herramienta Configuración de Reporting Services al configurar una dirección URL y en el archivo RSReportServer.config. Saber cómo se define la cadena de dirección URL puede ser útil al solucionar problemas de la reserva de direcciones URL o al consultar HTTP.SYS para ver las reservas de direcciones URL internas que se definen en el servidor.  
  
## <a name="url-syntax"></a>Sintaxis de las direcciones URL  
 Una dirección URL del servidor de informes se almacena en los elementos **UrlString** y **VirtualDirectory** . La razón para separar los elementos **UrlString** y **VirtualDirectory** en elementos independientes es que puede haber varias cadenas de dirección URL, pero solo un nombre de directorio virtual para cada aplicación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 En HTTP.SYS, la reserva de direcciones URL incluye tanto a **UrlString** como a **VirtualDirectory**. La sintaxis para una reserva de direcciones URL tiene los siguientes componentes:  
  
 \<esquema>://\<nombreHost>:\<puerto>/\<directorioVirtual>  
  
 En la tabla siguiente se describe cada propiedad y qué valores son válidos para cada una.  
  
|Propiedad|Valores válidos|Descripción|  
|--------------|------------------|-----------------|  
|Scheme|http o https|Prefijos para conexiones SSL y de otro tipo.|  
|Hostname|El comodín seguro (+) es igual al valor **(Todas asignadas)** de la dirección IP.<br /><br /> El comodín (\*) poco seguro es igual a una dirección IP de **(Todas sin asignar)** .<br /><br /> Nombre de dominio completo<br /><br /> Nombre de equipo<br /><br /> Dirección IP (IPV4)<br /><br /> Dirección IP (IPV6)|Identifica el servidor en la red.<br /><br /> El carácter comodín seguro (+) es el valor predeterminado. HTTP.SYS aceptará todas las solicitudes en todos los adaptadores de red de una combinación de puerto y directorio virtual determinados. El servidor de informes aceptará cualquier solicitud en el puerto.<br /><br /> Comodín poco seguro (\*). HTTP.SYS acepta todas las solicitudes no administradas por otras reservas de direcciones URL en todos los adaptadores de red para una combinación de puerto y directorio virtual determinados.<br /><br /> El nombre de equipo es el nombre NETBIOS del equipo en la red.<br /><br /> El nombre de dominio completo incluye la dirección de dominio y el nombre del servidor, como se registre con un controlador de dominio o servidor de nombres del dominio público.<br /><br /> La dirección IP (IPV4) es la de un adaptador de red del equipo en formato IPV4: *nnn.nnn.nnn.nnn*.<br /><br /> La dirección IP (IPV6) es la de un adaptador de red del equipo en formato IPV6: \<encabezado>:\<encabezado>:*nnn.nnn.nnn.nnn*.|  
|Port|80<br /><br /> 443<br /><br /> \<personalizado>|El puerto 80 es el puerto estándar para las solicitudes HTTP de un servidor.<br /><br /> El puerto 443 es el informe estándar para las conexiones SSL.<br /><br /> Puede utilizar cualquier puerto que aún no esté reservado por otra aplicación.|  
|VirtualDirectory|ReportServer *[_InstanceName]*<br /><br /> Reports *[_InstanceName]*<br /><br /> \<personalizado>|Especifica el nombre de la aplicación. Este valor es una cadena. De forma predeterminada, [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] utiliza ReportServer e Informes como nombres de las aplicaciones del servicio web del servidor de informes y el Administrador de informes. Puede utilizar nombres diferentes, si lo prefiere.<br /><br /> Este valor es necesario. Identifica la aplicación.<br /><br /> Especifique solo un directorio virtual para cada instancia de la aplicación. Para crear varias direcciones URL para la misma aplicación en la misma instancia, cree varias versiones de **UrlString**. Para crear nombres de directorios virtuales únicos para varias instancias de aplicación, considere incluir el nombre de instancia en el nombre del directorio virtual, utilizando el carácter de subrayado (_) para anexar el nombre de instancia. *InstanceName* es opcional, pero se recomienda si tiene varias instancias en el mismo equipo. Para más información sobre cómo establecer reservas de direcciones URL para las instancias con nombre, vea [Reservas de direcciones URL para implementaciones del servidor de informes de varias instancias &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/url-reservations-for-multi-instance-report-server-deployments.md).<br /><br /> El valor para el directorio virtual no distingue entre mayúsculas y minúsculas. Puede utilizar cualquier cadena siempre que no incluya caracteres separadores de direcciones URL o codificación de URL.|  
  
## <a name="see-also"></a>Consulte también  
 [Configurar las direcciones URL del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
 [Configurar una dirección URL &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)  
  
  
