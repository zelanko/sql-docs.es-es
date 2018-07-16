---
title: Instalar SQL Server 2014 desde el Asistente para la instalación (programa de instalación) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- installing SQL Server, steps
- Setup [SQL Server], steps
- SQL Server, installing
ms.assetid: 6ad23de1-2bab-4933-9122-c09f5565028d
caps.latest.revision: 79
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6ff8c854a7f2004b30caa11c48423de0995d4652
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37250625"
---
# <a name="install-sql-server-2014-from-the-installation-wizard-setup"></a>Instalar SQL Server 2014 desde el Asistente para la instalación (programa de instalación)
  En este tema se proporciona un procedimiento paso a paso para instalar una nueva instancia de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizando el Asistente para la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . El Asistente para la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona un único árbol de características para la instalación de todos los componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ; de este modo, no tendrá que instalarlos individualmente: Para obtener más información sobre los diversos componentes que se pueden instalar, consulte [instalación de SQL Server 2014](installation-for-sql-server.md).  Para obtener más información sobre cómo instalar el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] componentes por separado, consulte [instalar SQL Server 2014](install-sql-server.md).  
  
 En estos temas adicionales, se documentan otras maneras de instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   [Instalar SQL Server 2014 desde el símbolo del sistema](install-sql-server-from-the-command-prompt.md).  
  
-   [Instalar SQL Server 2014 mediante un archivo de configuración](install-sql-server-using-a-configuration-file.md)  
  
-   [Instalar SQL Server 2014 mediante SysPrep](install-sql-server-using-sysprep.md)  
  
