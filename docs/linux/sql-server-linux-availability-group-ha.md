---
title: "SQL Server Always On patrones de implementación del grupo de disponibilidad | Documentos de Microsoft"
ms.custom: 
ms.date: 06/16/2017
ms.prod: sql-linux
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: edd75f68-dc62-4479-a596-57ce8ad632e5
caps.latest.revision: 34
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 8e2d26fd9ce79fc8c47c7499313648d565ae1b97
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---

# <a name="high-availability-and-data-protection-for-availability-group-configurations"></a>Alta disponibilidad y protección de datos para las configuraciones de grupo de disponibilidad

Este artículo presenta las configuraciones de implementación admitido para grupos de disponibilidad AlwaysOn de SQL Server en servidores Linux. Un grupo de disponibilidad admite alta disponibilidad y protección de datos. Detección de errores automática, conmutación por error automática y transparente reconexión después de la conmutación por error proporcionan alta disponibilidad. Las réplicas sincronizadas proporcionan protección de datos. 

>[!NOTE]
>Además de alta disponibilidad y protección de datos, un grupo de disponibilidad también puede proporcionar recuperación ante desastres, migración de plataforma entre y escalado horizontal de lectura. En este artículo se aborda principalmente las implementaciones de alta disponibilidad y protección de datos. 

