---
title: sp_dropmergearticle (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 05/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_dropmergearticle
- sp_dropmergearticle_TSQL
helpviewer_keywords:
- sp_dropmergearticle
ms.assetid: 5ef1fbf7-c03d-4488-9ab2-64aae296fa4f
caps.latest.revision: 34
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 83034ea0a9c14ee1e8efb8c3ea3ea6d604bb367a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="spdropmergearticle-transact-sql"></a>sp_dropmergearticle (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita un artículo de una publicación de combinación. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_dropmergearticle [ @publication= ] 'publication'  
        , [ @article= ] 'article'   
    [ , [ @ignore_distributor= ] ignore_distributor   
    [ , [ @reserved= ] reserved   
    [ , [ @force_invalidate_snapshot= ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @ignore_merge_metadata = ] ignore_merge_metadata ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication=**] **'***publicación***'**  
 Es el nombre de la publicación de la que se va a quitar un artículo. *publicación*es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@article=**] **'***artículo***'**  
 Es el nombre del artículo que se va a quitar de la publicación especificada. *artículo*es **sysname**, no tiene ningún valor predeterminado. Si **todos los**, se quitan todos los artículos existentes en la publicación de combinación especificada. Aunque *artículo* es **todos los**, la publicación debe quitarse por separado desde el artículo.  
  
 [  **@ignore_distributor=**] *ignore_distributor*  
 Indica si este procedimiento almacenado se ejecuta sin conectarse al distribuidor. *ignore_distributor* es **bits**, su valor predeterminado es **0**.  
  
 [  **@reserved=**] *reservadas*  
 Está reservado para su uso futuro. *reservada* es **nvarchar (20)**, su valor predeterminado es null.  
  
 [  **@force_invalidate_snapshot=**] *force_invalidate_snapshot*  
 Habilita o deshabilita la capacidad de que se invalide una instantánea. *force_invalidate_snapshot* es un **bits**, su valor predeterminado es **0**.  
  
 **0** especifica que los cambios en el artículo de mezcla no invalidarán la instantánea no es válida.  
  
 **1** significa que los cambios en el artículo de mezcla puede invalidar la instantánea no es válida, y si ese es el caso, un valor de **1** concede permiso para la nueva instantánea para que se produzca.  
  
 [  **@force_reinit_subscription =** ] *force_reinit_subscription*  
 Confirma que para quitar el artículo deben reinicializarse las suscripciones existentes. *force_reinit_subscription* es un **bits**, su valor predeterminado es **0**.  
  
 **0** especifica que al quitar el artículo no harán que se reinicialice la suscripción.  
  
 **1** significa que al quitar el artículo que se reinicialicen las suscripciones existentes y concede permiso para que se lleve a cabo la reinicialización.  
  
 [  **@ignore_merge_metadata=** ] *ignore_merge_metadata*  
 Exclusivamente para uso interno.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_dropmergearticle** se utiliza en la replicación de mezcla. Para obtener más información acerca de cómo quitar artículos, vea [agregar y quitar artículos de publicaciones existentes](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
 Ejecutar **sp_dropmergearticle** quitar un artículo de una publicación no quita el objeto de la base de datos de publicación o el objeto correspondiente de la base de datos de suscripción. Si es necesario, utilice `DROP <object>` para quitar estos objetos manualmente.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor o el **db_owner** rol fijo de base de datos puede ejecutar **sp_dropmergearticle**.  
  
## <a name="example"></a>Ejemplo  
  
```sql  
DECLARE @publication AS sysname;  
DECLARE @article1 AS sysname;  
DECLARE @article2 AS sysname;  
SET @publication = N'AdvWorksSalesOrdersMerge';  
SET @article1 = N'SalesOrderDetail';   
SET @article2 = N'SalesOrderHeader';   
  
-- Remove articles from a merge publication.  
USE [AdventureWorks]  
EXEC sp_dropmergearticle   
  @publication = @publication,   
  @article = @article1,  
  @force_invalidate_snapshot = 1;  
EXEC sp_dropmergearticle   
  @publication = @publication,   
  @article = @article2,  
  @force_invalidate_snapshot = 1;  
GO  
```  
  
```sql  
DECLARE @publication AS sysname;  
DECLARE @table1 AS sysname;  
DECLARE @table2 AS sysname;  
DECLARE @table3 AS sysname;  
DECLARE @salesschema AS sysname;  
DECLARE @hrschema AS sysname;  
DECLARE @filterclause AS nvarchar(1000);  
SET @publication = N'AdvWorksSalesOrdersMerge';   
SET @table1 = N'Employee';   
SET @table2 = N'SalesOrderHeader';   
SET @table3 = N'SalesOrderDetail';   
SET @salesschema = N'Sales';  
SET @hrschema = N'HumanResources';  
SET @filterclause = N'Employee.LoginID = HOST_NAME()';  
  
-- Drop the merge join filter between SalesOrderHeader and SalesOrderDetail.  
EXEC sp_dropmergefilter   
  @publication = @publication,   
  @article = @table3,   
  @filtername = N'SalesOrderDetail_SalesOrderHeader',   
  @force_invalidate_snapshot = 1,   
  @force_reinit_subscription = 1;  
  
-- Drops the merge join filter between Employee and SalesOrderHeader.  
EXEC sp_dropmergefilter   
  @publication = @publication,   
  @article = @table2,   
  @filtername = N'SalesOrderHeader_Employee',   
  @force_invalidate_snapshot = 1,   
  @force_reinit_subscription = 1;  
  
-- Drops the article for the SalesOrderDetail table.  
EXEC sp_dropmergearticle   
  @publication = @publication,   
  @article = @table3,  
  @force_invalidate_snapshot = 1,   
  @force_reinit_subscription = 1;  
  
-- Drops the article for the SalesOrderHeader table.  
EXEC sp_dropmergearticle   
  @publication = @publication,   
  @article = @table2,   
  @force_invalidate_snapshot = 1,   
  @force_reinit_subscription = 1;  
  
-- Drops the article for the Employee table.  
EXEC sp_dropmergearticle   
  @publication = @publication,   
  @article = @table1,  
  @force_invalidate_snapshot = 1,   
  @force_reinit_subscription = 1;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Eliminar un artículo](../../relational-databases/replication/publish/delete-an-article.md)   
 [Agregar y quitar artículos de publicaciones existentes](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)   
 [sp_addmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)   
 [sp_changemergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)   
 [sp_helpmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)   
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
