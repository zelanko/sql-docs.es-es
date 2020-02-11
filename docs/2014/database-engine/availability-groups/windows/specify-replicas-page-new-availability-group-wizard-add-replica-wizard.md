---
title: Especificar la página de réplicas (Asistente para nuevo grupo de disponibilidad/Asistente para agregar réplica) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.newagwizard.listeners.f1
- sql12.swb.newagwizard.specifyreplicas.f1
- sql12.swb.addreplicawizard.specifyreplicas.f1
ms.assetid: 2d90fc12-a67b-4bd0-b0ab-899b73017196
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2a552b5847f1abda254da1d6c7348088ee0e8a03
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "76923039"
---
# <a name="specify-replicas-page-new-availability-group-wizard-add-replica-wizard"></a>Especificar la página de réplicas (Asistente para nuevo grupo de disponibilidad/Asistente para agregar réplica)
  En este tema se describen las opciones de la página **Especificar réplicas** . Esta página se aplica a [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)] y a [!INCLUDE[ssAoAddRepWiz](../../../includes/ssaoaddrepwiz-md.md)] de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Use la página **Especificar réplicas** para especificar y configurar una o varias réplicas de disponibilidad para agregar al grupo de disponibilidad. Esta página contiene cuatro pestañas, que se presentan en la tabla siguiente. Haga clic en el nombre de una pestaña de la tabla para ir a la sección correspondiente, más adelante en este tema.  
  
