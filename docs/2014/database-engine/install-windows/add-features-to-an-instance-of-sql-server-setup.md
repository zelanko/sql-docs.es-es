---
title: Agregar características a una instancia de SQL Server 2014 (programa de instalación) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- feature adding [SQL Server]
- SQL Server, features
- adding features to SQL Server
ms.assetid: 97931fdc-d943-48dd-81b9-ae8b8d2c6dad
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 147fe717919035c365ef2e3507e46a4323694570
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62779376"
---
# <a name="add-features-to-an-instance-of-sql-server-2014-setup"></a>Agregar características a una instancia de SQL Server 2014 (programa de instalación)
  En este tema se proporciona un procedimiento paso a paso para agregar características a una instancia de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Algunos componentes o servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] son específicos de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. También se denominan dependientes de la instancia. Comparten la misma versión que la instancia que los hospeda y se usan exclusivamente para dicha instancia. Puede agregar los componentes dependientes de la instancia a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], junto con los componentes compartidos si no están instalados. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
 Para agregar características a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde el símbolo del sistema, vea [install SQL Server 2014 desde el](install-sql-server-from-the-command-prompt.md)símbolo del sistema.  
  
## <a name="prerequisites"></a>Prerequisites  
 Antes de continuar, revise los temas de [Planning a SQL Server Installation](../../sql-server/install/planning-a-sql-server-installation.md).  
  
> [!NOTE]  
>  En instalaciones locales, debe ejecutar el programa de instalación como administrador. Si instala [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde un recurso compartido remoto, deberá usar una cuenta de dominio que tenga permisos de lectura para dicho recurso.  
  
> [!NOTE]  
>  Al agregar las características a una instancia de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], la configuración del informe de uso existente se aplica a las características agregadas recientemente. Para cambiar estos valores, use la herramienta **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del menú** Herramientas de configuración [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**de** .  
  
## <a name="procedures"></a>Procedimientos  
  
#### <a name="to-add-features-to-an-instance-of-includesscurrentincludessscurrent-mdmd"></a>Para agregar características a una instancia de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
  
1.  Inserte el medio de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . En la carpeta raíz, haga doble clic en setup.exe. Para realizar la instalación desde un recurso compartido de red, navegue hasta la carpeta raíz de dicho recurso y, a continuación, haga doble clic en setup.exe. Si aparece el cuadro de diálogo Programa de instalación de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] , haga clic en [!INCLUDE[clickOK](../../includes/clickok-md.md)] para instalar los requisitos previos y, a continuación, haga clic en **Cancelar** para salir de la instalación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
2.  El Asistente para la instalación iniciará el Centro de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para agregar una nueva característica a una instancia existente de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], haga clic en **Instalación** en el área de navegación del lado izquierdo y, después, haga clic en **Nueva instalación independiente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o agregar características a una instalación existente**.  
  
3.  El Comprobador de configuración del sistema ejecutará una operación de detección en su equipo. Para ver los detalles de la comprobación, haga clic en **Ver detalles**. Para continuar, [!INCLUDE[clickOK](../../includes/clickok-md.md)].  
  
4.  En la página Actualizaciones del producto se muestran las actualizaciones del producto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] más recientes disponibles. Si no quiere incluir las actualizaciones, desactive la casilla **Incluir actualizaciones de productos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** . Si no se detectan actualizaciones de producto, el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no muestra esta página y pasa automáticamente a la página **Instalar archivos de instalación** .  
  
5.  En la página Instalar archivos de instalación, el programa de instalación proporciona el progreso de descarga, extracción e instalación de los archivos de instalación. Si se encuentra una actualización para la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], y se especifica que debe incluirse, esa actualización también se instalará. Haga clic en **Instalar** para instalar los archivos auxiliares del programa de instalación.  
  
6.  El Comprobador de configuración del sistema comprobará el estado del sistema de su equipo antes de seguir con la instalación.  
  
