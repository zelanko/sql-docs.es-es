---
title: Replicación transaccional punto a punto | Microsoft Docs
ms.custom: ''
ms.date: 08/29/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- bidirectional replication
- transactional replication, bidirectional replication
- bidirectional transactional replication
- transactional replication, peer-to-peer replication
- peer-to-peer transactional replication
ms.assetid: 23e7e8c1-002f-4e69-8c99-d63e4100de64
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9513e58afc764fe8df5719ad03ac575a2632da6b
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52770087"
---
# <a name="peer-to-peer-transactional-replication"></a>Peer-to-Peer Transactional Replication
  La replicación punto a punto proporciona una solución escalada y de alta disponibilidad manteniendo copias de datos en varias instancias de servidor, también denominadas *nodos*. Generada en la base de replicación transaccional, la replicación punto a punto propaga transaccionalmente los cambios coherentes en tiempo casi real. Esto permite a las aplicaciones que requieran una escalada de las operaciones de lectura distribuir las lecturas de los clientes en varios nodos. Dado que los datos se mantienen en los nodos en tiempo casi real, la replicación punto a punto proporciona redundancia de datos, lo que aumenta la disponibilidad de los mismos.  
  
 Imagine una aplicación web. Ésta se puede beneficiar de la replicación punto a punto de las maneras siguientes:  
  
-   Las consultas del catálogo y otras lecturas se expanden por varios nodos. Esto permite que el rendimiento permanezca coherente conforme aumentan las lecturas.  
  
-   Si se produce un error en uno de los nodos del sistema, un nivel de aplicación puede redirigir las escrituras para dicho nodo a otro. Así se mantiene la disponibilidad.  
  
-   Si un nodo requiere el mantenimiento o el sistema completo requiere una actualización, cada nodo se puede tomar sin conexión y agregar de nuevo al sistema sin que se vea afectada la disponibilidad de la aplicación.  
  
 Aunque la replicación punto a punto habilita la escalada de las operaciones de lectura, el rendimiento de escritura para la topología es similar para un nodo único. Esto se debe a que en última instancia todas las inserciones, actualizaciones y eliminaciones se propagan a todos los nodos. La replicación reconoce cuándo se ha aplicado un cambio a un nodo determinado y evita cambios cíclicos en los nodos más de una vez. Se recomienda encarecidamente que las operaciones de escritura para cada fila se realicen en un solo nodo, por las razones siguientes:  
  
-   Si una fila se modifica en más de un nodo, puede producirse un conflicto o incluso la pérdida de una actualización cuando la fila se propaga a otros nodos.  
  
-   Siempre hay alguna latencia implicada cuando se replican los cambios. Para las aplicaciones que requieren que se vea el cambio más reciente inmediatamente, el equilibrio de carga dinámico de la aplicación en varios nodos puede ser problemático.  
  
 La replicación punto a punto incluye la opción de habilitar la detección de conflictos en una topología punto a punto. Esta opción ayuda a evitar problemas que se producen por conflictos no detectados, como comportamientos incoherentes de las aplicaciones y actualizaciones perdidas. Habilitando esta opción, de forma predeterminada, un cambio conflictivo se trata como un error crítico que produce el error del Agente de distribución. En caso de un conflicto, la topología permanece en un estado incoherente hasta que se resuelve el conflicto manualmente y los datos se hacen coherentes en toda la topología. Para más información, consulte [Conflict Detection in Peer-to-Peer Replication](peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).  
  
> [!NOTE]  
>  Para evitar la posible incoherencia de datos, asegúrese de evitar los conflictos en una topología punto a punto, incluso con la detección de conflictos habilitada. Para asegurarse de que las operaciones de escritura para una fila determinada se realizan en un solo nodo, las aplicaciones que tienen acceso y cambian datos deben particionar las operaciones de inserción, actualización y eliminación. Este particionamiento asegura que las modificaciones a una fila determinada que se originan en un nodo están sincronizadas con todos los demás nodos en la topología antes de que se modifique la fila por un nodo diferente. Si una aplicación requiere funcionalidades sofisticadas de detección y resolución de conflictos, use la replicación de mezcla. Para obtener más información, consulte [Replicación de mezcla](../merge/merge-replication.md) y [Detectar y solucionar conflictos de replicación de mezcla](../merge/advanced-merge-replication-resolve-merge-replication-conflicts.md).  
  
## <a name="peer-to-peer-topologies"></a>Topologías punto a punto  
 En los siguientes escenarios se ilustran los usos típicos de la replicación punto a punto.  
  
### <a name="topology-that-has-two-participating-databases"></a>Topología en la que participan dos bases de datos  
 ![Replicación punto a punto: dos nodos](../media/repl-multinode-01.gif "Replicación punto a punto: dos nodos")  
  
 En las ilustraciones anteriores se muestran dos bases de datos participantes, con tráfico de usuario dirigido a las bases de datos a través de un servidor de aplicaciones. Esta configuración se puede usar en varias aplicaciones, desde sitios web hasta aplicaciones de grupos de trabajo, y proporciona las siguientes ventajas:  
  
