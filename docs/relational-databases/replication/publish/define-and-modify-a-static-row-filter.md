---
title: Definición y modificación de un filtro de fila estático | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- modifying filters, static row
- static row filters
- filters [SQL Server replication], static row
ms.assetid: a6ebb026-026f-4c39-b6a9-b9998c3babab
caps.latest.revision: 38
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 27b03d53f60ae4c68c35645d5991b958f1c678d9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="define-and-modify-a-static-row-filter"></a>Definir y modificar un filtro de fila estático
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En este tema se describe cómo definir y modificar un filtro de fila estático en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Recomendaciones](#Recommendations)  
  
-   **Para definir y modificar un filtro de fila estático con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Si agrega, modifica o elimina un filtro de fila estático una vez inicializadas las suscripciones a la publicación, deberá generar una instantánea nueva y reinicializar todas las suscripciones después de realizar el cambio. Para obtener más información sobre los requisitos para los cambios de propiedad, consulte [Cambiar las propiedades de la publicación y de los artículos](../../../relational-databases/replication/publish/change-publication-and-article-properties.md) (Cambiar las propiedades de la publicación y de los artículos).  
  
-   Si la publicación está habilitada para la replicación transaccional punto a punto, no se pueden filtrar las tablas.  
  
###  <a name="Recommendations"></a> Recomendaciones  
  
-   Dado que estos filtros son estáticos, todos los suscriptores recibirán el mismo subconjunto de los datos. Si necesita filtrar dinámicamente las filas en un artículo de la tabla que pertenece a una publicación de combinación para que cada suscriptor reciba una partición diferente de los datos, vea [Define and Modify a Parameterized Row Filter for a Merge Article](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md). La replicación de mezcla también permite filtrar filas relacionadas con un filtro de filas existente. Para obtener más información, consulte [Define and Modify a Join Filter Between Merge Articles](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md).  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 Defina, modifique y elimine filtros de filas estáticas en la página **Filtrar filas de tabla** del Asistente para nueva publicación o en la página **Filtrar filas** del cuadro de diálogo **Propiedades de la publicación: \<publicación>**. Para obtener más información sobre el uso del asistente y el acceso al cuadro de diálogo, consulte [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md) (Crear una publicación) y [Ver y modificar propiedades de publicación](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### <a name="to-define-a-static-row-filter"></a>Para definir un filtro de fila estático  
  
1.  En la página **Filtrar filas de tabla** del Asistente para nueva publicación o en la página **Filtrar filas** del cuadro de diálogo **Propiedades de la publicación: \<publicación>**, la acción que realice depende del tipo de publicación:  
  
    -   Para una publicación de instantáneas o transaccional, haga clic en **Agregar**.  
  
    -   Para una publicación de combinación, haga clic en **Agregar**y, a continuación, en **Agregar filtro**.  
  
2.  En el cuadro de diálogo **Agregar filtro** , seleccione la tabla que va a filtrar en el cuadro de lista desplegable.  
  
3.  Cree una instrucción de filtro en el área de texto **Instrucción de filtro** . Puede escribir directamente en el área de texto o puede arrastrar y colocar columnas del cuadro de lista **Columnas** .  
  
    > [!NOTE]  
    >  La cláusula WHERE debe usar nombres de dos partes; los nombres de tres y cuatro partes no se admiten. Si la publicación es de un publicador de Oracle, la cláusula WHERE debe seguir la sintaxis de Oracle.  
  
    -   El área de texto **Instrucción de filtro** incluye el texto predeterminado, que tiene este formato:  
  
        ```sql  
        SELECT <published_columns> FROM [schema].[tablename] WHERE  
        ```  
  
    -   El texto predeterminado no se puede cambiar. Escriba la cláusula del filtro después de la palabra clave WHERE utilizando la sintaxis SQL estándar. La cláusula del filtro completa será similar a la siguiente:  
  
        ```sql  
        SELECT <published_columns> FROM [HumanResources].[Employee] WHERE [LoginID] = 'adventure-works\ranjit0'  
        ```  
  
    -   Un filtro de fila estático puede incluir una función definida por el usuario. La cláusula del filtro completa para un filtro de fila estático con una función definida por el usuario será similar a la siguiente:  
  
        ```sql  
        SELECT <published_columns> FROM [Sales].[SalesOrderHeader] WHERE MyFunction([Freight]) > 100  
        ```  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Si se encuentra en el cuadro de diálogo **Propiedades de la publicación: \<publicación>**, haga clic en **Aceptar** para guardar y cerrar el cuadro de diálogo.  
  
#### <a name="to-modify-a-static-row-filter"></a>Para modificar un filtro de fila estático  
  
1.  En la página **Filtrar filas de tabla** del Asistente para nueva publicación o la página **Filtrar filas** del cuadro de diálogo **Propiedades de la publicación: \<publicación>**, seleccione un filtro en el panel**Tablas filtradas** y, después, haga clic en **Editar**.  
  
2.  Modifique el filtro en el cuadro de diálogo **Editar filtro** .  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-delete-a-static-row-filter"></a>Para eliminar un filtro de fila estático  
  
1.  En la página **Filtrar filas de tabla** del Asistente para nueva publicación o la página **Filtrar filas** del cuadro de diálogo **Propiedades de la publicación: \<publicación>**, seleccione un filtro en el panel **Tablas filtradas** y, después, haga clic en **Eliminar**.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Al crear los artículos de la tabla, puede definir una cláusula WHERE para filtrar las filas de un artículo. También puede cambiar un filtro de fila una vez definido. Los filtros de fila estáticos se pueden crear y modificar mediante programación con los procedimientos almacenados de la replicación.  
  
#### <a name="to-define-a-static-row-filter-for-a-snapshot-or-transactional-publication"></a>Para definir un filtro de fila estático para una publicación transaccional o de instantáneas  
  
1.  Defina el artículo que se va a filtrar. Para más información, consulte [definir un artículo](../../../relational-databases/replication/publish/define-an-article.md).  
  
2.  En la base de datos de publicación del publicador, ejecute [sp_articlefilter &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md). Especifique el nombre del artículo para **@article**, el nombre de la publicación para **@publication**, un nombre de filtro para **@filter_name**y la cláusula de filtrado para **@filter_clause** (no se incluye `WHERE`).  
  
3.  Si todavía debe definirse un filtro de columna, vea [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md). De lo contrario, ejecute [sp_articleview &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md). Especifique el nombre de la publicación para **@publication**, el nombre del artículo filtrado para **@article**y la cláusula de filtro especificada en el paso 2 para **@filter_clause**. Esto crea los objetos de sincronización para el artículo filtrado.  
  
#### <a name="to-modify-a-static-row-filter-for-a-snapshot-or-transactional-publication"></a>Para modificar un filtro de fila estático para una publicación transaccional o de instantáneas  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_articlefilter &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md). Especifique el nombre del artículo para **@article**, el nombre de la publicación para **@publication**, un nombre de filtro nuevo para **@filter_name**y la cláusula de filtrado nueva para **@filter_clause** (no se incluye `WHERE`). Dado que este cambio invalidará los datos en las suscripciones existentes, especifique un valor de **1** para **@force_reinit_subscription**.  
  
2.  En la base de datos de publicación del publicador, ejecute [sp_articleview &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md). Especifique el nombre de la publicación para **@publication**, el nombre del artículo filtrado para **@article**y la cláusula de filtro especificada en el paso 1 para **@filter_clause**. Esto vuelve a crear la vista que define el artículo filtrado.  
  
3.  Vuelva a ejecutar el trabajo del Agente de instantáneas para que la publicación genere una instantánea actualizada. Para obtener más información, consulte [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
4.  Reinicialice las suscripciones. Para obtener más información, vea [Reinicializar suscripciones](../../../relational-databases/replication/reinitialize-subscriptions.md).  
  
#### <a name="to-delete-a-static-row-filter-for-a-snapshot-or-transactional-publication"></a>Para eliminar un filtro de fila estático para una instantánea o una publicación transaccional  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_articlefilter &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md). Especifique el nombre del artículo para **@article**, el nombre de la publicación para **@publication**, un valor de NULL para **@filter_name**y un valor de NULL para **@filter_clause**. Dado que este cambio invalidará los datos en las suscripciones existentes, especifique un valor de **1** para **@force_reinit_subscription**.  
  
2.  Vuelva a ejecutar el trabajo del Agente de instantáneas para que la publicación genere una instantánea actualizada. Para obtener más información, consulte [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
3.  Reinicialice las suscripciones. Para obtener más información, vea [Reinicializar suscripciones](../../../relational-databases/replication/reinitialize-subscriptions.md).  
  
#### <a name="to-define-a-static-row-filter-for-a-merge-publication"></a>Para definir un filtro de fila estático para una publicación de combinación  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_addmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Especifique la cláusula de filtrado para **@subset_filterclause** (no se incluye `WHERE`). Para obtener más información, consulte [definir un artículo](../../../relational-databases/replication/publish/define-an-article.md).  
  
2.  Si todavía debe definirse un filtro de columna, vea [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  
  
#### <a name="to-modify-a-static-row-filter-for-a-merge-publication"></a>Para modificar un filtro de fila estático para una publicación de combinación  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_changemergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md). Especifique el nombre de la publicación para **@publication**, el nombre del artículo filtrado para **@article**, un valor de **subset_filterclause** para **@property**y la cláusula de filtrado nueva para **@value** (no se incluye `WHERE`). Dado que este cambio invalidará los datos en las suscripciones existentes, especifique un valor de 1 para **@force_reinit_subscription**.  
  
2.  Vuelva a ejecutar el trabajo del Agente de instantáneas para que la publicación genere una instantánea actualizada. Para obtener más información, consulte [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
3.  Reinicialice las suscripciones. Para obtener más información, vea [Reinicializar suscripciones](../../../relational-databases/replication/reinitialize-subscriptions.md).  
  
###  <a name="TsqlExample"></a> Ejemplos (Transact-SQL)  
 En este ejemplo de la replicación transaccional, el artículo se filtra horizontalmente para quitar todos los productos desusados.  
  
 [!code-sql[HowTo#sp_AddTranArticle](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-stat_1.sql)]  
  
 En este ejemplo de replicación de mezcla, los artículos se filtran horizontalmente para devolver solo las filas que pertenecen al vendedor especificado. También se usa un filtro de combinación. Para más información, consulte [Define and Modify a Join Filter Between Merge Articles](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md).  
  
 [!code-sql[HowTo#sp_AddMergeArticle](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-stat_2.sql)]  
  
## <a name="see-also"></a>Ver también  
 [Definir y modificar un filtro de fila con parámetros para un artículo de mezcla](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)   
 [Cambiar las propiedades de la publicación y de los artículos](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Filtrar datos publicados](../../../relational-databases/replication/publish/filter-published-data.md)   
 [Filtrar datos publicados para la replicación de mezcla](../../../relational-databases/replication/merge/filter-published-data-for-merge-replication.md)  
  
  
