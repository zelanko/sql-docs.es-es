---
title: "Filtrar datos publicados | Microsoft Docs"
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
  - "filtros [replicación de SQL Server]"
  - "filtros [replicación de SQL Server], acerca del filtrado"
  - "filtrar [replicación de SQL Server]"
  - "filtros de fila estáticos"
  - "replicación transaccional, filtrar datos publicados"
  - "replicación [SQL Server], filtrar datos publicados"
  - "filtrar datos publicados [replicación de SQL Server]"
  - "replicación de instantáneas [SQL Server], filtrar datos publicados"
  - "filtros de columna [replicación de SQL Server]"
ms.assetid: 8a914947-72dc-4119-b631-b39c8070c71b
caps.latest.revision: 50
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 50
---
# Filtrar datos publicados
  Filtrar artículos de tabla permite crear particiones de los datos que se van a publicar. Si filtra los datos publicados, podrá:  
  
-   Minimizar la cantidad de datos que se envían a través de la red.  
  
-   Reducir la cantidad de espacio de almacenamiento necesario en el suscriptor.  
  
-   Personalizar las publicaciones y las aplicaciones en función de los requisitos de cada suscriptor.  
  
-   Evitar o reducir los conflictos si los suscriptores actualizan datos, ya que pueden enviarse particiones de datos diferentes a varios suscriptores (dos suscriptores distintos no actualizarán los mismos valores de datos).  
  
