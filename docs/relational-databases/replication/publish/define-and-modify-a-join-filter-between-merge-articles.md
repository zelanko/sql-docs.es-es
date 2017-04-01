---
title: "Definir y modificar un filtro de combinaci&#243;n entre art&#237;culos de mezcla | Microsoft Docs"
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
  - "filtros [replicación de SQL Server], combinar"
  - "filtros de combinación de replicación de mezcla [replicación de SQL Server]"
  - "modificar filtros, combinar"
  - "filtros de combinación"
ms.assetid: f7f23415-43ff-40f5-b3e0-0be1d148ee5b
caps.latest.revision: 46
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 46
---
# Definir y modificar un filtro de combinaci&#243;n entre art&#237;culos de mezcla
  En este tema, se describe cómo definir y modificar un filtro de combinación entre artículos de mezcla en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. La replicación de mezcla admite filtros de combinación, que se usan normalmente junto con los filtros con parámetros para extender la partición de tabla a otros artículos de tabla relacionados.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Recomendaciones](#Recommendations)  
  
-   **Para definir y modificar un filtro de combinación entre artículos de mezcla con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Para crear un filtro de combinación, una publicación debe contener dos tablas relacionadas, como mínimo. Un filtro de combinación amplía un filtro de fila. Por tanto, debe definir un filtro de fila en una tabla para poder extender el filtro con una combinación a otra. Una vez definido un filtro de combinación, puede extenderlo con otro si la publicación contiene más tablas relacionadas.  
  
-   Si agrega, modifica o elimina un filtro de combinación una vez inicializadas las suscripciones a la publicación, deberá generar una instantánea nueva y reinicializar todas las suscripciones después de realizar el cambio. Para obtener más información acerca de los requisitos para los cambios de propiedad, vea [Propiedades de artículo y publicación de cambio](../../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
###  <a name="Recommendations"></a> Recomendaciones  
  
-   Los filtros de combinación se deben crear manualmente para un conjunto de tablas, o la replicación puede generar los filtros automáticamente en función de las relaciones entre las claves externas y las claves principales definidas en las tablas. Para obtener más información acerca de cómo generar un conjunto de filtros de combinación automáticamente, consulte [generar automáticamente un conjunto de combinación filtros entre combinar artículos & #40; SQL Server Management Studio & #41;](../../../relational-databases/replication/publish/automatically generate join filters between merge articles.md).  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 Definir, modificar y eliminar filtros de combinación en el **filtrar filas de tabla** página del Asistente para nueva publicación o **filtrar filas** página de la **Propiedades de la publicación - \< publicación>** cuadro de diálogo. Para obtener más información sobre cómo usar el asistente y acceso al cuadro de diálogo, vea [crear una publicación](../../../relational-databases/replication/publish/create-a-publication.md) y [Ver y modificar propiedades de publicación](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### Para definir un filtro de combinación  
  
1.  En el **filtrar filas de tabla** página del Asistente para nueva publicación o **filtrar filas** página de la **Propiedades de la publicación - \< publicación>**, seleccione un filtro de fila existente o filtro de combinación el **tablas filtradas** panel.  
  
2.  Haga clic en **Agregar**y, a continuación, en **Agregar combinación para ampliar el filtro seleccionado**.  
  
3.  Cree la instrucción de combinación: seleccione **Usar generador de instrucciones para crear la instrucción** o **Escribir instrucción de combinación manualmente**.  
  
    -   Si selecciona utilizar el generador, use las columnas de la cuadrícula (**junto**, **columna de tabla filtrada**, **operador**, y **columna de tabla combinada**) para generar una instrucción de combinación.  
  
         Cada columna de la cuadrícula contiene un cuadro combinado desplegable, lo que permite seleccionar dos columnas y un operador (**=**, **<>**, **<=**, **\<**, **>=**, **>**, y **como**). Los resultados se muestran en el área de texto **Vista previa** . Si la combinación implica más de un par de columnas, seleccione una conjunción (y o OR) desde el **junto** columna y, a continuación, escriba dos columnas más y un operador.  
  
    -   Si selecciona escribir la instrucción manualmente, escriba la instrucción de combinación en el área de texto **Instrucción de combinación** . Utilice los cuadros de lista **Columnas de la tabla filtrada** y **Columnas de la tabla combinada** para arrastrar y colocar columnas en el área de texto **Instrucción de combinación** .  
  
    -   La instrucción de combinación completa aparecerá así:  
  
        ```  
        SELECT <published_columns> FROM [Sales].[SalesOrderHeader] INNER JOIN [Sales].[SalesOrderDetail] ON [SalesOrderHeader].[SalesOrderID] = [SalesOrderDetail].[SalesOrderID]  
        ```  
  
         La cláusula JOIN debe utilizar nombres de dos partes; los nombres de tres o cuatro partes no se permiten.  
  
4.  Especifique las opciones de combinación:  
  
    -   Si la columna en la que combina la tabla filtrada (la tabla primaria) es única, seleccione **clave Unique**.  
  
        > [!CAUTION]  
        >  Al seleccionar esta opción indica que la relación entre la tabla principal y la secundaria de un filtro de combinación es de uno a uno o de uno a varios. Seleccione esta opción únicamente si tiene una restricción en la columna combinada en la tabla secundaria que garantiza la exclusividad. Si la opción no se establece correctamente, se podría producir la no convergencia de datos.  
  
    -   De manera predeterminada, la replicación de mezcla procesa los cambios fila a fila durante la sincronización. Para que los cambios en las filas de la tabla filtrada y de la tabla combinada se procesen como una unidad relacionados, seleccione **registros lógicos** ([!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] y versiones posteriores únicamente). Esta opción solo está disponible si se cumplen los requisitos del artículo y de la publicación para utilizar registros lógicos. Para obtener más información, vea la sección "Consideraciones para utilizar registros lógicos" en [grupo cambios en las filas relacionadas con registros lógicos](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
6.  Si se encuentra en la **Propiedades de la publicación - \< publicación>** cuadro de diálogo, haga clic en **Aceptar** para guardar y cerrar el cuadro de diálogo.  
  
#### Para modificar un filtro de combinación  
  
1.  En el **filtrar filas de tabla** página del Asistente para nueva publicación o **filtrar filas** página de la **Propiedades de la publicación - \< publicación>**, seleccione un filtro en el **tablas filtradas** panel y, a continuación, haga clic en **Editar**.  
  
2.  Modifique el filtro en el cuadro de diálogo **Editar combinación** .  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### Para eliminar un filtro de combinación  
  
1.  En el **filtrar filas de tabla** página del Asistente para nueva publicación o **filtrar filas** página de la **Propiedades de la publicación - \< publicación>**, seleccione un filtro en el **tablas filtradas** panel y, a continuación, haga clic en **Eliminar**. Si el filtro de combinación que elimina está a su vez ampliado por otras combinaciones, esas combinaciones también se eliminarán.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Estos procedimientos muestran un filtro con parámetros en un artículo primario con filtros de combinación entre este artículo y los artículos secundarios relacionados. Los filtros de combinación se pueden definir y modificar mediante programación con los procedimientos almacenados de la replicación.  
  
#### Para definir un filtro de combinación para extender un filtro de artículo a los artículos relacionados en una publicación de combinación  
  
1.  Defina el filtrado para el artículo con el que se combina, conocido también como artículo primario.  
  
    -   Para obtener más información acerca de los artículos filtrados mediante un filtro de fila con parámetros, vea [Define and Modify a Parameterized Row Filter for a Merge Article](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md).  
  
    -   Para obtener más información acerca de los artículos filtrados mediante un filtro de fila estático, vea [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md).  
  
2.  En el publicador de la base de datos de publicación, ejecute [sp_addmergearticle & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) para definir uno o varios artículos relacionados, que son también conocido como artículos secundarios, para la publicación. Para más información, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
3.  En el publicador de la base de datos de publicación, ejecute [sp_addmergefilter & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md). Especifique **@publication**, un nombre único para este filtro para **@filtername**, el nombre del artículo secundario creado en el paso 2 para **@article**, el nombre del artículo primario que se combina con para **@join_articlename**, y uno de los siguientes valores para **@join_unique_key**:  
  
    -   **0** -indica una combinación de varios a uno o varios a varios entre los artículos primarios y secundarios.  
  
    -   **1** -indica una combinación de uno a uno o uno a varios entre los artículos primarios y secundarios.  
  
     Esto define un filtro de combinación entre los dos artículos.  
  
    > [!CAUTION]  
    >  Establecer sólo **@join_unique_key** a **1** Si tiene una restricción en la columna de combinación en la tabla subyacente para el artículo primario que garantiza la exclusividad. Si **@join_unique_key** está establecido en **1** incorrectamente, puede producirse la no convergencia de los datos.  
  
###  <a name="TsqlExample"></a> Ejemplos (Transact-SQL)  
 En este ejemplo se define un artículo para una publicación de combinación, donde el artículo de tabla `SalesOrderDetail` se filtra respecto a la tabla `SalesOrderHeader` que se filtra a su vez con un filtro de fila estático. Para más información, consulte [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md).  
  
 [!code-sql[HowTo#sp_AddMergeArticle](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-join_1.sql)]  
  
 Este ejemplo define un grupo de artículos en una publicación de mezcla, donde los artículos se filtran con una serie de filtros de combinación con el `Employee` tabla, es decir, filtra mediante un filtro de fila parametrizado en el valor de [HOST_NAME](../../../t-sql/functions/host-name-transact-sql.md) en el **IdDeInicioDeSesión** columna. Para más información, consulte [Define and Modify a Parameterized Row Filter for a Merge Article](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md).  
  
 [!code-sql[HowTo#sp_MergeDynamicPub1](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-join_2.sql)]  
  
## Vea también  
 [Filtros de combinación](../../../relational-databases/replication/merge/join-filters.md)   
 [Filtros de fila con parámetros](../../../relational-databases/replication/merge/parameterized-row-filters.md)   
 [Cambiar las propiedades de la publicación y de los artículos](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Filtrar datos publicados para la replicación de mezcla](../../../relational-databases/replication/merge/filter-published-data-for-merge-replication.md)   
 [Cómo definir y modificar un filtro de combinación entre artículos de mezcla (SQL Server Management Studio)](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)   
 [Conceptos sobre los procedimientos almacenados del sistema de replicación](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Definir una relación de registros lógicos entre artículos de tabla de mezcla](../../../relational-databases/replication/publish/define-a-logical-record-relationship-between-merge-table-articles.md)   
 [Definir y modificar un filtro de fila con parámetros para un artículo de mezcla](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)  
  
  