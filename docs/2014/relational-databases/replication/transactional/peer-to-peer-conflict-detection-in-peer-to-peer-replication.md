---
title: Detección de conflictos en la replicación punto a punto | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- transactional replication, peer-to-peer replication
- peer-to-peer transactional replication, conflict detection
ms.assetid: 754a1070-59bc-438d-998b-97fdd77d45ca
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 03a7640f95242538d01c8f135a005729b15042b5
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52813977"
---
# <a name="conflict-detection-in-peer-to-peer-replication"></a>Detección de conflictos en la replicación punto a punto
  La replicación transaccional punto a punto permite insertar, actualizar o eliminar datos en cualquier nodo de una topología y propagar los cambios de los datos a los demás nodos. Dado que se pueden cambiar los datos de cualquier nodo, podrían producirse conflictos entre los datos modificados en los distintos nodos. Si una fila se modifica en más de un nodo, puede producirse un conflicto o incluso la pérdida de una actualización cuando la fila se propaga a otros nodos.  
  
 La replicación punto a punto de [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] y versiones posteriores ofrece la posibilidad de habilitar la detección de conflictos en una topología punto a punto. Esta opción contribuye a evitar los problemas causados por los conflictos no detectados, como son el comportamiento incoherente de las aplicaciones y las actualizaciones perdidas. Cuando se habilita esta opción, de forma predeterminada, un cambio conflictivo se trata como un error crítico que produce el error del Agente de distribución. En caso de conflicto, la topología permanece en un estado incoherente hasta que se resuelve el conflicto y se restablece la coherencia de los datos en toda la topología.  
  
> [!NOTE]  
>  Para evitar la posible incoherencia de datos, asegúrese de evitar los conflictos en una topología punto a punto, incluso con la detección de conflictos habilitada. Para asegurarse de que las operaciones de escritura para una fila determinada se realizan en un solo nodo, las aplicaciones que tienen acceso y cambian datos deben particionar las operaciones de inserción, actualización y eliminación. Este particionamiento asegura que las modificaciones introducidas en una fila determinada que se originan en un nodo se sincronizan con todos los demás nodos de la topología antes de que se modifique la fila en otro nodo. Si una aplicación requiere funcionalidades sofisticadas de detección y resolución de conflictos, use la replicación de mezcla. Para obtener más información, consulte [Replicación de mezcla](../merge/merge-replication.md) y [Detectar y solucionar conflictos de replicación de mezcla](../merge/advanced-merge-replication-resolve-merge-replication-conflicts.md).  
  
## <a name="understanding-conflicts-and-conflict-detection"></a>Descripción de los conflictos y de la detección de conflictos  
 En una única base de datos, los cambios realizados en la misma fila por parte de aplicaciones diferentes no provocan conflictos. Esto se debe a que las transacciones se serializan y se utilizan bloqueos para controlar los cambios simultáneos. En un sistema distribuido asincrónico, como en uno de replicación punto a punto, las transacciones se producen de forma independiente en cada nodo, y no hay ningún mecanismo para serializarlas por los distintos nodos. Se podría usar una confirmación en dos fases de tipo protocolo, pero esto afecta de forma significativa al rendimiento.  
  
 En sistemas como la replicación punto a punto, los conflictos no se detectan cuando los cambios se confirman en cada uno de los nodos del mismo nivel. En su lugar, se detectan al replicar los cambios y aplicarlos a los demás nodos del mismo nivel. En la replicación punto a punto, los conflictos se detectan mediante los procedimientos almacenados que aplican los cambios a cada nodo, basándose en una columna oculta de cada tabla publicada. En esta columna oculta, se almacena un identificador que combina la versión de la fila con un *identificador de originador* que se especifica para cada nodo. Durante la sincronización, el Agente de distribución ejecuta los procedimientos para cada tabla. Estos procedimientos aplican las operaciones de inserción, actualización y eliminación procedentes de los demás nodos del mismo nivel. Si uno de los procedimientos detecta un conflicto cuando lee el valor de la columna oculta, genera el error 22815 que tiene un nivel de gravedad de 16:  
  
 `A conflict of type '%s' was detected at peer %d between peer %d (incoming), transaction id %s  and peer %d (on disk), transaction id %s`  
  
 Este error hace que, de forma predeterminada, el Agente de distribución deje de aplicar cambios a ese nodo. Para obtener información sobre cómo tratar los conflictos detectados, vea "Controlar los conflictos" más adelante en este tema.  
  
> [!NOTE]  
>  Solo pueden tener acceso a la columna oculta los usuarios que hayan iniciado una sesión a través de la conexión de administrador dedicada (DAC). Para obtener más información sobre DAC, vea [Conexión de diagnóstico para administradores de bases de datos](../../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md).  
  
 La replicación punto a punto detecta los tipos de conflictos siguientes:  
  