7.  En la página Tipo de instalación, seleccione la opción **Agregar características a una instancia existente de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** y seleccione la instancia que quiera actualizar.  
  
8.  En la página Selección de características, seleccione los componentes de la instalación. Después de seleccionar el nombre de la característica, la descripción de cada grupo de componentes aparece en el panel derecho. Puede activar cualquier combinación de casillas. Para obtener más información, vea [ediciones y componentes de SQL Server 2014](../../sql-server/editions-and-components-of-sql-server-2016.md). Cada componente solo se puede instalar una vez en cada instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para instalar varios componentes, deberá instalar una instancia adicional de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Los requisitos previos para las características seleccionadas se muestran en el recuadro del lado derecho. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] El programa de instalación instalará los requisitos previos que no se hayan instalado todavía durante el paso de instalación que se describe más adelante en este procedimiento.  
  
     El Comprobador de configuración del sistema comprobará el estado del sistema de su equipo antes de seguir con la instalación. Haga clic en **Siguiente** para continuar.  
  
9. La página Requisitos de espacio en disco calcula el espacio en disco necesario para las características especificadas, y compara los requisitos con el espacio en disco disponible en el equipo donde se ejecuta el programa de instalación.  
  
10. El flujo de trabajo en el resto del tema depende de las características que haya especificado en la instalación. Dependiendo de las selecciones, es posible que no vea todas las páginas.  
  
