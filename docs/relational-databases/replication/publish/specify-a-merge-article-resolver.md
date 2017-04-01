---
title: "Especificar un solucionador de art&#237;culos de mezcla | Microsoft Docs"
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
  - "artículos [replicación de SQL Server], resolución de conflictos"
  - "resolución de conflictos [replicación de SQL Server], replicación de mezcla"
  - "resolución de conflictos de replicación de mezcla [replicación de SQL Server], solucionador de artículos de mezcla"
ms.assetid: a40083b3-4f7b-4a25-a5a3-6ef67bdff440
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 39
---
# Especificar un solucionador de art&#237;culos de mezcla
  En este tema se describe cómo especificar un solucionador de artículos de mezcla en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Recomendaciones](#Recommendations)  
  
-   **Para especificar un solucionador de artículos de mezcla con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Recommendations"></a> Recomendaciones  
  
-   La replicación de mezcla admite los siguientes tipos de solucionadores de artículos:  
  
    -   El solucionador predeterminado. El comportamiento del solucionador predeterminado depende de si se trata de una suscripción de cliente o de servidor. Para obtener más información acerca de cómo especificar el tipo de suscripción, consulte [especificar un tipo de suscripción de mezcla y la prioridad de resolución de conflictos & #40; SQL Server Management Studio & #41;](../../../relational-databases/replication/specify a merge subscription type and conflict resolution priority.md).  
  
    -   Un solucionador personalizado, escrito por el usuario, que puede ser un controlador de lógica de negocios (escrito en código administrado) o un solucionador personalizado basado en COM. Para obtener más información, consulte [Advanced Merge Replication Conflict Detection and Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md). Si necesita implementar la lógica personalizada que se ejecuta para cada fila replicada, no sólo para las filas en conflicto, consulte [implementar un controlador de lógica de negocios para un artículo de mezcla](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md).  
  
    -   Un solucionador estándar basado en COM, que se incluye con [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Para utilizar un solucionador distinto del predeterminado, debe copiarlo en el equipo en el que se ejecuta el Agente de mezcla y registrarlo (si utiliza un controlador de lógica de negocios, también debe registrarlo en el publicador). El Agente de mezcla se ejecuta en:  
  
    -   El distribuidor, para una suscripción de inserción.  
  
    -   El suscriptor, para una suscripción de extracción.  
  
    -   El servidor con [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Internet Information Services (IIS), para una suscripción de extracción que utilice la sincronización web.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 Una vez registrado el solucionador, especificar que un artículo debe utilizar la resolución de la **resolución** ficha de la **Propiedades del artículo: \< artículo>** cuadro de diálogo, que está disponible en el Asistente para nueva publicación y la **Propiedades de la publicación - \< publicación>** cuadro de diálogo. Para obtener más información sobre cómo usar el asistente y acceso al cuadro de diálogo, vea [crear una publicación](../../../relational-databases/replication/publish/create-a-publication.md) y [Ver y modificar propiedades de publicación](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### Para especificar un solucionador  
  
1.  En el **artículos** página del Asistente para nueva publicación o **Propiedades de la publicación - \< publicación>** cuadro de diálogo, seleccione una tabla.  
  
2.  Haga clic en **Propiedades del artículo**y, a continuación, haga clic en **Establecer propiedades del artículo de tabla resaltado**.  
  
3.  En la **Propiedades del artículo: \< artículo>** haga clic en el **resolución** ficha.  
  
4.  Seleccione **utilizar una resolución personalizada (registrada en el distribuidor)**, y, a continuación, en la lista, haga clic en la resolución.  
  
5.  Si el solucionador requiere entrada (por ejemplo, un nombre de columna), especifíquela en el **Escriba la información necesaria para la resolución de** cuadro de texto.  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
7.  Repita este proceso para cada artículo que necesite un solucionador.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### Para registrar un solucionador de conflictos personalizado  
  
1.  Si piensa registrar su propio solucionador de conflictos personalizado, cree uno de los tipos siguientes:  
  
    -   Solucionador basado en código administrado como un controlador de lógica de negocios. Para más información, consulte [Implement a Business Logic Handler for a Merge Article](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md).  
  
    -   Solucionador basado en procedimientos almacenados y solucionador basado en COM. Para más información, consulte [Implement a Custom Conflict Resolver for a Merge Article](../../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md).  
  
2.  Para determinar si el solucionador deseado ya está registrado, ejecute [sp_enumcustomresolvers & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) en el publicador de cualquier base de datos. Esto muestra una descripción del solucionador personalizado así como del identificador de clase (CLSID) de cada solucionador basado en COM registrado en el distribuidor o información sobre el ensamblado administrado de cada controlador de lógica de negocios registrado en el distribuidor.  
  
3.  Si no se ha registrado el solucionador personalizado, ejecute [sp_registercustomresolver & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql.md) en el distribuidor. Especifique un nombre para la resolución de **@article_resolver**; para un controlador de lógica de negocios, es el nombre descriptivo del ensamblado. Para las resoluciones basadas en COM, especifique el CLSID de la DLL para **@resolver_clsid**, y para un controlador de lógica de negocios, especifique un valor de **true** para **@is_dotnet_assembly**, el nombre del ensamblado de **@dotnet_assembly_name**, y el nombre completo de la clase que reemplaza <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> de **@dotnet_class_name**.  
  
    > [!NOTE]  
    >  Si no se implementa un ensamblado de controlador de lógica de negocios en el mismo directorio que el ejecutable del agente de mezcla, en el mismo directorio que la aplicación que inicia de forma sincrónica el agente de mezcla o en la caché de ensamblados global (GAC), debe especificar la ruta de acceso completa con el nombre de ensamblado para **@dotnet_assembly_name**.  
  
4.  Si el solucionador es un solucionador basado en COM:  
  
    -   Copie la DLL del solucionador personalizado en el distribuidor para la suscripción de inserción o en el suscriptor para las suscripciones de extracción.  
  
        > [!NOTE]  
        >  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] solucionadores personalizados pueden encontrarse en el [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]directorio COM.  
  
    -   Utilice regsvr32.exe para registrar la DLL del solucionador personalizado con el sistema operativo. Por ejemplo, al ejecutar lo siguiente desde el símbolo del sistema se registra el solucionador de conflictos de suma de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] :  
  
        ```  
        regsvr32 ssradd.dll  
        ```  
  
5.  Si la resolución es un controlador de lógica de negocios, implemente el ensamblado en la misma carpeta que el ejecutable del agente de mezcla (replmerg.exe), en la misma carpeta que la aplicación que invoca el agente de mezcla, o en la carpeta especificada para la **@dotnet_assembly_name** parámetro en el paso 3.  
  
    > [!NOTE]  
    >  La ubicación de instalación predeterminada de la aplicación ejecutable de Agente de mezcla es [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]COM.  
  
#### Para especificar un solucionador personalizado al definir un artículo de mezcla  
  
1.  Si tiene previsto utilizar un solucionador de conflictos personalizado, cree y registre el solucionador mediante el procedimiento anterior.  
  
2.  En el publicador, ejecute [sp_enumcustomresolvers & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) y anote el nombre del solucionador personalizado deseado en el **valor** campo del conjunto de resultados.  
  
3.  En el publicador de la base de datos de publicación, ejecute [sp_addmergearticle & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Especifique el nombre del solucionador del paso 2 para **@article_resolver** y cualquier entrada necesaria para la resolución personalizada mediante el **@resolver_info** parámetro. Para almacenado solucionadores personalizados basados en procedimientos, **@resolver_info** es el nombre del procedimiento almacenado. Para obtener más información acerca de la entrada necesaria para las resoluciones proporcionado por [!INCLUDE[msCoName](../../../includes/msconame-md.md)], consulte [solucionadores basados en COM de Microsoft](../../../relational-databases/replication/merge/microsoft-com-based-resolvers.md).  
  
#### Para especificar o cambiar un solucionador personalizado para un artículo de mezcla existente  
  
1.  Para determinar si se ha definido una resolución personalizada para un artículo, o para obtener el nombre de la resolución, ejecute [sp_helpmergearticle & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md). Si hay una resolución personalizada definida para el artículo, su nombre se mostrará en el **article_resolver** campo. Cualquier entrada proporcionada a la resolución se mostrarán en el **resolver_info** campo del conjunto de resultados.  
  
2.  En el publicador, ejecute [sp_enumcustomresolvers & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) y anote el nombre del solucionador personalizado deseado en el **valor** campo del conjunto de resultados.  
  
3.  En el publicador de la base de datos de publicación, ejecute [sp_changemergearticle & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md). Especifique un valor de **article_resolver**, incluida la ruta completa de los controladores de lógica de negocios para **@property**, y el nombre del solucionador personalizado deseado del paso 2 para **@value**.  
  
4.  Para cambiar cualquier entrada necesaria para la resolución personalizada, ejecute [sp_changemergearticle & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) de nuevo. Especifique un valor de **resolver_info** para **@property** y cualquier entrada necesaria para la resolución personalizada para **@value**. Para almacenado solucionadores personalizados basados en procedimientos, **@resolver_info** es el nombre del procedimiento almacenado. Para obtener más información acerca de la entrada necesaria, consulte [solucionadores basados en COM de Microsoft](../../../relational-databases/replication/merge/microsoft-com-based-resolvers.md).  
  
#### Para eliminar del registro un solucionador de conflictos personalizado  
  
1.  En el publicador, ejecute [sp_enumcustomresolvers & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) y anote el nombre de la resolución personalizada para quitar de la **valor** campo del conjunto de resultados.  
  
2.  Ejecutar [sp_unregistercustomresolver & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql.md) en el distribuidor. Especifique el nombre completo de la resolución personalizada del paso 1 para **@article_resolver**.  
  
###  <a name="TsqlExample"></a> Ejemplos (Transact-SQL)  
 En este ejemplo se crea un nuevo artículo y se especifica que se utilice el Solucionador de conflictos de cálculo de media de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para calcular la media de la columna **UnitPrice** cuando se produzcan conflictos.  
  
 [!code-sql[HowTo#sp_addmerge_resolver](../../../relational-databases/replication/codesnippet/tsql/specify-a-merge-article-_1.sql)]  
  
 Este ejemplo cambia un artículo para especificar que se use el Solucionador de conflictos de suma de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con el fin de calcular la suma de la columna **UnitsOnOrder** cuando se produzcan conflictos.  
  
 [!code-sql[HowTo#sp_changemerge_resolver](../../../relational-databases/replication/codesnippet/tsql/specify-a-merge-article-_2.sql)]  
  
## Vea también  
 [Detección y resolución de conflictos de replicación de mezcla avanzada](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Implementar un controlador de lógica de negocios para un artículo de mezcla](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)  
  
  