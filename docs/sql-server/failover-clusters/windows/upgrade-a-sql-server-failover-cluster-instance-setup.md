---
title: Actualizar una instancia de clúster de conmutación por error de SQL Server (programa de instalación) | Microsoft Docs
ms.custom: ''
ms.date: 01/22/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: failover-clusters
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- upgrading clusters
- clusters [SQL Server], upgrading
- failover clustering [SQL Server], creating clusters
- clusters [SQL Server], creating
- failover clustering [SQL Server], upgrading
ms.assetid: ea8b7d66-e5a1-402f-9928-8f7310e84f5c
caps.latest.revision: 63
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d7bdf71944c3ac248ab61bb43fc07f2db7bc9eab
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="upgrade-a-sql-server-failover-cluster-instance-setup"></a>Actualizar una instancia de clúster de conmutación por error de SQL Server (programa de instalación)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Puede actualizar un clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a un clúster de conmutación por error de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] con la interfaz de usuario de configuración de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o desde un símbolo del sistema.  
  
 En las instalaciones locales debe ejecutar el programa de instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como administrador. Si instala [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] desde un recurso compartido remoto, deberá usar una cuenta de dominio que tenga permisos de lectura para dicho recurso.  
  
 Antes de actualizar, vea [Actualizar una instancia del clúster de conmutación por error de SQL Server](../../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance.md).  
  
##  <a name="UpgradeSteps"></a> Para actualizar un clústeres de conmutación por error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
#### <a name="to-upgrade-a-includessnoversionincludesssnoversion-mdmd-failover-cluster"></a>Para actualizar un clústeres de conmutación por error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
1.  Desde el medio de instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para la edición que coincide con la edición que actualiza, haga doble clic en setup.exe en la carpeta raíz. Puede que se le solicite que instale los requisitos previos si no se han instalado previamente.  
  
2.  Una vez instalados los requisitos previos, el Asistente para instalación inicia el Centro de instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para actualizar una instancia existente de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], seleccione la instancia.  
  
3.  Si son necesarios los archivos auxiliares del programa de instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , el citado programa de instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se encarga de instalarlos. Si se le solicita que reinicie el equipo, hágalo antes de continuar.  
  
4.  El Comprobador de configuración del sistema ejecuta una operación de detección en el equipo. Para continuar, [!INCLUDE[clickOK](../../../includes/clickok-md.md)].  
  
5.  En la página Clave del producto, escriba la clave de PID de la nueva edición de la versión, que debe ser la misma edición que la de la versión anterior del producto. Por ejemplo, para actualizar un clústeres de conmutación por error de Enterprise, debe especificar la clave de PID de [!INCLUDE[ssEnterprise](../../../includes/ssenterprise-md.md)]. Para continuar, haga clic en **Siguiente** . Tenga en cuenta que la clave de PID que use para actualizar los clústeres de conmutación por error debe ser coherente en todos los nodos de clúster de conmutación por error de la misma instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
6.  En la página Términos de licencia, lea el contrato de licencia y active la casilla para aceptar los términos y condiciones de la licencia. Para ayudar a mejorar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], también puede habilitar la opción de uso de características y enviar informes a [!INCLUDE[msCoName](../../../includes/msconame-md.md)]. Para continuar, haga clic en**Siguiente**. Para salir del programa de instalación, haga clic en **Cancelar**.  
  
