---
title: "Especificar las opciones del esquema | Microsoft Docs"
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
  - "esquemas [replicación de SQL Server], opciones"
  - "artículos [replicación de SQL Server], opciones de replicación transaccional"
  - "artículos [replicación de SQL Server], opciones de replicación de mezcla"
  - "artículos [replicación de SQL Server], opciones de esquemas"
ms.assetid: 1f85a479-bd6e-4023-abf7-7435a7e5b567
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 39
---
# Especificar las opciones del esquema
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
  
-   Para obtener una lista completa de opciones de esquema, consulte el **@schema_option** parámetro de [sp_addarticle & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) y [sp_addmergearticle & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md).  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 Especificar opciones de esquema, por ejemplo, si se deben copiar restricciones y desencadenadores a los suscriptores, en la **propiedades** ficha de la **Propiedades del artículo: \< artículo>** cuadro de diálogo. Esta pestaña está disponible en el Asistente para nueva publicación y **Propiedades de la publicación - \< publicación>** cuadro de diálogo. Para obtener más información sobre cómo usar el asistente y acceso al cuadro de diálogo, vea [crear una publicación](../../../relational-databases/replication/publish/create-a-publication.md) y [Ver y modificar propiedades de publicación](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### Para especificar las opciones del esquema  
  
1.  En el **artículos** página del Asistente para nueva publicación o **Propiedades de la publicación - \< publicación>** cuadro de diálogo, seleccione un artículo y, a continuación, haga clic en **Propiedades del artículo**.  
  
2.  Seleccione qué cambios de opción de esquema de artículos se deben aplicar:  
  
    -   Haga clic en **establecer propiedades de resaltado \< ObjectType> artículo** para iniciar el **Propiedades del artículo: \< ObjectName>** cuadro de diálogo; propiedad los cambios realizados en este cuadro de diálogo se aplican únicamente al objeto que está resaltado en el panel de objetos en el **artículos** página.  
  
    -   Haga clic en **establecer propiedades de todos los \< ObjectType> artículos** para iniciar el **Propiedades para todos \< ObjectType> artículos** cuadro de diálogo; propiedad los cambios realizados en este cuadro de diálogo se aplican a todos los objetos de ese tipo en el panel de objetos en el **artículos** página, las que todavía no se ha seleccionado para la publicación incluidas.  
  
        > [!NOTE]  
        >  Cambios de propiedades realizados en la **Propiedades para todos \< ObjectType> artículos** cuadro de diálogo reemplazan los realizados anteriormente en la **Propiedades del artículo: \< nombreDeObjeto>** cuadro de diálogo. Por ejemplo, si desea establecer varios valores predeterminados para todos los artículos de un tipo de objeto, pero solamente desea establecer algunas propiedades para objetos individuales, establezca primero los valores predeterminados para todos los artículos. A continuación, establezca las propiedades de los objetos individuales.  
  
3.  En el **Copiar objetos y configuración en el suscriptor** y **el objeto de destino** secciones de la **propiedades** ficha de la **Propiedades del artículo: \< artículo>** cuadro de diálogo, especifique valores para las opciones.  
  
4.  Modifique las propiedades si es necesario y, a continuación, haga clic en **Aceptar**.  
  
5.  Si se encuentra en la **Propiedades de la publicación - \< publicación>** cuadro de diálogo, haga clic en **Aceptar** para guardar y cerrar el cuadro de diálogo.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Opciones de esquema se especifican como un valor hexadecimal que es el [| (OR bit a bit)](../Topic/%7C%20\(Bitwise%20OR\)%20\(Transact-SQL\).md) resultado de una o más opciones. Para obtener más información, consulte [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) y [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md).  
  
> [!NOTE]  
>  Debe convertir los valores de opción de esquema de **binary** a **int** antes de realizar una operación bit a bit. Para obtener más información, consulte [CAST y CONVERT & #40; Transact-SQL & #41;](../../../t-sql/functions/cast-and-convert-transact-sql.md).  
  
#### Para especificar las opciones de esquema al definir un artículo para una publicación transaccional o de instantáneas  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Especifique el nombre de la publicación a la que pertenece el artículo para **@publication**, un nombre de artículo para **@article**, el objeto de base de datos que se publica para **@source_object**, el tipo de objeto de base de datos para **@type**, y el [| (OR bit a bit)](../Topic/%7C%20\(Bitwise%20OR\)%20\(Transact-SQL\).md) resultado de una o más opciones de esquema para **@schema_option**. Para más información, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
#### Para especificar las opciones de esquema al definir un artículo para una publicación de combinación  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Especifique el nombre de la publicación a la que pertenece el artículo para **@publication**, un nombre de artículo para **@article**, el objeto de base de datos que se publica para **@source_object**, y el [| (OR bit a bit)](../Topic/%7C%20\(Bitwise%20OR\)%20\(Transact-SQL\).md) resultado de una o más opciones de esquema para **@schema_option**. Para más información, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
#### Para cambiar las opciones de esquema para un artículo existente en una publicación transaccional o de instantáneas  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_helparticle](../../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md). Especifique el nombre de la publicación a la que pertenece el artículo para **@publication** y el nombre de artículo para **@article**. Tenga en cuenta el valor de la **schema_option** columna del conjunto de resultados.  
  
2.  Ejecutar un [& (AND bit a bit)](../../../t-sql/language-elements/bitwise-and-transact-sql.md) valor para determinar si se ha establecido la opción de la opción de operación mediante el valor del paso 1 y el esquema deseado.  
  
    -   Si el resultado es **0**, la opción no está establecida.  
  
    -   Si el resultado es el valor de opción, ésta ya está establecida.  
  
3.  Si no se establece la opción, ejecute un [| (OR bit a bit)](../Topic/%7C%20\(Bitwise%20OR\)%20\(Transact-SQL\).md) operación utilizando el valor del paso 1 y el valor de la opción de esquema que desee.  
  
4.  En el publicador de la base de datos de publicación, ejecute [sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md). Especifique el nombre de la publicación a la que pertenece el artículo para **@publication**, el nombre del artículo para **@article**, un valor de **schema_option** para **@property**, y el resultado hexadecimal del paso 3 para **@value**.  
  
5.  Ejecute el Agente de instantáneas para generar una nueva instantánea. Para obtener más información, consulte [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
#### Para cambiar las opciones de esquema de un artículo existente en una publicación de mezcla  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md). Especifique el nombre de la publicación a la que pertenece el artículo para **@publication** y el nombre de artículo para **@article**. Tenga en cuenta el valor de la **schema_option** columna del conjunto de resultados.  
  
2.  Ejecutar un [& (AND bit a bit)](../../../t-sql/language-elements/bitwise-and-transact-sql.md) valor para determinar si se ha establecido la opción de la opción de operación mediante el valor del paso 1 y el esquema deseado.  
  
    -   Si el resultado es **0**, la opción no está establecida.  
  
    -   Si el resultado es el valor de opción, ésta ya está establecida.  
  
3.  Si no se establece la opción, ejecute un [| (OR bit a bit)](../Topic/%7C%20\(Bitwise%20OR\)%20\(Transact-SQL\).md) operación utilizando el valor del paso 1 y el valor de la opción de esquema que desee.  
  
4.  En el publicador de la base de datos de publicación, ejecute [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md). Especifique el nombre de la publicación a la que pertenece el artículo para **@publication**, el nombre del artículo para **@article**, un valor de **schema_option** para **@property**, y el resultado hexadecimal del paso 3 para **@value**.  
  
5.  Ejecute el Agente de instantáneas para generar una nueva instantánea. Para obtener más información, consulte [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
## Vea también  
 [Publicar datos y objetos de base de datos](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Opciones de artículos para la replicación transaccional](../../../relational-databases/replication/transactional/article-options-for-transactional-replication.md)  
  
  