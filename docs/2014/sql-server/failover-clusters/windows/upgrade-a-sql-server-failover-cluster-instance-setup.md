---
title: Actualizar una instancia de clúster de conmutación por error de SQL Server (programa de instalación) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- upgrading clusters
- clusters [SQL Server], upgrading
- failover clustering [SQL Server], creating clusters
- clusters [SQL Server], creating
- failover clustering [SQL Server], upgrading
ms.assetid: ea8b7d66-e5a1-402f-9928-8f7310e84f5c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d018fb391c7633877f985b4e5e0798bfd803a5fc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62680388"
---
# <a name="upgrade-a-sql-server-failover-cluster-instance-setup"></a>Actualizar una instancia de clúster de conmutación por error de SQL Server (programa de instalación)
  Puede actualizar un clústeres de conmutación por error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a un clústeres de conmutación por error de [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] con el Asistente para la instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o el símbolo del sistema.  
  
 Durante el proceso de actualización de los clústeres de conmutación por error, el tiempo de inactividad se limita al tiempo de conmutación por error y al tiempo necesario para ejecutar los scripts de actualización. Si sigue el proceso de actualización gradual de los clústeres de conmutación por error, observará que el tiempo de inactividad es mínimo. Podría requerirse un tiempo de inactividad adicional para la instalación de todos los requisitos previos de los nodos de clúster de conmutación por error en caso de que no tuviese instalados estos requisitos previos. Para obtener más información sobre cómo minimizar el tiempo de inactividad durante la actualización, consulte el [prácticas recomendadas antes de actualizar conmutación por error de clústeres](#BestPractices) sección de esta página.  
  
 Para obtener más información sobre cómo actualizar, consulte [Supported Version and Edition Upgrades](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md) y [actualizar a SQL Server 2014](../../../database-engine/install-windows/upgrade-sql-server.md).  
  
 Para obtener más información sobre la sintaxis de ejemplo de uso del símbolo del sistema, consulte [instalar SQL Server 2014 desde el símbolo del sistema](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md).  
  
## <a name="prerequisites"></a>Requisitos previos  
 Antes de empezar, revise la siguiente información importante:  
  
-   [Antes de instalar los clústeres de conmutación por error](../install/before-installing-failover-clustering.md)  
  
-   [Utilice el Asesor de actualizaciones para preparar las actualizaciones](../../install/use-upgrade-advisor-to-prepare-for-upgrades.md).  
  
-   [Actualizar el motor de base de datos](../../../database-engine/install-windows/upgrade-database-engine.md)  
  
-   El programa de instalación instala .NET Framework 4.0 en un sistema operativo en clúster. Para reducir al mínimo el tiempo de inactividad, considere instalar .NET Framework 4.0 antes de ejecutar el programa de instalación.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] le exige que instale una actualización para asegurarse de que se puede instalar correctamente el componente de Visual Studio. El programa de instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] comprueba la presencia de esta actualización y, a continuación, le exige que descargue e instale la actualización antes de continuar con la instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para evitar la interrupción durante la instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , puede descargar e instalar la actualización antes de ejecutar el programa de instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , según se describe a continuación (o instalar todas las actualizaciones para .NET 3.5 SP1 disponibles en Windows Update):  
  
     Si instala [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] en un equipo con el sistema operativo Windows Server 2008 SP2, puede obtener la actualización requerida desde [aquí](https://go.microsoft.com/fwlink/?LinkId=198093)  
  
     Si instala [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] en un equipo que tiene el sistema operativo [!INCLUDE[win7](../../../includes/win7-md.md)] SP1 o [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] SP1, esta actualización ya está incluida.  
  
-   El programa de instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ya no instala .NET Framework 3.5 SP1 pero quizá se necesite al instalar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)]. Para más información, consulte las [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)][Notas de la versión](https://go.microsoft.com/fwlink/?LinkId=296445).  
  
-   En las instalaciones locales debe ejecutar el programa de instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como administrador. Si instala [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] desde un recurso compartido remoto, deberá usar una cuenta de dominio que tenga permisos de lectura para dicho recurso.  
  
-   Para actualizar una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a un [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] clúster de conmutación por error, la instancia que se va a actualizar debe ser un clúster de conmutación por error.  
  
     Para mover una instancia independiente de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a un clústeres de conmutación por error de [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)], instale un nuevo clústeres de conmutación por error de [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] y luego migre las bases de datos de usuario desde la instancia independiente con el Asistente para copiar bases de datos. Para más información, consulte [Use the Copy Database Wizard](../../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="rolling-upgrades"></a>Actualizaciones sucesivas  
 Para actualizar un clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)], debe ejecutar el programa de instalación con una acción de actualización en cada nodo de clúster de conmutación por error, de uno en uno, comenzando por los nodos pasivos. A medida que se actualiza cada nodo, se excluye de los posibles propietarios del clúster de conmutación por error. Si se produce una conmutación por error inesperada, los nodos actualizados no participan en ella hasta que el programa de instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mueve la propiedad del grupo de recursos del clúster a un nodo actualizado.  
  
 De forma predeterminada, el programa de instalación determina automáticamente cuándo debe realizarse la conmutación por error a un nodo actualizado. Para ello se basa en el número total de nodos de la instancia de los clústeres de conmutación por error y en el número de nodos que ya se han actualizado. Cuando se ha actualizado la mitad de los nodos o más, el programa de instalación realiza una conmutación por error a un nodo actualizado en el momento en que se realiza la actualización en el siguiente nodo. Tras la conmutación por error a un nodo actualizado, el grupo de clústeres se mueve a un nodo actualizado. Todos los nodos actualizados se colocan en la lista de propietarios posibles y todos los nodos que aún no se han actualizado se quitan de la lista. A medida que se actualiza cada uno de los nodos restantes, se agrega a los posibles propietarios de los clústeres de conmutación por error.  
  
 Este proceso da lugar a un tiempo de inactividad limitado a un tiempo de conmutación por error y un tiempo de ejecución de script de actualización de bases de datos durante la actualización completa de los clústeres de conmutación por error.  
  
 Para controlar el comportamiento de la conmutación por error de los nodos en clúster durante el proceso de actualización, ejecute la operación de actualización en el símbolo del sistema y use el parámetro /FAILOVERCLUSTERROLLOWNERSHIP. Para obtener más información, vea [Instalar SQL Server 2014 desde el símbolo del sistema](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md).  
  
 **Tenga en cuenta** si hay un clúster de conmutación por error de nodo único, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instalación toma la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sin conexión el grupo de recursos.  
  