7.  En la página Seleccionar instancia, especifique la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que desea a actualizar a [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Para continuar, haga clic en**Siguiente**.  
  
8.  En la página Selección de características aparecen seleccionadas las características que van a actualizarse. Después de seleccionar el nombre de la característica se muestra una descripción de cada grupo de componentes en el panel derecho. Tenga en cuenta que no puede cambiar las características que se van a actualizar, y no puede agregar características durante la operación de actualización. Para agregar características a una instancia actualizada de [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] una vez completada la operación de actualización, vea [Agregar características a una instancia de SQL Server 2016 &#40;programa de instalación&#41;](../../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md).  
  
     Los requisitos previos para las características seleccionadas se muestran en el recuadro del lado derecho. La instalación de SQL Server instalará los requisitos previos que no se hayan instalado todavía durante el paso de instalación que se describe más adelante en este procedimiento. Para ahorrar tiempo, debe instalar previamente estos requisitos previos en cada nodo.  
  
9. En la página Configuración de instancia, los campos se rellenan automáticamente con los valores de la instancia anterior. Si lo desea, puede especificar el nuevo valor de InstanceID.  
  
     **Id. de instancia:** de forma predeterminada, el nombre de instancia se usa como identificador de la instancia. Se usa para identificar los directorios de instalación y las claves del Registro para la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Es así en las instancias predeterminadas y en las instancias con nombre. Con una instancia predeterminada, el nombre y el identificador serían MSSQLSERVER. Para utilizar un identificador de instancia no predeterminado, active la casilla **Id. de instancia** y proporcione un valor. Si invalida el valor predeterminado, deberá especificar el mismo identificador de instancia para la instancia que se está actualizando en todos los nodos de clúster de conmutación por error. El identificador de la instancia actualizada debe coincidir en todos los nodos.  
  
     **Características e instancias detectadas:** la cuadrícula muestra las instancias de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hay en el equipo en el que se ejecuta el programa de instalación. Para continuar, haga clic en**Siguiente**.  
  
10. La página Requisitos de espacio en disco calcula el espacio en disco necesario para las características especificadas y compara los requisitos con el espacio en disco disponible en el equipo donde se ejecuta el programa de instalación.  
  
11. En la página Actualización de la búsqueda de texto completo, especifique las opciones de actualización para las bases de datos que van a actualizarse. Para obtener más información, vea [Opciones de actualización de búsqueda de texto completo](http://msdn.microsoft.com/library/16c9376b-5fbb-4495-a429-06a2493849c9).  
  
12. En la página **Informes de errores** , especifique la información que desee enviar a [!INCLUDE[msCoName](../../../includes/msconame-md.md)] y que ayudará a mejorar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. De forma predeterminada, se habilitan las opciones de informes de errores.  
  
13. El Comprobador de configuración del sistema ejecuta uno o varios conjuntos de reglas para validar la configuración del equipo con las características de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que ha especificado antes de que comience la operación de actualización.  
  
14. La página Informe de actualización de clúster muestra la lista de nodos de la instancia de los clústeres de conmutación por error y la información de versión de la instancia para los componentes de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de cada nodo. También muestra el estado del script de base de datos y el estado del script de replicación. Además, muestra mensajes informativos sobre lo que ocurrirá al hacer clic en **Siguiente**. En función del número de nodos de clúster de conmutación por error que se han actualizado y del número total de nodos, el programa de instalación muestra el comportamiento de conmutación por error que tiene lugar cuando se hace clic en **Siguiente**. También le advierte del posible tiempo de inactividad innecesario que puede producirse si aún no ha instalado los requisitos previos.  
  
15. La página Listo para actualizar muestra una vista de árbol de las opciones de instalación que se especificaron durante la instalación. Para continuar, haga clic en **Actualizar**. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] El programa de instalación instalará primero los requisitos previos necesarios para las características seleccionadas y a continuación realizará la instalación de características.  
  
16. Durante la actualización, la página Progreso muestra el estado para que pueda supervisar el progreso de la actualización en el nodo actual a medida que se ejecuta el programa de instalación.  
  
17. Tras la actualización del nodo actual, la página Informe de actualización de clúster muestra información sobre el estado de actualización de todos los nodos de clúster de conmutación por error, las características de cada uno de los nodos de clúster de conmutación por error y su información de versión. Confirme la información de versión que se muestra y prosiga con la actualización de los nodos restantes. En la página de estado también se indicará si se ha producido la conmutación por error a los nodos actualizados. También puede comprobarlo en la herramienta Administrador de clústeres de Windows de cara a una confirmación.  
  
18. Después de la actualización, la página Operación completada proporciona un vínculo al archivo de registro de resumen para la instalación y otras notas importantes. Para completar el proceso de instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , haga clic en **Cerrar**.  
  
19. Si el programa indica que se reinicie el equipo, hágalo ahora. Es importante leer el mensaje del Asistente para la instalación tras finalizar el programa de instalación. Para obtener más información sobre los archivos de registro de instalación, vea [Ver y leer los archivos de registro de instalación de SQL Server](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).  
  
20. Para completar el proceso de actualización, repita estos pasos en todos los demás nodos del clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="to-upgrade-a-includessnoversionincludesssnoversion-mdmd-multi-subnet-failover-cluster"></a>Para actualizar un clústeres de conmutación por error de varias subredes de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
#### <a name="to-upgrade-to-a-includessnoversionincludesssnoversion-mdmd-multi-subnet-failover-cluster-existing-includessnoversionincludesssnoversion-mdmd-cluster-is-a-non-multi-subnet-cluster"></a>Para actualizar a un clústeres de conmutación por error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (el clúster de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] existente es un clúster no de varias subredes).  
  
1.  Siga los pasos anteriores para actualizar el clúster a [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
2.  Agregue un nodo en otra subred utilizando la acción AddNode Setup y confirme la dependencia de recurso de dirección IP a OR en la página **Configuración de red en clúster** . Para obtener más información, vea [Agregar o quitar nodos en un clúster de conmutación por error de SQL Server &#40;programa de instalación&#41;](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md).  
  
#### <a name="to-upgrade-a-multi-subnet-cluster-currently-using-stretch-v-lan"></a>Para actualizar un clúster de varias subredes que actualmente usa la tecnología de V-Lan elástica.  
  
1.  Siga los pasos anteriores para actualizar el clúster a [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
2.  Cambie la configuración de red para mover el nodo remoto a una subred diferente.  
  
3.  Con la herramienta de administración de clústeres de conmutación por error de Windows, agregue una nueva dirección IP para la nueva subred, establezca la dependencia de recurso de dirección IP en OR.  
  
## <a name="next-steps"></a>Next Steps  
 Después de actualizar a [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], complete las tareas siguientes:  
  
-   [Completar la actualización motor de base de datos](../../../database-engine/install-windows/complete-the-database-engine-upgrade.md)  
  
-   [Cambiar el modo de compatibilidad de la base de datos y usar el almacén de consultas](../../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md)  
  
-   [Aprovechamiento de las nuevas características de SQL Server 2016](http://msdn.microsoft.com/library/d8879659-8efa-4442-bcbb-91272647ae16)  
  
## <a name="see-also"></a>Ver también  
 [Actualizar una instancia del clúster de conmutación por error de SQL Server](../../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance.md)   
 [Ver y leer los archivos de registro de instalación de SQL Server](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)   
 [Agregar características a una instancia de SQL Server 2016 &#40;programa de instalación&#41;](../../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md)  
  
  
