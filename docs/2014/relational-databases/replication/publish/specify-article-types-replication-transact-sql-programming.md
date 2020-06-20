---
title: Especificar tipos de artículo (programación de la replicación con Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- publishing [SQL Server replication], stored procedure execution
- articles [SQL Server replication], transactional replication options
- articles [SQL Server replication], merge replication options
- stored procedures [SQL Server replication], publishing
ms.assetid: d7effbac-c45b-423f-97ae-fd426b1050ba
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7864825891203530bf30015471ca22a1daccf9b9
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85060339"
---
# <a name="specify-article-types-replication-transact-sql-programming"></a>Especificar tipos de artículo (programación de la replicación con Transact-SQL)
  Los tipos de artículo predeterminados para la replicación son los artículos de tabla, pero puede publicar otros objetos de base de datos como los artículos, entre los que se incluyen las vistas, los procedimientos almacenados, las funciones definidas por el usuario y la ejecución de procedimientos almacenados. Puede usar los procedimientos almacenados de replicación para especificar mediante programación un tipo de artículo al definir un artículo. Los procedimientos que se usan dependen del tipo de replicación y del tipo de artículo.  
  
> [!NOTE]  
>  La designación solo de esquema al definir artículos de tabla, vista y procedimientos almacenados indica que solamente se replica la definición del objeto.  
  
### <a name="to-publish-a-table-article-in-a-transactional-or-snapshot-publication"></a>Para publicar un artículo de tabla en una publicación transaccional o de instantáneas  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql). Especifique uno de los siguientes valores para ** \@ tipo** para definir el tipo de artículo:  
  
    -   **logbased** - artículo de tabla basado en registro, que es el valor predeterminado para la replicación transaccional y de instantáneas. La replicación genera automáticamente el procedimiento almacenado usado para el filtrado horizontal y la vista que define un artículo filtrado verticalmente.  
  
    -   **logbased manualfilter** -artículo basado en registro y filtrado horizontalmente. el usuario crea y define manualmente el procedimiento almacenado usado para el filtrado horizontal, que se especifica para el ** \@ filtro**. Para más información, consulte [Define and Modify a Static Row Filter](define-and-modify-a-static-row-filter.md).  
  
    -   **logbased manualview** -artículo basado en registro y filtrado verticalmente. el usuario crea y define la vista que define el artículo filtrado verticalmente y se especifica para ** \@ sync_object**. Para obtener más información, consulte [Define and Modify a Static Row Filter](define-and-modify-a-static-row-filter.md) y [Define and Modify a Column Filter](define-and-modify-a-column-filter.md).  
  
    -   **logbased manualboth** -artículo basado en registro, horizontal y verticalmente filtrado, donde el procedimiento almacenado usado para el filtrado horizontal y la vista que define el artículo filtrado verticalmente son creados y definidos por el usuario, y se especifican para ** \@ filtrar** y ** \@ sync_object**, respectivamente. Para obtener más información, consulte [Define and Modify a Static Row Filter](define-and-modify-a-static-row-filter.md) y [Define and Modify a Column Filter](define-and-modify-a-column-filter.md).  
  
     Esto define un nuevo artículo para la publicación. Para más información, consulte [Define an Article](define-an-article.md).  
  
2.  Para los artículos **logbased manualboth** y **logbased manualfilter** , ejecute [sp_articlefilter](/sql/relational-databases/system-stored-procedures/sp-articlefilter-transact-sql) a fin de generar el procedimiento almacenado de filtrado para un artículo filtrado horizontalmente. Para más información, consulte [Define and Modify a Static Row Filter](define-and-modify-a-static-row-filter.md).  
  
3.  Para los artículos **logbased manualboth**, **logbased manualview**y **logbased manualfilter** , ejecute [sp_articleview](/sql/relational-databases/system-stored-procedures/sp-articleview-transact-sql) a fin de generar la vista que define el artículo filtrado verticalmente. Para más información, consulte [definir y modificar un filtro de columna](define-and-modify-a-column-filter.md).  
  
### <a name="to-publish-a-view-or-indexed-view-article-in-a-transactional-or-snapshot-publication"></a>Para publicar una vista o un artículo de vista indizada en una publicación transaccional o de instantáneas  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql). Especifique uno de los siguientes valores para ** \@ tipo** para definir el tipo de artículo:  
  
    -   **indexed view logbased** - artículo de vista indizada basado en registro. La replicación genera automáticamente el procedimiento almacenado usado para el filtrado horizontal y la vista que define un artículo filtrado verticalmente.  
  
    -   **view schema only** - artículo de vista solo de esquema. La tabla base debe replicarse también.  
  
    -   **indexed view schema only** - artículo de vista indizada solo de esquema. La tabla base debe replicarse también.  
  
    -   **indexed View logbased manualfilter** -artículo de vista indizada basado en registro y filtrado horizontalmente. el usuario crea y define manualmente el procedimiento almacenado usado para el filtrado horizontal, que se especifica para el ** \@ filtro**. Para más información, consulte [Define and Modify a Static Row Filter](define-and-modify-a-static-row-filter.md).  
  
    -   **indexed View logbased manualview** -artículo de vista indizada basado en registro y filtrado donde el usuario crea y define la vista que define un artículo filtrado verticalmente y se especifica para ** \@ sync_object**. Para obtener más información, consulte [Define and Modify a Static Row Filter](define-and-modify-a-static-row-filter.md) y [Define and Modify a Column Filter](define-and-modify-a-column-filter.md).  
  
    -   **indexed View logbased manualboth** -artículo de vista indizada basado en registro y filtrado. el usuario crea y define el procedimiento almacenado usado para el filtrado horizontal y la vista que define un artículo filtrado verticalmente, y se especifica para el ** \@ filtro** y el ** \@ sync_object**, respectivamente. Para obtener más información, consulte [Define and Modify a Static Row Filter](define-and-modify-a-static-row-filter.md) y [Define and Modify a Column Filter](define-and-modify-a-column-filter.md).  
  
     Esto define un nuevo artículo para la publicación. Para más información, consulte [Define an Article](define-an-article.md).  
  
2.  Para los artículos **logbased manualboth** y **logbased manualfilter** , ejecute [sp_articlefilter](/sql/relational-databases/system-stored-procedures/sp-articlefilter-transact-sql) a fin de generar el procedimiento almacenado de filtrado para un artículo filtrado horizontalmente. Para más información, consulte [Define and Modify a Static Row Filter](define-and-modify-a-static-row-filter.md).  
  
3.  Para los artículos **logbased manualboth**, **logbased manualview**y **logbased manualfilter** , ejecute [sp_articleview](/sql/relational-databases/system-stored-procedures/sp-articleview-transact-sql) a fin de generar la vista que define el artículo filtrado verticalmente. Para más información, consulte [definir y modificar un filtro de columna](define-and-modify-a-column-filter.md).  
  
### <a name="to-publish-a-stored-procedure-stored-procedure-execution-or-user-defined-function-article-in-a-transactional-or-snapshot-publication"></a>Para publicar un procedimiento almacenado, una ejecución de procedimiento almacenado o un artículo de función definida por el usuario en una publicación transaccional o de instantáneas  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql). Especifique uno de los siguientes valores para ** \@ tipo** para definir el tipo de artículo:  
  
    -   **proc schema only** - artículo de procedimiento almacenado solo de esquema.  
  
    -   **proc exec** - replica la ejecución del procedimiento almacenado en todos los suscriptores del artículo. Para más información, vea [Publishing Stored Procedure Execution in Transactional Replication](../transactional/publishing-stored-procedure-execution-in-transactional-replication.md).  
  
    -   **serializable proc exec** - replica la ejecución del procedimiento almacenado solamente si este se ejecuta dentro del contexto de una transacción serializable. Para más información, vea [Publishing Stored Procedure Execution in Transactional Replication](../transactional/publishing-stored-procedure-execution-in-transactional-replication.md).  
  
    -   **func schema only** - artículo de función definida por el usuario solo de esquema.  
  
     Esto define un nuevo artículo para la publicación. Para más información, consulte [Define an Article](define-an-article.md).  
  
### <a name="to-publish-a-table-or-view-article-in-a-merge-publication"></a>Para publicar un artículo de tabla o vista en una publicación de combinación  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql). Especifique uno de los siguientes valores para ** \@ tipo** para definir el tipo de artículo:  
  
    -   **tabla** - artículo de la tabla.  
  
    -   **indexed view schema only** - artículo de vista indizada solo de esquema.  
  
    -   **view schema only** - artículo de vista solo de esquema.  
  
     Esto define un nuevo artículo para la publicación. Para más información, consulte [Define an Article](define-an-article.md).  
  
### <a name="to-publish-a-stored-procedure-or-user-defined-function-article-in-a-merge-publication"></a>Para publicar un artículo de procedimiento almacenado o de función definida por el usuario en una publicación de combinación  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql). Especifique uno de los siguientes valores para ** \@ tipo** para definir el tipo de artículo:  
  
    -   **func schema only** - artículo de función definida por el usuario solo de esquema.  
  
    -   **proc schema only** - artículo de procedimiento almacenado solo de esquema.  
  
     Esto define un nuevo artículo para la publicación. Para más información, consulte [Define an Article](define-an-article.md).  
  
## <a name="see-also"></a>Consulte también  
 [Conceptos de procedimientos almacenados del sistema de replicación](../concepts/replication-system-stored-procedures-concepts.md)   
 [Publicar datos y objetos de base de datos](publish-data-and-database-objects.md)  
  
  
