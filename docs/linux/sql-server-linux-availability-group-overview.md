---
title: AlwaysOn de grupos de disponibilidad para SQL Server en Linux | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 04/17/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: e37742d4-541c-4d43-9ec7-a5f9b2c0e5d1
ms.openlocfilehash: e552b1392716625cd2ce3f7927a1554c25bdb8e4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66713395"
---
# <a name="always-on-availability-groups-on-linux"></a>AlwaysOn de grupos de disponibilidad en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

En este artículo se describe las características de grupos de disponibilidad AlwaysOn (AG) en basado en Linux [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] las instalaciones. También cubre las diferencias entre el clúster de conmutación por error de Windows Server (WSFC) y Linux-basado en grupos de disponibilidad. Consulte la [documentación basada en Windows](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md) para los aspectos básicos de grupos de disponibilidad, como funcionan igual en Windows y Linux, excepto el WSFC.

Desde la perspectiva de alto nivel, grupos de disponibilidad bajo [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] en Linux son los mismos que se encuentran en las implementaciones basadas en WSFC. Esto significa que todas las características y limitaciones son los mismos, con algunas excepciones. Las principales diferencias son:

-   Coordinador de transacciones distribuidas (DTC) no es compatible con Linux en [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]. Si las aplicaciones requieren el uso de transacciones distribuidas y necesitan un grupo de disponibilidad, implemente [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] en Windows.
-   Las implementaciones basadas en Linux usan a Pacemaker en lugar de un WSFC.
-   A diferencia de la mayoría de las configuraciones de grupos de disponibilidad en Windows, excepto el escenario de clúster del grupo de trabajo, Pacemaker nunca requiere servicios de dominio de Active Directory (AD DS).
-   Cómo se producirá un error en un grupo de disponibilidad de un nodo a otro es diferente entre Windows y Linux.
-   Determinadas opciones como `required_synchronized_secondaries_to_commit` sólo puede cambiarse a través de Pacemaker en Linux, mientras que una instalación basada en WSFC usa Transact-SQL.

## <a name="number-of-replicas-and-cluster-nodes"></a>Número de réplicas y los nodos del clúster

Un grupo de disponibilidad en [!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)] puede tener dos réplicas en total: uno principal y otra secundaria solo se puede usar para fines de disponibilidad. No se puede usar para nada más, como las consultas legibles. Un grupo de disponibilidad en [!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)] puede tener hasta nueve réplicas totales: uno principal y hasta ocho réplicas secundarias, de los cuales hasta tres (incluida la principal) puede ser sincrónica. Si usa un clúster subyacente, puede haber un máximo de 16 nodos total cuando está implicada en Corosync. Un grupo de disponibilidad puede abarcar a lo sumo nueve de los 16 nodos con [!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)]y dos con [!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)].

Una configuración de dos réplicas que requiere la capacidad de conmutación por error automáticamente a otra réplica requiere el uso de una réplica de solo configuración, como se describe en [réplica de solo configuración y quórum](#configuration-only-replica-and-quorum). Las réplicas de solo configuración se introdujeron en [!INCLUDE[sssql17-md](../includes/sssql17-md.md)] actualización acumulativa 1 (CU1), por lo que debe ser la versión mínima que se implementan para esta configuración.

Si se usa Pacemaker, debe estar correctamente configurado para que permanezca en marcha. Esto significa que quórum y STONITH deben implementarse correctamente desde una perspectiva de Pacemaker, además de cualquier [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] requisitos como una réplica de solo configuración.

Solo se admiten las réplicas secundarias legibles con [!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)].

## <a name="cluster-type-and-failover-mode"></a>Modo de conmutación por error y el tipo de clúster

Nuevo en [!INCLUDE[sssql17-md](../includes/sssql17-md.md)] es la introducción de un tipo de clúster para grupos de disponibilidad. Para Linux, hay dos valores válidos: External y None. Un tipo de clúster externo significa que va a usar Pacemaker debajo del grupo de disponibilidad. Uso externo para tipo de clúster requiere que el modo de conmutación por error se establece en externo también (también como novedad en [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]). Se admite la conmutación automática por error, pero a diferencia de un clúster de WSFC, el modo de conmutación por error se establece como externa, no es automática, cuando Pacemaker se utiliza. A diferencia de un clúster de WSFC, se crea la parte de Pacemaker del grupo de disponibilidad después de configura el grupo de disponibilidad.