Con Windows Server conmutación por error, una configuración común para alta disponibilidad usa dos réplicas sincrónicas y un [recurso compartido de archivos testigo](http://technet.microsoft.com/library/cc731739.aspx). El testigo de recurso compartido de archivos valida la configuración del grupo de disponibilidad - estado de sincronización y el rol de la réplica, por ejemplo. Esta configuración garantiza que la réplica secundaria que se elige como el destino de conmutación por error tiene los datos más recientes y los cambios de configuración de grupo de disponibilidad. 

Las soluciones de alta disponibilidad actual de Linux no se ajustan a un testigo externo como el testigo de recurso compartido de archivos en un clúster de conmutación por error de Windows Server. Cuando no hay ningún clúster de conmutación por error de Windows Server, la configuración del grupo de disponibilidad se almacena en la base de datos maestra en participantes instancias de SQL Server. Por lo tanto, el grupo de disponibilidad requiere al menos tres réplicas sincrónicas para alta disponibilidad y protección de datos. Después de crear un grupo de disponibilidad en servidores Linux, cree un recurso de clúster. La configuración de recursos de clúster determina la configuración de alta disponibilidad.

Elija un diseño de grupo de disponibilidad para satisfacer los requisitos empresariales específicos para alta disponibilidad y protección de datos y escalado horizontal de lectura.

>[!IMPORTANT]
>Las configuraciones siguientes describen los patrones de diseño del grupo de disponibilidad y las capacidades de cada patrón. Estos modelos de diseño que se aplican a los grupos de disponibilidad con `CLUSTER_TYPE = EXTERNAL` para soluciones de alta disponibilidad. 

Los patrones de diseño son dos configuraciones de grupo de disponibilidad. Las configuraciones incluyen:

- **Tres réplicas sincrónicas.**

- **Dos réplicas sincrónicas.**

## <a name="how-the-configuration-affects-default-resource-settings"></a>Cómo afecta la configuración a la configuración predeterminada de los recursos

La configuración de recurso de clúster `required_synchronized_secondaries_to_commit` garantiza que cada transacción se escribe en un número mínimo de registros de la réplica secundaria antes de confirmar la transacción en la réplica principal. Esta configuración puede afectar a alta disponibilidad y protección de datos, dependiendo de la configuración. Cuando se instala el agente de recursos de SQL Server - `mssql-server-ha` - y crear un recurso de clúster para el grupo de disponibilidad, el Administrador de clústeres detecta la disponibilidad del grupo Configuración y conjuntos de `required_synchronized_secondaries_to_commit` en consecuencia. 

Si se admite la configuración, el parámetro de agente de recurso `required_synchronized_secondaries_to_commit` se establece en el valor que proporciona alta disponibilidad y protección de datos. Para obtener más información, consulte [comprender Agente SQL Server del recurso para marcapasos](#pacemakerNotify).

Las siguientes secciones explican el comportamiento predeterminado para el recurso de clúster. 

<a name="threeSynch"></a>

## <a name="three-synchronous-replicas"></a>Tres réplicas sincrónicas.

Esta configuración se compone de tres réplicas sincrónicas. De forma predeterminada, proporciona alta disponibilidad y protección de datos. También puede proporcionar escalabilidad lectura.

![Tres réplicas][3]

En la tabla siguiente describe el comportamiento de protección alto de un disponibilidad y los datos según la configuración de un grupo de disponibilidad con tres réplicas sincrónicas: 

|`required_synchronized_secondaries_to_commit`|0 |1 \*|2
| --- |:---:|:---:|:---:
|Conmutación automática por error después de la interrupción de la réplica principal| |✔| 
|Réplica principal está disponible después de una interrupción de la réplica secundaria|✔|✔| 
|Réplica principal está disponible después de dos de las interrupciones de réplica secundaria|✔| |
|Conmutación por error manual después de la interrupción de la réplica principal - posible pérdida de datos|✔| | 

\*Valor al grupo de disponibilidad se agrega como un recurso en un clúster predeterminado.

<a name="twoSynch"></a>

## <a name="two-synchronous-replicas"></a>Dos réplicas sincrónicas.

Esta configuración habilita la protección de datos. Al igual que las otras configuraciones de grupo disponibilidad, puede habilitar la lectura de escalabilidad horizontal. La configuración de dos réplicas sincrónicas no proporciona alta disponibilidad automática. 

![Dos réplicas sincrónicas.][1]

Esta configuración requiere dos servidores. Estos servidores asumir el rol de réplica principal y secundaria. 

La configuración de dos réplicas sincrónicas está optimizada para datos de protección y la distribución de la carga de trabajo de lectura para las bases de datos. De forma predeterminada, el recurso está configurado para la protección de datos. Esta configuración no proporciona alta disponibilidad porque si se produce un error en alguna de las instancias de SQL Server, la base de datos no está totalmente disponible o no hay riesgo de pérdida de datos. 

En la tabla siguiente describe el comportamiento de protección de datos según los valores posibles para un grupo de disponibilidad con dos réplicas sincrónicas: 

|`required_synchronized_secondaries_to_commit`|0 \*|1 
| --- |:---|:---
|Conmutación automática por error después de la interrupción de la réplica principal| |✔ \*\* | 
|Réplica principal está disponible después de la interrupción de la réplica secundaria|✔| |

\*Valor al grupo de disponibilidad se agrega como un recurso en un clúster predeterminado.

\*\*En esta configuración, después de la interrupción de la réplica principal del grupo de disponibilidad automática que se conmuta por error. Las aplicaciones no se pueden conectar al grupo de disponibilidad hasta que la réplica principal está en línea - ahora como una réplica secundaria. 

La configuración de dos réplicas sincrónicas puede ser más económica porque solo requiere dos instancias de SQL Server en dos servidores.

<a name="pacemakerNotify"></a>

## <a name="understand-sql-server-resource-agent-for-pacemaker"></a>Comprender el agente de recursos de SQL Server para marcapasos

SQL Server de 2017 CTP 1.4 agrega `sequence_number` a `sys.availability_groups` para permitir marcapasos identificar el grado de actualización secundaria réplicas están con la réplica principal. `sequence_number`es un progresión BIGINT que representa el grado de actualización la réplica del grupo de disponibilidad local. Las actualizaciones de marcapasos el `sequence_number` con cada cambio de configuración del grupo de disponibilidad. Conmutación por error, adición de réplica o eliminación son ejemplos de cambios de configuración. El número se actualiza en el servidor principal, a continuación, replica en las réplicas secundarias. Por lo tanto, una réplica secundaria que tiene la configuración actualizada tiene el mismo número de secuencia que la réplica principal. 

Cuando decida marcapasos promocionar una réplica principal, en primer lugar envía una *previamente promover* notificación a todas las réplicas. Las réplicas devuelven el número de secuencia. A continuación, cuando realmente marcapasos intenta promover una réplica principal, la réplica solo promueve a sí mismo si su número de secuencia es el nivel más alto de todos los números de secuencia. Si su propio número de secuencia no coincide con el número de secuencia superior, la réplica rechaza la operación de promoción. De esta manera, solo se puede promover a principal la réplica con el número de secuencia más alto, lo que garantiza que no se producirá una pérdida de datos. 

Este proceso requiere al menos una réplica disponible para su promoción con el mismo número de secuencia que la réplica principal anterior. Los conjuntos de agente de recursos marcapasos `required_synchronized_secondaries_to_commit` forma que al menos una réplica secundaria sincrónica está actualizada y disponible para ser el destino de conmutación automática por error de forma predeterminada. Con cada acción de supervisión, el valor de `required_synchronized_secondaries_to_commit` es calculada (y actualiza si es necesario). El `required_synchronized_secondaries_to_commit` valor es 'número de réplicas sincrónicas' dividido por 2. Durante la conmutación por error, se requiere el agente de recursos (`total number of replicas`  -  `required_synchronized_secondaries_to_commit` réplicas) para responder a las previamente promover notificación. La réplica con el nivel más alto `sequence_number` promovido a principal. 

Por ejemplo, un grupo de disponibilidad con tres réplicas sincrónicas - una réplica principal y dos réplicas secundarias sincrónicas.

- `required_synchronized_secondaries_to_commit`es 1; (3 / 2 -> 1).

- El número necesario de réplicas para responder para promover la acción previamente es 2. (3 - 1 = 2). 

En este escenario, dos réplicas tengan que responder para que la conmutación por error para que se desencadene. Para correcta conmutación automática por error tras una interrupción de la réplica principal, ambas réplicas secundarias deben actualizarse y responder a las previamente promover notificación. Si están en línea y sincrónico, tienen el mismo número de secuencia. El grupo de disponibilidad promociona uno de ellos. Si solo una de las réplicas secundarias responde a las previamente promover acción, el agente de recursos no puede garantizar que la base de datos secundaria que respondió tiene el sequence_number más alto y no se desencadena una conmutación por error.

>[!IMPORTANT]
>Cuando `required_synchronized_secondaries_to_commit` es ahí 0 es el riesgo de pérdida de datos. Durante una interrupción de la réplica principal, el agente de recursos desencadenará automáticamente una conmutación por error. Puede esperar para que el elemento primario recuperar o conmutar de forma manual usando `FORCE_FAILOVER_ALLOW_DATA_LOSS`.

Puede invalidar el comportamiento predeterminado y evitar que el recurso de grupo de disponibilidad configuración `required_synchronized_secondaries_to_commit` automáticamente.

El siguiente script establece `required_synchronized_secondaries_to_commit` en 0 en un grupo de disponibilidad denominado `<**ag1**>`. Antes de ejecutar reemplazar `<**ag1**>` con el nombre del grupo de disponibilidad.

```bash
sudo pcs resource update <**ag1**> required_synchronized_secondaries_to_commit=0
```

Para volver al valor predeterminado, en función de la configuración del grupo de disponibilidad ejecutar:

```bash
sudo pcs resource update <**ag1**> required_synchronized_secondaries_to_commit=
```

>[!NOTE]
>Al ejecutar los comandos anteriores, el servidor principal está temporalmente degradado a secundaria, a continuación, volver a promover. La actualización de recursos hace que todas las réplicas detener y reiniciar. El nuevo valor de`required_synchronized_secondaries_to_commit` sólo se establece cuando se reinician las réplicas, no al instante.

<!--Image references-->
[1]: ./media/sql-server-linux-availability-group-ha/1-read-scale-out.png
[3]: ./media/sql-server-linux-availability-group-ha/3-three-replica.png
