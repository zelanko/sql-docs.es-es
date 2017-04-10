---
title: "Ver y modificar las propiedades de un art&#237;culo | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
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
  - "sp_changearticle"
  - "sp_helparticle"
  - "ver propiedades de replicación"
  - "sp_changemergearticle"
  - "sp_helpmergearticle"
  - "modificar las propiedades de replicación, artículos"
  - "artículos [replicación de SQL Server], modificar"
  - "artículos [replicación de SQL Server], propiedades"
ms.assetid: e71831fa-3d39-4e4a-9706-4d3a497082cc
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 37
---
# Ver y modificar las propiedades de un art&#237;culo
  En este tema se describe cómo ver y modificar las propiedades del artículo en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)] o Replication Management Objects (RMO).  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Recomendaciones](#Recommendations)  
  
-   **Para ver y modificar las propiedades del artículo con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Algunas propiedades no se pueden modificar después de crearlas, y otras no se pueden modificar si existen suscripciones a la publicación. Las propiedades que no se pueden modificar se muestran como de solo lectura.  
  
###  <a name="Recommendations"></a> Recomendaciones  
  
-   Una vez creada una publicación, algunos cambios de las propiedades requieren una nueva instantánea. Si una publicación tiene suscripciones, algunos cambios también requieren reinicializar todas las suscripciones. Para obtener más información, consulte [Propiedades de artículo y publicación de cambio](../../../relational-databases/replication/publish/change-publication-and-article-properties.md) y [Agregar y quitar artículos de publicaciones existentes](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 Ver y modificar las propiedades del artículo en el **Propiedades de la publicación - \< publicación>** cuadro de diálogo, que está disponible en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] y Monitor de replicación. Para obtener información acerca de cómo iniciar el Monitor de replicación, vea [iniciar el Monitor de replicación](../../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
-   La página **General** incluye el nombre y la descripción de la publicación, el nombre de la base de datos, el tipo de publicación y los valores de expiración de la suscripción.  
  
-   La página **Artículos** corresponde a la página **Artículos** del Asistente para nueva publicación. Utilice esta página para agregar y eliminar artículos, y para cambiar propiedades y el filtro de columna de artículos.  
  
-   La página **Filtrar filas** corresponde a la página **Filtrar filas de tabla** del Asistente para nueva publicación. Utilice esta página para agregar, editar y eliminar filtros de fila estáticos de todos los tipos de publicaciones, y para agregar, editar y eliminar filtros de fila con parámetros y filtros de combinación de publicaciones de combinación.  
  
-   La página **Instantánea** permite especificar el formato y la ubicación de la instantánea, si la instantánea debe comprimirse y si los scripts deben ejecutarse antes y después de aplicar la instantánea.  
  
-   El **instantánea de FTP** página (de instantáneas y publicaciones transaccionales y publicaciones de mezcla para publicadores que ejecutan versiones anteriores a SQL Server 2005) le permite especificar si los suscriptores pueden descargar los archivos de instantáneas a través del protocolo de transferencia de archivos (FTP).  
  
-   El **instantánea de FTP e Internet** página (para publicaciones de mezcla de publicadores que ejecutan SQL Server 2005 o posterior) le permite especificar si los suscriptores pueden descargar los archivos de instantáneas mediante FTP, y si los suscriptores pueden sincronizar suscripciones a través de HTTPS.  
  
-   La página **Opciones de suscripción** permite establecer diversas opciones que se aplican a todas las suscripciones. Las opciones varían según el tipo de publicación.  
  
-   La página **Lista de acceso a la publicación** permite especificar qué inicios de sesión y grupos pueden tener acceso a una publicación.  
  
-   La página **Seguridad del agente** le permite tener acceso a la configuración para las cuentas con las que se ejecutan los agentes siguientes y realizan conexiones a los equipos en una topología de replicación: el Agente de instantáneas para todas las publicaciones, el Agente de registro del LOG para todas las publicaciones transaccionales y el Agente de lectura de cola para las publicaciones transaccionales que permiten las suscripciones de actualización en cola.  
  
-   El **particiones de datos** página (para publicaciones de mezcla de publicadores que ejecutan SQL Server 2005 o posterior) le permite especificar si los suscriptores de publicaciones con filtros parametrizados pueden solicitar una instantánea si no está disponible. También permite generar instantáneas de una o varias particiones, solo una vez o varias veces.  
  
#### Para ver y modificar propiedades de un artículo  
  
1.  En el **artículos** página de la **Propiedades de la publicación - \< publicación>** cuadro de diálogo, seleccione un artículo y, a continuación, haga clic en **Propiedades del artículo**.  
  
2.  Seleccione a qué propiedades de artículos se deben aplicar los cambios:  
  
    -   Haga clic en **establecer propiedades de resaltado \< ObjectType> artículo** para iniciar el **Propiedades del artículo: \< ObjectName>** cuadro de diálogo; propiedad los cambios realizados en este cuadro de diálogo se aplican únicamente al objeto que está resaltado en el panel de objetos en el **artículos** página.  
  
    -   Haga clic en **establecer propiedades de todos los \< ObjectType> artículos**, para iniciar la **Propiedades para todos \< ObjectType> artículos** cuadro de diálogo; propiedad los cambios realizados en este cuadro de diálogo se aplican a todos los objetos de ese tipo en el panel de objetos en el **artículos** página, las que todavía no se ha seleccionado para la publicación incluidas.  
  
        > [!NOTE]  
        >  Cambios de propiedades realizados en la **Propiedades para todos \< ObjectType> artículos** cuadro de diálogo reemplazan los realizados anteriormente en la **Propiedades del artículo: \< nombreDeObjeto>** cuadro de diálogo. Por ejemplo, si desea establecer varios valores predeterminados para todos los artículos de un tipo de objeto, pero solamente desea establecer algunas propiedades para objetos individuales, establezca primero los valores predeterminados para todos los artículos. A continuación, establezca las propiedades de los objetos individuales.  
  
3.  Modifique las propiedades si es necesario y, a continuación, haga clic en **Aceptar**.  
  
4.  Haga clic en **Aceptar** en la **Propiedades de la publicación - \< publicación>** cuadro de diálogo.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Se pueden modificar los artículos y devolver sus propiedades mediante programación con los procedimientos almacenados de replicación. Los procedimientos almacenados que se usen dependerán del tipo de publicación a la que pertenece el artículo.  
  
#### Para ver las propiedades de un artículo que pertenece a una publicación transaccional o de instantáneas  
  
1.  Ejecutar [sp_helparticle](../../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md), especificando el nombre de la publicación para el **@publication** parámetro y el nombre del artículo para el **@article** parámetro. Si no especifica **@article**, se devolverá información para todos los artículos de la publicación.  
  
2.  Ejecutar [sp_helparticlecolumns](../../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md) para artículos de tabla mostrar todas las columnas disponibles en la tabla base.  
  
#### Para modificar las propiedades de un artículo que pertenece a una publicación transaccional o de instantáneas  
  
1.  Ejecutar [sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md), especificando la propiedad de artículo que se está cambiando en el **@property** parámetro y el nuevo valor de esta propiedad en el **@value** parámetro.  
  
    > [!NOTE]  
    >  Si el cambio requiere la generación de una nueva instantánea, también debe especificar un valor de **1** para **@force_invalidate_snapshot**, y si el cambio requiere que se reinicialicen los suscriptores, también debe especificar un valor de **1** para **@force_reinit_subscription**. Para obtener más información acerca de las propiedades que, si se cambian, requieren una nueva instantánea o reinicialización, vea [Propiedades de artículo y publicación de cambio](../../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
#### Para ver las propiedades de un artículo que pertenece a una publicación de combinación  
  
1.  Ejecutar [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md), especificando el nombre de la publicación para el **@publication** parámetro y el nombre del artículo para el **@article** parámetro. Si no especifica estos parámetros, se devolverá información para todos los artículos de una publicación o en el publicador.  
  
2.  Ejecutar [sp_helpmergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-helpmergearticlecolumn-transact-sql.md) para artículos de tabla mostrar todas las columnas disponibles en la tabla base.  
  
#### Para modificar las propiedades de un artículo que pertenece a una publicación de combinación  
  
1.  Ejecutar [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md), especificando la propiedad de artículo que se está cambiando en el **@property** parámetro y el nuevo valor de esta propiedad en el **@value** parámetro.  
  
    > [!NOTE]  
    >  Si el cambio requiere la generación de una nueva instantánea, también debe especificar un valor de **1** para **@force_invalidate_snapshot**, y si el cambio requiere que se reinicialicen los suscriptores, también debe especificar un valor de **1** para **@force_reinit_subscription**. Para obtener más información acerca de las propiedades que, si se cambian, requieren una nueva instantánea o reinicialización, vea [Propiedades de artículo y publicación de cambio](../../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
###  <a name="TsqlExample"></a> Ejemplo (Transact-SQL)  
 Este ejemplo de replicación transaccional devuelve las propiedades del artículo publicado.  
  
 [!code-sql[HowTo#sp_helptranarticle](../../../relational-databases/replication/codesnippet/tsql/view-and-modify-article-_1.sql)]  
  
 Este ejemplo de replicación transaccional cambia las opciones de esquema del artículo publicado.  
  
 [!code-sql[HowTo#sp_changetranarticle](../../../relational-databases/replication/codesnippet/tsql/view-and-modify-article-_2.sql)]  
  
 Este ejemplo de replicación de mezcla devuelve las propiedades del artículo publicado.  
  
 [!code-sql[HowTo#sp_helpmergearticle](../../../relational-databases/replication/codesnippet/tsql/view-and-modify-article-_3.sql)]  
  
 Este ejemplo de replicación de mezcla cambia los valores de detección de conflictos para un artículo publicado.  
  
 [!code-sql[HowTo#sp_changemergearticle](../../../relational-databases/replication/codesnippet/tsql/view-and-modify-article-_4.sql)]  
  
##  <a name="RMOProcedure"></a> Usar Replication Management Objects (RMO)  
 Puede modificar los artículos y obtener acceso mediante programación a sus propiedades utilizando Replication Management Objects (RMO). Las clases RMO que usa para ver o modificar las propiedades de artículo dependen del tipo de publicación a la que pertenece el artículo.  
  
#### Para ver o modificar propiedades de un artículo que pertenece a una publicación transaccional o de instantáneas  
  
1.  Crear una conexión al publicador mediante la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> clase.  
  
2.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.TransArticle> clase.  
  
3.  Establecer el <xref:Microsoft.SqlServer.Replication.Article.Name%2A>, <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>, y <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> Propiedades.  
  
4.  Establezca la conexión del paso 1 para el <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propiedad.  
  
5.  Llame a la <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obtener las propiedades del objeto. Si este método devuelve **false**, se definieron incorrectamente las propiedades de artículo en el paso 3, o bien el artículo no existe.  
  
6.  (Opcional) Para cambiar las propiedades, establezca un nuevo valor para uno de los <xref:Microsoft.SqlServer.Replication.TransArticle> propiedades que se pueden establecer.  
  
7.  (Opcional) Si especifica un valor de **true** para <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, llame a la <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> método para confirmar los cambios en el servidor. Si especifica un valor de **false** para <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> (valor predeterminado), cambios se envían al servidor inmediatamente.  
  
#### Para ver o modificar propiedades de un artículo que pertenece a una publicación de combinación  
  
1.  Crear una conexión al publicador mediante la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> clase.  
  
2.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.MergeArticle> clase.  
  
3.  Establecer el <xref:Microsoft.SqlServer.Replication.Article.Name%2A>, <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>, y <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> Propiedades.  
  
4.  Establezca la conexión del paso 1 para el <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propiedad.  
  
5.  Llame a la <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obtener las propiedades del objeto. Si este método devuelve **false**, se definieron incorrectamente las propiedades de artículo en el paso 3, o bien el artículo no existe.  
  
6.  (Opcional) Para cambiar las propiedades, establezca un nuevo valor para uno de los <xref:Microsoft.SqlServer.Replication.MergeArticle> propiedades que se pueden establecer.  
  
7.  (Opcional) Si especifica un valor de **true** para <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, llame a la <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> método para confirmar los cambios en el servidor. Si especifica un valor de **false** para <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> (valor predeterminado), cambios se envían al servidor inmediatamente.  
  
###  <a name="PShellExample"></a> Ejemplo (RMO)  
 Este ejemplo cambia un artículo de mezcla para especificar el controlador de lógica de negocios que usa el artículo.  
  
 [!code-csharp[HowTo#rmo_ChangeMergeArticle_BLH](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_changemergearticle_blh)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeMergeArticle_BLH](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_changemergearticle_blh)]  
  
## Vea también  
 [Implementar un controlador de lógica de negocios para un artículo de mezcla](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)   
 [Publicar datos y objetos de base de datos](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Cambiar las propiedades de la publicación y de los artículos](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Conceptos sobre los procedimientos almacenados del sistema de replicación](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Detección y resolución de conflictos de replicación de mezcla avanzada](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  