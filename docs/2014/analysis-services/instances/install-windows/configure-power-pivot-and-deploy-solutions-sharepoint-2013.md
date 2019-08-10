---
title: Configurar PowerPivot e implementar soluciones (SharePoint 2013) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 6401fd92-f43b-450e-8298-12db644c25bc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 48d96a731724717a398c2170d642c419a1f3e9da
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68888593"
---
# <a name="configure-powerpivot-and-deploy-solutions-sharepoint-2013"></a>Configurar PowerPivot e implementar soluciones (SharePoint 2013)
  En estos temas se describen la implementación y la configuración de mejoras de nivel intermedio realizadas en las características de PowerPivot en [!INCLUDE[SPS2013](../../../includes/sps2013-md.md)] , incluidas la galería de PowerPivot, la programación de actualización de datos, el panel de administración y los proveedores de datos. Ejecute la herramienta de **Configuración de PowerPivot para SharePoint 2013** para hacer lo siguiente:  
  
-   Implementar archivos de solución de SharePoint.  
  
-   Crear una aplicación de servicio PowerPivot.  
  
-   Configurar una aplicación de Excel Services para que use un servidor de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] en modo de SharePoint. Para obtener información sobre los servicios back- [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] end e instalar un servidor en modo de SharePoint, consulte [PowerPivot para SharePoint instalación de 2013](https://docs.microsoft.com/analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode).  
  
 Para obtener información sobre cómo instalar la herramienta de configuración de PowerPivot para SharePoint 2013, vea [instalar o desinstalar el &#40;complemento de&#41; PowerPivot para SharePoint de SharePoint 2013](https://docs.microsoft.com/analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013)  
  
 Este tema contiene las siguientes secciones:  
  
 [Ejecución de la configuración de PowerPivot para SharePoint 2013](#bkmk_run_configuration_tool)  
  
 [Comprobar la configuración de PowerPivot](#bkmk_verify_powerpivot)  
  
 [Solucionar problemas](#bkmk_troubleshoot_issues)  
  
##  <a name="bkmk_run_configuration_tool"></a>Ejecución de la configuración de PowerPivot para SharePoint 2013  
 **Nota:** El [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] Asistente para la instalación de instala dos herramientas de [!INCLUDE[ssGeminiLong](../../../includes/ssgeminilong-md.md)]configuración diferentes para. Cada una de ellas admite una versión diferente de SharePoint.  
  
|NOMBRE|Descripción|  
|----------|-----------------|  
|Configuración de PowerPivot para SharePoint 2013|SharePoint 2013|  
|Herramienta de configuración de PowerPivot|SharePoint 2010 con SharePoint 2010 Service Pack 1 (SP1)|  
  
 **Nota:** Para completar los pasos siguientes, debe ser administrador de la granja de servidores. Si ve un mensaje de error similar al siguiente:  
  
-   "El usuario no es un administrador de la granja de servidores. Solucione los errores de validación y vuelva a intentarlo."  
  
 Inicie sesión como la cuenta que instaló SharePoint o configure la cuenta de instalación como administrador principal del sitio de Administración central de SharePoint.  
  
1.  En el menú **Inicio** , haga clic sucesivamente en **Todos los programas**, [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)], **Herramientas de configuración**y **Configuración de PowerPivot para SharePoint 2013**. Esta herramienta solo se muestra cuando PowerPivot para SharePoint está instalado en el servidor local.  
  
2.  Haga clic en **Configurar o reparar PowerPivot para SharePoint** y, a continuación, haga clic en **Aceptar**.  
  
3.  La herramienta ejecuta una validación para comprobar el estado actual de PowerPivot y los pasos necesarios para completar la configuración. Expanda la ventana al tamaño máximo. Aparecerá una barra de botones en la parte inferior de la ventana con los comandos **Validar** **Ejecutar**y **Salir** .  
  
4.  En la pestaña **Parámetros** :  
  
    1.  **Nombre de usuario de cuenta predeterminada**: Escriba una cuenta de usuario de dominio para la cuenta predeterminada. Esta cuenta se usará para aprovisionar servicios, incluido el grupo de aplicaciones de servicios PowerPivot. No especifique ninguna cuenta integrada, como Network Service o Local System. La herramienta bloquea las configuraciones que especifican cuentas integradas.  
  
    2.  **Servidor de base de datos**: Puede usar SQL Server motor de base de datos compatible con la granja de servidores de SharePoint.  
  
    3.  **Frase de contraseña**: Escriba una frase de contraseña. Si va a crear una nueva granja de SharePoint, la frase de contraseña se usa siempre que se agrega un servidor o una aplicación a la granja de servidores de SharePoint. Si la granja existe todavía, escriba la frase de contraseña que le permitirá agregar una aplicación de servidor a la granja.  
  
    4.  **Servidor PowerPivot para Excel Services**: Escriba el nombre de un [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] servidor en modo de SharePoint. En una implementación de un solo servidor, es el mismo que el servidor de bases de datos. `[ServerName]\powerpivot`  
  
    5.  Haga clic en **Crear colección de sitios** en la ventana izquierda. Anote la **Dirección URL del sitio** para pueda consultarla en pasos posteriores. Si el servidor de SharePoint no está configurado todavía, el asistente para la configuración usa como valor predeterminado la aplicación web y las direcciones URL de las colecciones de sitios hasta la raíz de `http://[ServerName]`. Para modificar los valores predeterminados, revise las páginas siguientes en la ventana izquierda: **Crear aplicación web predeterminada** e **implementar solución de aplicación web**  
  
5.  Opcionalmente, revise los valores restantes de entrada utilizados para completar cada acción. Haga clic en cada acción de la ventana izquierda para ver y examinar los detalles de la acción. Para obtener más información acerca de cada uno, vea la sección "valores de entrada utilizados para configurar el servidor en [configurar o &#40;reparar PowerPivot para SharePoint herramienta&#41; de configuración de PowerPivot 2010](https://docs.microsoft.com/analysis-services/configure-repair-powerpivot-sharepoint-2010) " en este tema.  
  
6.  Si lo desea, quite cualquier acción que no desee procesar en este momento. Por ejemplo, si desea configurar el Servicio de almacenamiento seguro más adelante, haga clic en **Configurar el servicio de almacenamiento seguro**y, a continuación, desactive la casilla **Incluir esta acción en la lista de tareas**.  
  
7.  Haga clic en **Validar** para comprobar si la herramienta tiene suficiente información para procesar las acciones de la lista. Si ve errores de validación, haga clic las en advertencias en el panel izquierdo para ver detalles del error de validación. Corrija los errores de validación y vuelva a hacer clic en **Validar** .  
  
8.  Haga clic en **Ejecutar** para procesar todas las acciones de la lista de tareas. Tenga en cuenta que **Ejecutar** estará disponible cuando valide las acciones. Si **Ejecutar** no está habilitado, haga clic en **Validar** primero.  
  
 Para obtener más información, vea [configurar o reparar PowerPivot para SharePoint &#40;herramienta&#41; de configuración de PowerPivot 2010](https://docs.microsoft.com/analysis-services/configure-repair-powerpivot-sharepoint-2010)  
  
##  <a name="bkmk_verify_powerpivot"></a>Comprobar la configuración de PowerPivot  
 **Servicios:**  
  
1.  En Administración central, en Configuración del sistema, haga clic en **Administrar servicios en el servidor**.  
  
2.  Compruebe que se hayan iniciado **SQL Server Analysis Services** y **Servicio de sistema de SQL Server PowerPivot** .  
  
 **Característica de granja:**  
  
1.  En Administración central, en Configuración del sistema, haga clic en **Administrar características de la granja**.  
  
2.  Compruebe que la **Característica de integración de PowerPivot** está **Activa**.  
  
 **Característica de colección de sitios:**  
  
1.  Vaya a la dirección URL del sitio creada por la herramienta de configuración.  
  
     Haga clic en **configuración**configuración de![SharePoint]configuración de(https://docs.microsoft.com/analysis-services/analysis-services/media/as-sharepoint2013-settings-gear.gif "SharePoint")y, a continuación, en **configuración del sitio**.  
  
     Haga clic en **Características de la colección de sitios**.  
  
2.  Compruebe que **Característica de integración de PowerPivot para colecciones de sitios** está **Activa**.  
  
 **Aplicación de servicio PowerPivot:**  
  
1.  En Administración central, en **Administración de aplicaciones**, haga clic en **Administrar aplicaciones de servicio**.  
  
2.  Compruebe que el estado de la aplicación de servicio es **Iniciado**. El nombre predeterminado es **Aplicación de servicio PowerPivot predeterminada**.  
  
     Haga clic en el nombre de la aplicación de servicio para abrir el Panel de administración de PowerPivot para la aplicación de servicio. Al usarse por primera vez, el panel tarda varios minutos en cargarse.  
  
 Para obtener más información, consulte [Verify a PowerPivot for SharePoint Installation](https://docs.microsoft.com/analysis-services/instances/install-windows/verify-a-power-pivot-for-sharepoint-installation).  
  
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
  
 Para obtener más información acerca de la solución de problemas de la actualización de datos, https://social.technet.microsoft.com/wiki/contents/articles/3870.troubleshooting-powerpivot-data-refresh.aspx) consulte [Troubleshooting PowerPivot Data Refresh](https://social.technet.microsoft.com/wiki/contents/articles/3870.troubleshooting-powerpivot-data-refresh.aspx) (.  
  
 Para obtener más información acerca de la herramienta de configuración, vea [PowerPivot Configuration Tools](../../power-pivot-sharepoint/power-pivot-configuration-tools.md).  
  
  