-   Inserción-inserción  
  
     Todas las filas de cada tabla que participa en una replicación punto a punto se identifican de forma exclusiva mediante valores de clave principal. Se produce un conflicto de inserción-inserción al insertar una fila con el mismo valor de clave en más de un nodo.  
  
-   Actualización-actualización  
  
     Se produce cuando se actualiza la misma fila en más de un nodo.  
  
-   Inserción-actualización  
  
     Se produce cuando se actualiza una fila en un nodo, pero la misma fila se ha eliminado y, a continuación, se ha vuelto a insertar en otro nodo.  
  
-   Inserción-eliminación  
  
     Se produce cuando se elimina una fila en un nodo, pero la misma fila se ha eliminado y, a continuación, se ha vuelto a insertar en otro nodo.  
  
-   Actualización-eliminación  
  
     Se produce cuando se actualiza una fila en un nodo, pero la misma fila se ha eliminado en otro nodo.  
  
-   Eliminación-eliminación  
  
     Se produce cuando se elimina una fila en más de un nodo.  
  
## <a name="enabling-conflict-detection"></a>Habilitar la detección de conflictos  
 Para utilizar la detección de conflictos, todos los nodos deben estar ejecutando [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] o una versión posterior, y debe haberse habilitado la detección para todos los nodos. De forma predeterminada, en [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] y versiones posteriores, la detección de conflictos está habilitada en [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]. Se recomienda tener habilitada la detección, incluso en escenarios en los que no se espere ningún conflicto. La detección de conflictos se puede habilitar y deshabilitar utilizando [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] o procedimientos almacenados de [!INCLUDE[tsql](../../../includes/tsql-md.md)] :  
  
-   Puede habilitar y deshabilitar la detección en [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] mediante la página **Opciones de suscripción** del cuadro de diálogo **Propiedades de la publicación** o con la página **Configurar topología** del Asistente de configuración de la topología punto a punto.  
  
     Si configura la detección de conflictos mediante [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)], el Agente de distribución se configura para que deje de aplicar cambios cuando se detecte un conflicto.  
  
-   También puede habilitar y deshabilitar la detección con los procedimientos almacenados siguientes: [sp_addpublication](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql) o [sp_configure_peerconflictdetection](/sql/relational-databases/system-stored-procedures/sp-configure-peerconflictdetection-transact-sql).  
  
     Si configura la detección de conflictos mediante procedimientos almacenados, puede especificar si el Agente de distribución debe dejar de aplicar cambios cuando se detecte un conflicto. La configuración predeterminada hace que el agente se detenga. Se recomienda utilizar la configuración predeterminada.  
  
## <a name="handling-conflicts"></a>Controlar los conflictos  
 Cuando se produce un conflicto en la replicación punto a punto, se genera la alerta de detección de conflictos punto a punto. Se recomienda configurar esta alerta para que se notifique la existencia de conflictos. Para obtener más información sobre las alertas, vea [Usar alertas para eventos del Agente de replicación](../agents/use-alerts-for-replication-agent-events.md).  
  
 Una vez que se detenga el Agente de distribución y se genere la alerta, use uno de los métodos siguientes para controlar los conflictos existentes:  
  
-   Reinicialice el nodo en el que se detectó el conflicto a partir de la copia de seguridad de un nodo que contenga los datos necesarios (este es el enfoque recomendado). Este método garantiza que los datos sean coherentes.  
  
-   Intente sincronizar de nuevo el nodo permitiendo que el Agente de distribución continúe aplicando los cambios:  
  
    1.  Ejecutar [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql): especifique 'p2p_continue_onconflict' para el @property parámetro y `true` para el @value parámetro.  
  
    2.  Reinicie el Agente de distribución.  
  
    3.  Use el visor de conflictos para comprobar los conflictos detectados y determine las filas afectadas, el tipo de conflicto y la fila ganadora. El conflicto se resuelve en función del valor del identificador de originador que se especificó durante la configuración: la fila procedente del nodo con el identificador más alto gana el conflicto. Para obtener más información, vea [Ver conflictos de datos para publicaciones transaccionales &#40;SQL Server Management Studio&#41;](../view-data-conflicts-for-transactional-publications-sql-server-management-studio.md).  
  
    4.  Ejecute la validación para asegurarse de que las filas en conflicto convergieron correctamente. Para obtener más información, vea [Validar datos replicados](../validate-replicated-data.md).  
  
        > [!NOTE]  
        >  Si los datos son incoherentes después de este paso, debe actualizar manualmente las filas en el nodo que tenga la prioridad más alta y, a continuación, dejar que se propaguen los cambios desde ese nodo. Si no hay ningún otro conflicto relacionado con los cambios en la topología, todos los nodos se encontrarán en un estado coherente.  
  
    5.  Ejecutar [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql): especifique 'p2p_continue_onconflict' para el @property parámetro y `false` para el @value parámetro.  
  
## <a name="see-also"></a>Vea también  
 [Peer-to-Peer Transactional Replication](peer-to-peer-transactional-replication.md)  
  
  
