---
title: "Filtros de fila con par&#225;metros | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "publicaciones [replicación de SQL Server], filtros dinámicos"
  - "replicación de mezcla [replicación de SQL Server], filtros dinámicos"
  - "filtros con parámetros [replicación de SQL Server]"
  - "filtros [replicación de SQL Server], dinámicos"
  - "filtros con parámetros de replicación de mezcla [replicación de SQL Server]"
  - "publicaciones [replicación de SQL Server], filtros parametrizados"
  - "filtros parametrizados [replicación de SQL Server], sobre los filtros parametrizados"
  - "filtros [replicación de SQL Server], con parámetros"
  - "filtros dinámicos [replicación de SQL Server]"
ms.assetid: b48a6825-068f-47c8-afdc-c83540da4639
caps.latest.revision: 69
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Filtros de fila con par&#225;metros
  Los filtros de filas con parámetros permiten enviar diferentes particiones de datos a diferentes suscriptores sin necesidad de crear varias publicaciones (los filtros con parámetros se denominaban filtros dinámicos en versiones anteriores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]). Una partición es un subconjunto de filas de una tabla; dependiendo de la configuración elegida al crear un filtro de filas con parámetros, cada fila de una tabla publicada puede pertenecer a una sola partición (lo que produce particiones no superpuestas) o a dos o más particiones (lo que produce particiones superpuestas).  
  
 Las particiones no superpuestas se pueden compartir entre varias suscripciones o restringirse de forma que solo una suscripción reciba una partición determinada. La configuración que controla el comportamiento de la partición se describe en "Usar las opciones de filtrado apropiadas" más adelante en este tema. Con esta configuración, puede adaptar los filtros con parámetros a los requisitos de rendimiento y de la aplicación. En general, las particiones superpuestas proporcionan un mayor grado de flexibilidad, mientras que las particiones no superpuestas replicadas en una sola suscripción proporcionan un mejor rendimiento.  
  
 Los filtros con parámetros se utilizan en una sola tabla y generalmente se combinan con filtros de combinación para extender el filtrado a las tablas relacionadas. Para más información, vea [Join Filters](../../../relational-databases/replication/merge/join-filters.md).  
  
 Para definir o modificar un filtro de fila con parámetros, vea [Define and Modify a Parameterized Row Filter for a Merge Article](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md).  
  
## Cómo funcionan los filtros con parámetros  
 Un filtro de fila con parámetros utiliza una cláusula WHERE para seleccionar los datos apropiados para publicar. En vez de especificar un valor literal en la cláusula (como ocurre con un filtro de fila estático), se especifica una o las dos funciones del sistema siguientes: SUSER_SNAME() y HOST_NAME(). También se pueden utilizar funciones definidas por el usuario, pero deben incluir SUSER_SNAME() o HOST_NAME() en el cuerpo de la función, o evaluar una de estas funciones del sistema (como `MyUDF(SUSER_SNAME()`). Si una función definida por el usuario incluye SUSER_SNAME() o HOST_NAME() en el cuerpo de la función, no se pueden pasar parámetros a la función.  
  
 Las funciones del sistema SUSER_SNAME() y HOST_NAME() no son específicas para la replicación de mezcla, pero la replicación de mezcla las utiliza para el filtrado con parámetros:  
  
-   SUSER_SNAME() devuelve información de inicio de sesión para las conexiones establecidas con una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Cuando se utiliza en un filtro con parámetros, devuelve el inicio de sesión que utiliza el Agente de mezcla para conectarse al publicador (el inicio de sesión se especifica al crear una suscripción).  
  
-   HOST_NAME() devuelve el nombre del equipo que se está conectando a una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Cuando se utiliza en un filtro con parámetros, devuelve de manera predeterminada el nombre del equipo en el que se está ejecutando el Agente de mezcla. Para las suscripciones de extracción, es el nombre del suscriptor, y para las suscripciones de inserción, es el nombre del distribuidor.  
  
     También es posible anular esta función con un valor distinto del nombre del suscriptor o el distribuidor. Generalmente, las aplicaciones invalidan esta función con valores más significativos, como el nombre o el indentificador de un vendedor. Para obtener más información, vea la sección "Invalidar el valor de HOST_NAME_NAME()" en este mismo tema.  
  
 El valor que devuelve la función del sistema se compara con la columna especificada en la tabla que está filtrando y se descargan los datos apropiados al suscriptor. Esta comparación se lleva a cabo al inicializar la suscripción (para que la instantánea inicial contenga únicamente los datos correctos) y cada vez que se sincroniza la suscripción. De forma predeterminada, si se produce un cambio en el publicador en una fila que se mueven fuera de una partición, se elimina la fila en el suscriptor (este comportamiento se controla mediante la **@allow_partition_realignment** parámetro de [sp_addmergepublication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)).  
  