Un tipo de clúster ninguno significa que no hay ningún requisito para ni el grupo de disponibilidad utilizará, Pacemaker. Incluso en los servidores que tienen configurado de Pacemaker, si un grupo de disponibilidad está configurado con un tipo de clúster ninguno, Pacemaker no vea ni administrar ese grupo de disponibilidad. Un tipo de clúster ninguno solo admite manual de conmutación por error de un servidor principal a una réplica secundaria. Un grupo de disponibilidad creado con ninguno está dirigido principalmente para el escalado de lectura out escenario, así como las actualizaciones. Mientras que puede trabajar en escenarios como la recuperación ante desastres o disponibilidad local donde no es necesario ninguna conmutación por error automática, no se recomienda. La historia de agente de escucha también es más compleja sin Pacemaker.

Tipo de clúster se almacena en el [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] vista de administración dinámica (DMV) `sys.availability_groups`, en las columnas `cluster_type` y `cluster_type_desc`.

## <a name="requiredsynchronizedsecondariestocommit"></a>requiere\_sincronizado\_secundarias\_a\_confirmación

Nuevo en [!INCLUDE[sssql17-md](../includes/sssql17-md.md)] es un valor que se usa por grupos de disponibilidad denominados `required_synchronized_secondaries_to_commit`. Esto indica el grupo de disponibilidad en el número de réplicas secundarias que deben estar en modo "lockstep" con la principal. Esto permite cosas como la conmutación por error automática (solo cuando se integra con Pacemaker con un tipo de clúster externo) y controla el comportamiento de cosas como la disponibilidad de la réplica principal si el número correcto de las réplicas secundarias está en línea o sin conexión. Para conocer más acerca de cómo funciona esto, vea [alta disponibilidad y protección de datos para las configuraciones de grupo de disponibilidad](sql-server-linux-availability-group-ha.md). El `required_synchronized_secondaries_to_commit` valor se establece de forma predeterminada y mantenido por Pacemaker / [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. Puede invalidar este valor manualmente.

La combinación de `required_synchronized_secondaries_to_commit` y el nuevo número de secuencia (que se almacena en `sys.availability_groups`) le informa de Pacemaker y [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] que, por ejemplo, puede ocurrir conmutación automática por error. En ese caso, una réplica secundaria tendría el mismo número de secuencia que el servidor principal, lo que significa que está al día con toda la información de configuración más reciente.

Hay tres valores que se pueden establecer para `required_synchronized_secondaries_to_commit`: 0, 1 o 2. Controlan el comportamiento de lo que sucede cuando una réplica deja de estar disponible. Los números corresponden al número de réplicas secundarias que deben sincronizarse con la principal. El comportamiento es así en Linux:

-   0 - las réplicas secundarias no es necesario estar en estado sincronizado con la principal. Sin embargo si las secundarias no están sincronizadas, no habrá ninguna conmutación por error automática. 
-   1 - una réplica secundaria debe estar en un estado sincronizado con la principal; es posible la conmutación automática por error. La base de datos principal no está disponible hasta que una réplica secundaria sincrónica está disponible.
-   2 - ambas réplicas secundarias en una configuración de AG de tres o más nodos deben estar sincronizadas con el servidor principal; es posible la conmutación automática por error.

`required_synchronized_secondaries_to_commit` los controles no solo el comportamiento de las conmutaciones por error con réplicas sincrónicas, pero la pérdida de datos. Con un valor de 1 o 2, una réplica secundaria siempre es necesaria que se sincronizarán, por lo que siempre habrá redundancia de datos. Esto significa que no hay pérdida de datos.

Para cambiar el valor de `required_synchronized_secondaries_to_commit`, use la sintaxis siguiente:

>[!NOTE]
>Cambiar el valor hace que el recurso que se reinicie, lo que significa una breve interrupción. La única manera de evitar este problema es establecer el recurso que no se administrarán mediante el clúster temporalmente.

**Red Hat Enterprise Linux (RHEL) y Ubuntu**

```bash
sudo pcs resource update <AGResourceName> required_synchronized_secondaries_to_commit=<Value>
```

**SUSE Linux Enterprise Server (SLES)**

```bash
sudo crm resource param ms-<AGResourceName> set required_synchronized_secondaries_to_commit <value>
```

donde *AGResourceName* es el nombre del recurso configurado para el grupo de disponibilidad, y *valor* es 0, 1 o 2. Para volver a darle el valor predeterminado de administrar el parámetro de Pacemaker, ejecute la misma instrucción no tiene ningún valor.

Conmutación automática por error de un grupo de disponibilidad es posible cuando se cumplen las condiciones siguientes:

-   La principal y la réplica secundaria se establecen en el movimiento de datos sincrónico.
-   La base de datos secundaria tiene un estado de sincronizado (no sincronizar), lo que significa que los dos están en el mismo punto de datos.
-   El tipo de clúster se establece como externa. Conmutación automática por error no es posible con un tipo de clúster ninguno.
-   El `sequence_number` de la réplica secundaria se convierta en la réplica principal tiene el número de secuencia superior - en otras palabras, la réplica secundaria `sequence_number` coincida con el de la réplica principal original.

Si se cumplen estas condiciones y se produce un error en el servidor que hospeda la réplica principal, el grupo de disponibilidad cambiará la propiedad a una réplica sincrónica. El comportamiento de réplicas sincrónicas (de lo que puede haber tres total: uno principal y dos réplicas secundarias) adicional puede controlarse mediante `required_synchronized_secondaries_to_commit`. Esto funciona con grupos de disponibilidad en Windows y Linux, pero se configura de manera completamente diferente. En Linux, el valor se configura automáticamente el clúster en el propio recurso de grupo de disponibilidad.

## <a name="configuration-only-replica-and-quorum"></a>Quórum y la réplica de solo configuración

También como novedad en [!INCLUDE[sssql17-md](../includes/sssql17-md.md)] a partir de CU1 es una réplica de solo configuración. Dado que Pacemaker es diferente de un WSFC, especialmente cuando se trata de quórum y la necesidad de STONITH, con solo una configuración de dos nodos no funcionará cuando se trata de un grupo de disponibilidad. Una FCI, los mecanismos de quórum proporcionados por Pacemaker pueden ser todo bien, porque todos los arbitraje de conmutación por error FCI ocurre en el nivel de clúster. Para un grupo de disponibilidad, se produce el arbitraje en Linux en [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], donde se almacenan todos los metadatos. Esto es donde la réplica de solo configuración entra en juego.

Sin nada más, un tercer nodo y al menos una réplica sincronizada sería necesarios. La réplica de solo configuración almacena la configuración de AG en la base de datos maestra, igual que las otras réplicas en la configuración de AG. La réplica de solo configuración no tiene las bases de datos de usuario que participan en el grupo de disponibilidad. Los datos de configuración se envían de forma sincrónica desde el servidor principal. Estos datos de configuración, a continuación, se usan durante las conmutaciones por error, ya sean automática o manual.

Para que un grupo de disponibilidad mantener el cuórum y habilitar la conmutación por error automática con un tipo de clúster externo, ya sea debe:

-   Tiene tres réplicas sincrónicas ([!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)] sólo); o
-   Tiene dos réplicas (principales y secundarias), así como una réplica de solo configuración.

