---
title: SQL Server Always On patrones de implementación del grupo de disponibilidad
ms.date: 04/17/2019
ms.prod: sql
ms.technology: linux
ms.topic: conceptual
ms.assetid: edd75f68-dc62-4479-a596-57ce8ad632e5
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.openlocfilehash: 637d67767e17344d63498f8cb6a141fa78b11ecb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67996436"
---
# <a name="high-availability-and-data-protection-for-availability-group-configurations"></a>Alta disponibilidad y protección de datos para las configuraciones de grupo de disponibilidad

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

En este artículo presenta las configuraciones de implementación compatibles para grupos de disponibilidad de SQL Server Always On en servidores Linux. Un grupo de disponibilidad es compatible con alta disponibilidad y protección de datos. Detección automática de errores, conmutación por error automática y transparente reconexión después de la conmutación por error proporcionan alta disponibilidad. Réplicas sincronizadas proporcionan protección de datos. 

Una configuración común para alta disponibilidad en un clúster de conmutación por error de Windows Server (WSFC), utiliza dos réplicas sincrónicas y un tercer servidor o archivo compartido para proporcionar el quórum. El testigo de recurso compartido de archivos valida la configuración del grupo de disponibilidad - estado de sincronización y el rol de la réplica, por ejemplo. Esta configuración garantiza la réplica secundaria que se elige como el destino de conmutación por error tiene los datos más recientes y los cambios de configuración del grupo de disponibilidad. 

El WSFC sincroniza los metadatos de configuración para el arbitraje de conmutación por error entre las réplicas del grupo de disponibilidad y el testigo de recurso compartido de archivos. Cuando un grupo de disponibilidad no está en un WSFC, las instancias de SQL Server almacenan los metadatos de configuración en la base de datos maestra.

Por ejemplo, un grupo de disponibilidad en un clúster de Linux tiene `CLUSTER_TYPE = EXTERNAL`. No hay ningún WSFC arbitrar conmutación por error. En este caso los metadatos de configuración se administra y mantiene las instancias de SQL Server. Dado que no hay ningún servidor testigo en este clúster, se requiere una tercera instancia de SQL Server para almacenar los metadatos de estado de configuración. Las tres instancias de SQL Server proporcionan almacenamiento de metadatos distribuidos para el clúster. 

El Administrador de clústeres puede consultar las instancias de SQL Server en el grupo de disponibilidad y orquestar la conmutación por error para mantener la alta disponibilidad. En un clúster de Linux, Pacemaker es el Administrador de clústeres. 

SQL Server 2017 CU 1 habilita la alta disponibilidad para un grupo de disponibilidad con `CLUSTER_TYPE = EXTERNAL` para dos réplicas sincrónicas además de una réplica de solo configuración. La única réplica de configuración se puede hospedar en cualquier edición de SQL Server 2017 CU1 o posterior - incluido SQL Server Express edition. La réplica de solo configuración mantiene información de configuración sobre el grupo de disponibilidad en la base de datos maestra, pero no contiene las bases de datos de usuario del grupo de disponibilidad. 

## <a name="how-the-configuration-affects-default-resource-settings"></a>Cómo afecta la configuración a la configuración predeterminada de los recursos

SQL Server 2017 presenta el `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` configuración del recurso de clúster. Esta configuración garantiza al número especificado de la escritura de las réplicas secundarias de los datos de transacción para iniciar sesión antes de la réplica principal confirma cada transacción. Cuando se usa un administrador de clústeres externos, esta configuración afecta a la alta disponibilidad y protección de datos. El valor predeterminado para la configuración depende de la arquitectura en el momento en que se crea el recurso de clúster. Al instalar el agente de recursos de SQL Server - `mssql-server-ha` - y crear un recurso de clúster para el grupo de disponibilidad, el Administrador de clústeres detecta la disponibilidad de grupo Configuración y los conjuntos de `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` en consecuencia. 