> [!NOTE]  
>  Cuando se realizan comparaciones para los filtros con parámetros, se utiliza siempre la intercalación de base de datos. Por ejemplo, si la intercalación de base de datos no distingue entre mayúsculas y minúsculas, pero la intercalación de tabla o columna sí lo hace, la comparación no distinguirá entre mayúsculas y minúsculas.  
  
### Filtrar con SUSER_SNAME()  
 Considere la **tabla Employee** en la base de datos de ejemplo [!INCLUDE[ssSampleDBCoShort](../../../includes/sssampledbcoshort-md.md)] . Esta tabla incluye la columna **IdDeInicioDeSesión**, que contiene el inicio de sesión de cada empleado en el formulario '*domain\login*'. Para filtrar esta tabla con el fin de que los empleados reciban únicamente los datos relacionados con ellos, especifique la cláusula de filtro:  
  
```  
LoginID = SUSER_SNAME()  
```  
  
 Por ejemplo, el valor para uno de los empleados es 'adventure-works\john5'. Cuando el Agente de mezcla se conecta al publicador, utiliza el nombre de inicio de sesión especificado al crear la suscripción (en este caso, 'adventure-works\john5'). El agente de mezcla, a continuación, compara el valor devuelto por SUSER_SNAME () en los valores de la tabla y descarga únicamente la fila que contiene un valor de 'adventure-works\john5' en el **IdDeInicioDeSesión** columna.  
  
### Filtrar con HOST_NAME()  
 Considere la tabla **HumanResources.Employee** . Suponga que esta tabla contiene una columna como **nombreDeEquipo** con el nombre de equipo de cada empleado en el formulario '*nombre_tipodeequipo*'. Para filtrar esta tabla con el fin de que los empleados reciban únicamente los datos relacionados con ellos, especifique la cláusula de filtro:  
  
```  
ComputerName = HOST_NAME()  
```  
  
 Por ejemplo, el valor de uno de los empleados podría ser 'john5_laptop'. Cuando el agente de mezcla se conecta al publicador, compara el valor devuelto por HOST_NAME () en los valores de la tabla y descarga únicamente la fila que contiene un valor de 'john5_laptop' en el **nombreDeEquipo** columna.  
  
 También puede combinar las funciones en un filtro. Por ejemplo, si desea asegurarse de que un empleado reciba datos solamente cuando utilice su nombre de inicio de sesión en su equipo, la cláusula de filtro podría ser:  
  
```  
LoginID = SUSER_SNAME() AND ComputerName = HOST_NAME()  
```  
  
 A menos que vaya a reemplazar el valor de HOST_NAME(), el filtrado con HOST_NAME() solamente se suele utilizar con suscripciones de extracción. El valor que devuelve la función es el nombre del equipo en el que se está ejecutando el Agente de mezcla. Para las suscripciones de extracción, el valor es diferente para cada suscripción, pero para las suscripciones de inserción, el valor es el mismo (todos los agentes de mezcla se ejecutan en el distribuidor para las suscripciones de inserción).  
  
> [!IMPORTANT]  
>  El valor de la función HOST_NAME() se puede reemplazar; por lo tanto, no es posible utilizar filtros que incluyan HOST_NAME() para controlar el acceso a particiones de datos. Para controlar el acceso a particiones de datos, utilice SUSER_SNAME(), SUSER_SNAME() en combinación con HOST_NAME(), o utilice filtros de fila estáticos.  
  
#### Reemplazar el valor de HOST_NAME()  
 Como se indicó anteriormente, HOST_NAME() devuelve, de manera predeterminada, el nombre del equipo que se está conectando a una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Cuando se utilizan filtros con parámetros, es frecuente reemplazar este valor con otro suministrado al crear una suscripción. A continuación, la función HOST_NAME() devuelve el valor que se ha especificado en vez del nombre del equipo.  
  
