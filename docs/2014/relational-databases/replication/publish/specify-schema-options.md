---
title: Especificar las opciones del esquema | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- schemas [SQL Server replication], options
- articles [SQL Server replication], transactional replication options
- articles [SQL Server replication], merge replication options
- articles [SQL Server replication], schema options
ms.assetid: 1f85a479-bd6e-4023-abf7-7435a7e5b567
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e6826d28ec923de221e94b985b740a172bdaa7d5
ms.sourcegitcommit: 619917a0f91c8f1d9112ae6ad9cdd7a46a74f717
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2019
ms.locfileid: "73882163"
---
# <a name="specify-schema-options"></a>Especificar las opciones del esquema
  En este tema se describe cómo especificar las opciones de esquema en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Al publicar una tabla o una vista, puede controlar las opciones de creación de objetos que se replican para el objeto publicado. Puede establecer estas opciones cuando se haya creado el artículo y también puede modificarlas posteriormente. Si no especifican explícitamente estas opciones para un artículo, se definirá un conjunto predeterminado de opciones.  
  
> [!NOTE]  
>  Las opciones de esquema predeterminadas cuando se usan procedimientos almacenados de replicación pueden diferir de las opciones predeterminadas cuando los artículos se agregan mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Recomendaciones](#Recommendations)  
  
-   **Para especificar las opciones del esquema con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Si se cambian opciones de esquema después de crear una publicación, se debe generar una nueva instantánea.  
  
###  <a name="Recommendations"></a> Recomendaciones  
  
-   Para obtener una lista completa de las opciones de esquema, vea el parámetro **\@schema_option** de [ &#40;sp_addarticle&#41; Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql) y [ &#40;sp_addmergearticle&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql).  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 Especifique las opciones de los esquemas (por ejemplo, si quiere copiar las restricciones y los desencadenadores para los suscriptores) en la pestaña **Propiedades** del cuadro de diálogo **Propiedades del artículo: \<artículo>** . Dicha pestaña está disponible en el Asistente para nueva publicación y en el cuadro de diálogo **Propiedades de la publicación: \<publicación>** . Para más información sobre el uso del asistente y el acceso al cuadro de diálogo, vea [Crear una publicación](create-a-publication.md) y [Ver y modificar propiedades de publicación](view-and-modify-publication-properties.md).  
  
#### <a name="to-specify-schema-options"></a>Para especificar las opciones del esquema  
  
1.  En la página **Artículos** del Asistente para nueva publicación o en el cuadro de diálogo **Propiedades de la publicación: \<publicación>** , seleccione un artículo y, luego, haga clic en **Propiedades del artículo**.  
  
2.  Seleccione qué cambios de opción de esquema de artículos se deben aplicar:  
  
    -   Haga clic en **Establecer propiedades del artículo de \<tipoDeObjeto> resaltado** para iniciar el cuadro de diálogo **Propiedades del artículo: \<nombreDeObjeto>** . Los cambios de propiedad realizados en este cuadro de diálogo solo se aplican al objeto que está resaltado en el panel de objetos de la página **Artículos**.  
  
    -   Haga clic en **Establecer propiedades de todos los artículos de \<tipoDeObjeto>** para iniciar el cuadro de diálogo **Propiedades de todos los artículos de \<tipoDeObjeto>** ; los cambios de propiedad realizados en este cuadro de diálogo se aplican a todos los objetos de ese tipo en el panel de objetos de la página **Artículos**, incluidos los que todavía no se hayan seleccionado para la publicación.  
  
        > [!NOTE]  
        >  Los cambios de propiedades realizados en el cuadro de diálogo **Propiedades de todos los artículos de \<tipoDeObjeto>** reemplazan los que se hicieran anteriormente en el cuadro de diálogo **Propiedades del artículo: \<tipoDeObjeto>** . Por ejemplo, si desea establecer varios valores predeterminados para todos los artículos de un tipo de objeto, pero solamente desea establecer algunas propiedades para objetos individuales, establezca primero los valores predeterminados para todos los artículos. A continuación, establezca las propiedades de los objetos individuales.  
  
3.  En las secciones **Copiar objetos y configuración en el suscriptor** y **Objeto de destino** de la pestaña **Propiedades** del cuadro de diálogo **Propiedades del artículo: \<artículo>** , especifique los valores de las opciones.  
  
4.  Modifique las propiedades si es necesario y, a continuación, haga clic en **Aceptar**.  
  
5.  Si se encuentra en el cuadro de diálogo **Propiedades de la publicación: \<publicación>** , haga clic en **Aceptar** para guardar y cerrar el cuadro de diálogo.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Las opciones de esquema se especifican como un valor hexadecimal que es el resultado [| (OR bit a bit)](/sql/t-sql/language-elements/bitwise-or-transact-sql) de una o más opciones. Para obtener más información, vea [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql) y [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql).  
  
> [!NOTE]  
>  Debe convertir los valores de opción de esquema de **binary** a **int** antes de realizar una operación bit a bit. Para obtener más información, vea [CAST y CONVERT &#40;Transact-SQL&#41;](/sql/t-sql/functions/cast-and-convert-transact-sql).  
  
#### <a name="to-specify-schema-options-when-defining-an-article-for-a-snapshot-or-transactional-publication"></a>Para especificar las opciones de esquema al definir un artículo para una publicación transaccional o de instantáneas  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql). Especifique el nombre de la publicación a la que pertenece el artículo para **\@publicación**, un nombre para el artículo **\@artículo**, el objeto de base de datos que se publica para **\@source_object**, el tipo de objeto de base de datos para el **tipo de\@** y el [| (OR bit a bit)](/sql/t-sql/language-elements/bitwise-or-transact-sql) resultado de una o más opciones de esquema para **\@schema_option**. Para obtener más información, consulte [Define an Article](define-an-article.md).  
  
#### <a name="to-specify-schema-options-when-defining-an-article-for-a-merge-publication"></a>Para especificar las opciones de esquema al definir un artículo para una publicación de combinación  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql). Especifique el nombre de la publicación a la que pertenece el artículo para **\@publicación**, un nombre para el artículo **\@artículo**, el objeto de base de datos que se publica para **\@source_object**y el [| (OR bit a bit)](/sql/t-sql/language-elements/bitwise-or-transact-sql) resultado de una o más opciones de esquema para **\@schema_option**. Para obtener más información, consulte [Define an Article](define-an-article.md).  
  
#### <a name="to-change-schema-options-for-an-existing-article-in-a-snapshot-or-transactional-publication"></a>Para cambiar las opciones de esquema para un artículo existente en una publicación transaccional o de instantáneas  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_helparticle](/sql/relational-databases/system-stored-procedures/sp-helparticle-transact-sql). Especifique el nombre de la publicación a la que pertenece el artículo para **\@publicación** y el nombre del artículo para **\@artículo**. Tenga en cuenta el valor de la columna de **schema_option** en el conjunto de resultados.  
  
2.  Para determinar si la opción está o no establecida, ejecute una operación [& (AND bit a bit)](/sql/t-sql/language-elements/bitwise-and-transact-sql) con el valor del paso 1 y el valor de opción de esquema pertinente.  
  
    -   Si el resultado es **0**, la opción no está establecida.  
  
    -   Si el resultado es el valor de opción, ésta ya está establecida.  
  
3.  Si la opción no está establecida, ejecute una operación [| (OR bit a bit)](/sql/t-sql/language-elements/bitwise-or-transact-sql) con el valor del paso 1 y el valor de opción de esquema deseado.  
  
4.  En la base de datos de publicación del publicador, ejecute [sp_changearticle](/sql/relational-databases/system-stored-procedures/sp-changearticle-transact-sql). Especifique el nombre de la publicación a la que pertenece el artículo para **\@publicación**, el nombre del artículo para **\@artículo**, un valor de **schema_option** para **\@propiedad**y el resultado hexadecimal del paso 3 para **\@valor**.  
  
5.  Ejecute el Agente de instantáneas para generar una nueva instantánea. Para más información, consulte [Create and Apply the Initial Snapshot](../create-and-apply-the-initial-snapshot.md).  
  
#### <a name="to-change-schema-options-for-an-existing-article-in-a-merge-publication"></a>Para cambiar las opciones de esquema de un artículo existente en una publicación de mezcla  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_helpmergearticle](/sql/relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql). Especifique el nombre de la publicación a la que pertenece el artículo para **\@publicación** y el nombre del artículo para **\@artículo**. Tenga en cuenta el valor de la columna de **schema_option** en el conjunto de resultados.  
  
2.  Para determinar si la opción está o no establecida, ejecute una operación [& (AND bit a bit)](/sql/t-sql/language-elements/bitwise-and-transact-sql) con el valor del paso 1 y el valor de opción de esquema pertinente.  
  
    -   Si el resultado es **0**, la opción no está establecida.  
  
    -   Si el resultado es el valor de opción, ésta ya está establecida.  
  
3.  Si la opción no está establecida, ejecute una operación [| (OR bit a bit)](/sql/t-sql/language-elements/bitwise-or-transact-sql) con el valor del paso 1 y el valor de opción de esquema deseado.  
  
4.  En la base de datos de publicación del publicador, ejecute [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql). Especifique el nombre de la publicación a la que pertenece el artículo para **\@publicación**, el nombre del artículo para **\@artículo**, un valor de **schema_option** para **\@propiedad**y el resultado hexadecimal del paso 3 para **\@valor**.  
  
5.  Ejecute el Agente de instantáneas para generar una nueva instantánea. Para más información, consulte [Create and Apply the Initial Snapshot](../create-and-apply-the-initial-snapshot.md).  
  
## <a name="see-also"></a>Vea también  
 [Publicar datos y objetos de base de datos](publish-data-and-database-objects.md)   
 [Opciones de artículos para la replicación transaccional](../transactional/article-options-for-transactional-replication.md)  
  
  
