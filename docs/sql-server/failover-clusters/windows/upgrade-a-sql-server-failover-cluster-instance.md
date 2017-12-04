---
title: "Actualizar una instancia de clúster de conmutación por error de SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 10/01/2017
ms.prod: failover-clusters
ms.prod_service: sql-non-specified
ms.service: database-engine
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- upgrading failover clusters
- clusters [SQL Server], upgrading
- failover clustering [SQL Server], upgrading
ms.assetid: daac41fe-7d0b-4f14-84c2-62952ad8cbfa
caps.latest.revision: "47"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: b4cc4c589c9b30d3ae05ec4c273e5376da29dbcd
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="upgrade-a-sql-server-failover-cluster-instance"></a>Actualización de una instancia de clúster de conmutación por error de SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] admite la actualización de un clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a una nueva versión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], a una nueva actualización acumulativa o un nuevo Service Pack de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o, al instalar, a una nueva actualización acumulativa o un nuevo Service Pack de Windows por separado en todos los nodos del clúster de conmutación por error, con tiempo de inactividad limitado a una sola conmutación por error manual (o dos conmutaciones por error manuales si conmuta por recuperación a la base de datos primaria original).  
  
 No se admite la actualización del sistema operativo Windows de un clúster de conmutación por error para sistemas operativos anteriores a [!INCLUDE[winblue-server-2-md](../../../includes/winblue-server-2-md.md)]. Para actualizar un nodo de clúster con [!INCLUDE[winblue-server-2-md](../../../includes/winblue-server-2-md.md)] o superior, vea [Realizar una actualización gradual](#perform-a-rolling-upgrade-or-update).  
  
 Los detalles de compatibilidad son los siguientes:  
  
-   La actualización de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]se puede realizar tanto a través de la interfaz de usuario como desde el símbolo del sistema. Puede ejecutar la actualización desde el símbolo del sistema en cada nodo de clúster de conmutación por error, o usando la IU del programa de instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para actualizar cada nodo de clúster.  Para más información, vea [Actualizar una instancia de clúster de conmutación por error de SQL Server &#40;programa de instalación&#41;](../../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance-setup.md) e [Instalar SQL Server desde el símbolo del sistema](../../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md).  
  
-   Los escenarios siguientes no se admiten como parte de una actualización de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] :  
  
    -   No puede realizar la actualización desde una instancia independiente de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a un clúster de conmutación por error.  
  
    -   No puede agregar características a un clúster de conmutación por error. Por ejemplo, no se puede agregar [!INCLUDE[ssDE](../../../includes/ssde-md.md)] a un clúster de conmutación por error existente de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
    -   No puede degradar un nodo de clúster de conmutación por error a una instancia independiente.  
  
    -   El cambio de edición de los clústeres de conmutación por error está limitado a determinados escenarios. Para obtener información detallada, vea [Actualizaciones de ediciones y versiones admitidas](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md).  
  
-   Durante el proceso de actualización de los clústeres de conmutación por error, el tiempo de inactividad se limita al tiempo de conmutación por error y al tiempo necesario para ejecutar los scripts de actualización. Si sigue el proceso de actualización gradual de clúster de conmutación por error que se muestra a continuación y cumple todos los requisitos previos en todos los nodos antes de comenzar dicho proceso, el tiempo de inactividad es mínimo. Se necesitará un poco más de tiempo a la hora de actualizar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] si se usan tablas optimizadas para memoria. Para obtener más información, consulte [Plan and Test the Database Engine Upgrade Plan](../../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md).  
  
## <a name="prerequisites"></a>Requisitos previos  
 Antes de empezar, revise la siguiente información importante:  
  
-   [Actualizaciones de ediciones y versiones admitidas](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md): compruebe que puede actualizar a [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] desde la versión del sistema operativo Windows y la versión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Por ejemplo, no puede actualizar directamente desde una instancia de clúster de conmutación por error de SQL Server 2005 a [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] ni actualizar un clúster de conmutación por error que se ejecuta en [!INCLUDE[winxpsvr-md](../../../includes/winxpsvr-md.md)].  
  
-   [Choose a Database Engine Upgrade Method](../../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md): seleccione el método y los pasos de actualización adecuados en función de la revisión de versiones admitidas y actualizaciones de ediciones, y también teniendo en cuenta otros componentes instalados en el entorno con el fin de actualizar los componentes en el orden correcto.  
  
-   [Planeamiento y prueba del plan de actualización del motor de base de datos](../../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md): revise las notas de la versión y los problemas conocidos de actualización, la lista de comprobación previa a la actualización y desarrolle y pruebe el plan de actualización.  
  
-   [Requisitos de hardware y software para instalar SQL Server 2016](../../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md): revise los requisitos de software para instalar [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Si es necesario software adicional, puede instalarlo en cada nodo antes de comenzar el proceso de actualización para reducir los posibles tiempos de inactividad.  
  
## <a name="perform-a-rolling-upgrade-or-update"></a>Realizar una actualización gradual  
 Para actualizar un clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], use el programa de instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para actualizar cada nodo de clúster de conmutación por error, uno por uno, comenzando por los nodos pasivos. A medida que se actualiza cada nodo, se excluye de los posibles propietarios del clúster de conmutación por error. Si se produce una conmutación por error inesperada, los nodos actualizados no participan en ella hasta que el programa de instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mueve la propiedad del grupo de recursos del clúster a un nodo actualizado.  
  
 De forma predeterminada, el programa de instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] determina automáticamente cuándo debe realizarse la conmutación por error a un nodo actualizado. Para ello se basa en el número total de nodos de la instancia de los clústeres de conmutación por error y en el número de nodos que ya se han actualizado. Cuando se ha actualizado la mitad de los nodos o más, el programa de instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] realiza una conmutación por error a un nodo actualizado en el momento en que se realiza la actualización en el siguiente nodo. Tras la conmutación por error a un nodo actualizado, el grupo de clústeres se mueve a un nodo actualizado. Todos los nodos actualizados se colocan en la lista de propietarios posibles y todos los nodos que aún no se han actualizado se quitan de la lista. A medida que se actualiza cada uno de los nodos restantes, se agrega a los posibles propietarios de los clústeres de conmutación por error.  
  
 Este proceso da lugar a un tiempo de inactividad limitado a un tiempo de conmutación por error y un tiempo de ejecución de script de actualización de bases de datos durante la actualización completa de los clústeres de conmutación por error.  
  
 Para controlar el comportamiento de la conmutación por error de los nodos en clúster durante el proceso de actualización, ejecute la operación de actualización en el símbolo del sistema y use el parámetro /FAILOVERCLUSTERROLLOWNERSHIP. Para más información, consulte [Instalar SQL Server 2016 desde el símbolo del sistema](../../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md).  
  
## <a name="next-steps"></a>Pasos siguientes  
 [Actualizar SQL Server con el Asistente para instalación &#40;programa de instalación&#41;](../../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)   
 [Instalar SQL Server desde el símbolo del sistema](../../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)   
 [Actualizar una instancia de clúster de conmutación por error de SQL Server &#40;programa de instalación&#41;](../../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance-setup.md)  
  
  
