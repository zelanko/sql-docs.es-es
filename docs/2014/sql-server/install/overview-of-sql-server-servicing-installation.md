---
title: Información general de la instalación de servicios de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 6a9fd19b-2367-4908-b638-363b1e929e1e
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b8e9532c9d3ecbc32942e6a70d82f5837856a329
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66093590"
---
# <a name="overview-of-sql-server-servicing-installation"></a>Información general sobre la instalación de servicios de SQL Server
  Puede aplicar una actualización a cualquier componente instalado de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] con una actualización de servicio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Si el nivel de versión de un componente de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] existente es posterior al nivel de versión de la actualización, el programa de instalación lo excluirá de la actualización. Para obtener más información sobre cómo aplicar una actualización de servicio, consulte Instalación de actualizaciones de servicio de [SQL Server 2014](../../database-engine/install-windows/install-sql-server-servicing-updates.md).  
  
 Al instalar las actualizaciones de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], deben tenerse en cuenta las consideraciones siguientes:  
  
-   Todas las características que pertenezcan a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deben actualizarse al mismo tiempo. Por ejemplo, si actualiza [!INCLUDE[ssDE](../../includes/ssde-md.md)], también debe actualizar los componentes [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] si están instalados como parte de la misma instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Las características compartidas, como Herramientas de administración, [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], siempre deben estar totalmente actualizadas. Si un componente o una instancia del árbol de características no está seleccionado, dicho componente o instancia no se actualizará.  
  
-   De forma predeterminada [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , los archivos de registro de actualización se guardan\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]en%\\archivos de programa% \120\Setup Bootstrap\LOG.  
  
-   La instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ahora puede integrar una actualización con el medio original para ejecutar el medio original y la actualización al mismo tiempo. Para obtener más información, consulte [novedades de SQL Server instalación](../../../2014/sql-server/install/what-s-new-in-sql-server-installation.md).  
  
-   Antes de aplicar una actualización de servicio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , se recomienda que haga una copia de seguridad de los datos.  
  
-   Las actualizaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] están disponibles en [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update. Le recomendamos que busque actualizaciones regularmente para garantizar la seguridad y las actualizaciones de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] SP1 se proporciona como una instalación completa de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. En lugar de proporcionar el Service Pack en el paquete ejecutable estándar de la revisión que se va a aplicar a las instancias de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] RTM, para esta versión se ofrece un paquete de instalación que consta de dos archivos. Cuando se ejecute, instalará una nueva instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con SP1 preinstalado.  
  
## <a name="requirements-and-known-issues"></a>Requisitos y problemas conocidos  
 Para descargar, extraer e instalar el paquete se recomienda un espacio disponible equivalente a 2,5 veces el tamaño del paquete. Una vez instalado un Service Pack, puede eliminar el paquete descargado. Cualquier archivo temporal se quita automáticamente.  
  
 **Revise los problemas conocidos:** Para obtener más información sobre los problemas conocidos de la versión actual, vea el tema correspondiente de las notas de la versión aquí: [SQL Server notas](https://msdn.microsoft.com/f617a0af-92dd-47aa-82c3-f51b1346bcd8)de la versión.  
  
## <a name="installation-overview"></a>Información general sobre la instalación  
 En esta sección se explica la instalación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para las actualizaciones acumulativas y Service Pack, incluido cómo hacer lo siguiente:  
  
-   Preparar la instalación de actualizaciones de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
  
-   Instalar las actualizaciones de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
  
-   Reiniciar los servicios y las aplicaciones  
  
### <a name="prepare-for-a-includesscurrentincludessscurrent-mdmd-update-installation"></a>Preparar la instalación de actualizaciones de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 Se recomienda encarecidamente que haga lo siguiente antes de instalar las actualizaciones de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]:  
  
-   **Haga una copia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de seguridad** de las bases de datos del [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] sistema: antes de instalar `master`las `msdb`actualizaciones, `model` realice una copia de seguridad de las bases de datos de, y. Al instalar una actualización de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], estas bases de datos se modifican y se vuelven incompatibles con versiones anteriores de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Las copias de seguridad de estas bases de datos son necesarias si decide volver a instalar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] sin estas actualizaciones.  
  
     Asimismo, es una medida prudente hacer una copia de seguridad de las bases de datos de usuario.  
  
    > [!IMPORTANT]  
    >  Al aplicar actualizaciones a las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que participan en una topología de replicación, debe hacer una copia de seguridad de las bases de datos replicadas junto con las bases de datos del sistema antes de aplicar la actualización.  
  
