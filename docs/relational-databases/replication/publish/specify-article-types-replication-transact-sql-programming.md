---
title: "Especificar tipos de art&#237;culo (programaci&#243;n de la replicaci&#243;n con Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "publicar [replicación de SQL Server], ejecución de procedimiento almacenado"
  - "artículos [replicación de SQL Server], opciones de replicación transaccional"
  - "artículos [replicación de SQL Server], opciones de replicación de mezcla"
  - "procedimientos almacenados [replicación de SQL Server], publicar"
ms.assetid: d7effbac-c45b-423f-97ae-fd426b1050ba
caps.latest.revision: 26
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 26
---
# Especificar tipos de art&#237;culo (programaci&#243;n de la replicaci&#243;n con Transact-SQL)
  Los tipos de artículo predeterminados para la replicación son los artículos de tabla, pero puede publicar otros objetos de base de datos como los artículos, entre los que se incluyen las vistas, los procedimientos almacenados, las funciones definidas por el usuario y la ejecución de procedimientos almacenados. Puede usar los procedimientos almacenados de replicación para especificar mediante programación un tipo de artículo al definir un artículo. Los procedimientos que se usan dependen del tipo de replicación y del tipo de artículo.  
  
> [!NOTE]  
>  La designación solo de esquema al definir artículos de tabla, vista y procedimientos almacenados indica que solamente se replica la definición del objeto.  
  
### Para publicar un artículo de tabla en una publicación transaccional o de instantáneas  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Especifique uno de los valores siguientes para **@type** a fin de definir el tipo de artículo:  
  
    -   **logbased** -un artículo de tabla basada en el registro, que es el valor predeterminado para la replicación de instantáneas y transaccional. La replicación genera automáticamente el procedimiento almacenado usado para el filtrado horizontal y la vista que define un artículo filtrado verticalmente.  
  
    -   **logbased manualfilter** -artículo basado en registro y filtrado horizontalmente donde el procedimiento almacenado utilizado para el filtrado horizontal es manualmente creado y definido por el usuario y especificado para **@filter**. Para más información, consulte [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md).  
  
    -   **logbased manualview** -artículo basado en registro y filtrado vertical donde la vista que define el artículo filtrado verticalmente es creada y definida por el usuario y especificada para **@sync_object**. Para obtener más información, consulte [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md) y [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  
  
    -   **logbased manualboth** -basado en registro, horizontal y verticalmente filtra el artículo en el procedimiento almacenado usado para el filtrado horizontal y la vista que define el artículo filtrado verticalmente se crean y definido por el usuario y especificado para **@filter** y **@sync_object**, respectivamente. Para obtener más información, consulte [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md) y [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  
  
     Esto define un nuevo artículo para la publicación. Para más información, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
2.  Para **logbased manualboth** y **logbased manualfilter** artículos, ejecutar [sp_articlefilter](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md) para generar el procedimiento almacenado de filtrado para un artículo filtrado horizontalmente. Para más información, consulte [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md).  
  
3.  Para **logbased manualboth**, **logbased manualview**, y **logbased manualfilter** artículos, ejecutar [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) para generar la vista que define el artículo filtrado verticalmente. Para más información, consulte [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  
  
### Para publicar una vista o un artículo de vista indizada en una publicación transaccional o de instantáneas  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Especifique uno de los valores siguientes para **@type** a fin de definir el tipo de artículo:  
  
    -   **indizar la vista logbased** -un artículo de vista indizada basado en registro. La replicación genera automáticamente el procedimiento almacenado usado para el filtrado horizontal y la vista que define un artículo filtrado verticalmente.  
  
    -   **esquema de la vista sólo** -un artículo de sólo esquema de vista. La tabla base debe replicarse también.  
  
    -   **esquema de la vista indizada solo** -un artículo de sólo esquema de vista indizada. La tabla base debe replicarse también.  
  
    -   **indizar la vista logbased manualfilter** -un artículo de vista indizada basado en registro y filtrado horizontalmente donde el procedimiento almacenado utilizado para el filtrado horizontal es manualmente creado y definido por el usuario y especificado para **@filter**. Para más información, consulte [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md).  
  
    -   **indizar la vista logbased manualview** -donde la vista que define un artículo filtrado verticalmente está creada y definida por el usuario y especificada para un artículo de vista indizada basado en registro y filtrado **@sync_object**. Para obtener más información, consulte [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md) y [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  
  
    -   **indizar la vista logbased manualboth** -donde el procedimiento almacenado usado para el filtrado horizontal y la vista que define un artículo filtrado verticalmente se creó y definido por el usuario y especificado para un artículo de vista indizada basado en registro y filtrado **@filter** y **@sync_object**, respectivamente. Para obtener más información, consulte [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md) y [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  
  
     Esto define un nuevo artículo para la publicación. Para más información, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
2.  Para **logbased manualboth** y **logbased manualfilter** artículos, ejecutar [sp_articlefilter](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md) para generar el procedimiento almacenado de filtrado para un artículo filtrado horizontalmente. Para más información, consulte [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md).  
  
3.  Para **logbased manualboth**, **logbased manualview**, y **logbased manualfilter** artículos, ejecutar [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) para generar la vista que define el artículo filtrado verticalmente. Para más información, consulte [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  
  
### Para publicar un procedimiento almacenado, una ejecución de procedimiento almacenado o un artículo de función definida por el usuario en una publicación transaccional o de instantáneas  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Especifique uno de los valores siguientes para **@type** a fin de definir el tipo de artículo:  
  
    -   **proc schema sólo** -un artículo de sólo esquema de procedimiento almacenado.  
  
    -   **proc exec** -replica la ejecución del procedimiento almacenado a todos los suscriptores del artículo. Para obtener más información, consulte [Publishing Stored Procedure Execution in Transactional Replication](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md).  
  
    -   **serializable proc exec** -replica la ejecución del procedimiento almacenado sólo si se ejecuta dentro del contexto de una transacción serializable. Para obtener más información, consulte [Publishing Stored Procedure Execution in Transactional Replication](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md).  
  
    -   **solo esquema Func** -un artículo de sólo esquema de función definida por el usuario.  
  
     Esto define un nuevo artículo para la publicación. Para más información, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
### Para publicar un artículo de tabla o vista en una publicación de combinación  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Especifique uno de los valores siguientes para **@type** a fin de definir el tipo de artículo:  
  
    -   **tabla** -un artículo de tabla.  
  
    -   **esquema de la vista indizada solo** -un artículo de sólo esquema de vista indizada.  
  
    -   **esquema de la vista sólo** -un artículo de sólo esquema de vista.  
  
     Esto define un nuevo artículo para la publicación. Para más información, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
### Para publicar un artículo de procedimiento almacenado o de función definida por el usuario en una publicación de combinación  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Especifique uno de los valores siguientes para **@type** a fin de definir el tipo de artículo:  
  
    -   **solo esquema Func** -un artículo de sólo esquema de función definida por el usuario.  
  
    -   **proc schema sólo** -un artículo de sólo esquema de procedimiento almacenado.  
  
     Esto define un nuevo artículo para la publicación. Para más información, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
## Vea también  
 [Conceptos sobre los procedimientos almacenados del sistema de replicación](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Publicar datos y objetos de base de datos](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  