Las conmutaciones por error manual pueden ocurrir si usa External o tipos para las configuraciones de grupo de disponibilidad del clúster. Mientras que una réplica de solo configuración puede configurarse con un grupo de disponibilidad que tiene un tipo de clúster ninguno, no se recomienda, ya que complica la implementación. Para estas configuraciones, modifique manualmente `required_synchronized_secondaries_to_commit` tenga un valor de al menos 1, por lo que hay al menos una réplica sincronizada.

Se puede hospedar una réplica de solo configuración en cualquier edición de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], incluyendo [!INCLUDE[ssexpress-md](../includes/ssexpress-md.md)]. Esto reducirá los costos de licencia y se asegura de funciona con grupos de disponibilidad en [!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)]. Esto significa que la tercera requiere servidor solo debe cumplir las especificaciones mínimas para [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], ya que no recibe tráfico de la transacción de usuario para el grupo de disponibilidad.

Cuando se usa una réplica de solo configuración, tiene el siguiente comportamiento:

-   De forma predeterminada, `required_synchronized_secondaries_to_commit` se establece en 0. Si lo desea, esto puede modificarse manualmente en 1.
-   Si se produce un error en el servidor principal y `required_synchronized_secondaries_to_commit` es 0, la réplica secundaria se convertirá en la nueva réplica principal y esté disponible para operaciones de lectura y escritura. Si el valor es 1, se producirán conmutación automática por error, pero no aceptará las nuevas transacciones hasta que la otra réplica está en línea.
-   Si se produce un error en una réplica secundaria y `required_synchronized_secondaries_to_commit` es 0, la réplica principal sigue aceptando las transacciones, pero si el servidor principal produce un error en este momento, no hay ninguna protección para los datos ni la conmutación por error posibles (manual o automático), puesto que una réplica secundaria no está disponible.
-   Si se produce un error en las réplicas de solo configuración, el grupo de disponibilidad seguirán funcionando con normalidad, pero no es posible ninguna conmutación por error automática.
-   Si se producirá un error en una réplica secundaria sincrónica y la réplica de solo configuración, el servidor principal no puede aceptar las transacciones y no hay ningún destino para la réplica principal no se pueda.

