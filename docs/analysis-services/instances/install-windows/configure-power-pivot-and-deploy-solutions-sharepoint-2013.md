---
title: Configuración de PowerPivot e implementar soluciones (SharePoint 2013) | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 93374b25f377265f1eafa09cf46714ed79927243
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34019332"
---
# <a name="configure-power-pivot-and-deploy-solutions-sharepoint-2013"></a>Configuración de PowerPivot e implementación de soluciones (SharePoint 2013)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  En estos temas se explica cómo configurar e implementar mejoras de nivel intermedio efectuadas en las características de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] en [!INCLUDE[SPS2013](../../../includes/sps2013-md.md)] , incluidas la galería [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] , la programación de actualización de datos, el panel de administración y los proveedores de datos. Ejecute la herramienta **[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint 2013** para hacer lo siguiente:  
  
-   Implementar archivos de solución de SharePoint.  
  
-   Crear una aplicación de servicio [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] .  
  
-   Configurar una aplicación de Excel Services para que use un servidor de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] en modo de SharePoint. Para obtener información sobre los servicios back-end y la instalación de un servidor de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] en modo de SharePoint, vea [Instalación de Analysis Services en el modo PowerPivot](../../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md).  
  
 Para obtener información sobre cómo instalar la herramienta de configuración de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint 2013, vea [Instalar o desinstalar el complemento PowerPivot para SharePoint &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md).  
  
##  <a name="bkmk_run_configuration_tool"></a> Ejecución de la configuración de PowerPivot para SharePoint 2013  
 **Nota** : el asistente para la instalación de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] instala dos herramientas de configuración diferentes para [!INCLUDE[ssGeminiLong](../../../includes/ssgeminilong-md.md)]. Cada una de ellas admite una versión diferente de SharePoint.  
  