-   Evitar la transmisión de datos reservados. Se pueden utilizar filtros de fila y filtros de columna para restringir el acceso de un suscriptor a los datos. Para la replicación de mezcla, existen consideraciones de seguridad que se deben tener en cuenta si utiliza un filtro con parámetros que incluya HOST_NAME(). Para obtener más información, vea la sección "Filtrar con HOST_NAME ()" en [filtros de fila parametrizados](../../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
 La replicación ofrece cuatro tipos de filtros:  
  
-   Filtros de fila estáticos que están disponibles con todos los tipos de replicación.  
  
     Mediante los filtros de fila estáticos, puede elegir un subconjunto de filas para publicarlo. Todos los suscriptores de una publicación filtrada reciben el mismo subconjunto de filas para la tabla filtrada. Para obtener más información, vea la sección "Filtros de fila estáticos" de este tema.  
  
-   Filtros de columna que están disponibles con todos los tipos de replicación.  
  
     Al utilizar los filtros de columna, puede elegir un subconjunto de columnas para publicarlo. Para obtener más información, vea la sección "Filtros de columna" de este tema.  
  
-   Filtros de fila con parámetros que están disponibles solamente con la replicación de mezcla.  
  
     Al utilizar los filtros de fila con parámetros, puede elegir un subconjunto de filas para publicarlo. A diferencia de los filtros estáticos que envían el mismo subconjunto de filas a cada suscriptor, los filtros de fila con parámetros utilizan un valor de datos suministrado por el suscriptor para enviar a los suscriptores diferentes subconjuntos de filas. Para más información, consulte [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
-   Filtros de combinación que están disponibles solamente con la replicación de mezcla.  
  
     Al utilizar los filtros de combinación, puede ampliar un filtro de fila de una tabla publicada a otra. Para más información, consulte [Join Filters](../../../relational-databases/replication/merge/join-filters.md).  
  
## Filtros de fila estáticos  
 En la siguiente ilustración se muestra una tabla publicada que está filtrada para que solamente se incluyan las filas 2, 3 y 6 en la publicación.  
  
 ![Filtrar filas](../../../relational-databases/replication/publish/media/repl-16.gif "Filtrar filas")  
  
 Un filtro de fila estático utiliza una sola cláusula WHERE para seleccionar los datos apropiados que se publicarán; se especifica la parte final de la cláusula WHERE. Considere la tabla **Product** en la base de datos de ejemplo AdventureWorks, que contiene la columna **ProductLine**. Para publicar solamente las filas con datos sobre los productos relacionados con las bicicletas de montaña, especifique `ProductLine = 'M'`.  
  
 Un filtro de fila estático produce un único conjunto de datos para cada publicación. En el ejemplo anterior, todos los suscriptores recibirían únicamente las filas con datos sobre productos relacionados con las bicicletas de montaña. Si tiene otro suscriptor que solamente requiera las filas con los datos sobre productos relacionados con bicicletas de paseo:  
  
-   Con la replicación de instantáneas o la replicación transaccional, puede crear otra publicación e incluir la tabla en ambas publicaciones (en la cláusula del filtro para el artículo de dicha publicación, especifique `ProductLine = 'R')`).  
  
    > [!NOTE]  
    >  Los filtros de fila en las publicaciones transaccionales pueden producir una sobrecarga significativa porque la cláusula de filtro de artículos se evalúa para cada fila de registro escrita en una tabla publicada para determinar si la fila se debe replicar. Se deben evitar los filtros de fila en publicaciones transaccionales si cada nodo de replicación puede admitir la carga de datos completa y el conjunto de datos global es suficientemente pequeño.  
  
-   Con la replicación de mezcla, utilice filtros de fila con parámetros en vez de crear varias publicaciones con filtros de fila estáticos. Para más información, consulte [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
 Para definir o modificar un filtro de fila estático, vea [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md).  
  
## Filtros de columnas  
 En la siguiente ilustración se muestra una publicación que filtra la columna C.  
  
 ![Filtros de columnas](../../../relational-databases/replication/publish/media/repl-17.gif "Filtros de columnas")  
  
 También puede utilizar conjuntamente el filtrado de filas y columnas, como se ilustra a continuación.  
  
 ![Filtrar filas y columnas](../../../relational-databases/replication/publish/media/repl-18.gif "Filtrar filas y columnas")  
  
 Tras crear una publicación, puede utilizar un filtro de columna para quitar una columna de una publicación existente, pero conservar la columna en la tabla en el publicador e incluir también una columna existente en la publicación. Para otros cambios, tales como agregar una columna nueva a una tabla y después agregarla al artículo publicado, utilice la replicación de cambios de esquema. Para obtener más información, consulte las secciones "Agregar columnas" y "quitar" en el tema [hacer cambios de esquema en bases de datos de publicación](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md).  
  
 Los tipos de columnas enumerados en la siguiente tabla no se pueden eliminar de ciertos tipos de publicaciones.  
  
|Tipo de columna|Tipo de publicación y opciones|  
|-----------------|-------------------------------------|  
|Columna de clave principal|Las columnas de clave principal son necesarias para todas las tablas en las publicaciones transaccionales. Las claves principales no son necesarias para las tablas en publicaciones de combinación, pero si hay una columna de clave principal, ésta no se puede filtrar.|  
|Columna de clave externa|Todas las publicaciones creadas mediante el Asistente para nueva aplicación. Puede filtrar columnas de clave externa mediante procedimientos almacenados de Transact-SQL. Para obtener más información, vea [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).|  
|Columna **rowguid**|Publicaciones de combinación*|  
|El **msrepl_tran_version** columna|Publicaciones de instantáneas o transaccionales que permiten suscripciones actualizables|  
|Columnas que no permiten valores NULL y no tienen valores predeterminados ni el conjunto de propiedades IDENTITY.|Publicaciones de instantáneas o transaccionales que permiten suscripciones actualizables|  
|Columnas con restricciones UNIQUE o índices|Publicaciones de instantáneas o transaccionales que permiten suscripciones actualizables|  
|Todas las columnas en una publicación de combinación de SQL Server 7.0|Las columnas no se pueden filtrar en las publicaciones de combinación de SQL Server 7.0.|  
|Timestamp|Publicaciones de instantáneas o transaccionales de SQL Server 7.0 que permiten suscripciones actualizables|  
  
 \*Si va a publicar una tabla en una publicación de mezcla y que la tabla ya contiene una columna de tipo de datos **uniqueidentifier** con el **ROWGUIDCOL** conjunto de propiedades, la replicación puede utilizar esta columna en lugar de crear una columna adicional denominada **rowguid**. En este caso, se debe publicar la columna existente.  
  
 Para definir o modificar un filtro de columna, vea [definir y modificar un filtro de columna](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  
  
## Consideraciones de filtrado  
 Tenga en cuenta las siguientes consideraciones al filtrar datos:  
  
-   Todas las columnas a las que se hace referencia en filtros de fila se deben incluir en la publicación. Es decir, no puede utilizar un filtro de columna para excluir una columna utilizada en un filtro de fila.  
  
-   Si se agrega o cambia un filtro después de que se hayan inicializado las suscripciones, éstas deben reinicializarse.  
  
-   El número máximo de bytes permitido en una columna utilizada en un filtro es de 1024 para un artículo en una publicación de combinación y 8000 en un artículo de una publicación transaccional.  
  
-   En filtros de fila o filtros de combinación no se puede hacer referencia a columnas con los siguientes tipos de datos:  
  
    -   **varchar(max) y nvarchar(max)**  
  
    -   **varbinary(max)**  
  
    -   **Text y ntext**  
  
    -   **imagen**  
  
    -   **XML**  
  
    -   **UDT**  
  
-   La replicación transaccional le permite replicar una vista indizada como vista o como tabla. Si replica la vista como tabla, no podrá filtrar columnas de la tabla.  
  
 Los filtros de fila no están diseñados para funcionar entre bases de datos. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] limita intencionadamente la ejecución de **sp_replcmds** (que filtra la ejecución debajo) al propietario de la base de datos (**dbo**). El **dbo** no tiene privilegios entre bases de datos. Con la incorporación de CDC (captura de datos modificados) en [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] el **sp_replcmds** lógica rellena las tablas con la información que el usuario puede volver a y de consulta de seguimiento de cambios. Por motivos de seguridad, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] limita la ejecución de esta lógica para que un malintencionado **dbo** no pueda asaltar esta ruta de acceso de ejecución. Por ejemplo, un malintencionado **dbo** podría agregar desencadenadores a tablas de CDC que se ejecutarían en el contexto de usuario, que llama a **sp_replcmds**, en este caso el agente de lector del registro.  Si la cuenta bajo la que se está ejecutando el agente tiene privilegios mayores, el **dbo** malintencionado podría escalar sus privilegios.  
  
## Vea también  
 [Publicar datos y objetos de base de datos](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  