## <a name="considerations-when-upgrading-from-includessversion2005includesssversion2005-mdmd"></a>Consideraciones al actualizar desde [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]  
 Si especificó grupos de dominio para la directiva de seguridad de clúster, no puede especificar el SID de servicio en [!INCLUDE[nextref_longhorn](../../../includes/nextref-longhorn-md.md)]. Si desea usar el SID de servicio, tendrá que realizar una actualización en paralelo.  
  
 Cuando se selecciona [!INCLUDE[ssDE](../../../includes/ssde-md.md)] para la actualización, se incluye la búsqueda de texto completo en la instalación con independencia de si se instaló en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
 Si se habilitó la búsqueda de texto completo en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], el programa de instalación vuelve a generar el catálogo de búsqueda de texto completo con independencia de las opciones disponibles.  
  
## <a name="upgrading-to-a-includesssql14includessssql14-mdmd-multi-subnet-failover-cluster"></a>Actualización a un clústeres de conmutación por error de varias subredes de [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]  
 Hay dos posibles escenarios para las actualizaciones:  
  
1.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] clúster de conmutación por error está configurado actualmente en una sola subred: Primero debe actualizar el clúster existente a [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] iniciando el programa de instalación y siguiendo el proceso de actualización. Después de completar la actualización del clúster de conmutación por error existente, agregue un nodo que esté en otra subred mediante la funcionalidad AddNode. Confirme el cambio de dependencia de recurso de dirección IP a OR en la página de configuración de red en clúster. Tiene ahora un clústeres de conmutación por error de varias subredes de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
2.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] clúster de conmutación por error está configurado actualmente en varias subredes mediante la tecnología de V-LAN stretch: Primero debe actualizar el clúster existente a [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]. Dado que la tecnología de V-LAN elástica configura una subred única, se debe cambiar la configuración de red a varias subredes, cambiar la dependencia de recurso de dirección IP mediante la herramienta de administración de clúster de conmutación por error de Windows y cambiar la dependencia de IP a OR.  
  