|Pestaña|Breve descripción|  
|---------|-----------------------|  
|[Réplicas](#ReplicasTab)|Utilice esta pestaña para especificar cada instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospedará u hospeda actualmente una réplica secundaria. Tenga en cuenta que la instancia de servidor a la que está conectado actualmente debe hospedar la réplica principal.<br /><br /> Sugerencia: Termine de especificar todas las réplicas en la pestaña **Réplicas** antes de iniciar las demás pestañas.|  
|[Extremos](#EndpointsTab)|Utilice esta pestaña para comprobar los extremos de creación de reflejo de base de datos existentes y también, si este extremo falta en una instancia de servidor cuyas cuentas de servicio utilizan la autenticación de Windows, para crear el extremo automáticamente.|  
|[Preferencias de copia de seguridad](#BackupPreferencesTab)|Utilice esta pestaña para especificar sus preferencias de copias de seguridad para el grupo de disponibilidad en conjunto y las prioridades de copias de seguridad para las réplicas de disponibilidad individuales.|  
|[Agente de escucha](#Listener)|Utilice esta pestaña, si está disponible, para crear un agente de escucha del grupo de disponibilidad. De forma predeterminada, no se crea un agente de escucha.<br /><br /> Nota: Esta pestaña está disponible solo si se ejecuta [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)].|  
  
##  <a name="ReplicasTab"></a>Pestaña réplicas  
 **Instancia del servidor**  
 Muestra el nombre de la instancia del servidor que hospedará la réplica de disponibilidad.  
  
 Si una instancia de servidor que se usa para hospedar una réplica secundaria no aparece en la cuadrícula **Réplicas de disponibilidad** , haga clic en el botón **Agregar réplica** . Si configura un grupo de disponibilidad en un entorno de tecnologías de la información híbrido (consulte [Alta disponibilidad y recuperación ante desastres para SQL Server en Azure Virtual Machines](https://msdn.microsoft.com/library/windowsazure/jj870962.aspx)), puede hacer clic en el botón **Agregar réplica de Azure** para crear máquinas virtuales con réplicas secundarias en Azure.  
  
 **Rol inicial**  
 Indica el rol que la nueva réplica realizará inicialmente: **Principal** o **Secundario**.  
  
 **Conmutación automática por error (hasta 2)**  
 Active esta casilla solo si desea que esta réplica de disponibilidad sea un asociado de conmutación por error automática. Para configurar la conmutación por error automática, debe elegir esta opción para la réplica principal inicial y para una réplica secundaria. Estas dos réplicas utilizarán el modo de disponibilidad de confirmación sincrónica. Solo dos réplicas pueden admitir la conmutación por error automática.  
  
 Para obtener información sobre el modo de disponibilidad de confirmación sincrónica, vea [modos de disponibilidad (grupos de disponibilidad AlwaysOn)](availability-modes-always-on-availability-groups.md). Para obtener información sobre la conmutación por error automática, vea [Conmutación por error y modos de conmutación por error &#40;grupos de disponibilidad AlwaysOn&#41;](failover-and-failover-modes-always-on-availability-groups.md).  
  
 **Confirmación sincrónica (hasta 3)**  
 Si ha seleccionado **Conmutación por error automática (hasta 2)** para la réplica, también se selecciona **Confirmación sincrónica (hasta 3)** . Si la casilla está en blanco, selecciónela solo si desea que esta réplica utilice el modo de confirmación sincrónica con solo la conmutación por error manual planeada. Solo tres réplicas pueden utilizar el modo de confirmación sincrónica.  
  
 Si desea que esta réplica utilice el modo de disponibilidad de confirmación asincrónica, deje en blanco esta casilla. La réplica solo admitirá la conmutación por error manual forzada (con posible pérdida de datos). Para obtener información sobre el modo de disponibilidad de confirmación asincrónica, vea [modos de disponibilidad (grupos de disponibilidad AlwaysOn)](availability-modes-always-on-availability-groups.md). Para obtener información sobre la conmutación por error manual planeada y la conmutación por error manual forzada, vea [Conmutación por error y modos de conmutación por error &#40;grupos de disponibilidad AlwaysOn&#41;](failover-and-failover-modes-always-on-availability-groups.md).  
  
 **Rol secundario legible**  
 Seleccione un valor en la lista desplegable **Secundario legible** del siguiente modo:  
  
 **No**  
 No se permiten conexiones directas a las bases de datos secundarias de esta réplica. No están disponibles para acceso de lectura. Esta es la configuración predeterminada.  
  
 **Solo intento de lectura**  
 Únicamente se permiten conexiones directas de solo lectura a las bases de datos secundarias de esta réplica. Todas las bases de datos secundarias están disponibles para acceso de lectura.  
  
 **Sí**  
 Se permiten todas las conexiones a las bases de datos secundarias de esta réplica, pero solo para acceso de lectura. Todas las bases de datos secundarias están disponibles para acceso de lectura.  
  
 **Agregar réplica**  
 Haga clic para agregar una réplica secundaria al grupo de disponibilidad.  
  
 **Agregar réplica de Azure**  
 Haga clic para crear una máquina virtual de Azure que ejecute una réplica secundaria en el grupo de disponibilidad. Esta opción solo se aplica a un grupo de disponibilidad en tecnologías de la información híbridas que contienen réplicas locales. Para obtener más información, consulte [alta disponibilidad y recuperación ante desastres para SQL Server en Azure virtual machines](https://msdn.microsoft.com/library/windowsazure/jj870962.aspx).  
  
 **Quitar réplica**  
 Haga clic para quitar la réplica secundaria seleccionada del grupo de disponibilidad.  
  
##  <a name="EndpointsTab"></a>Pestaña extremos  
 Para cada instancia del servidor que hospedará una réplica de disponibilidad, la pestaña **Extremos** muestra los valores reales del extremo de creación de reflejo de la base de datos existente, en su caso, o los valores sugeridos para un nuevo extremo posible que utilizaría la Autenticación de Windows. Tanto para los extremos existentes como para los posibles, la cuadrícula Valores de extremo muestra la información siguiente:  
  
 **Nombre del servidor**  
 Muestra el nombre de una instancia del servidor que hospedará una réplica de disponibilidad.  
  
 **Dirección URL del extremo**  
 Muestra la dirección URL real o propuesta del extremo de creación de reflejo de la base de datos. En el caso de un nuevo extremo propuesto, puede cambiar este valor. Para obtener más información sobre el formato de estas direcciones URL, vea [Especificar la dirección URL del punto de conexión al agregar o modificar una réplica de disponibilidad &#40;SQL Server&#41;](specify-endpoint-url-adding-or-modifying-availability-replica.md).  
  
 **Número de puerto**  
 Muestra el número de puerto real o propuesto del extremo. En el caso de un nuevo extremo propuesto, puede cambiar este valor.  
  
 **Nombre del punto de conexión**  
 Muestra el nombre real o propuesto del extremo. En el caso de un nuevo extremo propuesto, puede cambiar este valor.  
  
 **Cifrar datos**  
 Indica si los datos enviados a través de este extremo están cifrados. En el caso de un nuevo extremo propuesto, puede cambiar este valor.  
  
 **SQL Server cuenta de servicio**  
 Nombre de usuario de la cuenta de servicio de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 Para que una instancia del servidor use un extremo que utilice la Autenticación de Windows, la cuenta de servicio de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] debe ser una cuenta de dominio.  
  
 Este requisito determina el siguiente paso de configuración, del modo siguiente:  
  
-   Si cada instancia del servidor se ejecuta con una cuenta de servicio de dominio, es decir, si la columna **Cuenta de servicio de SQL Server** muestra una cuenta de servicio de dominio para cada instancia del servidor, haga clic en **Siguiente**.  
  
-   Si una instancia del servidor se ejecuta con una cuenta de servicio que no es de dominio, se debe realizar un cambio manual en la instancia del servidor antes de continuar con el asistente. En este caso, al hacer clic en **siguiente** se abre un cuadro de diálogo de advertencia; debe hacer clic en **no**, lo que le devolverá a la pestaña**extremos** . Mientras sale del asistente en la página **especificar réplicas** , realice uno de los siguientes cambios en cada instancia del servidor para la que la columna **cuenta de servicio de SQL Server** muestra una cuenta de servicio que no es de dominio, ya sea:  
  
    -   Usar el Administrador de configuración de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para cambiar la cuenta de servicio de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a una cuenta de dominio. Para obtener más información, vea [Cambiar la cuenta de inicio del servicio para SQL Server &#40;Administrador de configuración de SQL Server&#41;](../../configure-windows/scm-services-change-the-service-startup-account.md).  
  
    -   Use [!INCLUDE[tsql](../../../includes/tsql-md.md)] o PowerShell para crear manualmente un extremo de creación de reflejo de la base de datos que use un certificado. Para más información, vea [CREATE ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-endpoint-transact-sql) o [Crear un punto de conexión de creación de reflejo de la base de datos para grupos de disponibilidad AlwaysOn &#40;SQL Server PowerShell&#41;](database-mirroring-always-on-availability-groups-powershell.md).  
  
     Si deja la página **Especificar réplicas de disponibilidad** abierta mientras configura los extremos, vuelva a la pestaña **Extremos** y haga clic en **Actualizar** para actualizar la cuadrícula **Valores de extremo** .  
  
##  <a name="BackupPreferencesTab"></a>Pestaña Preferencias de copia de seguridad  
 Para especificar dónde deben producirse las copias de seguridad, elija una de las opciones siguientes:  
  
 **Preferir secundaria**  
 Especifica que las copias de seguridad se deben realizar en una réplica secundaria a menos que la réplica principal sea la única réplica en línea. En ese caso, la copia de seguridad se debe realizar en la réplica principal. Ésta es la opción predeterminada.  
  
 **Solo secundaria**  
 Especifica que las copias de seguridad no deben realizarse nunca en la réplica principal. Si la réplica principal es la única réplica en línea, no se debe realizar la copia de seguridad.  
  
 **Principal**  
 Especifica que las copias de seguridad deben realizarse siempre en la réplica principal. Esta opción es útil si necesita usar características de copia de seguridad, como crear copias de seguridad diferenciales, que no se admiten cuando la copia de seguridad se ejecuta en una réplica secundaria.  
  
 **Cualquier réplica**  
 Especifica que, de acuerdo con sus preferencias, los trabajos de copia de seguridad omitan el rol de las réplicas de disponibilidad cuando la réplica realiza copias de seguridad. Tenga en cuenta que los trabajos de copia de seguridad pueden evaluar otros factores, como la prioridad de copia de seguridad de cada réplica de disponibilidad junto con su estado operativo y de conexión.  
  
> [!IMPORTANT]  
>  No se aplica el valor de preferencia de copia de seguridad. La interpretación de esta preferencia depende de la lógica, si existe, del script con los trabajos de copia de seguridad ejecutado para las bases de datos de un grupo de disponibilidad dado. Para obtener más información, vea [secundarias activas: copia de seguridad en las réplicas secundarias (grupos de disponibilidad AlwaysOn)](active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md).  
  
### <a name="replica-backup-priorities-grid"></a>Cuadrícula de prioridades de copia de seguridad de réplica  
 Use la cuadrícula **Prioridades de copia de seguridad de réplica** para especificar sus prioridades de copia de seguridad para cada una de las réplicas del grupo de disponibilidad. Esta cuadrícula contiene las columnas siguientes:  
  
 **Instancia del servidor**  
 Muestra el nombre de la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospeda la réplica de disponibilidad.  
  
 **Prioridad de copia de seguridad (Mínima=1, Máxima=100)**  
 Asigne la prioridad para realizar copias de seguridad en esta réplica en relación con las otras réplicas del mismo grupo de disponibilidad. El valor predeterminado es 50. Puede seleccionar cualquier otro entero en el rango de 0 a 100. 1 indica la prioridad mínima y 100 indica la prioridad máxima. Si establece la **prioridad de copia de seguridad** en 1, se elegirá la réplica de disponibilidad para realizar copias de seguridad solo si no hay disponible actualmente ninguna réplica de disponibilidad con prioridad más alta.  
  
 **Excluir réplica**  
 Para evitar que esta réplica de disponibilidad se elija nunca para realizar copias de seguridad. Esto es útil, por ejemplo, para una réplica de disponibilidad remota en la que no desee nunca realizar la conmutación por error para las copias de seguridad.  
  
##  <a name="Listener"></a>Pestaña agente de escucha  
 Especifique sus preferencias para una[escucha de grupo de disponibilidad](../../listeners-client-connectivity-application-failover.md)que proporcionará un punto de conexión de cliente; puede ser:  
  
 **No cree ahora un agente de escucha del grupo de disponibilidad.**  
 Seleccione esta opción para omitir este paso. Puede crear un agente de escucha más adelante. Para obtener más información, vea [Crear o configurar un agente de escucha de grupo de disponibilidad &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md).  
  
 **Cree un agente de escucha del grupo de disponibilidad.**  
 Especifique sus preferencias de agente de escucha para este grupo de disponibilidad del siguiente modo:  
  
 **Nombre DNS del agente de escucha**  
 Especifique el nombre de red del agente de escucha. Este nombre debe ser único en el dominio y solo puede contener caracteres alfanuméricos, guiones**-**() y guiones (**_**), en cualquier orden. Cuando se especifica mediante la pestaña **Agente de escucha** , el nombre DNS puede tener hasta 15 caracteres.  
  
> [!IMPORTANT]  
>  Si escribe un nombre de agente de escucha DNS (o número de puerto) no válido en la pestaña **Agente de escucha** , el botón **Siguiente** de la página **Especificar réplicas** estará deshabilitado.  
  
 **Puerto**  
 Especifique el puerto TCP usado por este agente de escucha.  
  
> [!NOTE]  
>  Si escribe un número de puerto (o nombre de agente de escucha DNS) no válido en la pestaña **Agente de escucha** , el botón **Siguiente** de la página **Especificar réplicas** estará deshabilitado.  
  
 **Modo de red**  
 Utilice la lista desplegable para seleccionar el modo de red que utilizará este agente de escucha; puede ser:  
  
 **Dirección IP estática**  
 Seleccione esta opción si desea que el agente de escucha escuche en más de una subred. Para utilizar el modo de red de dirección IP estática, un agente de escucha del grupo de disponibilidad debe escuchar en cada subred que hospeda una réplica de disponibilidad para el grupo de disponibilidad. Para cada subred, haga clic en **Agregar** para seleccionar una dirección de subred y especificar una dirección IP.  
  
 Si se selecciona **Dirección IP estática** como modo de red (esta es la selección predeterminada), una cuadrícula muestra las columnas **Subret** y **Dirección IP** , y se muestran los botones **Agregar** y **Quitar** asociados. Tenga en cuenta que la cuadrícula estará vacía hasta que se agregue la primera subred.  
  
 Columna **subred**  
 Muestra la dirección de subred seleccionada para cada subred agregada para el agente de escucha.  
  
 Columna **dirección IP**  
 Muestra la dirección IPv4 o IPv6 especificada para una subred determinada.  
  
 **Add (Agregar)**  
 Haga clic para agregar una subred a este agente de escucha. Se abrirá el cuadro de diálogo de **Agregar dirección IP** . Para obtener más información, vea el tema de ayuda [Agregar dirección IP &#40;cuadro de diálogo - SQL Server Management Studio&#41;](add-ip-address-dialog-box-sql-server-management-studio.md).  
  
 **Remove**  
 Haga clic para quitar la subred actualmente seleccionada en la cuadrícula.  
  
 **DHCP**  
 Seleccione esta opción si desea que el agente de escucha escuche en una única subred y use una dirección IPv4 dinámica asignada por un servidor que ejecuta el protocolo DHCP (Protocolo de configuración dinámica de host). DHCP está limitado a una sola subred que es común a cada instancia del servidor que hospeda una réplica de disponibilidad para el grupo de disponibilidad.  
  
> [!IMPORTANT]  
>  No se recomienda DHCP en el entorno de producción. Si hay un tiempo de inactividad y expira la concesión de IP para DHCP, se necesitará más tiempo para registrar la nueva dirección IP de red DHCP que está asociada con el nombre DNS de escucha, lo que puede afectar a la conectividad de cliente. Sin embargo, DHCP es adecuado para configurar el entorno de desarrollo y pruebas para comprobar características básicas de los grupos de disponibilidad y para la integración con las aplicaciones.  
  
 Cuando **DHCP** está seleccionado, se muestra el campo **Subred** .  
  
 **Subnet**  
 Si selecciona **DHCP** como modo de red, use la lista desplegable **Subret** para seleccionar una dirección para la subred que hospeda las réplicas de disponibilidad del grupo de disponibilidad.  
  
> [!IMPORTANT]
>  Después de definir un agente de escucha del grupo de disponibilidad, es absolutamente recomendable que haga lo siguiente:  
> 
>  -   Pida al administrador de red que reserve la dirección IP del agente de escucha para su uso exclusivo. Proporcione el nombre del host DNS del agente de escucha a los desarrolladores de aplicaciones para que lo usen en las cadenas de conexión cuando soliciten conexiones cliente a este grupo de disponibilidad.  
> -   Proporcione el nombre del host DNS del agente de escucha a los desarrolladores de aplicaciones para que lo usen en las cadenas de conexión cuando soliciten conexiones cliente a este grupo de disponibilidad.  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Usar el Asistente para grupo de disponibilidad &#40;SQL Server Management Studio&#41;](use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Usar el Asistente para agregar una réplica al grupo de disponibilidad &#40;SQL Server Management Studio&#41;](use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Crear o configurar un agente de escucha de grupo de disponibilidad &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [Usar certificados para un punto de conexión de creación de reflejo de la base de datos &#40;Transact-SQL&#41;](../../database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
-   [CREATE ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-endpoint-transact-sql)  
  
-   [Cree un extremo de creación de reflejo de la base de datos para Grupos de disponibilidad AlwaysOn &#40;SQL Server PowerShell&#41;](database-mirroring-always-on-availability-groups-powershell.md)  
  
## <a name="see-also"></a>Consulte también  
 [Información general de Grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-availability-group-transact-sql)   
 [Requisitos previos, restricciones y recomendaciones para el SQL Server de &#40;de Grupos de disponibilidad AlwaysOn&#41;](prereqs-restrictions-recommendations-always-on-availability.md)  
  
  
