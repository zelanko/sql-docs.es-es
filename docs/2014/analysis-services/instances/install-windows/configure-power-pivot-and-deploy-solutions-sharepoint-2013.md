---
title: Configurar PowerPivot e implementar soluciones (SharePoint 2013) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6401fd92-f43b-450e-8298-12db644c25bc
caps.latest.revision: 10
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: f06b47e8f30c60152912c49901341a2d8fdef359
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36196151"
---
# <a name="configure-powerpivot-and-deploy-solutions-sharepoint-2013"></a>Configurar PowerPivot e implementar soluciones (SharePoint 2013)
  Estos temas se explica la implementación y configuración de mejoras de nivel intermedio a las características de PowerPivot en [!INCLUDE[SPS2013](../../../includes/sps2013-md.md)] incluidas la Galería de PowerPivot, programar los proveedores de datos, panel de administración y actualización de datos. Ejecute la herramienta de **Configuración de PowerPivot para SharePoint 2013** para hacer lo siguiente:  
  
-   Implementar archivos de solución de SharePoint.  
  
-   Crear una aplicación de servicio PowerPivot.  
  
-   Configurar una aplicación de Excel Services para que use un servidor de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] en modo de SharePoint. Para obtener información sobre servicios back-end y la instalación una [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] server en el modo de SharePoint, consulte [PowerPivot para SharePoint 2013 Installation](../../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md).  
  
 Para obtener información acerca de cómo instalar PowerPivot para SharePoint 2013, vea [instalar o desinstalar PowerPivot para SharePoint Add- &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)  
  
 Este tema contiene las siguientes secciones:  
  
 [Ejecute PowerPivot para SharePoint 2013](#bkmk_run_configuration_tool)  
  
 [Compruebe la configuración de PowerPivot](#bkmk_verify_powerpivot)  
  
 [Solucionar problemas](#bkmk_troubleshoot_issues)  
  
##  <a name="bkmk_run_configuration_tool"></a> Ejecute PowerPivot para SharePoint 2013  
 **Nota** : el asistente para la instalación de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] instala dos herramientas de configuración diferentes para [!INCLUDE[ssGeminiLong](../../../includes/ssgeminilong-md.md)]. Cada una de ellas admite una versión diferente de SharePoint.  
  
|Nombre|Descripción|  
|----------|-----------------|  
|Configuración de PowerPivot para SharePoint 2013|SharePoint 2013|  
|Herramienta de configuración de PowerPivot|SharePoint 2010 con SharePoint 2010 Service Pack 1 (SP1)|  
  
 **Nota** : para completar los pasos siguientes, debe ser administrador de la granja de servidores. Si ve un mensaje de error similar al siguiente:  
  
-   "El usuario no es un administrador de granja. Solucione los errores de validación y vuelva a intentarlo."  
  
 Inicie sesión como la cuenta que instaló SharePoint o configure la cuenta de instalación como administrador principal del sitio de Administración central de SharePoint.  
  
1.  En el **iniciar** menú, haga clic en **todos los programas**y, a continuación, haga clic en [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)], haga clic en **herramientas de configuración**y, a continuación, haga clic en **PowerPivot para SharePoint Configuración de 2013**. Esta herramienta solo se muestra cuando PowerPivot para SharePoint está instalado en el servidor local.  
  
2.  Haga clic en **Configurar o reparar PowerPivot para SharePoint** y, a continuación, haga clic en **Aceptar**.  
  
3.  La herramienta ejecuta una validación para comprobar el estado actual de PowerPivot y los pasos necesarios para completar la configuración. Expanda la ventana al tamaño máximo. Aparecerá una barra de botones en la parte inferior de la ventana con los comandos **Validar** **Ejecutar**y **Salir** .  
  
4.  En la pestaña **Parámetros** :  
  
    1.  **Nombre de usuario de cuenta predeterminada**: escriba una cuenta de usuario de dominio para la cuenta predeterminada. Esta cuenta se usará para aprovisionar servicios, incluido el grupo de aplicaciones de servicios PowerPivot. No especifique ninguna cuenta integrada, como Network Service o Local System. La herramienta bloquea las configuraciones que especifican cuentas integradas.  
  
    2.  **Servidor de bases de datos**: puede usar el motor de bases de datos de SQL Server admitido para la granja de servidores de SharePoint.  
  
    3.  **Frase de contraseña**: escriba una frase de contraseña. Si va a crear una nueva granja de SharePoint, la frase de contraseña se usa siempre que se agrega un servidor o una aplicación a la granja de servidores de SharePoint. Si la granja existe todavía, escriba la frase de contraseña que le permitirá agregar una aplicación de servidor a la granja.  
  
    4.  **Servidor de PowerPivot para Excel Services**: escriba el nombre de un [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] servidor de modo de SharePoint. En una implementación de un solo servidor, es el mismo que el servidor de bases de datos. `[ServerName]\powerpivot`  
  
    5.  Haga clic en **Crear colección de sitios** en la ventana izquierda. Anote la **Dirección URL del sitio** para pueda consultarla en pasos posteriores. Si el servidor de SharePoint no está configurado todavía, el asistente para la configuración usa como valor predeterminado la aplicación web y las direcciones URL de las colecciones de sitios hasta la raíz de `http://[ServerName]`. Para modificar los valores predeterminados, examine las páginas siguientes en la ventana izquierda: **Crear aplicación web predeterminada** e **Implementar solución de aplicación web**  
  
5.  Opcionalmente, revise los valores restantes de entrada utilizados para completar cada acción. Haga clic en cada acción de la ventana izquierda para ver y examinar los detalles de la acción. Para obtener más información acerca de cada uno, vea la sección "valores de entrada utilizados para configurar el servidor en [configurar o reparar PowerPivot para SharePoint 2010 &#40;PowerPivot configuración herramienta&#41; ](../../../analysis-services/configure-repair-powerpivot-sharepoint-2010.md) en este tema.  
  
6.  Si lo desea, quite cualquier acción que no desee procesar en este momento. Por ejemplo, si desea configurar el Servicio de almacenamiento seguro más adelante, haga clic en **Configurar el servicio de almacenamiento seguro**y, a continuación, desactive la casilla **Incluir esta acción en la lista de tareas**.  
  
7.  Haga clic en **Validar** para comprobar si la herramienta tiene suficiente información para procesar las acciones de la lista. Si ve errores de validación, haga clic las en advertencias en el panel izquierdo para ver detalles del error de validación. Corrija los errores de validación y vuelva a hacer clic en **Validar** .  
  
8.  Haga clic en **Ejecutar** para procesar todas las acciones de la lista de tareas. Tenga en cuenta que **Ejecutar** estará disponible cuando valide las acciones. Si **Ejecutar** no está habilitado, haga clic en **Validar** primero.  
  
 Para obtener más información, consulte [configurar o reparar PowerPivot para SharePoint 2010 &#40;herramienta de configuración de PowerPivot&#41;](../../../analysis-services/configure-repair-powerpivot-sharepoint-2010.md)  
  
##  <a name="bkmk_verify_powerpivot"></a> Compruebe la configuración de PowerPivot  
 **Servicios:**  
  
1.  En Administración central, en Configuración del sistema, haga clic en **Administrar servicios en el servidor**.  
  
2.  Compruebe que se hayan iniciado **SQL Server Analysis Services** y **Servicio de sistema de SQL Server PowerPivot** .  
  
 **Característica de granja:**  
  
1.  En Administración central, en Configuración del sistema, haga clic en **Administrar características de la granja**.  
  
2.  Compruebe que la **Característica de integración de PowerPivot** está **Activa**.  
  
 **Característica de colección de sitios:**  
  
1.  Vaya a la dirección URL del sitio creada por la herramienta de configuración.  
  
     Haga clic en **configuración**![configuración de SharePoint](../../../analysis-services/media/as-sharepoint2013-settings-gear.gif "configuración de SharePoint")y, a continuación, haga clic en **configuración del sitio**.  
  
     Haga clic en **Características de la colección de sitios**.  
  
2.  Compruebe que **Característica de integración de PowerPivot para colecciones de sitios** está **Activa**.  
  
 **Aplicación de servicio PowerPivot:**  
  
1.  En Administración central, en **Administración de aplicaciones**, haga clic en **Administrar aplicaciones de servicio**.  
  
2.  Compruebe que el estado de la aplicación de servicio es **Iniciado**. El nombre predeterminado es **Aplicación de servicio PowerPivot predeterminada**.  
  
     Haga clic en el nombre de la aplicación de servicio para abrir el Panel de administración de PowerPivot para la aplicación de servicio. Al usarse por primera vez, el panel tarda varios minutos en cargarse.  
  
 Para obtener más información, consulte [Verify a PowerPivot para SharePoint](../../../analysis-services/instances/install-windows/verify-a-power-pivot-for-sharepoint-installation.md).  
  
##  <a name="bkmk_troubleshoot_issues"></a> Solucionar problemas  
 Como ayuda para solucionar problemas, es conveniente comprobar que el registro de diagnósticos esté habilitado.  
  
1.  En Administración central de SharePoint, haga clic en **Supervisión** y, a continuación, haga clic en **Configurar la recolección de datos de uso y estado**.  
  
2.  Compruebe que **Habilitar la recolección de datos de uso** esté activada.  
  
3.  Compruebe que los eventos siguientes estén seleccionados:  
  
    -   Definición de campos de uso para telemetría de educación  
  
    -   Conexiones de PowerPivot  
  
    -   Uso de datos de carga de PowerPivot  
  
    -   Uso de consultas de PowerPivot  
  
    -   Uso de datos de descarga de PowerPivot  
  
4.  Compruebe que **Habilitar la recolección de datos de mantenimiento** esté activada.  
  
5.  Haga clic en **Aceptar**.  
  
 Para obtener más información sobre la actualización de datos de solución de problemas, consulte [Troubleshooting PowerPivot Data Refresh](http://social.technet.microsoft.com/wiki/contents/articles/3870.troubleshooting-powerpivot-data-refresh.aspx) (http://social.technet.microsoft.com/wiki/contents/articles/3870.troubleshooting-powerpivot-data-refresh.aspx).  
  
 Para obtener más información acerca de la herramienta de configuración, consulte [PowerPivot Configuration Tools](../../power-pivot-sharepoint/power-pivot-configuration-tools.md).  
  
  