11. En la página Configuración del servidor - Cuentas de servicio, especifique las cuentas de inicio de sesión para los servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los servicios reales que se configuran en esta página dependen de las características que se van a instalar.  
  
     Puede asignar la misma cuenta de inicio de sesión a todos los servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o configurar cada cuenta de servicio individualmente. También puede especificar si los servicios se inician de forma automática o manual, o si están deshabilitados. [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomienda configurar las cuentas de servicio de forma individual para proporcionar a cada servicio los privilegios mínimos; así, los servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] obtendrán los permisos mínimos que necesitan para completar sus tareas. Para obtener más información, vea [Configuración del servidor - Cuentas de servicio](../../sql-server/install/server-configuration-service-accounts.md) y [Configurar los permisos y las cuentas de servicio de Windows](../configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
     Para especificar la misma cuenta de inicio de sesión para todas las cuentas de servicio en esta instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se han de proporcionar credenciales en los campos de la parte inferior de la página.  
  
     **Nota de seguridad** : [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
     Cuando termine de especificar la información de inicio de sesión para los servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , haga clic en **Siguiente**.  
  
12. Use la pestaña **Configurar servidor - Intercalación** para especificar intercalaciones no predeterminadas para [!INCLUDE[ssDE](../../includes/ssde-md.md)] y [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para obtener más información, vea [Configuración del servidor - Intercalación](../../sql-server/install/server-configuration-collation.md).  
  
13. Use la página Configuración de [!INCLUDE[ssDE](../../includes/ssde-md.md)] - Aprovisionamiento de cuentas para especificar lo siguiente:  
  
    -   Modo de Seguridad: seleccione la autenticación de Windows o la autenticación de modo mixto para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si selecciona la autenticación de modo mixto, debe proporcionar una contraseña segura para la cuenta de administrador del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] integrada.  
  
         Una vez que un dispositivo establece una conexión correcta con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el mecanismo de seguridad es el mismo para la autenticación de Windows y para el modo mixto. Para obtener más información, vea [Database Engine Configuration - Account Provisioning](../../sql-server/install/database-engine-configuration-account-provisioning.md).  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Administradores: debe especificar al menos un administrador del sistema para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para agregar la cuenta en la que se ejecuta el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , haga clic en **Agregar usuario actual**. Para agregar o quitar cuentas de la lista de administradores del sistema, haga clic en **Agregar** o en **Quitar**y, a continuación, modifique la lista de usuarios, grupos o equipos que tendrán privilegios de administrador para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, vea [Database Engine Configuration - Account Provisioning](../../sql-server/install/database-engine-configuration-account-provisioning.md).  
  
     Cuando haya terminado de modificar la lista, haga clic en **Aceptar**. Compruebe la lista de administradores en el cuadro de diálogo de configuración. Cuando la lista esté completa, haga clic en **Siguiente**.  
  
14. Use la página Configuración de [!INCLUDE[ssDE](../../includes/ssde-md.md)] - Directorios de datos para especificar los directorios de instalación no predeterminados. Para instalar en los directorios predeterminados, haga clic en **Siguiente**.  
  
    > [!IMPORTANT]  
    >  Si especifica los directorios de instalación no predeterminados, asegúrese de que las carpetas de instalación sean únicas para esta instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ninguno de los directorios de este cuadro de diálogo se debe compartir con los de otras instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Para obtener más información, vea [Configuración del motor de base de datos - Directorios de datos](../../sql-server/install/database-engine-configuration-data-directories.md).  
  
15. Use la página Configuración de [!INCLUDE[ssDE](../../includes/ssde-md.md)] - FILESTREAM para habilitar FILESTREAM para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información sobre FILESTREAM, vea [Configuración del motor de base de datos - Secuencia de archivo](../../sql-server/install/database-engine-configuration-filestream.md). Para continuar, haga clic en Siguiente.  
  
16. Use la página Configuración de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] - Aprovisionamiento de cuentas para especificar el modo de servidor y los usuarios o las cuentas que tendrán permisos de administrador para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. El modo servidor determina los subsistemas de memoria y de almacenamiento que se utilizan en el servidor. Tipos diferentes de solución se ejecutan en modos servidor diferentes. Si tiene previsto ejecutar bases de datos multidimensionales de cubo en el servidor, elija la opción predeterminada, el modo servidor multidimensional y de minería de datos. En lo que respecta a los permisos de administrador, debe especificar al menos un administrador del sistema para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para agregar la cuenta en la que se ejecuta el programa de instalación de SQL Server, haga clic en **Agregar usuario actual**. Para agregar o quitar cuentas de la lista de administradores del sistema, haga clic en **Agregar** o **Quitar**y, a continuación, modifique la lista de usuarios, grupos o equipos que tendrán privilegios de administrador para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para obtener más información sobre los permisos de administrador y de modo de servidor, vea [Configuración de Analysis Services - Aprovisionamiento de cuentas](../../sql-server/install/analysis-services-configuration-account-provisioning.md).  
  
     Cuando haya terminado de modificar la lista, haga clic en **Aceptar**. Compruebe la lista de administradores en el cuadro de diálogo de configuración. Cuando la lista esté completa, haga clic en **Siguiente**.  
  
17. Use la página Configuración de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] - Directorios de datos para especificar los directorios de instalación no predeterminados. Para instalar en los directorios predeterminados, haga clic en **Siguiente**.  
  
    > [!IMPORTANT]  
    >  Si especifica los directorios de instalación no predeterminados, asegúrese de que las carpetas de instalación sean únicas para esta instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ninguno de los directorios de este cuadro de diálogo se debe compartir con los de otras instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Para obtener más información, vea [Configuración de Analysis Services - Directorios de datos](../../sql-server/install/analysis-services-configuration-data-directories.md).  
  