###  <a name="BestPractices"></a> Prácticas recomendadas antes de actualizar un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] clúster de conmutación por error  
 Para eliminar el tiempo de inactividad inesperado debido al reinicio, instale por adelantado el paquete para no reiniciar de .NET Framework 4.0 en todos los nodos de clúster de conmutación por error antes de ejecutar la actualización en los nodos en clúster. Se recomienda seguir estos pasos para instalar por adelantado los requisitos previos:  
  
-   Instale el paquete para no reiniciar de .NET Framework 4.0 y actualice solo los componentes compartidos con los nodos pasivos. De esta forma se instalan los archivos auxiliares de [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 4.0, Windows Installer 4.5 y [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Reinicie las veces que sean necesarias.  
  
-   Realice la conmutación por error a un nodo actualizado.  
  
-   Actualice los componentes compartidos en el último nodo restante.  
  
 Una vez actualizados todos los componentes compartidos y una vez instalados los requisitos previos, inicie el proceso de actualización de los clústeres de conmutación por error. Deberá ejecutar actualizaciones en cada nodo de clúster de conmutación por error, comenzando por los nodos pasivos en primer lugar y dirigiéndose hacia el nodo que posee el grupo de recursos del clúster.  
  
-   No es posible agregar características a un clústeres de conmutación por error existente.  
  
-   El cambio de edición de los clústeres de conmutación por error está limitado a determinados escenarios. Para obtener información detallada, vea [Actualizaciones de ediciones y versiones admitidas](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md).  
  
##  <a name="UpgradeSteps"></a> Para actualizar un clústeres de conmutación por error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
#### <a name="to-upgrade-a-includessnoversionincludesssnoversion-mdmd-failover-cluster"></a>Para actualizar un clústeres de conmutación por error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
1.  Inserte el disco de instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y, en la carpeta raíz, haga doble clic en Setup.exe. Para realizar la instalación desde un recurso compartido de red, vaya a la carpeta raíz de dicho recurso y, a continuación, haga doble clic en Setup.exe. Puede que se le solicite que instale los requisitos previos si no se han instalado previamente.  
  
2.  > [!IMPORTANT]  
    >  Para obtener más información sobre los pasos 3 y 4, consulte el [prácticas recomendadas antes de actualizar conmutación por error de clústeres](#BestPractices) sección.  
  
3.  Una vez instalados los requisitos previos, el Asistente para instalación inicia el Centro de instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para actualizar una instancia existente de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], haga clic en **actualizar desde [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)], o [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)].**  
  
4.  Si son necesarios los archivos auxiliares del programa de instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , el citado programa se encarga de instalarlos. Si se le solicita que reinicie el equipo, hágalo antes de continuar.  
  
5.  El Comprobador de configuración del sistema ejecuta una operación de detección en el equipo. Para continuar, [!INCLUDE[clickOK](../../../includes/clickok-md.md)].  
  
6.  En la página Clave del producto, escriba la clave de PID de la nueva edición de la versión, que debe ser la misma edición que la de la versión anterior del producto. Por ejemplo, para actualizar un clústeres de conmutación por error de Enterprise, debe especificar la clave de PID de [!INCLUDE[ssEnterprise](../../../includes/ssenterprise-md.md)]. Para continuar, haga clic en **Siguiente** . Tenga en cuenta que la clave de PID que use para actualizar los clústeres de conmutación por error debe ser coherente en todos los nodos de clúster de conmutación por error de la misma instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para obtener más información, consulte [ediciones y componentes de SQL Server 2014](../../editions-and-components-of-sql-server-2016.md) y [Supported Version and Edition Upgrades](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md).  
  