Si es compatible con la configuración, el parámetro de agente de recursos `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` está establecido en el valor que proporciona alta disponibilidad y protección de datos. Para obtener más información, consulte [agente de recursos de comprender SQL Server para pacemaker](#pacemakerNotify).

Las siguientes secciones explican el comportamiento predeterminado para el recurso de clúster. 

Elegir un diseño de grupo de disponibilidad para cumplir los requisitos empresariales específicos de alta disponibilidad, protección de datos y escalado de lectura.

Las configuraciones siguientes describen los patrones de diseño del grupo de disponibilidad y las capacidades de cada patrón. Estos patrones de diseño se aplican a grupos de disponibilidad con `CLUSTER_TYPE = EXTERNAL` para soluciones de alta disponibilidad. 

- **Tres réplicas sincrónicas.**
- **Dos réplicas sincrónicas**
- **Dos réplicas sincrónicas y una réplica de solo configuración**

<a name="threeSynch"></a>

## <a name="three-synchronous-replicas"></a>Tres réplicas sincrónicas

Esta configuración consta de tres réplicas sincrónicas. De forma predeterminada, proporciona alta disponibilidad y protección de datos. Además, puede proporcionar escalado de lectura.

![Tres réplicas][3]

Escalado de lectura, alta disponibilidad y protección de datos, puede proporcionar un grupo de disponibilidad con tres réplicas sincrónicas. En la tabla siguiente se describe el comportamiento de disponibilidad. 

| |escalado de lectura|Alta disponibilidad & </br> protección de datos | Protección de datos|
|:---|---|---|---|
|`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT=`|0 |1<sup>\*</sup>|2|
|Interrupción principal |Conmutación por error automática. La nueva réplica principal es R / w. |Conmutación por error automática. La nueva réplica principal es R / w. |Conmutación por error automática. La nueva réplica principal no está disponible para las transacciones de usuario hasta que el objeto principal anterior se recupera y grupo de disponibilidad como la secundaria une. |
|Interrupción de réplica secundaria  | La réplica principal es R / w. No hay conmutación automática por error si se produce un error en la principal. |La réplica principal es R / w. No hay conmutación automática por error si la principal produce un error también. | Principal no está disponible para las transacciones de usuario. |

<sup>\*</sup> Valor predeterminado

<a name="twoSynch"></a>

## <a name="two-synchronous-replicas"></a>Dos réplicas sincrónicas

Esta configuración habilita la protección de datos. Al igual que las demás configuraciones de grupo disponibilidad, puede habilitar el escalado de lectura. La configuración de dos réplicas sincrónicas no proporciona alta disponibilidad automática. Una configuración de dos réplicas solo es aplicable a SQL Server 2017 RTM y ya no es compatible con versiones posteriores (CU1 y versiones posteriores) las versiones de SQL Server 2017...

![Dos réplicas sincrónicas][1]

Un grupo de disponibilidad con dos réplicas sincrónicas proporciona protección de datos y escalado de lectura. En la tabla siguiente se describe el comportamiento de disponibilidad. 

| |escalado de lectura |Protección de datos|
|:---|---|---|
|`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT=`|0 <sup>\*</sup>|1|
|Interrupción principal | Conmutación por error manual. Es posible que haya pérdida de datos. La nueva réplica principal es R / w.| Conmutación por error automática. La nueva réplica principal no está disponible para las transacciones de usuario hasta que el objeto principal anterior se recupera y grupo de disponibilidad como la secundaria une.|
|Interrupción de réplica secundaria  |Réplica principal es de lectura/escritura, ejecución se expone a pérdida de datos. |Principal no está disponible para las transacciones de usuario hasta que se recupere la secundaria.|

<sup>\*</sup> Valor predeterminado

<a name = "configOnly"></a>

## <a name="two-synchronous-replicas-and-a-configuration-only-replica"></a>Dos réplicas sincrónicas y una réplica de solo configuración

Un grupo de disponibilidad con réplicas sincrónicas de dos (o más) y una réplica de solo configuración ofrece protección de datos y también puede proporcionar una alta disponibilidad. El siguiente diagrama representa esta arquitectura:

![Grupo de disponibilidad de solo configuración][2]

1. Replicación sincrónica de datos de usuario a la réplica secundaria. También incluye los metadatos de configuración del grupo de disponibilidad.
2. Replicación sincrónica de metadatos de configuración del grupo de disponibilidad. No incluye datos de usuario.

En el diagrama del grupo de disponibilidad, una réplica principal envía datos de configuración a la réplica secundaria y la réplica de solo configuración. La réplica secundaria también recibe datos de usuario. La réplica de solo configuración no recibe los datos de usuario. La réplica secundaria está en modo de disponibilidad sincrónica. La réplica de solo configuración no contiene las bases de datos en el grupo de disponibilidad: solo los metadatos sobre el grupo de disponibilidad. Datos de configuración en la réplica de solo configuración se confirma sincrónicamente.

> [!NOTE]
> Un grupo de availabilility con réplica de solo configuración es nuevo en SQL Server 2017 CU1. Todas las instancias de SQL Server en el grupo de disponibilidad deben ser SQL Server 2017 CU1 o una versión posterior. 

El valor predeterminado de `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` es 0. En la tabla siguiente se describe el comportamiento de disponibilidad. 

| |Alta disponibilidad & </br> protección de datos | Protección de datos|
|:---|---|---|
|`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT=`|0 <sup>\*</sup>|1|
|Interrupción principal | Conmutación por error automática. La nueva réplica principal es R / w. | Conmutación por error automática. La nueva réplica principal no está disponible para las transacciones de usuario. |
|Interrupción de la réplica secundaria | Réplica principal es de lectura/escritura, ejecución se expone a pérdida de datos (si la principal se produce un error y no se puede recuperar). No hay conmutación automática por error si la principal produce un error también. | Principal no está disponible para las transacciones de usuario. No hay ninguna réplica de la conmutación por error a si la principal produce un error también. |
|Interrupción de réplica de solo configuración | La réplica principal es R / w. No hay conmutación automática por error si la principal produce un error también. | La réplica principal es R / w. No hay conmutación automática por error si la principal produce un error también. |
|Elemento secundario sincrónico + configuración sólo la interrupción de réplica| Principal no está disponible para las transacciones de usuario. Ninguna conmutación por error automática. | Principal no está disponible para las transacciones de usuario. No hay ninguna réplica en conmutación por error como si principal se produce un error también. |

<sup>\*</sup> Valor predeterminado

> [!NOTE]
> La instancia de SQL Server que hospeda la réplica de solo configuración también puede hospedar a otras bases de datos. También puede participar como una configuración única base de datos de más de un grupo de disponibilidad. 

## <a name="requirements"></a>Requisitos

- Todas las réplicas de un grupo de disponibilidad con una réplica de solo configuración deben ser SQL Server 2017 CU 1 o posterior.
- Cualquier edición de SQL Server puede hospedar una réplica de solo configuración, incluido SQL Server Express. 
- El grupo de disponibilidad necesita al menos una réplica secundaria - además de la réplica principal.
- Las réplicas sola configuración no cuentan para el número máximo de réplicas por cada instancia de SQL Server. SQL Server standard edition permite hasta tres réplicas, SQL Server Enterprise Edition permite hasta 9.

## <a name="considerations"></a>Consideraciones

- Réplica de solo de no más de una configuración por grupo de disponibilidad. 
- Una réplica de solo configuración no puede ser una réplica principal.
- No se puede modificar el modo de disponibilidad de una réplica de solo configuración. Para cambiar de una réplica de solo configuración a una réplica secundaria sincrónica o asincrónica, quite la réplica de solo configuración y agregar una réplica secundaria con el modo de disponibilidad necesarios. 
- Una réplica de solo configuración está sincronizada con los metadatos del grupo de disponibilidad. No hay ningún dato de usuario. 
- Un grupo de disponibilidad con una réplica principal y réplica de solo una configuración, pero no hay ninguna réplica secundaria no es válido. 
- No se puede crear un grupo de disponibilidad en una instancia de SQL Server Express edition. 

<a name="pacemakerNotify"></a>

## <a name="understand-sql-server-resource-agent-for-pacemaker"></a>Comprender el agente de recursos de SQL Server para pacemaker

SQL Server 2017 CTP 1.4 agrega `sequence_number` a `sys.availability_groups` para permitir que Pacemaker identificar el grado de actualización secundaria réplicas están con la réplica principal. `sequence_number` es un valor BIGINT progresión que representa el grado de actualización la réplica del grupo de disponibilidad local. Las actualizaciones de pacemaker el `sequence_number` con cada cambio de configuración del grupo de disponibilidad. Conmutación por error, la adición de réplica o la eliminación son ejemplos de cambios de configuración. El número se actualiza en la réplica principal y luego replican en réplicas secundarias. Por lo tanto, una réplica secundaria que tiene la configuración actualizada tiene el mismo número de secuencia que la réplica principal. 

Cuando Pacemaker decide promover una réplica a principal, en primer lugar envía una *previa a la promoción* notificación a todas las réplicas. Las réplicas devuelven el número de secuencia. A continuación, cuando Pacemaker intenta realmente promover una réplica a principal, la réplica solo se promueve a sí misma si su número de secuencia es el más alto de todos los números de secuencia. Si su propio número de secuencia no coincide con el número de secuencia más alto, la réplica rechaza la operación de promoción. De esta manera, solo se puede promover a principal la réplica con el número de secuencia más alto, lo que garantiza que no se producirá una pérdida de datos. 

Este proceso requiere al menos una réplica disponible para su promoción con el mismo número de secuencia que la réplica principal anterior. Los conjuntos de agente de recursos de Pacemaker `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` que al menos una réplica secundaria sincrónica está actualizada y disponible para ser el destino de conmutación automática por error de forma predeterminada. Con cada acción de supervisión, el valor de `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` es calculada (y actualizar si es necesario). El `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` es el valor de 'número de réplicas sincrónicas' dividido entre 2. Durante la conmutación por error, se requiere el agente de recursos (`total number of replicas`  -  `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` réplicas) para responder a la notificación previa a la promoción. La réplica con el nivel más alto `sequence_number` se promueve a principal. 

Por ejemplo, un grupo de disponibilidad con tres réplicas sincrónicas: una réplica principal y dos réplicas secundarias sincrónicas.

- `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` es 1; (3 / 2 -> 1).

- El número necesario de réplicas para responder acción previa a la promoción es 2. (3 - 1 = 2). 

En este escenario, las dos réplicas tienen que responder para que la conmutación por error para que se desencadene. Correcta conmutación automática por error tras una interrupción de la réplica principal, ambas réplicas secundarias deben actualizada y responder a la notificación previa a la promoción. Si son sincrónicas y en línea, tienen el mismo número de secuencia. El grupo de disponibilidad promueve una de ellas. Si solo una de las réplicas secundarias responde a la acción previa a la promoción no puede garantizar el agente de recursos que la base de datos secundaria que ha respondido tenga el sequence_number más alto y no se desencadena una conmutación por error.

> [!IMPORTANT]
> Cuando `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` es 0, existe riesgo de pérdida de datos. Durante una interrupción de la réplica principal, el agente de recursos no desencadenará automáticamente una conmutación por error. Puede esperar principal recuperar o una conmutación manual utilizando `FORCE_FAILOVER_ALLOW_DATA_LOSS`.

Puede elegir invalidar el comportamiento predeterminado y evitar que el recurso de grupo de disponibilidad configuración `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` automáticamente.

El siguiente script establece `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` en 0 en un grupo de disponibilidad denominado `<**ag1**>`. Antes de efectuar la ejecución, reemplace `<**ag1**>` por el nombre del grupo de disponibilidad.

```bash
sudo pcs resource update <**ag1**> required_synchronized_secondaries_to_commit=0
```

Para revertir al valor predeterminado, según la configuración del grupo de disponibilidad ejecutar:

```bash
sudo pcs resource update <**ag1**> required_synchronized_secondaries_to_commit=
```

> [!NOTE]
> Al ejecutar los comandos anteriores, la réplica principal está temporalmente degradan a una réplica secundaria, promover de nuevo. La actualización de recursos hace que todas las réplicas detener y reiniciar. El nuevo valor de`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` sólo se establece una vez que se reinicien las réplicas, no al instante.

## <a name="see-also"></a>Vea también

[Grupos de disponibilidad en Linux](sql-server-linux-availability-group-overview.md)

<!--Image references-->
[1]: ./media/sql-server-linux-availability-group-ha/1-read-scale-out.png
[2]: ./media/sql-server-linux-availability-group-ha/2-configuration-only.png
[3]: ./media/sql-server-linux-availability-group-ha/3-three-replica.png
[4]: ./media/sql-server-linux-availability-group-ha/configuration-only-example.png