En CU1 hay un problema conocido en el registro en el archivo corosync.log que se genera mediante `mssql-server-ha`. Si una réplica secundaria no puede ser el principal debido al número de réplicas necesarios disponibles, el mensaje actual indica que "se esperaba recibir los números de secuencia 1 pero sólo recibe 2. No hay suficientes réplicas están en línea para promover la réplica local de forma segura." Los números que se deben invertir, y debería aparecer como "esperaba recibir 2 números de secuencia, pero solo reciben 1. No hay suficientes réplicas están en línea para promover la réplica local de forma segura." 

## <a name="multiple-availability-groups"></a>Varios grupos de disponibilidad 

Cada clúster de Pacemaker o conjunto de servidores se puede crear más de un grupo de disponibilidad. La única limitación es que los recursos del sistema. El maestro, se muestra la propiedad del grupo de disponibilidad. Pueden ser propiedad de distintos grupos de disponibilidad en nodos diferentes; No todos deben estar ejecutándose en el mismo nodo.

## <a name="drive-and-folder-location-for-databases"></a>Ubicación de unidad y carpeta para las bases de datos

Como en los grupos de disponibilidad basado en Windows, la estructura de unidad y carpeta para las bases de datos de usuario que participan en un grupo de disponibilidad debe ser idéntica. Por ejemplo, si las bases de datos de usuario se encuentran en `/var/opt/mssql/userdata` en el servidor A, esa misma carpeta debe existir en el servidor B. La única excepción a esto se indica en la sección [interoperabilidad con grupos de disponibilidad basados en Windows y las réplicas](#interoperability-with-windows-based-availability-groups-and-replicas).

## <a name="the-listener-under-linux"></a>El agente de escucha en Linux

El agente de escucha es una funcionalidad opcional para un grupo de disponibilidad. Proporciona un único punto de entrada para todas las conexiones (lectura/escritura a la réplica principal o réplicas de solo lectura a una réplica secundaria) para que las aplicaciones y los usuarios finales no es necesario saber qué servidor hospeda los datos. En un clúster de WSFC, esto es la combinación de un recurso de nombre de red y un recurso IP, que, a continuación, se registra en AD DS (si es necesario), así como DNS. En combinación con el propio recurso de AG, proporciona dicha abstracción. Para obtener más información sobre un agente de escucha, vea [los agentes de escucha, conectividad de cliente y conmutación por error de aplicación](../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md).

El agente de escucha en Linux está configurado de forma diferente, pero su funcionalidad es la misma. No hay ningún concepto de un recurso de nombre de red en Pacemaker, ni se crea un objeto de AD DS; hay solo un recurso de dirección IP creado en Pacemaker que se puede ejecutar en cualquiera de los nodos. Debe crearse una entrada asociada con el recurso de IP para el agente de escucha en el DNS con el nombre"descriptivo". El recurso IP para el agente de escucha sólo estará activo en el servidor que hospeda la réplica principal para ese grupo de disponibilidad.

Si Pacemaker se usa y se crea un recurso de dirección IP que está asociado con el agente de escucha, habrá una breve interrupción como la dirección IP se detiene en el servidor y se inicia en el otro, ya sea de conmutación por error automática o manual. Si bien esto proporciona la abstracción mediante la combinación de un nombre único y la dirección IP, no se enmascara la interrupción. Una aplicación debe ser capaz de controlar la desconexión al tener algún tipo de funcionalidad para detectar esto y vuelva a conectar.

Sin embargo, la combinación del nombre DNS y dirección IP es aún no lo suficiente para proporcionar toda la funcionalidad que proporciona un agente de escucha en un WSFC, como el enrutamiento de solo lectura para las réplicas secundarias. Al configurar un grupo de disponibilidad, un "agente de escucha" todavía debe configurarse en [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. Esto puede verse en el asistente, así como la sintaxis de Transact-SQL. Hay dos maneras de que esto se puede configurar para que funcione el mismo que en Windows:

-   Para un grupo de disponibilidad con un tipo de clúster externo, la dirección IP asociada con la "escucha" que creó en [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] debe ser la dirección IP del recurso creado en Pacemaker.
-   Para un grupo de disponibilidad creado con un tipo de clúster ninguno, utilice la dirección IP asociada con la réplica principal.

La instancia asociada con la dirección IP proporcionada, a continuación, se convierte en el coordinador para cosas como las solicitudes de enrutamientos de solo lectura de aplicaciones.

## <a name="interoperability-with-windows-based-availability-groups-and-replicas"></a>Interoperabilidad con grupos de disponibilidad basados en Windows y las réplicas 

Un grupo de disponibilidad que tiene un clúster de tipo externo o uno que sea WSFC no puede tener sus réplicas entre plataformas. Esto es cierto si el grupo de disponibilidad es [!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)] o [!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)]. Esto significa que en una configuración de grupo de disponibilidad tradicional con un clúster subyacente, no puede ser una réplica en un clúster de WSFC y otro en Linux con Pacemaker.

