---
title: "Definir y modificar un filtro de fila con par&#225;metros para un art&#237;culo de mezcla | Microsoft Docs"
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
  - "filtros con parámetros [replicación de SQL Server], definición"
  - "filtros con parámetros [replicación de SQL Server], modificación"
  - "replicación de mezcla [replicación de SQL Server], filtros dinámicos"
  - "filtros con parámetros de replicación de mezcla [replicación de SQL Server]"
  - "filtros [replicación de SQL Server], con parámetros"
  - "modificación de filtros, fila con parámetros"
  - "filtros dinámicos [replicación de SQL Server]"
ms.assetid: de0482a2-3cc8-4030-8a4a-14364549ac9f
caps.latest.revision: 44
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 44
---
# Definir y modificar un filtro de fila con par&#225;metros para un art&#237;culo de mezcla
  En este tema se describe cómo definir y modificar un filtro de fila con parámetros en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 Al crear los artículos de la tabla, puede usar filtros de fila con parámetros. Estos filtros usan una cláusula [WHERE](../../../t-sql/queries/where-transact-sql.md) para seleccionar los datos adecuados que se van a publicar. En lugar de especificar un valor literal en la cláusula (como ocurre con un filtro de fila estático), especifique una o ambas de las siguientes funciones del sistema: [SUSER_SNAME](../../../t-sql/functions/suser-sname-transact-sql.md) y [HOST_NAME](../../../t-sql/functions/host-name-transact-sql.md). Para más información, consulte [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
-   **Para definir y modificar un filtro de fila con parámetros con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Si agrega, modifica o elimina un filtro de fila con parámetros una vez inicializadas las suscripciones a la publicación, deberá generar una instantánea nueva y reinicializar todas las suscripciones después de realizar el cambio. Para obtener más información acerca de los requisitos para los cambios de propiedad, vea [Propiedades de artículo y publicación de cambio](../../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
###  <a name="Recommendations"></a> Recomendaciones  
  
-   Por motivos de rendimiento, se recomienda no aplicar funciones a los nombres de columna en las cláusulas de filtro de fila con parámetros, como `LEFT([MyColumn]) = SUSER_SNAME()`. Si utiliza HOST_NAME en una cláusula de filtro y reemplaza el valor HOST_NAME, puede que sea necesario convertir los tipos de datos utilizando CONVERT. Para obtener más información acerca de las prácticas recomendadas para este caso, consulte la sección "Reemplazar el valor de HOST_NAME ()" en el tema [filtros de fila parametrizados](../../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 Definir, modificar y eliminar filtros de fila parametrizados en la **filtrar filas de tabla** página del Asistente para nueva publicación o **filtrar filas** página de la **Propiedades de la publicación - \< publicación>** cuadro de diálogo. Para obtener más información sobre cómo usar el asistente y acceso al cuadro de diálogo, vea [crear una publicación](../../../relational-databases/replication/publish/create-a-publication.md) y [Ver y modificar propiedades de publicación](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### Para definir un filtro de fila con parámetros  
  
1.  En el **filtrar filas de tabla** página del Asistente para nueva publicación o **filtrar filas** página de la **Propiedades de la publicación - \< publicación>**, haga clic en **Agregar**, y, a continuación, haga clic en **Agregar filtro**.  
  
2.  En el **Agregar filtro** cuadro de diálogo, seleccione una tabla para filtrar en el cuadro de lista desplegable.  
  
3.  Cree una instrucción para el filtro en el cuadro de texto **Instrucción de filtro** . Puede escribir directamente en el área de texto o puede arrastrar y colocar columnas del cuadro de lista **Columnas** .  
  
    -   El área de texto **Instrucción de filtro** incluye el texto predeterminado, que tiene este formato:  
  
        ```  
        SELECT <published_columns> FROM [tableowner].[tablename] WHERE  
        ```  
  
    -   El texto predeterminado no se puede cambiar. Escriba la cláusula del filtro después de la palabra clave WHERE utilizando la sintaxis SQL estándar. Un filtro con parámetros incluye una llamada a la función de sistema **HOST_NAME ()** o **SUSER_SNAME ()**, o una función definida por el usuario que hace referencia a una o ambas de estas funciones. La línea siguiente es un ejemplo de una cláusula de filtro completa de un filtro de fila con parámetros:  
  
        ```  
        SELECT <published_columns> FROM [HumanResources].[Employee] WHERE LoginID = SUSER_SNAME()  
        ```  
  
         La cláusula WHERE debe usar nombres de dos partes; los nombres de tres y cuatro partes no se admiten.  
  
4.  Seleccione la opción que indique cómo se van a compartir los datos entre los suscriptores:  
  
    -   **Una fila de esta tabla irá a varias suscripciones**  
  
    -   **Una fila de esta tabla irá a una sola suscripción**  
  
     Si selecciona **Una fila de esta tabla irá a una sola suscripción**, la replicación de mezcla puede optimizar el rendimiento almacenando y procesando menos metadatos. No obstante, debe asegurarse de que los datos se particionan de forma que una fila no se pueda replicar en más de un suscriptor. Para obtener más información, vea la sección sobre cómo configurar opciones de partición en el tema [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
6.  Si se encuentra en la **Propiedades de la publicación - \< publicación>** cuadro de diálogo, haga clic en **Aceptar** para guardar y cerrar el cuadro de diálogo.  
  
#### Para modificar un filtro de fila con parámetros  
  
1.  En el **filtrar filas de tabla** página del Asistente para nueva publicación o **filtrar filas** página de la **Propiedades de la publicación - \< publicación>**, seleccione un filtro en el **tablas filtradas** panel y, a continuación, haga clic en **Editar**.  
  
2.  Modifique el filtro en el cuadro de diálogo **Editar filtro** .  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### Para eliminar un filtro de fila con parámetros  
  
1.  En el **filtrar filas de tabla** página del Asistente para nueva publicación o **filtrar filas** página de la **Propiedades de la publicación - \< publicación>**, seleccione un filtro en el **tablas filtradas** panel y, a continuación, haga clic en **Eliminar**.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Los filtros de fila con parámetros se pueden crear y modificar mediante programación con los procedimientos almacenados de la replicación.  
  
#### Para definir un filtro de fila con parámetros para un artículo en una publicación de combinación  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_addmergearticle & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Especifique **@publication**, un nombre de artículo para **@article**, la tabla que se publica para **@source_object**, la cláusula WHERE que define el filtro con parámetros para **@subset_filterclause** (sin incluir `WHERE`), y uno de los siguientes valores para **@partition_options**, que describe el tipo de partición que se generará el filtro de fila con parámetros:  
  
    -   **0** : el filtro del artículo es estático o no produce un único subconjunto de datos para cada partición (una partición "superpuesta").  
  
    -   **1** : particiones resultantes se superponen y las actualizaciones realizadas en el suscriptor no pueden cambiar la partición a la que pertenece una fila.  
  
    -   **2** : el filtro del artículo produce particiones no superpuestas, pero varios suscriptores pueden recibir la misma partición.  
  
    -   **3** : el filtro del artículo produce particiones no superpuestas que son únicas para cada suscripción.  
  
#### Para cambiar un filtro de fila con parámetros para un artículo en una publicación de combinación  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md). Especifique **@publication**, **@article**, un valor de **subset_filterclause** para **@property**, la expresión que define el filtro con parámetros para **@value** (sin incluir `WHERE`) y un valor de **1** para ambos **@force_invalidate_snapshot** y **@force_reinit_subscription**.  
  
2.  Si este cambio provoca un comportamiento diferente en las particiones, a continuación, ejecute [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) nuevo. Especifique **@publication**, **@article**, un valor de **partition_options** para **@property**, y la opción de partición más apropiada para **@value**, que puede ser uno de los siguientes:  
  
    -   **0** : el filtro del artículo es estático o no produce un único subconjunto de datos para cada partición (una partición "superpuesta").  
  
    -   **1** : particiones resultantes se superponen y las actualizaciones realizadas en el suscriptor no pueden cambiar la partición a la que pertenece una fila.  
  
    -   **2** : el filtro del artículo produce particiones no superpuestas, pero varios suscriptores pueden recibir la misma partición.  
  
    -   **3** : el filtro del artículo produce particiones no superpuestas que son únicas para cada suscripción.  
  
###  <a name="TsqlExample"></a> Ejemplo (Transact-SQL)  
 En este ejemplo se define un grupo de artículos en una publicación de mezcla, donde los artículos se filtran con una serie de filtros de combinación con la tabla `Employee` que a su vez se filtra mediante un filtro de fila con parámetros en la columna **LoginID** . Durante la sincronización, el valor devuelto por el [HOST_NAME](../../../t-sql/functions/host-name-transact-sql.md) se reemplaza la función. Para obtener más información, vea invalidar el valor de HOST_NAME () en el tema [filtros de fila parametrizados](../../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
 [!code-sql[HowTo#sp_MergeDynamicPub1](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-para_1.sql)]  
  
## Vea también  
 [Definir y modificar un filtro de combinación entre artículos de mezcla](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)   
 [Cambiar las propiedades de la publicación y de los artículos](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Filtros de combinación](../../../relational-databases/replication/merge/join-filters.md)   
 [Filtros de fila con parámetros](../../../relational-databases/replication/merge/parameterized-row-filters.md)  
  
  