7.  En la página Términos de licencia, lea el contrato de licencia y active la casilla para aceptar los términos y condiciones de la licencia. Para ayudar a mejorar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], también puede habilitar la opción de uso de características y enviar informes a [!INCLUDE[msCoName](../../../includes/msconame-md.md)]. Para continuar, haga clic en**Siguiente**. Para salir del programa de instalación, haga clic en **Cancelar**.  
  
8.  En la página Seleccionar instancia, especifique la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que desea a actualizar a [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]. Para continuar, haga clic en**Siguiente**.  
  
9. En la página Selección de características aparecen seleccionadas las características que van a actualizarse. Después de seleccionar el nombre de la característica se muestra una descripción de cada grupo de componentes en el panel derecho. Tenga en cuenta que no puede cambiar las características que se van a actualizar, y no puede agregar características durante la operación de actualización. Para agregar características a una instancia actualizada de [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] una vez completada la operación de actualización, vea [agregar características a una instancia de SQL Server 2014 &#40;instalación&#41;](../../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-setup.md).  
  
     Los requisitos previos para las características seleccionadas se muestran en el recuadro del lado derecho. La instalación de SQL Server instalará los requisitos previos que no se hayan instalado todavía durante el paso de instalación que se describe más adelante en este procedimiento.  
  
10. En la página Configuración de instancia, los campos se rellenan automáticamente con los valores de la instancia anterior. Si lo desea, puede especificar el nuevo valor de InstanceID.  
  
     **Id. de instancia:** de forma predeterminada, el nombre de instancia se usa como identificador de la instancia. Se usa para identificar los directorios de instalación y las claves del Registro para la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Es así en las instancias predeterminadas y en las instancias con nombre. Con una instancia predeterminada, el nombre y el identificador serían MSSQLSERVER. Para utilizar un identificador de instancia no predeterminado, active la casilla **Id. de instancia** y proporcione un valor. Si invalida el valor predeterminado, deberá especificar el mismo identificador de instancia para la instancia que se está actualizando en todos los nodos de clúster de conmutación por error. El identificador de la instancia actualizada debe coincidir en todos los nodos.  
  
     **Características e instancias detectadas** -la cuadrícula muestra las instancias de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que están en el equipo donde se ejecuta el programa de instalación. Para continuar, haga clic en**Siguiente**.  
  
11. La página Requisitos de espacio en disco calcula el espacio en disco necesario para las características especificadas y compara los requisitos con el espacio en disco disponible en el equipo donde se ejecuta el programa de instalación.  
  
12. En la página Actualización de la búsqueda de texto completo, especifique las opciones de actualización para las bases de datos que van a actualizarse. Para obtener más información, vea [Opciones de actualización de búsqueda de texto completo](../../install/full-text-search-upgrade-options.md).  
  
13. En la página **Informes de errores** , especifique la información que desee enviar a [!INCLUDE[msCoName](../../../includes/msconame-md.md)] y que ayudará a mejorar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. De forma predeterminada, se habilitan las opciones de informes de errores.  
  
14. El Comprobador de configuración del sistema ejecuta uno o varios conjuntos de reglas para validar la configuración del equipo con las características de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que ha especificado antes de que comience la operación de actualización.  
  
15. La página Informe de actualización de clúster muestra la lista de nodos de la instancia de los clústeres de conmutación por error y la información de versión de la instancia para los componentes de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de cada nodo. También muestra el estado del script de base de datos y el estado del script de replicación. Además, muestra mensajes informativos sobre lo que ocurrirá al hacer clic en **Siguiente**. Dependiendo del número de nodos de clúster de conmutación por error que ya se han actualizado y del número total de nodos, el programa de instalación muestra el comportamiento de conmutación por error que se produce al hacer clic en **siguiente**. También le advierte del posible tiempo de inactividad innecesario que puede producirse si aún no ha instalado los requisitos previos.  
  
16. La página Listo para actualizar muestra una vista de árbol de las opciones de instalación que se especificaron durante la instalación. Para continuar, haga clic en **Actualizar**. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] El programa de instalación instalará primero los requisitos previos necesarios para las características seleccionadas y a continuación realizará la instalación de características.  
  
