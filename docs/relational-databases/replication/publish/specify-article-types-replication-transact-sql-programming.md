---
title: Especificar tipos de artículo (programación de la replicación con Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- publishing [SQL Server replication], stored procedure execution
- articles [SQL Server replication], transactional replication options
- articles [SQL Server replication], merge replication options
- stored procedures [SQL Server replication], publishing
ms.assetid: d7effbac-c45b-423f-97ae-fd426b1050ba
caps.latest.revision: 26
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 09fa4bbe567677cbabe237d25790369d31ab7ec2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="specify-article-types-replication-transact-sql-programming"></a>Especificar tipos de artículo (programación de la replicación con Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Los tipos de artículo predeterminados para la replicación son los artículos de tabla, pero puede publicar otros objetos de base de datos como los artículos, entre los que se incluyen las vistas, los procedimientos almacenados, las funciones definidas por el usuario y la ejecución de procedimientos almacenados. Puede usar los procedimientos almacenados de replicación para especificar mediante programación un tipo de artículo al definir un artículo. Los procedimientos que se usan dependen del tipo de replicación y del tipo de artículo.  
  
> [!NOTE]  
>  La designación solo de esquema al definir artículos de tabla, vista y procedimientos almacenados indica que solamente se replica la definición del objeto.  
  
### <a name="to-publish-a-table-article-in-a-transactional-or-snapshot-publication"></a>Para publicar un artículo de tabla en una publicación transaccional o de instantáneas  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Especifique uno de los valores siguientes para **@type** a fin de definir el tipo de artículo:  
  
    -   **logbased** - artículo de tabla basado en registro, que es el valor predeterminado para la replicación transaccional y de instantáneas. La replicación genera automáticamente el procedimiento almacenado usado para el filtrado horizontal y la vista que define un artículo filtrado verticalmente.  
  
    -   **logbased manualfilter** - artículo basado en registro y filtrado horizontalmente. El usuario crea y define manualmente el procedimiento almacenado usado para el filtrado horizontal, que se especifica para **@filter**. Para más información, consulte [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md).  
  
    -   **logbased manualview** - artículo basado en registro y filtrado verticalmente. El usuario crea y define la vista que define el artículo filtrado verticalmente, que se especifica para **@sync_object**. Para obtener más información, consulte [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md) y [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  
  
    -   **logbased manualboth** - artículo basado en registro y filtrado horizontal y verticalmente. El usuario crea y define el procedimiento almacenado usado para el filtrado horizontal y la vista que define el artículo filtrado verticalmente; éstos se especifican para **@filter** y **@sync_object**, respectivamente. Para obtener más información, consulte [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md) y [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  
  
     Esto define un nuevo artículo para la publicación. Para más información, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
2.  Para los artículos **logbased manualboth** y **logbased manualfilter** , ejecute [sp_articlefilter](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md) a fin de generar el procedimiento almacenado de filtrado para un artículo filtrado horizontalmente. Para más información, consulte [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md).  
  
3.  Para los artículos **logbased manualboth**, **logbased manualview**y **logbased manualfilter** , ejecute [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) a fin de generar la vista que define el artículo filtrado verticalmente. Para más información, consulte [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  
  
### <a name="to-publish-a-view-or-indexed-view-article-in-a-transactional-or-snapshot-publication"></a>Para publicar una vista o un artículo de vista indizada en una publicación transaccional o de instantáneas  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Especifique uno de los valores siguientes para **@type** a fin de definir el tipo de artículo:  
  
    -   **indexed view logbased** - artículo de vista indizada basado en registro. La replicación genera automáticamente el procedimiento almacenado usado para el filtrado horizontal y la vista que define un artículo filtrado verticalmente.  
  
    -   **view schema only** - artículo de vista solo de esquema. La tabla base debe replicarse también.  
  
    -   **indexed view schema only** - artículo de vista indizada solo de esquema. La tabla base debe replicarse también.  
  
    -   **indexed view logbased manualfilter** - artículo de vista indizada basado en registro y filtrado horizontalmente. El usuario crea y define manualmente el procedimiento almacenado usado para el filtrado horizontal, que se especifica para **@filter**. Para más información, consulte [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md).  
  
    -   **indexed view logbased manualview** - artículo de vista indizada basado en registro y filtrado. El usuario crea y define la vista que define el artículo filtrado verticalmente, que se especifica para **@sync_object**. Para obtener más información, consulte [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md) y [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  
  
    -   **indexed view logbased manualboth** - artículo de vista indizada basado en registro y filtrado. El usuario crea y define el procedimiento almacenado usado para el filtrado horizontal y la vista que define un artículo filtrado verticalmente; éstos se especifican para **@filter** y **@sync_object**, respectivamente. Para obtener más información, consulte [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md) y [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  
  
     Esto define un nuevo artículo para la publicación. Para más información, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
2.  Para los artículos **logbased manualboth** y **logbased manualfilter** , ejecute [sp_articlefilter](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md) a fin de generar el procedimiento almacenado de filtrado para un artículo filtrado horizontalmente. Para más información, consulte [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md).  
  
3.  Para los artículos **logbased manualboth**, **logbased manualview**y **logbased manualfilter** , ejecute [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) a fin de generar la vista que define el artículo filtrado verticalmente. Para más información, consulte [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  
  
### <a name="to-publish-a-stored-procedure-stored-procedure-execution-or-user-defined-function-article-in-a-transactional-or-snapshot-publication"></a>Para publicar un procedimiento almacenado, una ejecución de procedimiento almacenado o un artículo de función definida por el usuario en una publicación transaccional o de instantáneas  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Especifique uno de los valores siguientes para **@type** a fin de definir el tipo de artículo:  
  
    -   **proc schema only** - artículo de procedimiento almacenado solo de esquema.  
  
    -   **proc exec** - replica la ejecución del procedimiento almacenado en todos los suscriptores del artículo. Para más información, consulte [Publishing Stored Procedure Execution in Transactional Replication](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md).  
  
    -   **serializable proc exec** - replica la ejecución del procedimiento almacenado solamente si este se ejecuta dentro del contexto de una transacción serializable. Para más información, vea [Publishing Stored Procedure Execution in Transactional Replication](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md).  
  
    -   **func schema only** - artículo de función definida por el usuario solo de esquema.  
  
     Esto define un nuevo artículo para la publicación. Para más información, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
### <a name="to-publish-a-table-or-view-article-in-a-merge-publication"></a>Para publicar un artículo de tabla o vista en una publicación de combinación  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Especifique uno de los valores siguientes para **@type** a fin de definir el tipo de artículo:  
  
    -   **tabla** - artículo de la tabla.  
  
    -   **indexed view schema only** - artículo de vista indizada solo de esquema.  
  
    -   **view schema only** - artículo de vista solo de esquema.  
  
     Esto define un nuevo artículo para la publicación. Para más información, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
### <a name="to-publish-a-stored-procedure-or-user-defined-function-article-in-a-merge-publication"></a>Para publicar un artículo de procedimiento almacenado o de función definida por el usuario en una publicación de combinación  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Especifique uno de los valores siguientes para **@type** a fin de definir el tipo de artículo:  
  
    -   **func schema only** - artículo de función definida por el usuario solo de esquema.  
  
    -   **proc schema only** - artículo de procedimiento almacenado solo de esquema.  
  
     Esto define un nuevo artículo para la publicación. Para más información, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
## <a name="see-also"></a>Ver también  
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Publicar datos y objetos de base de datos](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