-   Rendimiento de lectura mejorado, porque las lecturas se reparten en dos servidores.  
  
-   Alta disponibilidad si se requiere mantenimiento o en caso de error en un nodo.  
  
 En ambas ilustraciones, la actividad de lectura tiene equilibrio de carga entre las bases de datos participantes, pero las actualizaciones se controlan de forma diferente:  
  
-   En la izquierda, las actualizaciones se particionan entre los dos servidores. Si la base de datos contiene un catálogo de productos, podría, por ejemplo, hacer que una aplicación personalizada dirija las actualizaciones al nodo **A** para los nombres de productos que empiecen con la letra A hasta la M y que dirija las actualizaciones al nodo **B** para los nombres de productos que empiecen con la letra N hasta la Z. Más tarde, las actualizaciones se replican en el otro nodo.  
  
-   A la derecha, todas las actualizaciones se dirigen al nodo **B**. Desde ahí, las actualizaciones se replican en el nodo **A**. Si **B** se encuentra en modo sin conexión (por ejemplo, por motivos de mantenimiento), el servidor de aplicaciones puede dirigir toda la actividad a **A**. Cuando **B** vuelve a estar en línea, las actualizaciones pueden pasar a él, y el servidor de aplicaciones puede mover todas las actualizaciones de vuelta al nodo **B** o seguir dirigiéndolas al nodo **A**.  
  
 La replicación punto a punto puede admitir este método, pero el ejemplo de actualización centralizada de la derecha también se utiliza frecuentemente con la replicación transaccional estándar.  
  
### <a name="topologies-that-have-three-or-more-participating-databases"></a>Topología en la que participan tres o más bases de datos  
 ![Replicación punto a punto en ubicaciones dispersas](../media/repl-multinode-02.gif "Replicación punto a punto en ubicaciones dispersas")  
  
 En la ilustración anterior se muestran tres bases de datos participantes que proporcionan datos para una organización de soporte de software internacional, con oficinas en Los Ángeles, Londres y Taipei. Los ingenieros de soporte de cada oficina reciben llamadas de clientes e incluyen y actualizan la información de las llamadas de los clientes. Las zonas horarias de las tres oficinas tienen una diferencia de ocho horas, por lo que no se superponen en la jornada laboral. Cuando la oficina de Taipei cierra, se abre la oficina de Londres. Si hay una llamada en curso cuando se cierra una oficina, la llamada se transfiere a un representante de la siguiente oficina abierta.  
  
 Cada ubicación tiene una base de datos y un servidor de aplicaciones, que los ingenieros de soporte utilizan para incluir y actualizar la información de las llamadas de los clientes. La topología se particiona por tiempo. Por consiguiente, las actualizaciones solo se producen en el nodo que está abierto; a continuación, las actualizaciones pasan al resto de bases de datos participantes. Esta topología proporciona las siguientes ventajas:  
  
-   Independencia sin aislamiento: Cada oficina puede insertar, actualizar, o eliminar datos de forma independiente, pero también puede compartir los datos porque se replican a todos los demás participantes bases de datos.  
  
-   Alta disponibilidad en caso de error o para permitir el mantenimiento en una o más de las bases de datos participantes.  
  
     ![Replicación punto a punto: tres y cuatro nodos](../media/repl-multinode-04.gif "Replicación punto a punto: tres y cuatro nodos")  
  
 La ilustración anterior muestra la adición de un nodo a la topología de tres nodos. Se podría agregar un nodo en este escenario por las razones siguientes:  
  
-   Porque se abre otra oficina.  
  
-   Para proporcionar mayor disponibilidad para admitir el mantenimiento o aumentar la tolerancia a errores si se produce un error de disco u otro error principal.  
  
 Observe que en ambas topologías de tres y cuatro nodos, todas las bases de datos publican y se suscriben a todas las demás bases de datos. Esto proporciona la máxima disponibilidad en caso de necesidades de mantenimiento o error de uno o más nodos. Al agregar nodos, se deben equilibrar las necesidades de disponibilidad y escalabilidad respecto al rendimiento y la complejidad de implementación y administración.  
  
## <a name="configuring-peer-to-peer-replication"></a>Configurar la replicación punto a punto  
 La configuración de una topología de replicación punto a punto es muy similar a la configuración de una serie de suscripciones y publicaciones transaccionales estándar. En los pasos descritos en los temas siguientes se muestra la configuración de un sistema de tres nodos, similar a la configuración mostrada a la izquierda en la ilustración anterior que muestra topología punto a punto.  
  
## <a name="considerations-for-using-peer-to-peer-replication"></a>Consideraciones para utilizar la replicación punto a punto  
 Esta sección proporciona información e instrucciones para tener en cuenta al usar la replicación punto a punto.  
  
### <a name="general-considerations"></a>Consideraciones generales  
  
