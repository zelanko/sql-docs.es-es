---
title: Actualice a SQL Server 2014 con el Asistente para la instalación (programa de instalación) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- upgrading Database Engine
- Database Engine [SQL Server], upgrading
ms.assetid: cef118a5-a7ce-4bfa-8b9d-c81996284cfc
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8330702d8c886cc9197dcd944878c3f794780205
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62775425"
---
# <a name="upgrade-to-sql-server-2014-using-the-installation-wizard-setup"></a>Actualizar a SQL Server 2014 mediante el Asistente para la instalación (programa de instalación)
  El Asistente para la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona un único árbol de características para la actualización de los componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. También puede instalar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] en paralelo con una versión anterior, o migrar los valores de configuración y las bases de datos existentes de una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y aplicarlos a una instancia de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Para más información, consulte los temas siguientes:  
  
-   [Actualizaciones de ediciones y versiones admitidas](supported-version-and-edition-upgrades.md)  
  
-   [Trabajar con varias versiones e instancias de SQL Server](../../sql-server/install/work-with-multiple-versions-and-instances-of-sql-server.md)  
  
-   [Actualizar una instancia de clúster de conmutación por error de SQL Server &#40;programa de instalación&#41;](../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance-setup.md)  
  
-   [Instalar SQL Server 2014 desde el símbolo del sistema](install-sql-server-from-the-command-prompt.md)  
  
-   [Usar el Asistente para copiar bases de datos](../../relational-databases/databases/use-the-copy-database-wizard.md)  
  
> [!NOTE]  
>  La actualización de una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] no se admite en un equipo que ejecute [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Server Core SP1. Para obtener más información sobre las instalaciones Server Core, consulte [instalación de SQL Server 2014 en Server Core](install-sql-server-on-server-core.md).  
  
## <a name="prerequisites"></a>Requisitos previos  
 Debe ejecutar el programa de instalación como administrador. Si instala [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde un recurso compartido remoto, debe usar una cuenta de dominio que tenga permisos de lectura y ejecución para el recurso compartido remoto y que sea de un administrador local.  
  
 Antes de actualizar el [!INCLUDE[ssDE](../../includes/ssde-md.md)], revise los siguientes temas:  
  
-   [Actualizar a SQL Server 2014](upgrade-sql-server.md)  
  
-   [Requisitos de hardware y software para instalar SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
  
-   [Comprobar los parámetros del Comprobador de configuración del sistema](check-parameters-for-the-system-configuration-checker.md)  
  
-   [Consideraciones de seguridad para una instalación de SQL Server](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
-   [Compatibilidad con versiones anteriores del Motor de base de datos de SQL Server](../sql-server-database-engine-backward-compatibility.md)  
  
> [!WARNING]  
>  Tenga en cuenta que no puede cambiar las características que se van a actualizar, y no puede agregar características durante la operación de actualización. Para obtener más información sobre cómo agregar características a una instancia actualizada de una vez [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] completada la operación de actualización, vea [Agregar características a una instancia de SQL Server 2014 &#40;&#41;de instalación ](add-features-to-an-instance-of-sql-server-setup.md).  
  
## <a name="procedure"></a>Procedimiento  
  
#### <a name="to-upgrade-to-sscurrent"></a>Para actualizar a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
  
1.  Inserte el disco de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y, en la carpeta raíz, haga doble clic en Setup.exe. Para realizar la instalación desde un recurso compartido de red, vaya a la carpeta raíz de dicho recurso y, a continuación, haga doble clic en Setup.exe.  
  
2.  El Asistente para la instalación inicia el Centro de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para actualizar una instancia existente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], haga clic en **instalación** en el área de navegación de la izquierda y, a continuación, haga clic en **actualizar desde [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)],, [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] **.  
  
3.  En la página Clave del producto, haga clic en una opción para indicar si va a actualizar a una edición gratuita de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o si tiene una clave de PID para una versión de producción del producto. Para obtener más información, vea las [ediciones y los componentes de SQL Server 2014](../../sql-server/editions-and-components-of-sql-server-2016.md) y las actualizaciones de ediciones [y versiones admitidas](supported-version-and-edition-upgrades.md).  
  
4.  En la página Términos de licencia, revise el contrato de licencia y, si está de acuerdo, active la casilla **Acepto los términos de licencia** y haga clic en **Siguiente**. Para ayudar a mejorar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], también puede habilitar la opción de uso de características y enviar informes a [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
5.  En la ventana Reglas globales, el procedimiento de instalación avanzará automáticamente hasta la ventana Actualizaciones de productos si no hay ningún error de regla.  
  
6.  La página [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update aparecerá a continuación si la casilla [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update del Panel de control\Todos los elementos de Panel de control\Windows Update\Cambiar configuración no está activada. Si se pone una marca de verificación en la página [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update, cambiará la configuración del equipo para incluir las últimas actualizaciones al buscar actualizaciones en Windows Update.  
  
7.  En la página Actualizaciones del producto se muestran las actualizaciones del producto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] más recientes disponibles. Si no quiere incluir las actualizaciones, desactive la casilla **Incluir actualizaciones de productos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**. Si no se detectan actualizaciones de producto, el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no muestra esta página y pasa automáticamente a la página **Instalar archivos de instalación** .  
  
8.  En la página Instalar archivos de instalación, el programa de instalación proporciona el progreso de descarga, extracción e instalación de los archivos de instalación. Si se encuentra una actualización para la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], y se especifica que debe incluirse, esa actualización también se instalará.  
  
9. En la ventana Reglas de actualización, el procedimiento de instalación avanzará automáticamente hasta la ventana Seleccionar instancia si no hay ningún error de regla.  
  
10. En la página Seleccionar instancia, especifique la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que va a actualizar. Para actualizar las herramientas de administración y las características compartidas, seleccione **Actualizar solo características compartidas**.  
  
11. En la página Seleccionar características, aparecen seleccionadas previamente las características que se van a actualizar. Después de seleccionar el nombre de la característica se muestra una descripción de cada grupo de componentes en el panel derecho.  
  
     Los requisitos previos para las características seleccionadas se muestran en el recuadro del lado derecho. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] El programa de instalación instalará los requisitos previos que no se hayan instalado todavía durante el paso de instalación que se describe más adelante en este procedimiento.  
  
    > [!NOTE]  
    >  Si ha optado por actualizar las características compartidas seleccionando ** \<actualizar solo características compartidas>** en la página **seleccionar instancia** , todas las características compartidas están preseleccionadas en la página selección de características. Todos los componentes compartidos se actualizan al mismo tiempo.  
  
12. En la página Configuración de instancia, especifique el identificador de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     **ID** . de instancia: de forma predeterminada, el nombre de instancia se usa como identificador de instancia. Se usa para identificar los directorios de instalación y las claves del Registro para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Es así en las instancias predeterminadas y en las instancias con nombre. Con una instancia predeterminada, el nombre y el identificador serían MSSQLSERVER. Para usar un identificador de instancia no predeterminado, proporcione un valor para el cuadro de texto **Id. de instancia** .  
  
     Todos los Service Pack y actualizaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se aplicarán a cada componente de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     **Instancias instaladas**: la cuadrícula mostrará las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que están en el equipo en el que se ejecuta el programa de instalación. Si ya hay una instancia predeterminada instalada en el equipo, debe instalar una instancia con nombre de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
13. El flujo de trabajo para el resto del tema depende de las características que haya especificado para la instalación. Dependiendo de las selecciones, es posible que no vea todas las páginas.  
  
14. En la página Configuración del servidor - Cuentas de servicio, las cuentas de servicio predeterminadas se muestran para los servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los servicios reales que se configuran en esta página dependen de las características que se van a actualizar.  
  
     La información sobre autenticación e inicio de sesión se obtiene de la instancia anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Puede asignar la misma cuenta de inicio de sesión a todos los servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o configurar cada cuenta de servicio individualmente. También puede especificar si los servicios se inician de forma automática o manual, o si están deshabilitados. [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomienda configurar las cuentas de servicio de forma individual para que se concedan a los servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los permisos mínimos que necesitan para completar sus tareas. Para obtener más información, vea [configurar los permisos y las cuentas de servicio de Windows](../configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
     Para especificar la misma cuenta de inicio de sesión para todas las cuentas de servicio en esta instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se han de proporcionar credenciales en los campos de la parte inferior de la página.  
  
     **Nota de seguridad** [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
     Cuando termine de especificar la información de inicio de sesión para los servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , haga clic en **Siguiente**.  
  
15. En la página Opción de actualización de búsqueda de texto completo, especifique las opciones de actualización para las bases de datos que se van a actualizar. Para obtener más información, vea [Opciones de actualización de búsqueda de texto completo](../../sql-server/install/full-text-search-upgrade-options.md).  
  
16. La ventana Reglas de características se pasará automáticamente si se cumplen todas las reglas.  
  
17. La página Listo para actualizar muestra una vista de árbol de las opciones de instalación que se especificaron durante la instalación. Para continuar, haga clic en **Instalar**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] El programa de instalación instalará primero los requisitos previos necesarios para las características seleccionadas y a continuación realizará la instalación de características.  
  
18. Durante la instalación, la página de progreso muestra el estado para que pueda supervisar el progreso de la instalación durante la ejecución del programa de instalación.  
  
19. Después de la instalación, la página Operación completada proporciona un vínculo al archivo de registro de resumen para la instalación y otras notas importantes. Para completar el proceso de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , haga clic en **Cerrar**.  
  
20. Si el programa indica que se reinicie el equipo, hágalo ahora. Es importante leer el mensaje del Asistente para la instalación tras finalizar el programa de instalación. Para obtener más información sobre los archivos de registro de instalación, vea [Ver y leer los archivos de registro de instalación de SQL Server](view-and-read-sql-server-setup-log-files.md).  
  
## <a name="next-steps"></a>Pasos a seguir  
 Después de actualizar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], complete las tareas siguientes:  
  
-   **Registrar los servidores**: la actualización quita la configuración del Registro de la instancia anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Tras la actualización, debe volver a registrar los servidores.  
  
-   **Actualizar las estadísticas**: para poder optimizar el rendimiento de las consultas, es recomendable actualizar las estadísticas de todas las bases de datos tras la actualización. Use el procedimiento almacenado `sp_updatestats` para actualizar las estadísticas de las tablas definidas por el usuario en las bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   **Configurar la nueva instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**: para reducir el área expuesta del sistema susceptible de recibir ataques, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instala y habilita los servicios y características clave de forma selectiva. Para obtener más información sobre la configuración del área expuesta, vea el archivo Léame correspondiente a esta versión.  
  
## <a name="see-also"></a>Consulte también  
 [Actualización a SQL Server 2014](upgrade-sql-server.md)   
 [Compatibilidad con versiones anteriores](../../getting-started/backward-compatibility.md)  
  
  
