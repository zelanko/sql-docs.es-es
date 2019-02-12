---
title: Página de configuración (Administrador de informes) del sitio | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 4d67a01c-eae4-49ba-a6e8-8e983c0248f5
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: b097b327121656cda3ff8c93ec24bfe1cb35921e
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56035036"
---
# <a name="site-settings-page-report-manager"></a>Página Configuración del sitio (Administrador de informes)
  Use la página Configuración del sitio para cambiar el título de la aplicación, establecer los valores predeterminados para los valores de tiempo de espera de procesamiento de informes y límites del historial de informes, administrar asignaciones de roles del nivel del sistema y administrar programaciones compartidas. Debe tener permisos de Administrador de contenido y Administrador del sistema para ver esta página.  
  
> [!NOTE]  
>  Las siguientes características no están disponibles en todas las ediciones de SQL Server: historial de informes, ejecución de informes y programaciones compartidas. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], vea [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="navigation"></a>Navegación  
 Utilice el procedimiento siguiente para navegar hasta esta ubicación en la interfaz de usuario (IU).  
  
### <a name="to-open-the-site-settings-page"></a>Para abrir la página Configuración del sitio  
  
1.  Abra el Administrador de informes.  
  
2.  En la parte superior de la página, haga clic en **Configuración del sitio**. Esto abre la página de propiedades General del sitio.  
  
     **Nota:** Si no ve el **configuración del sitio** opción en el menú, no tiene los permisos necesarios, para obtener más información, consulte la sección "configuración del sitio" de [configurar un servidor de informes de modo nativo para la administración Local &#40;SSRS&#41;](report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).  
  
## <a name="options"></a>Opciones  
 **Name**  
 Especifique el título que se utilizará para esta instancia del Administrador de informes de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . De forma predeterminada, el título es "[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]".  
  
 **Seleccione la configuración predeterminada para el historial de informes**  
 Seleccione un valor predeterminado para el número de copias del historial del informe que deben guardarse. El valor predeterminado proporciona un valor inicial que establece los límites del historial del informe. Esta configuración se puede modificar en el nivel de informe. Para más información, vea [Página de propiedades de opciones de instantánea &#40;Administrador de informes&#41;](../../2014/reporting-services/snapshot-options-properties-page-report-manager.md).  
  
 Si posteriormente limita el historial del informe, cuando el historial del informe existente exceda el límite especificado, el servidor de informes lo reducirá según el nuevo límite. Las instantáneas de informe más antiguas son las que se eliminan primero. Si el historial del informe está vacío o por debajo del límite, se agregan nuevas instantáneas de informe. Cuando se alcanza el límite, se elimina la instantánea del informe más antigua cuando se agrega una nueva.  
  
 **Tiempo de espera de ejecución de informes**  
 Especifique si el procesamiento del informe debe terminar después de que hayan transcurrido un número de segundos concreto.  
  
 Este valor se aplica al procesamiento de informes en un servidor de informes. No afecta al procesamiento de los datos del servidor de base de datos que proporciona los datos del informe.  
  
 El temporizador de procesamiento del informe empieza cuando se selecciona el informe y termina cuando éste se abre. Cuando establezca este valor, especifique tiempo suficiente para completar el procesamiento de los datos y del informe.  
  
 **URL de inicio del generador de informes personalizado**  
 Especifique una dirección URL personalizada si el servidor de informes no utiliza la dirección URL predeterminada del Generador de informes. Este valor es opcional. Si no especifica un valor, se usará la dirección URL predeterminada, que inicia el Generador de informes como aplicación ClickOnce. La dirección URL predeterminada es una de las siguientes:  
  
 **Servidor de informes de modo nativo:** En una instalación en modo nativo, la dirección URL predeterminada adoptará el formato http://\<*computername*> / reportserver/ReportBuilder/ReportBuilder_3_0_0_0.application.  
  
 Modo integrado de SharePoint: La dirección URL predeterminada adoptará el formato http://\<*SharePoint_site*> / _vti_bin/ReportBuilder/ReportBuilder_3_0_0_0.application. "  
  
 **Aplicar**  
 Haga clic para guardar los cambios en el servidor de informes.  
  
 **Seguridad**  
 Haga clic en este vínculo para abrir la página Asignaciones de roles del sistema, en la que se pueden asignar cuentas de usuario y de grupo a roles del sistema predefinidos.  
  
 **Programaciones**  
 Haga clic en este vínculo para abrir la página Programaciones compartidas, en la que puede predefinir las programaciones compartidas que los usuarios pueden seleccionar para sus informes y suscripciones.  
  
## <a name="see-also"></a>Vea también  
 [Administrador de informes &#40;Modo nativo de SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Conceder permisos en un servidor de informes en modo nativo](security/granting-permissions-on-a-native-mode-report-server.md)   
 [Roles predefinidos](security/role-definitions-predefined-roles.md)   
 [Administrador de informes (Ayuda F1)](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