> [!NOTE]  
>  Si reemplaza HOST_NAME(), todas las llamadas a la función HOST_NAME() devolverán el valor especificado. Asegúrese de que otras aplicaciones no dependen de HOST_NAME() al devolver el nombre del equipo.  
  
 Considere la tabla **HumanResources.Employee** . Esta tabla incluye la columna **EmployeeID**. Para filtrar esta tabla con el fin de que cada empleado reciba únicamente los datos relacionados con él, especifique la cláusula de filtro:  
  
 `EmployeeID = CONVERT(int,HOST_NAME())`  
  
 Por ejemplo, a la empleada Pamela Ansman-Wolfe se le ha asignado el identificador 280. Especifique el valor de identificador de empleado (280 en este ejemplo) como valor de HOST_NAME() al crear una suscripción para esta empleada. Cuando el agente de mezcla se conecta al publicador, compara el valor devuelto por HOST_NAME () en los valores de la tabla y descarga únicamente la fila que contiene un valor de 280 en la **EmployeeID** columna.  
  
> [!IMPORTANT]  
>  La función HOST_NAME () devuelve un **nchar** valor, lo que debe usar CONVERT si la columna en la cláusula de filtro es de un tipo de datos numéricos, como en el ejemplo anterior. Por motivos de rendimiento, se recomienda no aplicar funciones a los nombres de columna en las cláusulas de los filtros de fila con parámetros, como `CONVERT(nchar,EmployeeID) = HOST_NAME()`. En su lugar, se recomienda usar el método que se muestra en el ejemplo: `EmployeeID = CONVERT(int,HOST_NAME())`. Esta cláusula se puede usar para la **@subset_filterclause** parámetro de [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md), pero normalmente no se puede usar el Asistente para nueva publicación (la cláusula de filtro para validarlo, que produce un error porque no se puede convertir el nombre del equipo que ejecuta el Asistente una **int**). Si utiliza el Asistente para nueva publicación, se recomienda especificar `CONVERT(nchar,EmployeeID) = HOST_NAME()` en el asistente y después usar [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) para cambiar la cláusula `EmployeeID = CONVERT(int,HOST_NAME())` antes de crear una instantánea para la publicación.  
  
 **Para reemplazar el valor de HOST_NAME()**  
  
 Utilice uno de los métodos siguientes para reemplazar el valor de HOST_NAME():  
  
-   [! INCLUIR [ssManStudioFull] (.. / Token/ssManStudioFull_md.md)]: specify a value on the **HOST\_NAME\(\) Values** page of the New Subscription Wizard. For more information about creating subscriptions, see [Subscribe to Publications](../../../relational-databases/replication/subscribe-to-publications.md).  
  
-   Replicación [!INCLUDE[tsql](../../../includes/tsql-md.md)] de programación: especifique un valor para el **@hostname** parámetro de [sp_addmergesubscription & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md) (para suscripciones de inserción) o [sp_addmergepullsubscription_agent & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md) (para suscripciones de extracción).  
  
