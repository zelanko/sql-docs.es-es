---
title: SQL Server Always On patrones de implementación del grupo de disponibilidad | Documentos de Microsoft
ms.custom: sql-linux
ms.date: 10/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: edd75f68-dc62-4479-a596-57ce8ad632e5
caps.latest.revision: 34
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: be101608971d9bb40def9f8f1df22bc867c4dd0d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="high-availability-and-data-protection-for-availability-group-configurations"></a>Alta disponibilidad y protección de datos para las configuraciones de grupo de disponibilidad

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artículo presenta las configuraciones de implementación admitido para grupos de disponibilidad AlwaysOn de SQL Server en servidores Linux. Un grupo de disponibilidad admite alta disponibilidad y protección de datos. Detección de errores automática, conmutación por error automática y transparente reconexión después de la conmutación por error proporcionan alta disponibilidad. Las réplicas sincronizadas proporcionan protección de datos. 

En un clúster de conmutación por error de Windows Server (WSFC), una configuración común para alta disponibilidad usa dos réplicas sincrónicas y un tercer servidor o archivo compartido para proporcionar el quórum. El testigo de recurso compartido de archivos valida la configuración del grupo de disponibilidad - estado de sincronización y el rol de la réplica, por ejemplo. Esta configuración garantiza que la réplica secundaria que se elige como el destino de conmutación por error tiene los datos más recientes y los cambios de configuración de grupo de disponibilidad. 

El WSFC sincroniza los metadatos de configuración para el arbitraje de conmutación por error entre las réplicas del grupo de disponibilidad y el testigo de recurso compartido de archivos. Cuando un grupo de disponibilidad no está en un WSFC, las instancias de SQL Server almacenan los metadatos de configuración en la base de datos maestra.

Por ejemplo, tiene un grupo de disponibilidad en un clúster de Linux `CLUSTER_TYPE = EXTERNAL`. No hay ningún WSFC para arbitran conmutación por error. En este caso los metadatos de configuración es administrar y mantener las instancias de SQL Server. Porque no hay ningún servidor testigo en este clúster, se requiere una tercera instancia de SQL Server para almacenar los metadatos de estado de configuración. En conjunto, las tres instancias de SQL Server proporcionan almacenamiento de metadatos distribuidos para el clúster. 

El Administrador de clústeres puede consultar las instancias de SQL Server en el grupo de disponibilidad y orquestar la conmutación por error para mantener una alta disponibilidad. En un clúster de Linux, marcapasos es el Administrador de clústeres. 

SQL Server de 2017 CU 1 permite una alta disponibilidad para un grupo de disponibilidad con `CLUSTER_TYPE = EXTERNAL` para dos réplicas sincrónicas además de una única réplica de configuración. La única réplica de configuración se puede hospedar en cualquier edición de SQL Server de 2017 CU1 o posterior - incluidas SQL Server Express edition. La única réplica de configuración mantiene información de configuración sobre el grupo de disponibilidad en la base de datos maestra, pero no contiene las bases de datos de usuario del grupo de disponibilidad. 

## <a name="how-the-configuration-affects-default-resource-settings"></a>Cómo afecta la configuración a la configuración predeterminada de los recursos

SQL Server 2017 presenta el `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` recurso de clúster. Esta configuración garantiza que el número especificado de escritura de las réplicas secundarias los datos de transacción para iniciar sesión antes de la réplica principal confirma cada transacción. Cuando se utiliza un administrador de clúster externo, esta configuración afecta a la alta disponibilidad y protección de datos. El valor predeterminado de la configuración depende de la arquitectura en el momento de que crea el recurso de clúster. Cuando se instala el agente de recursos de SQL Server - `mssql-server-ha` - y crear un recurso de clúster para el grupo de disponibilidad, el Administrador de clústeres detecta la disponibilidad del grupo Configuración y conjuntos de `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` en consecuencia. 