-   **Haga [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] una copia de seguridad** de las bases de datos, el archivo de configuración y el repositorio antes de actualizar una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], debe realizar una copia de seguridad de lo siguiente:  
  
    -   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]bases. De forma predeterminada, se instalan en c:\Archivos\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]de programa \MSAS12. \<InstanceID> \olap\data\\. Para la instalación de WoW, la ruta de acceso predeterminada es C:\ProgramFiles [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)](x86) \ \MSAS12. \<InstanceID> \olap\data\\.  
  
    -   Valor de configuración de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en el archivo de configuración msmdsrv.ini. De forma predeterminada, se encuentra en la carpeta c:\Archivos\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]de programa \MSAS12. \<InstanceID> directorio \olap\config\  
  
    -   (Opcional) La base de datos que contiene el repositorio de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Este paso únicamente es necesario si se configuró [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para trabajar con la biblioteca de objetos de ayuda para la toma de decisiones (DSO).  
  
    > [!NOTE]  
    >  Si no realiza ninguna copia de seguridad de las bases de datos, del archivo de configuración y del repositorio de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , no podrá revertir una instancia actualizada de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] a la versión anterior.  
  
-   **Compruebe que las bases de datos del sistema tienen suficiente espacio libre** : Si la opción de crecimiento automático no está seleccionada `master` para `msdb` las bases de datos del sistema y, cada una de ellas debe tener al menos 500 KB de espacio libre. Para comprobar que las bases de datos tienen suficiente espacio, ejecute el procedimiento almacenado del sistema `sp_spaceused` en las bases de datos `master` y `msdb`. Si el espacio sin asignar de alguna de las bases de datos es inferior a 500 KB, aumente el tamaño de la base de datos.  
  
-   **Detener servicios y aplicaciones** : para evitar un posible reinicio del sistema, detenga todas las aplicaciones y servicios que realicen conexiones con las [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancias de que se están actualizando antes de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] instalar las actualizaciones. Incluyen [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]y [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Para más información, consulte [Iniciar, detener, pausar, reanudar y reiniciar el motor de base de datos, Agente SQL Server o el Servicio SQL Server Browser](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md).  
  
    > [!NOTE]  
    >  Los servicios no pueden detenerse en un entorno de clúster de conmutación por error. Para obtener más información, vea la sección sobre instalación de clúster de conmutación por error más adelante en este tema.  
  
-   Para eliminar el requisito de reinicio del equipo tras la instalación de las actualizaciones, el programa de instalación mostrará una lista de los procesos que están bloqueando archivos. Si el programa de instalación de las actualizaciones debe finalizar un servicio durante el proceso de instalación, lo reiniciará una vez que concluya la instalación.  
  
-   Si el programa de instalación determina que hay archivos bloqueados durante el proceso de instalación, puede que sea necesario reiniciar el equipo una vez finalizada la instalación. Si es necesario, el programa de instalación le indicará que reinicie el equipo.  
  
### <a name="install-includesscurrentincludessscurrent-mdmd-updates"></a>Instalar las actualizaciones de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 En esta sección se describe el proceso de instalación.  
  
> [!IMPORTANT]  
>  Las actualizaciones de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] se deben instalar con una cuenta que tenga privilegios de administrador en el equipo en el que se instalarán. En instalaciones locales, debe ejecutar el programa de instalación como administrador. Si instala [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde un recurso compartido remoto, deberá usar una cuenta de dominio que tenga permisos de lectura y ejecución para dicho recurso.  
  
#### <a name="starting-a-includesscurrentincludessscurrent-mdmd-update"></a>Iniciar una actualización de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 Para instalar una actualización de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], ejecute el archivo de paquete autoextraíble.  
  
 Paquete de actualización acumulativa (CU) \<: SQLServer2014>-KBxxxxxx-*PPP*. exe  
  
 Paquete de Service Pack (PCU) \<: SQLServer2014 \<>SPX>-KBxxxxxx-PPP-LLL. exe  
  
-   Las x indican el número de Service Pack  
  
-   PPP indica la plataforma concreta.  
  
-   LLL indica la abreviatura de caracteres del idioma de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ; por ejemplo, LLL para inglés es ENU.  
  
 Para aplicar actualizaciones a los componentes de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] que forman parte de un clúster de conmutación por error, vea la sección correspondiente a la instalación de clústeres de conmutación por error. Para obtener más información acerca de cómo ejecutar una instalación de actualización en modo desatendido, vea [Install SQL Server 2014 desde el símbolo del sistema](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md).  
  
####  <a name="Slipstream"></a>Actualizaciones del producto [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] en la instalación  
 Actualización de producto es una característica del programa de instalación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Integra las actualizaciones más recientes del producto con la instalación del producto principal, de modo que este y las actualizaciones aplicables se instalan al mismo tiempo. Actualización del producto puede buscar las actualizaciones aplicables en [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update, Windows Server Update Services (WSUS), una carpeta local o un recurso compartido de red.  Una vez que el programa de instalación encuentra las versiones más recientes de las actualizaciones aplicables, las descarga y las integra con el proceso de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] actual. La actualización del producto puede extraer una actualización acumulativa, un Service Pack o un Service Pack más la actualización acumulativa. La funcionalidad de Actualización de producto es una extensión de la funcionalidad de instalación integrada que estaba disponible en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] PCU1.  
  
