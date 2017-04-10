---
title: "Definir un art&#237;culo | Microsoft Docs"
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
  - "artículos [replicación de SQL Server], definir"
  - "sp_addmergearticle"
  - "agregar artículos"
  - "sp_addarticle"
  - "artículos [replicación de SQL Server], agregar"
ms.assetid: 220584d8-b291-43ae-b036-fbba3cc07a2e
caps.latest.revision: 45
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 45
---
# Definir un art&#237;culo
  En este tema se describe cómo definir un artículo en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)] o Replication Management Objects (RMO).  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para definir un artículo, mediante:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Los nombres del artículo no pueden incluir ninguno de los caracteres siguientes: % , * , [ , ] , | , : , " , ? , ' , \ , / , \< , >. Si los objetos de la base de datos incluyen cualquiera de estos caracteres y desea replicarlos, debe especificar un nombre de artículo diferente del nombre de objeto.  
  
##  <a name="Security"></a> Seguridad  
 Cuando sea posible, pida a los usuarios que proporcionen credenciales de seguridad en tiempo de ejecución. Si debe almacenar credenciales, use los [servicios de cifrado](http://go.microsoft.com/fwlink/?LinkId=34733) (en inglés) proporcionados por [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows .NET Framework.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 Cree publicaciones y defina artículos con el Asistente para nueva publicación. Después de crea una publicación, ver y modificar propiedades de la publicación en la **Propiedades de la publicación - \< publicación>** cuadro de diálogo. Para obtener información acerca de cómo crear una publicación de una base de datos de Oracle, vea [crear una publicación de una base de datos de Oracle](../../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md).  
  
#### Para crear publicaciones y definir artículos  
  
1.  Conéctese al publicador en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]y, a continuación, expanda el nodo del servidor.  
  
2.  Expanda el **replicación** carpeta y, a continuación, con el botón secundario del **publicaciones locales** carpeta.  
  
3.  Haga clic en **Nueva publicación**.  
  