Si se admite la configuración, el parámetro de agente de recurso `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` se establece en el valor que proporciona alta disponibilidad y protección de datos. Para obtener más información, consulte [comprender Agente SQL Server del recurso para marcapasos](#pacemakerNotify).

Las siguientes secciones explican el comportamiento predeterminado para el recurso de clúster. 

Elija un diseño de grupo de disponibilidad para cumplir los requisitos empresariales específicos para alta disponibilidad, la protección de datos y la escala de lectura.

Las configuraciones siguientes describen los patrones de diseño del grupo de disponibilidad y las capacidades de cada patrón. Estos modelos de diseño que se aplican a los grupos de disponibilidad con `CLUSTER_TYPE = EXTERNAL` para soluciones de alta disponibilidad. 

- **Tres réplicas sincrónicas.**
- **Dos réplicas sincrónicas.**
- **Dos réplicas sincrónicas y una única réplica de configuración**

<a name="threeSynch"></a>

## <a name="three-synchronous-replicas"></a>Tres réplicas sincrónicas.

Esta configuración se compone de tres réplicas sincrónicas. De forma predeterminada, proporciona alta disponibilidad y protección de datos. También puede proporcionar escala de lectura.

![Tres réplicas][3]

Escala de lectura, alta disponibilidad y protección de datos, puede proporcionar un grupo de disponibilidad con tres réplicas sincrónicas. En la tabla siguiente se describe el comportamiento de disponibilidad. 

| |escala de lectura|Alta disponibilidad & </br> protección de datos | Protección de los datos
|:---|---|---|---
|`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT=`|0 |1<sup>*</sup>|2
|Interrupción principal | Conmutación por error manual. Es posible que haya pérdida de datos. Nuevo elemento principal es R / w. |Conmutación por error automática. Nuevo elemento principal es R / w. |Conmutación por error automática. Nuevo elemento principal no está disponible para las transacciones de usuario hasta que el objeto principal anterior se recupera y une a grupo de disponibilidad como secundaria. 
|Interrupción de réplica secundaria  | Principal es R / w. No hay conmutación automática por error si se produce un error en la principal. |Principal es R / w. No hay conmutación automática por error si falla el sitio primario también. | Principal no está disponible para las transacciones de usuario. 
<sup>*</sup> Valor predeterminado

<a name="twoSynch"></a>

## <a name="two-synchronous-replicas"></a>Dos réplicas sincrónicas.

Esta configuración habilita la protección de datos. Al igual que las otras configuraciones de grupo disponibilidad, puede habilitar la escala de lectura. La configuración de dos réplicas sincrónicas no proporciona alta disponibilidad automática. 

![Dos réplicas sincrónicas.][1]

Un grupo de disponibilidad con dos réplicas sincrónicas proporciona protección de datos y la escala de lectura. En la tabla siguiente se describe el comportamiento de disponibilidad. 

| |escala de lectura |Protección de los datos
|:---|---|---
|`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT=`|0 <sup>*</sup>|1
|Interrupción principal | Conmutación por error manual. Es posible que haya pérdida de datos. Nuevo elemento principal es R / w.| Conmutación por error automática. Nuevo elemento principal no está disponible para las transacciones de usuario hasta que el objeto principal anterior se recupera y une a grupo de disponibilidad como secundaria.
|Interrupción de réplica secundaria  |Principal es lectura/escritura, ejecución expuesta a la pérdida de datos. |Principal no está disponible para las transacciones de usuario hasta que recupera secundaria.
<sup>*</sup> Valor predeterminado

>[!NOTE]
>El escenario anterior es el comportamiento antes de 2017 CU 1 de SQL Server. 

<a name = "configOnly"></a>

## <a name="two-synchronous-replicas-and-a-configuration-only-replica"></a>Dos réplicas sincrónicas y una única réplica de configuración

Un grupo de disponibilidad con réplicas sincrónicas dos (o más) y una única réplica de configuración proporciona protección de datos y también puede proporcionar una alta disponibilidad. El siguiente diagrama representa esta arquitectura:

![Grupo de disponibilidad solo de configuración][2]

1. Replicación sincrónica de datos de usuario a la réplica secundaria. También incluye los metadatos de configuración del grupo de disponibilidad.
2. Replicación sincrónica de metadatos de configuración del grupo de disponibilidad. No incluye datos de usuario.

En el diagrama de grupo de disponibilidad, una réplica principal envía datos de configuración a la réplica secundaria y la única réplica de configuración. La réplica secundaria también recibe datos de usuario. La única réplica de configuración no recibe los datos de usuario. La réplica secundaria está en modo sincrónico. La única réplica de configuración no contiene las bases de datos en el grupo de disponibilidad: solo los metadatos sobre el grupo de disponibilidad. Datos de configuración de la única réplica de configuración se confirma sincrónicamente.

>[!NOTE]
>Un grupo de availabilility con la única réplica de la configuración es nuevo en SQL Server de 2017 CU1. Todas las instancias de SQL Server en el grupo de disponibilidad deben ser SQL Server 2017 CU1 o una versión posterior. 

El valor predeterminado de `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` es 0. En la tabla siguiente se describe el comportamiento de disponibilidad. 

| |Alta disponibilidad & </br> protección de datos | Protección de los datos
|:---|---|---
|`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT=`|0 <sup>*</sup>|1
|Interrupción principal | Conmutación por error automática. Nuevo elemento principal es R / w. | Conmutación por error automática. Nuevo elemento principal no está disponible para las transacciones de usuario. 
|Interrupción de la réplica secundaria | Principal es de lectura/escritura, ejecución expuesta a la pérdida de datos (si principal produce un error y no se puede recuperar). No hay conmutación automática por error si falla el sitio primario también. | Principal no está disponible para las transacciones de usuario. No hay ninguna réplica para conmutar a si falla el sitio primario también. 
|Interrupción de réplica solo configuración | Principal es R / w. No hay conmutación automática por error si falla el sitio primario también. | Principal es R / w. No hay conmutación automática por error si falla el sitio primario también. 
|Elemento secundario sincrónico + configuración solo interrupción de réplica| Principal no está disponible para las transacciones de usuario. No hay conmutación por error automática. | Principal no está disponible para las transacciones de usuario. No hay ninguna réplica en conmutación por error como si también generará errores principales. 
<sup>*</sup> Valor predeterminado

>[!NOTE]
>La instancia de SQL Server que hospeda la única réplica de configuración también puede hospedar otras bases de datos. También puede participar como una configuración única base de datos de más de un grupo de disponibilidad. 

## <a name="requirements"></a>Requisitos

* Todas las réplicas de un grupo de disponibilidad con una única réplica de configuración deben ser SQL Server 2017 CU 1 o posterior.
* Cualquier edición de SQL Server puede hospedar una réplica de solo de configuración, incluido SQL Server Express. 
* El grupo de disponibilidad necesita al menos una réplica secundaria - además de la réplica principal.
* Réplicas sola de configuración no se cuentan en el número máximo de réplicas por instancia de SQL Server. SQL Server standard edition permite hasta tres réplicas, SQL Server Enterprise Edition permite hasta 9.

## <a name="considerations"></a>Consideraciones

* Réplica solo de no más de una configuración por grupo de disponibilidad. 
* Una única réplica de configuración no puede ser una réplica principal.
* No se puede modificar el modo de disponibilidad de una única réplica de configuración. Para cambiar de una única réplica de configuración a una réplica secundaria sincrónica o asincrónica, quitar la única réplica de configuración y agregar una réplica secundaria con el modo de disponibilidad necesario. 
* Una única réplica de configuración está sincronizada con los metadatos del grupo de disponibilidad. No hay ningún dato de usuario. 
* Un grupo de disponibilidad con una réplica principal y la única réplica de una configuración, pero no hay ninguna réplica secundaria no es válido. 
* No se puede crear un grupo de disponibilidad en una instancia de SQL Server Express edition. 

<a name="pacemakerNotify"></a>

## <a name="understand-sql-server-resource-agent-for-pacemaker"></a>Comprender el agente de recursos de SQL Server para marcapasos

SQL Server de 2017 CTP 1.4 agrega `sequence_number` a `sys.availability_groups` para permitir marcapasos identificar el grado de actualización secundaria réplicas están con la réplica principal. `sequence_number` es un progresión BIGINT que representa el grado de actualización la réplica del grupo de disponibilidad local. Las actualizaciones de marcapasos el `sequence_number` con cada cambio de configuración del grupo de disponibilidad. Conmutación por error, adición de réplica o eliminación son ejemplos de cambios de configuración. El número se actualiza en el servidor principal, a continuación, replica en las réplicas secundarias. Por lo tanto, una réplica secundaria que tiene la configuración actualizada tiene el mismo número de secuencia que la réplica principal. 

Cuando decida marcapasos promocionar una réplica principal, en primer lugar envía una *previamente promover* notificación a todas las réplicas. Las réplicas devuelven el número de secuencia. A continuación, cuando realmente marcapasos intenta promover una réplica principal, la réplica solo promueve a sí mismo si su número de secuencia es el nivel más alto de todos los números de secuencia. Si su propio número de secuencia no coincide con el número de secuencia superior, la réplica rechaza la operación de promoción. De esta manera, solo se puede promover a principal la réplica con el número de secuencia más alto, lo que garantiza que no se producirá una pérdida de datos. 

Este proceso requiere al menos una réplica disponible para su promoción con el mismo número de secuencia que la réplica principal anterior. Los conjuntos de agente de recursos marcapasos `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` forma que al menos una réplica secundaria sincrónica está actualizada y disponible para ser el destino de conmutación automática por error de forma predeterminada. Con cada acción de supervisión, el valor de `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` es calculada (y actualiza si es necesario). El `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` valor es 'número de réplicas sincrónicas' dividido por 2. Durante la conmutación por error, se requiere el agente de recursos (`total number of replicas`  -  `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` réplicas) para responder a las previamente promover notificación. La réplica con el nivel más alto `sequence_number` promovido a principal. 

Por ejemplo, un grupo de disponibilidad con tres réplicas sincrónicas - una réplica principal y dos réplicas secundarias sincrónicas.

- `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` es 1; (3 / 2 -> 1).

- El número necesario de réplicas para responder para promover la acción previamente es 2. (3 - 1 = 2). 

En este escenario, dos réplicas tengan que responder para que la conmutación por error para que se desencadene. Para correcta conmutación automática por error tras una interrupción de la réplica principal, ambas réplicas secundarias deben actualizarse y responder a las previamente promover notificación. Si están en línea y sincrónico, tienen el mismo número de secuencia. El grupo de disponibilidad promociona uno de ellos. Si solo una de las réplicas secundarias responde a las previamente promover acción, el agente de recursos no puede garantizar que la base de datos secundaria que respondió tiene el sequence_number más alto y no se desencadena una conmutación por error.

>[!IMPORTANT]
>Cuando `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` es 0, existe riesgo de pérdida de datos. Durante una interrupción de la réplica principal, el agente de recursos desencadenará automáticamente una conmutación por error. Puede esperar para que el elemento primario recuperar o conmutar de forma manual usando `FORCE_FAILOVER_ALLOW_DATA_LOSS`.

Puede invalidar el comportamiento predeterminado y evitar que el recurso de grupo de disponibilidad configuración `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` automáticamente.

El siguiente script establece `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` en 0 en un grupo de disponibilidad denominado `<**ag1**>`. Antes de efectuar la ejecución, reemplace `<**ag1**>` por el nombre del grupo de disponibilidad.

```bash
sudo pcs resource update <**ag1**> required_synchronized_secondaries_to_commit=0
```

Para volver al valor predeterminado, en función de la configuración del grupo de disponibilidad ejecutar:

```bash
sudo pcs resource update <**ag1**> required_synchronized_secondaries_to_commit=
```

>[!NOTE]
>Al ejecutar los comandos anteriores, el servidor principal está temporalmente degradado a secundaria, a continuación, volver a promover. La actualización de recursos hace que todas las réplicas detener y reiniciar. El nuevo valor de`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` sólo se establece cuando se reinician las réplicas, no al instante.

## <a name="see-also"></a>Vea también

[Grupos de disponibilidad en Linux](sql-server-linux-availability-group-overview.md)

<!--Image references-->
[1]: ./media/sql-server-linux-availability-group-ha/1-read-scale-out.png
[2]: ./media/sql-server-linux-availability-group-ha/2-configuration-only.png
[3]: ./media/sql-server-linux-availability-group-ha/3-three-replica.png
[4]: ./media/sql-server-linux-availability-group-ha/configuration-only-example.png