Un grupo de disponibilidad con un tipo de clúster ninguno puede tener sus réplicas cruzar los límites de sistema operativo, por lo que podría haber ambas réplicas basadas en Windows y Linux en el mismo grupo de disponibilidad. Aquí se muestra un ejemplo donde la réplica principal está basado en Windows, mientras que la base de datos secundaria se encuentra en una de las distribuciones de Linux.

![Híbrido ninguno](./media/sql-server-linux-availability-group-overview/image1.png)

Un grupo de disponibilidad distribuido también puede cruzar los límites del sistema operativo. Los grupos de disponibilidad subyacentes están limitadas por las reglas de cómo estén configuradas, por ejemplo, una configurada con la que se va a externo solo para Linux, pero se pudo configurar el grupo de disponibilidad que se une a mediante un WSFC. Considere el ejemplo siguiente:

![Híbrido Dist AG](./media/sql-server-linux-availability-group-overview/image2.png)

<!-- Distributed AGs are also supported for upgrades from [!INCLUDE[sssql15-md](../includes/sssql15-md.md)] to [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]. For more information on how to achieve this, see [the article "x"].

If using automatic seeding with a distributed availability group that crosses OSes, it can handle the differences in folder structure. How this works is described in [the documentation for automatic seeding].
-->
 
## <a name="next-steps"></a>Pasos siguientes
[Configurar el grupo de disponibilidad para SQL Server en Linux](sql-server-linux-availability-group-configure-ha.md)

[Configurar el grupo de disponibilidad de escalado de lectura para SQL Server en Linux](sql-server-linux-availability-group-configure-rs.md)

[Agregue el recurso de clúster del grupo de disponibilidad en RHEL](sql-server-linux-availability-group-cluster-rhel.md)

[Agregue el recurso de clúster del grupo de disponibilidad en SLES](sql-server-linux-availability-group-cluster-sles.md)

[Agregue el recurso de clúster del grupo de disponibilidad en Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md)

[Configurar un grupo de disponibilidad multiplataforma](sql-server-linux-availability-group-cross-platform.md)