17. Durante la actualización, la página Progreso muestra el estado para que pueda supervisar el progreso de la actualización en el nodo actual a medida que se ejecuta el programa de instalación.  
  
18. Tras la actualización del nodo actual, la página Informe de actualización de clúster muestra información sobre el estado de actualización de todos los nodos de clúster de conmutación por error, las características de cada uno de los nodos de clúster de conmutación por error y su información de versión. Confirme la información de versión que se muestra y prosiga con la actualización de los nodos restantes. En la página de estado también se indicará si se ha producido la conmutación por error a los nodos actualizados. También puede comprobarlo en la herramienta Administrador de clústeres de Windows de cara a una confirmación.  
  
19. Después de la actualización, la página Operación completada proporciona un vínculo al archivo de registro de resumen para la instalación y otras notas importantes. Para completar el proceso de instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , haga clic en **Cerrar**.  
  
20. Si el programa indica que se reinicie el equipo, hágalo ahora. Es importante leer el mensaje del Asistente para la instalación tras finalizar el programa de instalación. Para obtener más información sobre los archivos de registro de instalación, vea [Ver y leer los archivos de registro de instalación de SQL Server](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).  
  
21. Para completar el proceso de actualización, repita los pasos 1 a 21 en todos los demás nodos de los clústeres de conmutación por error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="to-upgrade-a-includessnoversionincludesssnoversion-mdmd-multi-subnet-failover-cluster"></a>Para actualizar un clústeres de conmutación por error de varias subredes de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
#### <a name="to-upgrade-to-a-includessnoversionincludesssnoversion-mdmd-multi-subnet-failover-cluster-existing-includessnoversionincludesssnoversion-mdmd-cluster-is-a-non-multi-subnet-cluster"></a>Para actualizar a un clústeres de conmutación por error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (el clúster de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] existente es un clúster no de varias subredes).  
  
1.  Siga los pasos 1 a 24 descritos en el [para actualizar un clúster de conmutación por error de SQL Server](#UpgradeSteps) sección anterior para actualizar el clúster a [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)].  
  
2.  Agregue un nodo en otra subred utilizando la acción AddNode Setup y confirme la dependencia de recurso de dirección IP a OR en la página **Configuración de red en clúster** . Para obtener más información, vea [Agregar o quitar nodos en un clúster de conmutación por error de SQL Server &#40;programa de instalación&#41;](../install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md).  
  
#### <a name="to-upgrade-a-multi-subnet-cluster-currently-using-stretch-v-lan"></a>Para actualizar un clúster de varias subredes que actualmente usa la tecnología de V-Lan elástica.  
  
1.  Siga los pasos 1 a 24 descritos en el [para actualizar un clúster de conmutación por error de SQL Server](#UpgradeSteps) sección anterior para actualizar el clúster a [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
2.  Cambie la configuración de red para mover el nodo remoto a una subred diferente.  
  
3.  Con la herramienta de administración de clústeres de conmutación por error de Windows, agregue una nueva dirección IP para la nueva subred, establezca la dependencia de recurso de dirección IP en OR.  
  
## <a name="next-steps"></a>Pasos siguientes  
 Después de actualizar a [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)], complete las tareas siguientes:  
  
-   Registrar los servidores  
  
     La actualización quita la configuración del Registro de la instancia anterior de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Tras la actualización, debe volver a registrar los servidores.  
  
-   Actualizar estadísticas  
  
     Para ayudar a optimizar el rendimiento de las consultas, es recomendable actualizar las estadísticas de todas las bases de datos tras la actualización. Use el procedimiento almacenado **sp_updatestats** para actualizar las estadísticas de las tablas definidas por el usuario en las bases de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Configurar la nueva instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
     Para reducir el área expuesta de un sistema susceptible de recibir ataques, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instala y habilita de manera selectiva los servicios y características clave. Para obtener más información sobre la configuración del área expuesta, vea el archivo Léame correspondiente a esta versión.  
  
## <a name="see-also"></a>Vea también  
 [Instalar a SQL Server 2014 desde el símbolo del sistema](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)   
 [Ver y leer los archivos de registro de instalación de SQL Server](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
  