18. Use la página Configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para especificar el tipo de instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que se creará. Para obtener más información sobre los modos de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], vea [Opciones de configuración de Reporting Services &#40;SSRS&#41;](../../sql-server/install/reporting-services-configuration-options-ssrs.md).  
  
19. Use la página Configuración de Distributed Replay Controller para especificar los usuarios a los que desee conceder permisos administrativos para el servicio Distributed Replay Controller. Los usuarios con permisos administrativos tendrán acceso ilimitado al servicio Controlador de Distributed Replay.  
  
     Haga clic en el botón **Agregar usuario actual** para agregar los usuarios a los que desee conceder permisos de acceso para el servicio Distributed Replay Controller. Haga clic en el botón **Agregar** para agregar permisos de acceso para el servicio Distributed Replay Controller. Haga clic en el botón **Quitar** para quitar permisos de acceso del servicio Distributed Replay Controller.  
  
     Para continuar, haga clic en **Siguiente**.  
  
20. Use la página Configuración de Distributed Replay Client para especificar los usuarios a los que desee conceder permisos administrativos para el servicio Distributed Replay Client. Los usuarios con permisos administrativos tendrán acceso ilimitado al servicio Distributed Replay Client.  
  
     **Nombre del controlador** es un parámetro opcional y el valor predeterminado es \<*blank*>. Escriba el nombre del controlador con el que se comunicará el equipo cliente para el servicio Distributed Replay Client. Tenga en cuenta lo siguiente:  
  
    -   Si ya ha configurado un controlador, escriba el nombre del controlador mientras configura cada cliente.  
  
    -   Si aún no ha configurado ningún controlador, puede dejar el nombre del controlador en blanco. Sin embargo, debe escribir manualmente el nombre del controlador en el archivo de **configuración de cliente** .  
  
     Especifique el **Directorio de trabajo** para el servicio Distributed Replay Client. El directorio de trabajo predeterminado es \<*letra de unidad*>:\Archivos de programa\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\DReplayClient\WorkingDir\\.  
  
     Especifique el **Directorio de resultados** para el servicio Distributed Replay Client. El directorio de resultados predeterminado es \<*letra de unidad*>:\Archivos de programa\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\DReplayClient\ResultDir\\.  
  
     Para continuar, haga clic en **Siguiente**.  
  
21. En la página Informes de errores, especifique la información que desea enviar a [!INCLUDE[msCoName](../../includes/msconame-md.md)] y que ayudará a mejorar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. De forma predeterminada, se habilitan las opciones de informes de errores.  
  
22. El Comprobador de configuración del sistema ejecutará uno o varios conjuntos de reglas para validar la configuración del equipo con las características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que ha especificado.  
  
23. La página Listo para instalar muestra una vista de árbol de las opciones de instalación que se especificaron durante la instalación. En esta página, el programa de instalación indica si la característica de actualización de producto está habilitada o deshabilitada y la versión final de actualización. Después de hacer clic en la opción de instalación, el Programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalará primero los requisitos previos necesarios para las características seleccionadas y, a continuación, instalará las características.  
  
24. La página Progreso de la instalación muestra el estado para que pueda supervisar el progreso de la instalación durante la ejecución del programa de instalación.  
  
25. Después de la instalación, la página Operación completada proporciona un vínculo al archivo de registro de resumen para la instalación y otras notas importantes. Para completar el proceso de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , haga clic en **Cerrar**.  
  
26. Si el programa indica que se reinicie el equipo, hágalo ahora. Es importante leer el mensaje del Asistente para la instalación tras completar el programa de instalación. Para obtener más información sobre los archivos de registro de instalación, vea [Ver y leer los archivos de registro de instalación de SQL Server](view-and-read-sql-server-setup-log-files.md).  
  
## <a name="next-steps"></a>Pasos siguientes  
 Configurar la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Para reducir el área expuesta del sistema susceptible de recibir ataques, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instala y activa de manera selectiva los servicios y las características clave. Para obtener más información, vea [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md).  
  
## <a name="see-also"></a>Consulte también  
 [Ver y leer los archivos de registro de instalación de SQL Server](view-and-read-sql-server-setup-log-files.md)   
 [Validar una instalación de SQL Server](validate-a-sql-server-installation.md)   
 [Quitar una instalación SQL Server 2014](repair-a-failed-sql-server-installation.md)   
 [Actualice a SQL Server 2014 mediante el Asistente para la instalación &#40;la instalación&#41;](upgrade-sql-server-using-the-installation-wizard-setup.md)   
 [Instalar SQL Server 2014 desde el símbolo del sistema](install-sql-server-from-the-command-prompt.md)  
  
  