-   [Crear un nuevo clúster de conmutación por error SQL Server &#40;instalación&#41;](../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md).  
  
-   [Actualización a SQL Server 2014 mediante el Asistente para instalación &#40;instalación&#41;](upgrade-sql-server-using-the-installation-wizard-setup.md).  
  
## <a name="prerequisites"></a>Requisitos previos  
 Antes de instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], revise los temas de [Planear una instalación de SQL Server](../../sql-server/install/planning-a-sql-server-installation.md).  
  
> [!NOTE]  
>  En instalaciones locales, debe ejecutar el programa de instalación como administrador. Si instala [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde un recurso compartido remoto, deberá usar una cuenta de dominio que tenga permisos de lectura y ejecución para dicho recurso.  
  
### <a name="to-install-includesscurrentincludessscurrent-mdmd"></a>Para instalar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
  
1.  Inserte el medio de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Desde la carpeta raíz, haga doble clic en Setup.exe. Para realizar la instalación desde un recurso compartido de red, localice la carpeta raíz de dicho recurso y, a continuación, haga doble clic en Setup.exe.  
  
2.  El Asistente para instalación ejecuta el Centro de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para crear una nueva instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], haga clic en **Instalación** en el área de navegación del lado izquierdo y, luego, haga clic en **Nueva instalación independiente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o agregar características a una instalación existente**.  
  
3.  En la página Clave del producto, seleccione una opción para indicar si está instalando una edición gratuita de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o una versión de producción del producto con una clave de PID. Para obtener más información, consulte [ediciones y componentes de SQL Server 2014](../../sql-server/editions-and-components-of-sql-server-2016.md).  
  
     Para continuar, haga clic en **Siguiente**.  
  
4.  En la página Términos de licencia, revise el contrato de licencia y, si está de acuerdo, active la casilla **Acepto los términos de licencia** y haga clic en **Siguiente**. Para ayudar a mejorar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], también puede habilitar la opción de uso de características y enviar informes a [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
5.  En la ventana Reglas globales, el procedimiento de instalación avanzará automáticamente hasta la ventana Actualizaciones de productos si no hay ningún error de regla.  
  
6.  La página [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update aparecerá a continuación si la casilla [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update del Panel de control\Todos los elementos de Panel de control\Windows Update\Cambiar configuración no está activada. Si se pone una marca de verificación en la página [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update, cambiará la configuración del equipo para incluir las últimas actualizaciones al buscar actualizaciones en Windows Update.  
  
7.  En la página Actualizaciones del producto se muestran las actualizaciones del producto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] más recientes disponibles. Si no se detectan actualizaciones de producto, el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no muestra esta página y pasa automáticamente a la página **Instalar archivos de instalación** .  
  
8.  En la página Instalar archivos de instalación, el programa de instalación proporciona el progreso de descarga, extracción e instalación de los archivos de instalación. Si se encuentra una actualización para la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], y se especifica que debe incluirse, esa actualización también se instalará.  
  
9. En la página Rol de instalación, seleccione **Instalación de características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** y, luego, haga clic en **Siguiente** para continuar en la página Selección de características.  
  
10. En la página Selección de características, seleccione los componentes de la instalación. Después de seleccionar el nombre de la característica, aparece una descripción de cada grupo del componente en el panel **Descripción de característica** . Puede activar cualquier combinación de casillas. Para obtener más información, consulte [ediciones y componentes de SQL Server 2014](../../sql-server/editions-and-components-of-sql-server-2016.md) y [características compatibles con las ediciones de SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
     Los requisitos previos para las características seleccionadas se muestran en el panel **Requisitos previos de las características seleccionadas** . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] El programa de instalación instalará los requisitos previos que no se hayan instalado todavía durante el paso de instalación que se describe más adelante en este procedimiento.  
  
     Si desea especificar un directorio personalizado para los componentes compartidos, use el campo situado en la parte inferior de la página Selección de características. Para cambiar la ruta de instalación de los componentes compartidos, actualice el nombre de ruta en el campo situado en la parte inferior del cuadro de diálogo o haga clic en **Examinar** para moverse a un directorio de instalación. La ruta de instalación predeterminada es [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)].  
  
     La ruta de acceso especificada para los componentes compartidos debe ser una ruta de acceso absoluta. La carpeta no se debe comprimir ni cifrar. No se admiten las unidades asignadas.  
  
     Si está instalando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un sistema operativo de 64 bits, verá las opciones siguientes:  
  
    1.  Directorio de características compartidas  
  
    2.  Directorio de características compartidas (x86)  
  
     La ruta de acceso especificada para cada una de las opciones anteriores debe ser diferente.  
  
11. La ventana Reglas de características se pasará automáticamente si se cumplen todas las reglas.  
  
12. En la página Configuración de instancia, especifique si desea instalar una instancia predeterminada o una instancia con nombre. Para obtener más información, vea [Instance Configuration](../../sql-server/install/instance-configuration.md).  
  
     **Id. de instancia** : de forma predeterminada, el nombre de instancia se usa como identificador de la instancia. Se usa para identificar los directorios de instalación y las claves del Registro para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Es así en las instancias predeterminadas y en las instancias con nombre. Con una instancia predeterminada, el nombre y el identificador serían MSSQLSERVER. Para usar un identificador de instancia no predeterminado, especifique un valor diferente en el cuadro de texto **Id. de instancia** .  
  
    > [!NOTE]  
    >  Las instancias independientes típicas de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], tanto si son predeterminadas como si son instancias con nombre, no usan un valor no predeterminado para el cuadro **Id. de instancia**.  
  
     Todos los Service Pack y actualizaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se aplicarán a cada componente de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     **Instancias instaladas:** la cuadrícula muestra las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que están en el equipo en el que se ejecuta el programa de instalación. Si ya hay una instancia predeterminada instalada en el equipo, debe instalar una instancia con nombre de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
     El flujo de trabajo del resto de la instalación depende de las características que haya especificado en la instalación. Dependiendo de las selecciones, es posible que no vea todas las páginas.  
  
13. En la página Configuración del servidor - Cuentas de servicio, especifique las cuentas de inicio de sesión para los servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Los servicios reales que se configuran en esta página dependen de las características que se van a instalar.  
  
     Puede asignar la misma cuenta de inicio de sesión a todos los servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o configurar cada cuenta de servicio individualmente. También puede especificar si los servicios se inician de forma automática o manual, o si están deshabilitados. [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomienda configurar las cuentas de servicio de forma individual para proporcionar a cada servicio los privilegios mínimos; así, los servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] obtendrán los permisos mínimos que necesitan para completar sus tareas. Para obtener más información, vea [Configuración del servidor - Cuentas de servicio](../../sql-server/install/server-configuration-service-accounts.md) y [Configurar los permisos y las cuentas de servicio de Windows](../configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
     Para especificar la misma cuenta de inicio de sesión para todas las cuentas de servicio en esta instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], las credenciales se proporcionan en los campos de la parte inferior de la página.  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
     Use la página Configuración del servidor - Intercalación para especificar intercalaciones no predeterminadas para el [!INCLUDE[ssDE](../../includes/ssde-md.md)] y para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para obtener más información, vea [Configurar servidor - Intercalación](../../sql-server/install/server-configuration-collation.md).  
  