|Nombre|Description|  
|----------|-----------------|  
|[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint 2013|SharePoint 2013|  
|[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Herramienta de configuración|SharePoint 2010 con SharePoint 2010 Service Pack 1 (SP1)|  
  
 **Nota** : para completar los pasos siguientes, debe ser administrador de la granja de servidores. Si ve un mensaje de error similar al siguiente:  
  
-   "El usuario no es un administrador de granja. Solucione los errores de validación y vuelva a intentarlo."  
  
 Inicie sesión como la cuenta que instaló SharePoint o configure la cuenta de instalación como administrador principal del sitio de Administración central de SharePoint.  
  
1.  En el menú **Inicio** , haga clic sucesivamente en **Todos los programas**, [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)], **Herramientas de configuración**y **[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint 2013**. Esta herramienta solo se muestra cuando [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint está instalado en el servidor local.  
  
2.  Haga clic en **Configurar o reparar [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint** y haga clic en **Aceptar**.  
  
3.  La herramienta ejecuta una validación para comprobar el estado actual de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] y los pasos necesarios para completar la configuración. Expanda la ventana al tamaño máximo. Aparecerá una barra de botones en la parte inferior de la ventana con los comandos **Validar** **Ejecutar**y **Salir** .  
  
4.  En la pestaña **Parámetros** :  
  
    1.  **Nombre de usuario de cuenta predeterminada**: escriba una cuenta de usuario de dominio para la cuenta predeterminada. Esta cuenta se usará para aprovisionar servicios, incluido el grupo de aplicaciones de servicio [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] . No especifique ninguna cuenta integrada, como Network Service o Local System. La herramienta bloquea las configuraciones que especifican cuentas integradas.  
  
    2.  **Servidor de bases de datos**: puede usar el motor de bases de datos de SQL Server admitido para la granja de servidores de SharePoint.  
  
    3.  **Frase de contraseña**: escriba una frase de contraseña. Si va a crear una nueva granja de SharePoint, la frase de contraseña se usa siempre que se agrega un servidor o una aplicación a la granja de servidores de SharePoint. Si la granja existe todavía, escriba la frase de contraseña que le permitirá agregar una aplicación de servidor a la granja.  
  
    4.  **[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para Excel Services**: escriba el nombre de un servidor de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] en modo de SharePoint. En una implementación de un solo servidor, es el mismo que el servidor de bases de datos. `[ServerName]\powerpivot`  
  
    5.  Haga clic en **Crear colección de sitios** en la ventana izquierda. Anote la **Dirección URL del sitio** para pueda consultarla en pasos posteriores. Si el servidor de SharePoint no está configurado todavía, el asistente para la configuración usa como valor predeterminado la aplicación web y las direcciones URL de las colecciones de sitios hasta la raíz de `http://[ServerName]`. Para modificar los valores predeterminados, examine las páginas siguientes en la ventana izquierda: **Crear aplicación web predeterminada** e **Implementar solución de aplicación web**  
  
5.  Opcionalmente, revise los valores restantes de entrada utilizados para completar cada acción. Haga clic en cada acción de la ventana izquierda para ver y examinar los detalles de la acción. Para obtener más información sobre cada una, vea la sección "Valores de entrada utilizados para configurar el servidor" en [Configurar o reparar PowerPivot para SharePoint 2010 (Herramienta de configuración de PowerPivot)](http://msdn.microsoft.com/en-us/d61f49c5-efaa-4455-98f2-8c293fa50046) en este tema.  
  
6.  Si lo desea, quite cualquier acción que no desee procesar en este momento. Por ejemplo, si desea configurar el Servicio de almacenamiento seguro más adelante, haga clic en **Configurar el servicio de almacenamiento seguro**y, a continuación, desactive la casilla **Incluir esta acción en la lista de tareas**.  
  
7.  Haga clic en **Validar** para comprobar si la herramienta tiene suficiente información para procesar las acciones de la lista. Si ve errores de validación, haga clic las en advertencias en el panel izquierdo para ver detalles del error de validación. Corrija los errores de validación y vuelva a hacer clic en **Validar** .  
  
8.  Haga clic en **Ejecutar** para procesar todas las acciones de la lista de tareas. Tenga en cuenta que **Ejecutar** estará disponible cuando valide las acciones. Si **Ejecutar** no está habilitado, haga clic en **Validar** primero.  
  
 Para obtener más información, vea [Configurar o reparar Power Pivot para SharePoint 2010 (Herramienta de configuración de Power Pivot)](http://msdn.microsoft.com/en-us/d61f49c5-efaa-4455-98f2-8c293fa50046).  
  
##  <a name="bkmk_verify_powerpivot"></a> Comprobación de la configuración de Power Pivot  
 **Servicios:**  
  
1.  En Administración central, en Configuración del sistema, haga clic en **Administrar servicios en el servidor**.  
  
2.  Compruebe que se hayan iniciado **SQL Server Analysis Services** y **SQL Server [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] System Service**.  
  
 **Característica de granja:**  
  
1.  En Administración central, en Configuración del sistema, haga clic en **Administrar características de la granja**.  
  
2.  Compruebe que la **Característica de integración de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]** está **Activa**.  
  
 **Característica de colección de sitios:**  
  
1.  Vaya a la dirección URL del sitio creada por la herramienta de configuración.  
  
     Haga clic en **configuración**![configuración de SharePoint](../../../analysis-services/media/as-sharepoint2013-settings-gear.gif "configuración de SharePoint")y, a continuación, haga clic en **configuración del sitio**.  
  
     Haga clic en **Características de la colección de sitios**.  
  
2.  Compruebe que **[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para colecciones de sitios** está **Activa**.  
  
 **[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] :**  
  
1.  En Administración central, en **Administración de aplicaciones**, haga clic en **Administrar aplicaciones de servicio**.  
  
2.  Compruebe que el estado de la aplicación de servicio es **Iniciado**. El nombre predeterminado es **Aplicación de servicio [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] predeterminada**.  
  
     Haga clic en el nombre de la aplicación de servicios para abrir el Panel de administración de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para la aplicación de servicio. Al usarse por primera vez, el panel tarda varios minutos en cargarse.  
  
 Para más información, vea [Verify a Power Pivot for SharePoint Installation](../../../analysis-services/instances/install-windows/verify-a-power-pivot-for-sharepoint-installation.md).  
  
##  <a name="bkmk_troubleshoot_issues"></a> Solucionar problemas  
 Como ayuda para solucionar problemas, es conveniente comprobar que el registro de diagnósticos esté habilitado.  
  
1.  En Administración central de SharePoint, haga clic en **Supervisión** y, a continuación, haga clic en **Configurar la recolección de datos de uso y estado**.  
  
2.  Compruebe que **Habilitar la recolección de datos de uso** esté activada.  
  
3.  Compruebe que los eventos siguientes estén seleccionados:  
  
    -   Definición de campos de uso para telemetría de educación  
  
    -   [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Conexiones de  
  
    -   [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Uso de datos de carga de  
  
    -   [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Uso de consultas  
  
    -   [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Uso de datos de descarga  
  
4.  Compruebe que **Habilitar la recolección de datos de mantenimiento** esté activada.  
  
5.  Haga clic en **Aceptar**.  
  
 Para obtener más información sobre la actualización de datos de solución de problemas, consulte [solución de problemas de actualización de datos PowerPivot](http://social.technet.microsoft.com/wiki/contents/articles/3870.troubleshooting-powerpivot-data-refresh.aspx) (http://social.technet.microsoft.com/wiki/contents/articles/3870.troubleshooting-powerpivot-data-refresh.aspx).  
  
 Para obtener más información acerca de la herramienta de configuración, vea [Power Pivot Configuration Tools](../../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md).  
  
  
