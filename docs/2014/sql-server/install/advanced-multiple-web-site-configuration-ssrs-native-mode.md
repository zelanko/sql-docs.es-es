---
title: Configuración avanzada de varios sitios Web (modo nativo de SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.advancedmultiplewebsiteconfig.F1
ms.assetid: af4ede43-2225-45b5-ae7e-9202411551ba
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 01ed7ed806cc064b05180347fa41905b57c4c98e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66096826"
---
# <a name="advanced-multiple-web-site-configuration-ssrs-native-mode"></a>Configuración avanzada de varios sitios web (Modo nativo de SSRS)
  Utilice este cuadro de diálogo para crear y administrar las direcciones URL que se usan para tener acceso a un servidor de informes o al Administrador de informes. El cuadro de diálogo **Configuración avanzada de varios sitios web** se utiliza para crear direcciones URL adicionales y direcciones URL personalizadas que incluyen un nombre de encabezado de host, o para especificar una dirección IP en el formato de IPv4 o IPv6.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Crear varias direcciones URL resulta útil si desea configurar maneras diferentes de acceso a un servidor de informes. Por ejemplo, el acceso al servidor de informes a través de una conexión de una intranet o de una extranet suele requerir direcciones URL diferentes para cada tipo de conexión.  
  
 Para abrir el cuadro de diálogo **Configuración avanzada de varios sitios web** , haga clic en **Opciones avanzadas** en la página **Dirección URL del servicio web** o **Dirección URL del Administrador de informes** del Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Cuando se abra el cuadro de diálogo **Configuración avanzada de varios sitios web** , puede hacer clic en **Agregar** o en **Modificar** para definir direcciones URL nuevas o para modificar o eliminar las existentes.  
  
 Haga clic en **Aceptar** para guardar los cambios. Si agrega o quita direcciones URL, pero a continuación cierra el cuadro de diálogo sin hacer clic en **Aceptar**primero, los cambios se perderán.  
  
## <a name="options"></a>Opciones  
 **Dirección IP**  
 Identifica el equipo del servidor de informes en una red TCP/IP. Los valores válidos incluyen:  
  
-   **Todas asignadas** especifica que cualquiera de las direcciones IP que están asignadas al equipo se puede utilizar en una dirección URL que señale a una aplicación de servidor de informes. Este valor también abarca nombres de host descriptivos (como nombres de equipo) que un servidor de nombres de dominio puede resolver en una dirección IP que se asigna al equipo. Éste es el valor predeterminado de una dirección URL de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
-   **Todas sin asignar** especifica que el servidor de informes aceptará cualquier solicitud que no tenga una coincidencia exacta para la dirección IP o nombre de host. No utilice este valor si otra aplicación web ya está utilizándolo. Si hace esto, interrumpirá el servicio para la otra aplicación.  
  
-   **127.0.0.1** se utilizan para tener acceso al host local. Admite la administración local en el equipo del servidor de informes. Si selecciona solo este valor, únicamente los usuarios que hayan iniciado sesión de forma local en el equipo servidor de informes tendrán acceso a la aplicación.  
  
-   *Nnn.nnn.nnn.nnn* es la dirección IPv4 de una tarjeta adaptadora de red del equipo. Si la red usa direccionamiento IPv6, la dirección IP será un valor de 128 bits de 8 campos de 4 bytes similar al siguiente formato: \<encabezado >:*nnnn:nnnn:nnnn:nnnn*.  
  
     Si tiene varias tarjetas, verá una dirección IP para cada una. Si selecciona solo este valor, limitará el acceso de la aplicación únicamente a la dirección IP (y a cualquier nombre de host que un servidor de nombres de dominio asigne a esa dirección). No puede utilizar el host local para tener acceso a un servidor de informes y no puede utilizar las direcciones IP de otras tarjetas de adaptadores de red que estén instalados en el equipo del servidor de informes.  
  
 **Puerto**  
 Especifica el puerto en el que el servidor de informes supervisa las solicitudes. El puerto predeterminado es 80. Si utiliza el puerto 80, no tiene que incluirlo en la dirección URL. Si utiliza cualquier otro número de puerto, siempre debe incluir en la dirección URL (por ejemplo, http://localhost:8181/reports).  
  
 **Encabezado de host**  
 Si ya tiene definido un encabezado de host en un servidor de nombres de dominio que se resuelva como su equipo, puede especificar ese encabezado de host en una dirección URL que configure para el acceso al servidor de informes.  
  
 Un encabezado de host es un nombre único que permite que varios sitios web compartan una única dirección IP y puerto. Los nombres de encabezado de host son más fáciles de recordar y escribir que los números de dirección IP y puerto. Un ejemplo de nombre de encabezado de host podría ser www.adventure-works.com.  
  
 **Puerto SSL**  
 Especifica el puerto para las conexiones SSL. El número de puerto para SSL es 443.  
  
 **Certificado SSL**  
 Especifica el nombre del certificado de un certificado SSL que instaló en este equipo. Si el certificado se asigna a un carácter comodín, puede utilizarlo para una conexión de servidor de informes.  
  
 Especifica el nombre completo del equipo para el que se registra el certificado. El nombre que se especifica debe ser idéntico al nombre para el que se registra el certificado.  
  
 Para utilizar esta opción debe tener instalado un certificado. También debe modificar la opción de configuración UrlRoot del archivo RSReportServer.config de manera que especifique el nombre completo del equipo para el que se ha registrado el certificado. Para obtener más información, vea [Configurar conexiones SSL en un servidor de informes en modo nativo](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md) en Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Emitido a**  
 Muestra el nombre del equipo para el que se creó el certificado.  
  
 **Agregar**  
 Defina una dirección URL adicional.  
  
 **Editar**  
 Modifique cualquier parte de la sintaxis de la dirección URL.  
  
 **Quitar**  
 Borre una entrada de dirección URL de la lista.  
  
## <a name="see-also"></a>Vea también  
 [Administrador de configuración de Reporting Services &#40;modo nativo&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [Configurar una dirección URL &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)   
 [Configurar las direcciones URL del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)  
  
  