14. Use la página Configuración del [!INCLUDE[ssDE](../../includes/ssde-md.md)] - Configuración del servidor para especificar lo siguiente:  
  
    -   Modo de seguridad: seleccione la autenticación de Windows o la autenticación de modo mixto para su instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si selecciona la autenticación de modo mixto, debe proporcionar una contraseña segura para la cuenta de administrador del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] integrada.  
  
         Una vez que un dispositivo establece una conexión correcta con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el mecanismo de seguridad es el mismo para la autenticación de Windows y para el modo mixto. Para obtener más información, consulte [configuración del motor de base de datos - aprovisionamiento de cuentas](../../sql-server/install/database-engine-configuration-account-provisioning.md).  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] : debe especificar al menos un administrador del sistema para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para agregar la cuenta en la que se ejecuta el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , haga clic en **Agregar usuario actual**. Para agregar o quitar cuentas de la lista de administradores del sistema, haga clic en **Agregar** o en **Quitar**y, a continuación, modifique la lista de usuarios, grupos o equipos que tendrán privilegios de administrador para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Use la página Configuración de [!INCLUDE[ssDE](../../includes/ssde-md.md)] - Directorios de datos para especificar los directorios de instalación no predeterminados. Para instalar en los directorios predeterminados, haga clic en **Siguiente**.  
  
    > [!IMPORTANT]  
    >  Si especifica los directorios de instalación no predeterminados, asegúrese de que las carpetas de instalación sean únicas para esta instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ninguno de los directorios de este cuadro de diálogo se debe compartir con los de otras instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Además, la instalación de SQL Server con los directorios de datos en la carpeta raíz de una unidad o un punto de montaje se producirá un error. Para obtener más información, consulte [soporte técnico de SQL Server para volúmenes montados.](http://support.microsoft.com/kb/819546/en-us)  
  
     Para obtener más información, vea [Configuración del motor de base de datos - Directorios de datos](../../sql-server/install/database-engine-configuration-data-directories.md).  
  
     Use la página Configuración de [!INCLUDE[ssDE](../../includes/ssde-md.md)] - FILESTREAM para habilitar FILESTREAM para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, vea [Configuración del motor de base de datos - Secuencia de archivo](../../sql-server/install/database-engine-configuration-filestream.md).  
  
15. Use la página Configuración de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] - Aprovisionamiento de cuentas para especificar el modo de servidor y los usuarios o las cuentas que tendrán permisos de administrador para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. El modo servidor determina los subsistemas de memoria y de almacenamiento que se utilizan en el servidor. Tipos diferentes de solución se ejecutan en modos servidor diferentes. Si tiene previsto ejecutar bases de datos multidimensionales de cubo en el servidor, elija la opción predeterminada, el modo servidor multidimensional y de minería de datos. En lo que respecta a los permisos de administrador, debe especificar al menos un administrador del sistema para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para agregar la cuenta en la que se ejecuta el programa de instalación de SQL Server, haga clic en **Agregar usuario actual**. Para agregar o quitar cuentas de la lista de administradores del sistema, haga clic en **Agregar** o **Quitar**y, a continuación, modifique la lista de usuarios, grupos o equipos que tendrán privilegios de administrador para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para obtener más información sobre los permisos de administrador y de modo de servidor, vea [Configuración de Analysis Services - Aprovisionamiento de cuentas](../../sql-server/install/analysis-services-configuration-account-provisioning.md).  
  
     Cuando haya terminado de modificar la lista, haga clic en **Aceptar**. Compruebe la lista de administradores en el cuadro de diálogo de configuración. Cuando la lista esté completa, haga clic en **Siguiente**.  
  
     Use la página Configuración de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] - Directorios de datos para especificar los directorios de instalación no predeterminados. Para instalar en los directorios predeterminados, haga clic en **Siguiente**.  
  
    > [!IMPORTANT]  
    >  Si especifica los directorios de instalación no predeterminados, asegúrese de que las carpetas de instalación sean únicas para esta instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ninguno de los directorios de este cuadro de diálogo se debe compartir con los de otras instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Además, la instalación de SQL Server con los directorios de datos en la carpeta raíz de una unidad o un punto de montaje se producirá un error. Para obtener más información, consulte [soporte técnico de SQL Server para volúmenes montados.](http://support.microsoft.com/kb/819546/en-us)  
  
     Para obtener más información, vea [Configuración de Analysis Services - Directorios de datos](../../sql-server/install/analysis-services-configuration-data-directories.md).  
  
16. Use la página Configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para especificar el tipo de instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que se creará. Para obtener más información sobre los modos de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y las opciones disponibles, vea [Opciones de configuración de Reporting Services &#40;SSRS&#41;](../../sql-server/install/reporting-services-configuration-options-ssrs.md).  
  
     Después de elegir una opción, haga clic en **Siguiente** para continuar.  
  
17. Use la página Configuración de Distributed Replay Controller para especificar los usuarios a los que desee conceder permisos administrativos para el servicio Distributed Replay Controller. Los usuarios con permisos administrativos tendrán acceso ilimitado al servicio Controlador de Distributed Replay.  
  
     Haga clic en el botón **Agregar usuario actual** para agregar los usuarios a los que desee conceder permisos de acceso para el servicio Distributed Replay Controller. Haga clic en el botón **Agregar** para agregar permisos de acceso para el servicio Distributed Replay Controller. Haga clic en el botón **Quitar** para quitar permisos de acceso del servicio Distributed Replay Controller.  
  
     Para continuar, haga clic en **Siguiente**.  
  
18. Use la página Configuración de Distributed Replay Client para especificar los usuarios a los que desee conceder permisos administrativos para el servicio Distributed Replay Client. Los usuarios con permisos administrativos tendrán acceso ilimitado al servicio Distributed Replay Client.  
  
     **Nombre del controlador** es un parámetro opcional y el valor predeterminado es \<*blank*>. Escriba el nombre del controlador con el que se comunicará el equipo cliente para el servicio Distributed Replay Client. Observe lo siguiente:  
  
    -   Si ya ha configurado un controlador, escriba el nombre del controlador mientras configura cada cliente.  
  
    -   Si aún no ha configurado ningún controlador, puede dejar el nombre del controlador en blanco. Sin embargo, debe escribir manualmente el nombre del controlador en el archivo de **configuración de cliente** .  
  
     Especifique el **Directorio de trabajo** para el servicio Distributed Replay Client. El directorio de trabajo predeterminado es \<*letra de unidad*>:\Archivos de programa\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\DReplayClient\WorkingDir\\.  
  
     Especifique el **Directorio de resultados** para el servicio Distributed Replay Client. El directorio de resultados predeterminado es \<*letra de unidad*>:\Archivos de programa\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\DReplayClient\ResultDir\\.  
  
     Para continuar, haga clic en **Siguiente**.  
  
19. La página Listo para instalar muestra una vista de árbol de las opciones de instalación que se especificaron durante la instalación. En esta página, el programa de instalación indica si la característica de actualización de producto está habilitada o deshabilitada y la versión final de actualización.  
  
     Para continuar, haga clic en **Instalar**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] El programa de instalación instalará primero los requisitos previos necesarios para las características seleccionadas y a continuación realizará la instalación de características.  
  
20. La página Progreso de la instalación muestra el estado para que pueda supervisar el progreso de la instalación durante la ejecución del programa de instalación.  
  
21. Después de la instalación, la página Operación completada proporciona un vínculo al archivo de registro de resumen para la instalación y otras notas importantes. Para completar el proceso de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , haga clic en **Cerrar**.  
  
22. Si el programa indica que se reinicie el equipo, hágalo ahora. Es importante leer el mensaje del Asistente para la instalación tras finalizar el programa de instalación. Para obtener más información, vea [View and Read SQL Server Setup Log Files](view-and-read-sql-server-setup-log-files.md).  
  
## <a name="next-steps"></a>Pasos siguientes  
 Configurar la nueva instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Para reducir el área expuesta de un sistema susceptible de recibir ataques, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instala y habilita de manera selectiva los servicios y características clave. Para obtener más información, vea [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Validar una instalación de SQL Server](validate-a-sql-server-installation.md)   
 [Quitar una instalación de SQL Server 2014](repair-a-failed-sql-server-installation.md)   
 [Ver y leer los archivos de registro de instalación de SQL Server](view-and-read-sql-server-setup-log-files.md)   
 [Actualización a SQL Server 2014 mediante el Asistente para instalación &#40;el programa de instalación&#41;](upgrade-sql-server-using-the-installation-wizard-setup.md)   
 [Instalar SQL Server 2014 desde el símbolo del sistema](install-sql-server-from-the-command-prompt.md)  
  
  