-   La replicación punto a punto solo está disponible en las versiones Enterprise de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Todas las bases de datos que participan en la replicación punto a punto deberían contener datos y esquema idénticos:  
  
    -   Los nombres de objeto, esquema de objeto y nombres de publicación deberían ser idénticos.  
  
    -   Las publicaciones deben permitir la replicación de los cambios de esquema. (Este es un valor de **1** para la propiedad de publicación **replicate_ddl**, que es el valor predeterminado). Para obtener más información, vea [Make Schema Changes on Publication Databases](../publish/make-schema-changes-on-publication-databases.md) (Realizar cambios de esquema en bases de datos de publicaciones).  
  
    -   No se admite el filtrado de filas y columnas.  
  
-   Se recomienda que cada nodo use su propia base de datos de distribución. Esto elimina la posibilidad de tener un punto de error único.  
  
-   Las tablas y otros objetos no se pueden incluir en varias publicaciones punto a punto de una única base de datos de publicación.  
  
-   Debe habilitarse una publicación para la replicación punto a punto antes de crear las suscripciones.  
  
-   Las suscripciones se deben inicializar con una copia de seguridad o con la opción **'Solo compatibilidad con replicación'** . Para obtener más información, consulte [Initialize a Transactional Subscription Without a Snapshot](../initialize-a-transactional-subscription-without-a-snapshot.md).  
  
-   No se recomienda el uso de columnas de identidad. Cuando se utilizan identidades, se deben administrar manualmente los intervalos asignados a las tablas en cada base de datos participante. Para obtener más información, vea la sección sobre cómo asignar rangos para la administración manual de rangos de identidad en el tema [Replicar columnas de identidad](../publish/replicate-identity-columns.md).  
  
### <a name="feature-restrictions"></a>Restricciones de características  
 La replicación punto a punto admite las características principales de replicación transaccional pero no admite las opciones siguientes:  
  
-   Inicialización y reinicialización con una instantánea.  
  
-   Filtros de filas y columnas.  
  
-   Columnas de marca de tiempo.  
  
-   Suscriptores y publicadores que no son de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   Suscripciones de actualización inmediata y de actualización en cola.  
  
-   Suscripciones anónimas.  
  
-   Suscripciones parciales.  
  
-   Suscripciones adjuntables y suscripciones transformables (Ambas opciones han quedado desusadas en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]).  
  
-   Agentes de distribución compartidos.  
  
-   El parámetro **-SubscriptionStreams** del Agente de distribución y el parámetro **-MaxCmdsInTran**del Agente de registro del LOG.  
  
-   Las propiedades de artículo **@destination_owner** y **@destination_table**.  

-   La replicación transaccional punto a punto no admite la creación de una suscripción transaccional unidireccional para una publicación punto a punto.
  
 Las siguientes propiedades requieren consideraciones especiales:  
  
-   La propiedad de publicación **@allow_initialize_from_backup** requiere un valor de `true`.  
  
-   La propiedad de artículo **@replicate_ddl** requiere un valor de `true`; **@identityrangemanagementoption** requiere un valor de `manual`; y **@status** requiere que la opción **24** está establecido.  
  
-   El valor de las propiedades de artículo **@ins_cmd**, **@del_cmd**, y **@upd_cmd** no puede establecerse en `SQL`.  
  
-   La propiedad de suscripción **@sync_type** requiere un valor de `none` o `automatic`.  
  
### <a name="maintenance-considerations"></a>Consideraciones de mantenimiento  
 Las acciones siguientes exigen que se detenga el sistema. Esto significa que hay que detener la actividad de las tablas publicadas en todos los nodos y asegurarse de que cada nodo haya recibido todos los cambios de los demás nodos.  
  
-   Agregar un [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] nodo a una topología existente  
  
-   Agregar un artículo a una publicación existente  
  
-   Realizar cambios en el esquema  
  
-   Restaurar un nodo desde una copia de seguridad  
  
 Para obtener más información, consulte [Quiesce a Replication Topology &#40;Replication Transact-SQL Programming&#41;](../administration/quiesce-a-replication-topology-replication-transact-sql-programming.md) (Cómo detener una topología de replicación [programación de la replicación con Transact-SQL]) y [Administrar una topología punto a punto &#40;programación de la replicación con Transact-SQL&#41;](../administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md).  
  
-   Si agrega un nuevo nodo a una topología punto a punto, solo debe restaurar a partir de las copias de seguridad que se crearon una vez agregado el nuevo nodo.  
  
-   No puede reinicializar las suscripciones en una topología punto a punto. Si tiene que asegurarse de que un nodo tiene una copia nueva de los datos, restaure una copia de seguridad en el nodo.  
  
## <a name="see-also"></a>Vea también  
 [Administrar una topología punto a punto &#40;programación de la replicación con Transact-SQL&#41;](../administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)   
 [Estrategias para hacer copias de seguridad y restaurar replicación de instantáneas o replicación transaccional](../administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md)   
 [Tipos de publicaciones para la replicación transaccional](publication-types-for-transactional-replication.md)  
  
  