-   El agente de mezcla: especifique un valor para el **- Hostname** parámetro en la línea de comandos o a través de un perfil de agente. Para obtener más información acerca del Agente de mezcla, vea [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md). Para obtener más información acerca de los perfiles de agente, vea [Replication Agent Profiles](../../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
## Inicializar una suscripción a una publicación con filtros con parámetros  
 Cuando se utilizan filtros de fila con parámetros en las publicaciones de combinación, la replicación inicializa cada suscripción con una instantánea en dos partes. Para más información, consulte [Snapshots for Merge Publications with Parameterized Filters](../../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md).  
  
## Usar las opciones de filtrado apropiadas  
 Hay dos áreas clave que puede controlar cuando se utilizan filtros con parámetros:  
  
-   Cómo procesa los filtros la replicación de mezcla, que se controla con una de las dos opciones de publicación siguientes: **use partition groups** y **keep partition changes**.  
  
-   Cómo se comparten los datos entre los suscriptores, que debe reflejarse en la opción de artículo **partition options**(opciones de partición).  
  
 Para establecer opciones de filtrado, vea [Optimize Parameterized Row Filters](../../../relational-databases/replication/publish/optimize-parameterized-row-filters.md).  
  
### Configurar 'use partition groups' y 'keep partition changes'  
 Las opciones **use partition groups** y **keep partition changes** mejoran el rendimiento de la sincronización para las publicaciones con artículos filtrados, ya que almacenan metadatos adicionales en la base de datos de publicaciones. La opción **use partition groups** proporciona una mayor mejora en el rendimiento mediante la característica de particiones precalculadas. Esta opción se establece de manera predeterminada en **true** si los artículos de la publicación cumplen una serie de requisitos. Para obtener más información acerca de estos requisitos, consulte [optimizar el rendimiento de filtro con parámetros con particiones precalculadas](../../../relational-databases/replication/merge/optimize-parameterized-filter-performance-with-precomputed-partitions.md). Si los artículos no cumplen los requisitos para usar particiones precalculadas, se establecerá la opción **keep partition changes** en **true**.  
  
### Configurar 'partition options'  
 Al crear un artículo, se especifica un valor para la propiedad **partition options** , en función de cómo van a compartir los suscriptores los datos de la tabla filtrada. La propiedad puede establecerse en uno de cuatro valores usando [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md), [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md), y el **Propiedades del artículo** cuadro de diálogo. La propiedad se puede establecer en uno de dos valores en los cuadros de diálogo **Agregar filtro** o **Editar filtro** , disponibles desde el Asistente para nueva publicación y el cuadro de diálogo **Propiedades de la publicación** . La tabla siguiente resume los valores disponibles:  
  
|Descripción|Valor en Agregar filtro y Editar filtro|Valor en Propiedades del artículo|Valor en procedimientos almacenados|  
|-----------------|-----------------------------------------|---------------------------------|--------------------------------|  
|Los datos de las particiones se superponen y el suscriptor puede actualizar las columnas a las que se hace referencia en un filtro con parámetros.|**Una fila de esta tabla irá a varias suscripciones**|**Superpuestas**|**0**|  
|Los datos de las particiones se superponen y el suscriptor no puede actualizar las columnas a las que se hace referencia en un filtro con parámetros.|N/A*|**Superpuestas, no permitir cambios de datos fuera de la partición**|**1**|  
|Los datos de las particiones no se superponen y los datos se comparten entre las suscripciones. El suscriptor no puede actualizar columnas a las que se hace referencia en un filtro con parámetros.|N/A*|**No superpuestas, compartir entre suscripciones**|**2**|  
|Los datos de las particiones no se superponen y hay una sola suscripción por partición. El suscriptor no puede actualizar columnas a las que se hace referencia en un filtro parametrizado.**|**Una fila de esta tabla irá a una sola suscripción**|**No superpuestas, una sola suscripción**|**3**|  
  
 \*Si la opción de filtrado subyacente se establece en **0**, o **1**, o **2**, el **Agregar filtro** y **Editar filtro** mostrarán cuadros de diálogo **una fila de esta tabla irá a varias suscripciones**.  
  
 **Si especifica esta opción, solo podrá haber una suscripción para cada partición de datos de ese artículo. Si se crea una segunda partición en la que el criterio de filtrado de la nueva suscripción se resuelve en la misma partición que la suscripción existente, se quitará la suscripción existente.  
  
> [!IMPORTANT]  
>  El valor de **partition options** debe establecerse en función de cómo comparten los datos los suscriptores. Por ejemplo, si especifica una partición sin superposición con una sola suscripción por partición, pero después actualiza los datos en otro suscriptor, se puede producir un error en el Agente de mezcla durante la sincronización y dar lugar a una falta de convergencia.  
  
#### Seleccionar la opción de partición apropiada  
 Las particiones no superpuestas funcionan en combinación con las particiones precalculadas para mejorar el rendimiento en situaciones en las que se admiten algunas limitaciones funcionales. Las particiones precalculadas aceleran la descarga de datos para los suscriptores, pero hacen más lenta la carga. Las particiones no superpuestas minimizan el costo de carga asociado a las particiones precalculadas. La ventaja en el rendimiento de las particiones no superpuestas es más evidente cuando los filtros con parámetros y de combinación utilizados son más complejos.  
  
 Tenga en cuenta los siguientes escenarios al decidir qué opciones de partición debe utilizar en una publicación.  
  
-   [!INCLUDE[ssSampleDBCoShort](../../../includes/sssampledbcoshort-md.md)] tiene un equipo de ventas móvil en el que cada vendedor es responsable de los clientes de un código postal determinado. La aplicación requiere que se actualice el código postal si un cliente se traslada de un área de ventas a otra, para poder asignar el cliente a otro vendedor. El filtro con parámetros se basa en el código postal del cliente, y la actualización quita el código postal de la partición de un vendedor y lo inserta en la partición de otro vendedor. Para esto, se requieren particiones superpuestas y la capacidad de actualizar columnas a las que se hace referencia en un filtro con parámetros. Esta opción proporciona la máxima flexibilidad, pero es posible que no funcione tan bien con particiones no superpuestas.  
  
-   Una agencia de empleo suministra datos a las oficinas regionales de cada condado del estado. Los datos no se superponen; cada fila de la tabla de la oficina principal de la agencia está incluida en una sola partición, pero esa partición se envía a varias oficinas del mismo condado. Es apropiado utilizar la opción de particiones no superpuestas con las particiones compartidas entre suscripciones, lo que proporciona una mejora en el rendimiento en comparación con las particiones superpuestas, a la vez que satisface los requisitos de la aplicación.  
  
-   Si tiene particiones no superpuestas y solo una suscripción recibe y actualiza los datos de una partición, puede obtener ventajas adicionales en el rendimiento. Este escenario es común para los sistemas de punto de venta y las aplicaciones de personal de campo en las que los datos se recopilan principalmente en el suscriptor y se cargan en el publicador. Considere una tabla **Package** en una aplicación de entrega: a medida que se cargan los paquetes en un camión, el estado de cada paquete cambia en la tabla **Package** , y el cambio se replica en la oficina principal. Los conductores no actualizan el estado del mismo paquete en dos camiones distintos, por lo que la tabla **Package** es un buen candidato para una partición no superpuesta con una sola suscripción por partición.  
  
#### Consideraciones para particiones no superpuestas  
 Tenga en cuenta las consideraciones siguientes al utilizar particiones no superpuestas:  
  
##### Consideraciones generales  
  
-   La publicación debe utilizar particiones precalculadas.  
  
-   Una fila debe pertenecer a una sola partición.  
  
-   Los artículos no pueden formar parte de un registro lógico.  
  
-   No se admiten otros asociados de sincronización (esta característica ha quedado desusada).  
  
-   El suscriptor no puede actualizar columnas a las que se hace referencia en un filtro con parámetros.  
  
-   Si una inserción en un suscriptor no pertenece a la partición, no se eliminará. Sin embargo, tampoco se replicará en otros suscriptores.  
  
-   En algunas circunstancias con particiones superpuestas, los intervalos de identidad se ajustan cuando el Agente de mezcla inserta datos. Con las particiones no superpuestas, los intervalos solo se pueden ajustar durante las inserciones realizadas por un usuario con permisos para ajustar intervalos de identidad en la base de datos de suscripciones. El usuario debe poseer la tabla o ser miembro de la **sysadmin** rol fijo de servidor el **db_owner** función fija de base de datos, o la **db_ddladmin** rol fijo de base de datos.  
  
##### Otras consideraciones para las particiones no superpuestas con una sola suscripción por partición  
  
-   Los artículos solo pueden existir en una publicación y no se pueden volver a publicar.  
  
-   La publicación debe permitir que los suscriptores inicien el proceso de instantánea. Para más información, consulte [Snapshots for Merge Publications with Parameterized Filters](../../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md).  
  
##### Otras consideraciones para los filtros de combinación  
  
-   En una jerarquía de filtros de combinación, un artículo con una partición superpuesta no puede aparecer por encima de un artículo con una partición no superpuesta. Es decir, un artículo primario debe usar particiones no superpuestas si las utiliza el artículo secundario. Para obtener información acerca de los filtros de combinación, vea [Join Filters](../../../relational-databases/replication/merge/join-filters.md).  
  
-   Un filtro de combinación en el que la partición no superpuesta es un proceso secundario debe tener la propiedad **join unique key** establecida en 1. Para más información, vea [Join Filters](../../../relational-databases/replication/merge/join-filters.md).  
  
-   El artículo solamente debe tener un filtro con parámetros o un filtro de combinación. Se admite tener un filtro con parámetros y ser el proceso primario en un filtro de combinación. No se permite tener un filtro con parámetros y ser el proceso secundario en un filtro de combinación. Tampoco se permite tener más de un filtro de combinación.  
  
-   Si dos tablas del publicador tienen una relación de filtro de combinación y la tabla secundaria tiene filas que no tienen una fila correspondiente en la tabla primaria, la inserción de la fila que falta en la tabla primaria no hará que las filas relacionadas se descarguen al suscriptor (las filas se descargarían con particiones superpuestas). Por ejemplo, si la tabla **SalesOrderDetail** tiene filas sin una fila correspondiente en la tabla **SalesOrderHeader** , e inserta la fila que falta en **SalesOrderHeader**, la fila se descargará en el suscriptor, pero las filas correspondientes en **SalesOrderDetail** no lo harán.  
  
## Vea también  
 [Prácticas recomendadas para filtros de fila basados en el tiempo](../../../relational-databases/replication/merge/best-practices-for-time-based-row-filters.md)   
 [Filtrar datos publicados](../../../relational-databases/replication/publish/filter-published-data.md)   
 [Filtrar datos publicados para la replicación de mezcla](../../../relational-databases/replication/merge/filter-published-data-for-merge-replication.md)  
  
  