4.  Siga las indicaciones de las páginas del Asistente para nueva publicación para:  
  
    -   Especificar un distribuidor si la distribución no se ha configurado en el servidor. Para obtener más información acerca de cómo configurar la distribución, consulte [Configurar publicación y distribución](../../../relational-databases/replication/configure-publishing-and-distribution.md).  
  
         Si se especifica en el **distribuidor** página que el servidor del publicador actuará como su propio distribuidor (distribuidor local) y el servidor no está configurado como distribuidor, el Asistente para nueva publicación configurará el servidor. Especifique una carpeta de instantáneas predeterminada para el distribuidor en la página **Carpeta de instantáneas** . La carpeta de instantáneas es simplemente un directorio designado como recurso compartido; los agentes que leen y escriben en esta carpeta deben tener permisos de acceso suficientes a ella. Para obtener más información acerca de cómo proteger la carpeta adecuadamente, consulte [proteger la carpeta de instantáneas](../../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
         Si especifica que otro servidor actúe como distribuidor, deberá escribir una contraseña en la página **Contraseña administrativa** para las conexiones que se realicen desde el publicador al distribuidor. Esta contraseña debe coincidir con la especificada cuando se habilitó el publicador en el distribuidor remoto.  
  
         Para obtener más información, consulte [Configurar distribución](../../../relational-databases/replication/configure-distribution.md).  
  
    -   Elegir una base de datos de publicación.  
  
    -   Seleccionar un tipo de publicación. Para obtener más información, consulte [tipos de replicación](../../../relational-databases/replication/types-of-replication.md).  
  
    -   Especificar los datos y los objetos de base de datos que se van a publicar; de forma opcional, filtrar columnas de artículos de tablas y establecer las propiedades de los artículos.  
  
    -   De forma opcional, filtrar filas de artículos de tablas. Para obtener más información, consulte [filtrar datos publicados](../../../relational-databases/replication/publish/filter-published-data.md).  
  
    -   Establecer la programación del Agente de instantáneas.  
  
    -   Especificar las credenciales con las que los siguientes agentes de replicación se ejecutan y efectúan conexiones:  
  
         \- Agente de instantáneas para todas las publicaciones.  
  
         \- Agente de lector del registro para todas las publicaciones transaccionales.  
  
         \- Agente de lectura de cola para publicaciones transaccionales que permiten suscripciones de actualización.  
  
         Para obtener más información, consulte [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md) y [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md).  
  
    -   De forma opcional, incluir la publicación. Para más información, consulte [Scripting Replication](../../../relational-databases/replication/scripting-replication.md).  
  
    -   Especificar un nombre para la publicación.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Una vez creada una publicación, los artículos se pueden crear mediante programación usando los procedimientos almacenados de replicación. Los procedimientos almacenados usados para crear un artículo dependerán del tipo de publicación para la que se está definiendo el artículo. Para más información, consulte [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md).  
  
#### Para definir un artículo para una publicación transaccional o de instantáneas  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Especifique el nombre de la publicación a la que pertenece el artículo para **@publication**, un nombre de artículo para **@article**, el objeto de base de datos que se publica para **@source_object**, y cualquier otro parámetro opcional. Utilice **@source_owner** para especificar la propiedad del esquema del objeto, si no **dbo**. Si el artículo no es un artículo de tabla basado en el registro, especifique el tipo de artículo para **@type**; para obtener más información, consulte [especificar tipos de artículo & #40; Programación de Transact-SQL de replicación & #41;](../../../relational-databases/replication/publish/specify-article-types-replication-transact-sql-programming.md).  
  
2.  Para horizontalmente filtrar filas en una tabla o ver un artículo, utilice [sp_articlefilter](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md) para definir la cláusula de filtro. Para más información, consulte [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md).  
  
3.  Para verticalmente filtrar columnas de una tabla o ver un artículo, utilice [sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md). Para más información, consulte [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  
  
4.  Ejecutar [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) Si se filtra el artículo.  
  
5.  Si la publicación tiene suscripciones existentes y [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md) devuelve un valor de **0** en el **immediate_sync** columna, se debe llamar a [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) para agregar el artículo a cada suscripción existente.  
  
6.  Si la publicación tiene existente suscripciones de extracción, ejecute [sp_refreshsubscriptions](../../../relational-databases/system-stored-procedures/sp-refreshsubscriptions-transact-sql.md) en el publicador para crear una nueva instantánea para suscripciones de extracción existente que contiene únicamente el nuevo artículo.  
  
    > [!NOTE]  
    >  Para las suscripciones que no se inicializan con una instantánea, no necesitará ejecutar [sp_refreshsubscriptions](../../../relational-databases/system-stored-procedures/sp-refreshsubscriptions-transact-sql.md) este procedimiento se ejecuta por [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md).  
  
#### Para definir un artículo para una publicación de combinación  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Especifique el nombre de la publicación para **@publication**, un nombre para el nombre del artículo para **@article**, y el objeto que se publica para **@source_object**. Para filtrar horizontalmente filas de tabla, especifique un valor para **@subset_filterclause**. Para obtener más información, consulte [Define and Modify a Parameterized Row Filter for a Merge Article](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md) y [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md). Si el artículo no es un artículo de tabla, especifique el tipo de artículo para **@type**. Para obtener más información, consulte [especificar tipos de artículo & #40; Programación de Transact-SQL de replicación & #41;](../../../relational-databases/replication/publish/specify-article-types-replication-transact-sql-programming.md).  
  
2.  (Opcional) En el publicador de la base de datos de publicación, ejecute [sp_addmergefilter](../../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md) para definir un filtro de combinación entre dos artículos. Para obtener más información, consulte [Define and Modify a Join Filter Between Merge Articles](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md).  
  
3.  (Opcional) En el publicador de la base de datos de publicación, ejecute [sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md) para filtrar columnas de tabla. Para más información, consulte [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  
  
###  <a name="TsqlExample"></a> Ejemplos (Transact-SQL)  
 En este ejemplo se define un artículo basado en la tabla `Product` para una publicación transaccional, donde el artículo se filtra tanto horizontal como verticalmente.  
  
 [!code-sql[HowTo#sp_AddTranArticle](../../../relational-databases/replication/codesnippet/tsql/define-an-article_1.sql)]  
  
 En este ejemplo se definen artículos para una publicación de mezcla, donde el artículo `SalesOrderHeader` se filtra estáticamente según **SalesPersonID**y el artículo `SalesOrderDetail` se filtra por combinación según `SalesOrderHeader`.  
  
 [!code-sql[HowTo#sp_AddMergeArticle](../../../relational-databases/replication/codesnippet/tsql/define-an-article_2.sql)]  
  
##  <a name="RMOProcedure"></a> Usar Replication Management Objects (RMO)  
 Puede definir artículos mediante programación utilizando Replication Management Objects (RMO). Las clases RMO que usa para definir un artículo dependen del tipo de publicación para la que se define el artículo.  
  
###  <a name="PShellExample"></a> Ejemplos (RMO)  
 El ejemplo siguiente agrega un artículo con filtros de filas y columnas a una publicación transaccional.  
  
 [!code-csharp[HowTo#rmo_CreateTranArticles](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createtranarticles)]  
  
 [!code-vb[HowTo#rmo_vb_CreateTranArticles](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createtranarticles)]  
  
 El ejemplo siguiente agrega tres artículos a una publicación de combinación. Los artículos tienen filtros de columna y se usan dos filtros de combinación para propagar un filtro de fila con parámetros a los demás artículos.  
  
 [!code-csharp[HowTo#rmo_CreateMergeArticles](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createmergearticles)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergeArticles](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createmergearticles)]  
  
## Vea también  
 [Crear una publicación](../../../relational-databases/replication/publish/create-a-publication.md)   
 [Conceptos sobre los procedimientos almacenados del sistema de replicación](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Agregar y quitar artículos de publicaciones existentes](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)   
 [Filtrar datos publicados](../../../relational-databases/replication/publish/filter-published-data.md)   
 [Publicar datos y objetos de base de datos](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Conceptos sobre los procedimientos almacenados del sistema de replicación](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)  
  
  