## <a name="updating-a-prepared-image-of-includessnoversionincludesssnoversion-mdmd"></a>Actualizar una imagen preparada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Puede aplicar una actualización a una instancia preparada no configurada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sin completar la configuración de la instancia preparada. A continuación se explican distintas formas de aplicar una actualización a una instancia preparada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
-   Actualizar una instancia preparada previamente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
     Las actualizaciones de una instancia preparada se pueden aplicar antes de la configuración. El paquete de actualización detecta que la instancia está en estado preparado y aplica la revisión a la instancia preparada, sin completar la configuración.  
  
-   Actualizar una instancia preparada usando [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update:  
  
     Puede aplicar las actualizaciones a una instancia preparada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a través de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update. El paquete de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update detectará que la instancia está en estado preparado y aplicará la revisión a la instancia preparada, sin completar la configuración.  
  
 Si está actualizando una imagen preparada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], tendrá que especificar el parámetro InstanceID. Para obtener más información y la sintaxis de muestra, vea [Installing Updates from the Command Prompt](../../database-engine/install-windows/installing-updates-from-the-command-prompt.md).  
  
## <a name="updating-a-completed-image-of-includessnoversionincludesssnoversion-mdmd"></a>Actualizar una imagen completada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Al actualizar una instancia completada y configurada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , se siguen los mismos procesos que con cualquier otra instancia instalada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="rebuilding-a-includesscurrentincludessscurrent-mdmd-failover-cluster-node"></a>Volver a generar un nodo de clúster de conmutación por error de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 Si es necesario volver a generar un nodo del clúster de conmutación por error tras aplicar las actualizaciones, lleve a cabo los pasos que se indican a continuación:  
  
1.  Vuelva a generar el nodo en el clúster de conmutación por error. Para obtener más información sobre la reconstrucción de un nodo, vea [Recover from Failover Cluster Instance Failure](../failover-clusters/windows/recover-from-failover-cluster-instance-failure.md).  
  
2.  Ejecute el programa de instalación original de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para instalar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] en el nodo de clúster de conmutación por error.  
  
3.  Ejecute el programa de instalación de las actualizaciones de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] en el nodo que ha agregado.  
  
## <a name="restart-services-and-applications"></a>Reiniciar los servicios y las aplicaciones  
 Una vez finalizado el programa de instalación, es posible que se le pida que reinicie el equipo. Una vez reiniciado el sistema, o cuando el programa de instalación finalice sin solicitar el reinicio, utilice el nodo **Servicios** del Panel de control para reiniciar los servicios que detuvo antes de aplicar las actualizaciones de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Esto incluye servicios como Microsoft DTC (Coordinador de transacciones distribuidas) y [!INCLUDE[msCoName](../../includes/msconame-md.md)] Search, o bien servicios equivalentes específicos de las instancias.  
  
 Reinicie las aplicaciones que cerró antes de ejecutar el programa de instalación de las actualizaciones de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Es recomendable también hacer otra copia de seguridad de las bases de datos `master`, `msdb` y `model` actualizadas, justo después de que finalice correctamente la instalación.  
  
## <a name="uninstalling-updates-from-includesscurrentincludessscurrent-mdmd"></a>Desinstalar actualizaciones de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 Puede desinstalar las actualizaciones acumulativas o los Service Pack de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] desde **Programas y características** en el Panel de control. Para ver la lista de actualizaciones instaladas, abra Actualizaciones instaladas; para ello, haga clic sucesivamente en el botón **Inicio** , **Panel de control**, **Programas**y, después, en **Programas y características**, haga clic en **Ver actualizaciones instaladas**. Cada actualización acumulativa se relaciona de forma separada. Sin embargo, cuando se instala un Service Pack posterior a las actualizaciones acumulativas, las entradas de las actualizaciones se ocultan y solamente estarán disponibles si desinstala el Service Pack.  
  
 Para desinstalar los Service Pack y las actualizaciones, inicie sesión con la actualización o el Service Pack más reciente aplicado a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y vaya hacia atrás. En los siguientes ejemplos, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] termine con la actualización acumulativa 1 después de completar la desinstalación para otros Service Pack o actualizaciones:  
  
-   Para una instancia de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] con la actualización acumulativa 1 y el SP1 instalados, desinstale el SP1.  
  
-   Para una instancia de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] con las actualizaciones acumulativas 1 y 2 y el SP1 instalados, desinstale la actualización acumulativa 2 primero y, a continuación, desinstale el SP1.  
  
## <a name="see-also"></a>Consulte también  
 [Instalación de SQL Server 2014 desde el símbolo del sistema](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)   
 [Instalar actualizaciones de servicio de SQL Server 2014](../../database-engine/install-windows/install-sql-server-servicing-updates.md)   
 [Validar una instalación de SQL Server](../../database-engine/install-windows/validate-a-sql-server-installation.md)   
 [Ver y leer los archivos de registro de instalación de SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
  
