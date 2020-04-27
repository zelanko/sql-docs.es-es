---
title: Página Configuración del sitio (Administrador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 4d67a01c-eae4-49ba-a6e8-8e983c0248f5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 07fc0207020887d7e3ceb8716ee76c78a55d2bac
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66101119"
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
  
     **Nota:** Si no ve la opción **configuración del sitio** en el menú, no tiene los permisos necesarios. para obtener más información, vea la sección "configuración del sitio" de [configurar un servidor de informes en modo nativo para la Administración Local &#40;SSRS&#41;](report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).  
  
## <a name="options"></a>Opciones  
 **Nombre**  
 Especifique el título que se utilizará para esta instancia del Administrador de informes de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . De forma predeterminada, el título es[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]"".  
  
 **Seleccione la configuración predeterminada para el historial de informe**  
 Seleccione un valor predeterminado para el número de copias del historial del informe que deben guardarse. El valor predeterminado proporciona un valor inicial que establece los límites del historial del informe. Esta configuración se puede modificar en el nivel de informe. Para más información, vea [Página de propiedades de opciones de instantánea &#40;Administrador de informes&#41;](../../2014/reporting-services/snapshot-options-properties-page-report-manager.md).  
  
 Si posteriormente limita el historial del informe, cuando el historial del informe existente exceda el límite especificado, el servidor de informes lo reducirá según el nuevo límite. Las instantáneas de informe más antiguas son las que se eliminan primero. Si el historial del informe está vacío o por debajo del límite, se agregan nuevas instantáneas de informe. Cuando se alcanza el límite, se elimina la instantánea del informe más antigua cuando se agrega una nueva.  
  
 **Tiempo de espera de ejecución de informe**  
 Especifique si el procesamiento del informe debe terminar después de que hayan transcurrido un número de segundos concreto.  
  
 Este valor se aplica al procesamiento de informes en un servidor de informes. No afecta al procesamiento de los datos del servidor de base de datos que proporciona los datos del informe.  
  
 El temporizador de procesamiento del informe empieza cuando se selecciona el informe y termina cuando éste se abre. Cuando establezca este valor, especifique tiempo suficiente para completar el procesamiento de los datos y del informe.  
  
 **URL de inicio del Generador de informes personalizada**  
 Especifique una dirección URL personalizada si el servidor de informes no utiliza la dirección URL predeterminada del Generador de informes. Esta configuración es opcional. Si no especifica un valor, se usará la dirección URL predeterminada, que inicia el Generador de informes como aplicación ClickOnce. La dirección URL predeterminada es una de las siguientes:  
  
 **Servidor de informes en modo nativo:** En una instalación en modo nativo, la dirección URL predeterminada tendrá el formato http://\<*ComputerName*>/ReportServer/ReportBuilder/ReportBuilder_3_0_0_0. Application.  
  
 Modo integrado de SharePoint: la dirección URL predeterminada adoptará el formato\<http://*SharePoint_site*>/_vti_bin/ReportBuilder/ReportBuilder_3_0_0_0. Application. "  
  
 **Aplicar**  
 Haga clic para guardar los cambios en el servidor de informes.  
  
 **Seguridad**  
 Haga clic en este vínculo para abrir la página Asignaciones de roles del sistema, en la que se pueden asignar cuentas de usuario y de grupo a roles del sistema predefinidos.  
  
 **Programaciones**  
 Haga clic en este vínculo para abrir la página Programaciones compartidas, en la que puede predefinir las programaciones compartidas que los usuarios pueden seleccionar para sus informes y suscripciones.  
  
## <a name="see-also"></a>Consulte también  
 [Administrador de informes &#40;Modo nativo de SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Conceder permisos en un servidor de informes en modo nativo](security/granting-permissions-on-a-native-mode-report-server.md)   
 [Roles predefinidos](security/role-definitions-predefined-roles.md)   
 [Administrador de informes (Ayuda F1)](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
