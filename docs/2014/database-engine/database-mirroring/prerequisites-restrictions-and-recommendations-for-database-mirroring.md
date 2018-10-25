---
title: Requisitos previos, restricciones y recomendaciones para la creación de reflejo de la base de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], deployment
- partners [SQL Server]
- database mirroring [SQL Server], prerequisites
- database mirroring [SQL Server], recommendations
- database mirroring [SQL Server], restrictions
- database mirroring [SQL Server], planning
- database mirroring [SQL Server], about database mirroring
ms.assetid: fdcf2251-9895-44c6-b81e-768fef32e732
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 9763385093db6e649e60ab7a6be74f8f28466e1d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48164795"
---
# <a name="prerequisites-restrictions-and-recommendations-for-database-mirroring"></a>Requisitos previos, restricciones y recomendaciones para la creación de reflejo de la base de datos
    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] en su lugar.  
  
 En este tema se describen los requisitos previos y las recomendaciones para configurar la creación de reflejo de la base de datos. Para obtener una introducción a la creación de reflejo de la base de datos, vea [Creación de reflejo de la base de datos &#40;SQL Server&#41;](database-mirroring-sql-server.md).  
  
> [!NOTE]  
>  El formato de almacenamiento en disco de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es el mismo en los entornos de 64 bits y 32 bits. Por lo tanto, una sesión de creación de reflejo de la base de datos puede combinar instancias del servidor que se ejecuten en entornos de 32 bits e instancias del servidor que se ejecuten en entornos de 64 bits.  
  

  
##  <a name="DbmSupport"></a> Compatibilidad con la creación de reflejo de la base de datos  
 Para más información sobre la compatibilidad con la creación de reflejo de la base de datos en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], vea [Características compatibles con las ediciones de SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
 Tenga en cuenta que la creación de reflejo de la base de datos funciona con cualquier nivel de compatibilidad de base de datos. Para obtener información sobre los niveles de compatibilidad admitidos, vea [Nivel de compatibilidad de ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).  
  

  
##  <a name="Prerequisites"></a> Requisitos previos  
  
-   Para establecer una sesión de creación de reflejo, los asociados y el testigo, si los hay, deben estar en ejecución en la misma versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Los dos asociados, el servidor principal y el servidor reflejado, deben ejecutar la misma edición de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El testigo, si existe, puede ejecutarse en cualquier edición de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que admita la creación de reflejo de la base de datos.  
  
    > [!NOTE]  
    >  Puede actualizar las instancias del servidor que sean asociados en una sesión de creación de reflejo a una versión más reciente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para más información, consulte [Minimizar el tiempo de inactividad de las bases de datos reflejadas al actualizar instancias de servidor](upgrading-mirrored-instances.md).  
  
-   La base de datos debe usar el modelo de recuperación completa. Los modelos de recuperación simple y de recuperación optimizado para cargas masivas de registros no admiten la creación de reflejo de la base de datos. Por tanto, las operaciones masivas siempre se registran completamente para una base de datos reflejada. Para obtener información sobre los modelos de recuperación, vea [Modelos de recuperación &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md).  
  
-   Compruebe que el servidor reflejado tenga suficiente espacio en disco para la base de datos reflejada.  
  
    > [!NOTE]  
    >  Para obtener información sobre cómo usar la creación de reflejo de base de datos en una base de datos replicada, vea [Replicación y creación de reflejo de la base de datos &#40;SQL Server&#41;](database-mirroring-and-replication-sql-server.md).  
  
-   Al crear la base de datos reflejada en el servidor reflejado, asegúrese de restaurar la copia de seguridad de la base de datos principal especificando la misma base de datos con la opción WITH NORECOVERY. Además, todas las copias de seguridad de registros creadas después de realizar esa copia de seguridad deben aplicarse de nuevo con WITH NORECOVERY.  
  
    > [!IMPORTANT]  
    >  Si la creación de reflejo de la base de datos se ha detenido, para poder reiniciarla, cualquier copia de seguridad de registros posterior que se realice en la base de datos principal se debe aplicar a la base de datos reflejada.  
  

  
##  <a name="Restrictions"></a> Restricciones  
  
-   Solo se pueden reflejar las bases de datos de usuario. No es posible reflejar las bases de datos **maestra**, **msdb**, **tempdb**o **model** .  
  
-   No se puede cambiar el nombre de una base de datos reflejada durante una sesión de creación de reflejo de la base de datos.  
  
-   La creación de reflejo de la base de datos no es compatible con FILESTREAM. No se puede crear un grupo de archivos FILESTREAM en el servidor principal. La creación de reflejo de la base de datos no puede configurarse para una base de datos que contiene grupos de archivos FILESTREAM.  
  
-   En un sistema de 32 bits, la creación de reflejo de la base de datos puede admitir un máximo de 10 bases de datos por instancia de servidor debido a los números de subproceso de trabajo consumidos por cada sesión de creación de reflejo de la base de datos.  
  
-   La creación de reflejo de la base de datos no está admitida con transacciones entre bases de datos o transacciones distribuidas. Para más información, vea [Transacciones entre bases de datos no compatibles para la creación de reflejo de la base de datos o grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md).  
  

  
##  <a name="RecommendationsForPartners"></a> Recomendaciones para configurar servidores asociados  
  
-   Los servidores asociados deben ejecutarse en sistemas comparables que puedan manejar cargas de trabajo idénticas.  
  
    > [!NOTE]  
    >  Si piensa usar el modo de alta seguridad con conmutación automática por error, la carga normal de cada uno de los servidores asociados de conmutación por error debe usar la CPU en un porcentaje menor del 50 por ciento. Si se sobrecarga la CPU, un servidor asociado de conmutación por error podría ser incapaz de hacer ping a las otras instancias de servidor en la sesión de creación de reflejo. Esto produce una conmutación por error innecesaria. Si no puede mantener el uso de la CPU por debajo del 50 por ciento, se recomienda usar el modo de alta seguridad sin conmutación automática por error o el modo de alto rendimiento.  
  
-   Si es posible, la ruta de acceso (incluida la letra de unidad) de la base de datos reflejada debería ser idéntica a la de la base de datos principal. Debe incluir la opción MOVE en la instrucción RESTORE si los diseños de archivo deben ser distintos. Por ejemplo, si la base de datos principal está en unidad 'F:' y en el sistema reflejado no existe la unidad F:.  
  
    > [!IMPORTANT]  
    >  Si mueve los archivos de la base de datos al crear la base de datos reflejada, es posible que no pueda agregar archivos a la base de datos posteriormente sin que se tenga que suspender la creación de reflejo.  
  
-   Todas las instancias de servidor de una sesión reflejada deberían usar la misma intercalación y página de códigos principal. Las diferencias pueden causar un problema durante la configuración de la creación de reflejo.  
  
-   Otra opción sería calcular el tiempo para la conmutación por error en una base de datos para asegurarse de que la configuración del sistema ofrecerá el rendimiento necesario. Para obtener más información, vea [Calcular la interrupción del servicio durante la conmutación de roles &#40;creación de reflejo de la base de datos&#41;](estimate-the-interruption-of-service-during-role-switching-database-mirroring.md).  
  
-   Para obtener el mejor rendimiento, utilice un adaptador de red (tarjeta de interfaz de red) dedicado para la creación de reflejo.  
  
-   No hay ninguna recomendación acerca de si una red de área extensa (WAN) es lo suficientemente confiable para la creación de reflejo de la base de datos en modo de alta seguridad. Si decide usar el modo de alta seguridad en una WAN, tenga cuidado al agregar un testigo a la sesión, ya que se pueden producir conmutaciones automáticas por error no deseadas. Para obtener más información, vea [Recomendaciones para implementar la creación de reflejo de la base de datos](#RecommendationsForDeploying)más adelante en este tema.  
  

  
##  <a name="RecommendationsForDeploying"></a> Recomendaciones para implementar la creación de reflejo de la base de datos  
 El rendimiento óptimo de la creación de reflejo de la base de datos se obtiene mediante el funcionamiento asincrónico. Una sesión de creación de reflejo que utiliza el funcionamiento sincrónico puede disminuir el rendimiento cuando su carga de trabajo genera grandes cantidades de datos del registro de transacciones.  
  
 En entornos de prueba, es adecuado explorar todos los modos de funcionamiento para evaluar la forma en que tiene lugar la creación de reflejo de la base de datos. Sin embargo, antes de implementar la creación de reflejo en un entorno de producción, asegúrese de que comprende cómo funciona red en la realidad.  
  
 El modo de alta seguridad con conmutación automática por error está diseñado para una red con un servicio elevado y una conexión dedicada, o bien para una configuración de red bastante sencilla que minimice los orígenes de posibles errores de red. Dicho entorno de red de alta calidad es necesario para el modo de alta seguridad con conmutación automática por error y es recomendable en todas las sesiones de creación de reflejo de la base de datos. Sin embargo, la confiabilidad de la red afecta mucho menos a los modos de alto rendimiento y de alta seguridad sin conmutación automática por error.  
  
 Por tanto, para entornos de producción, se recomienda que siga estas directrices de implementación:  
  
1.  Comience ejecutando en el modo de alto rendimiento asincrónico. Este modo es el menos sensible al entorno de red y proporciona la mejor configuración para explorar la forma en que funciona la creación de reflejo. Se recomienda ejecutar el sistema de manera asincrónica hasta que esté seguro de que el ancho de banda admite la creación de reflejo y ha desarrollado conocimientos de la configuración de la creación de reflejo y del rendimiento del modo asincrónico en el entorno. Para más información, consulte [Database Mirroring Operating Modes](database-mirroring-operating-modes.md).  
  
    > [!IMPORTANT]  
    >  A través de las pruebas, se recomienda controlar las sesiones en busca de errores de red que impidan la creación de reflejo de la base de datos. Para obtener más información acerca de los posibles orígenes de errores, vea [Possible Failures During Database Mirroring](possible-failures-during-database-mirroring.md). Para obtener información sobre cómo supervisar la creación de reflejo de la base de datos, vea [Supervisar la creación de reflejo de la base de datos &#40;SQL Server&#41;](monitoring-database-mirroring-sql-server.md).  
  
2.  Cuando esté seguro de que el funcionamiento asincrónico cumple las necesidades empresariales, puede que desee intentar el funcionamiento sincrónico para mejorar la protección de datos. Cuando pruebe la manera en que funciona la creación de reflejo sincrónica en el entorno, se recomienda probar primero el modo de alta seguridad sin conmutación automática por error. El fin principal de esta prueba es comprobar cómo afecta el funcionamiento sincrónico al rendimiento de la base de datos. Para más información, consulte [Database Mirroring Operating Modes](database-mirroring-operating-modes.md).  
  
3.  Espere a habilitar la conmutación automática por error hasta que tenga la seguridad de que el modo de alta seguridad sin conmutación automática por error cumple las necesidades empresariales y que los errores de red no están ocasionando problemas. Para obtener más información, vea [Conmutación de roles durante una sesión de creación de reflejo de la base de datos &#40;SQL Server&#41;](role-switching-during-a-database-mirroring-session-sql-server.md).  
  

  
## <a name="see-also"></a>Vea también  
 [Configurar la creación de reflejo de la base de datos &#40;SQL Server&#41;](setting-up-database-mirroring-sql-server.md)   
 [Seguridad de transporte para la creación de reflejo de base de datos y grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](transport-security-database-mirroring-always-on-availability.md)   
 [Creación de reflejo de la base de datos &#40;SQL Server&#41;](database-mirroring-sql-server.md)   
 [Solucionar problemas de configuración de creación de reflejo de la base de datos &#40;SQL Server&#41;](troubleshoot-database-mirroring-configuration-sql-server.md)  
  
  
