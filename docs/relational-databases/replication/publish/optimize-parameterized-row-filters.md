---
title: "Optimizar los filtros de fila con par&#225;metros | Microsoft Docs"
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
  - "particiones precalculadas [replicación de SQL Server]"
  - "filtros [replicación de SQL Server], con parámetros"
  - "particiones precalculadas de replicación de mezcla [replicación de SQL Server], SQL Server Management Studio"
  - "filtros con parámetros [replicación de SQL Server], optimización"
ms.assetid: 49349605-ebd0-4757-95be-c0447f30ba13
caps.latest.revision: 44
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 44
---
# Optimizar los filtros de fila con par&#225;metros
  En este tema se describe cómo optimizar los filtros de fila con parámetros en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Recomendaciones](#Recommendations)  
  
-   **Para optimizar los filtros de fila con parámetros con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Recommendations"></a> Recomendaciones  
  
-   Al usar los filtros con parámetros, puede controlar cómo se procesan los filtros por la replicación de mezcla especificando la opción **use partition groups** o la opción **keep partition changes** al crear una publicación. Estas opciones mejoran el rendimiento de la sincronización para las publicaciones con artículos filtrados almacenando los metadatos adicionales en la base de datos de publicación. Puede controlar cómo se comparten los datos entre los Suscriptores estableciendo **partition options** al crear un artículo. Para obtener más información acerca de estos requisitos, vea [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
     Con suscriptores de [!INCLUDE[ssEW](../../../includes/ssew-md.md)]SQL Server Compact, keep_partition_changes se debe establecer en true para asegurarse de que las eliminaciones se propagan correctamente. Si se establece en false, el suscriptor puede tener más filas de las esperadas.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 Para optimizar los filtros de fila con parámetros se puede utilizar la siguiente configuración:  
  
 **Opciones de partición**  
 Establezca esta opción en la **propiedades** página de la **Propiedades del artículo: \< artículo>** cuadro de diálogo, o en la **Agregar filtro** cuadro de diálogo. Ambos cuadros de diálogo están disponibles en el Asistente para nueva publicación y **Propiedades de la publicación - \< publicación>** cuadro de diálogo. El **Propiedades del artículo: \< artículo>** cuadro de diálogo le permite especificar valores adicionales para esta opción que no están disponibles en la **Agregar filtro** cuadro de diálogo.  
  
 **Calcular particiones previamente**  
 Esta opción se establece en **True** de forma predeterminada, si los artículos de la publicación cumplen un conjunto de requisitos. Para obtener más información acerca de estos requisitos, consulte [optimizar el rendimiento de filtro con parámetros con particiones precalculadas](../../../relational-databases/replication/merge/optimize-parameterized-filter-performance-with-precomputed-partitions.md). Modifique esta opción en el **Opciones de suscripción** página de la **Propiedades de la publicación - \< publicación>** cuadro de diálogo.  
  
 **Optimizar sincronización**  
 Esta opción debe establecerse en **True** solo si **calcular particiones previamente** está establecido en **False**. Establezca esta opción en el **Opciones de suscripción** página de la **Propiedades de la publicación - \< publicación>** cuadro de diálogo.  
  
 Para obtener más información acerca de usar el Asistente para nueva publicación y obtener acceso a la **Propiedades de la publicación - \< publicación>** cuadro de diálogo, vea [crear una publicación](../../../relational-databases/replication/publish/create-a-publication.md) y [Ver y modificar propiedades de publicación](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### Para establecer opciones de partición en el cuadro de diálogo Agregar filtro o Editar filtro  
  
1.  En el **filtrar filas de tabla** página del Asistente para nueva publicación o **filtrar filas** página de la **Propiedades de la publicación - \< publicación>** cuadro de diálogo, haga clic en **Agregar**, y, a continuación, haga clic en **Agregar filtro**.  
  
2.  Cree un filtro con parámetros. Para más información, consulte [Define and Modify a Parameterized Row Filter for a Merge Article](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md).  
  
3.  Seleccione la opción que indique cómo se van a compartir los datos entre los suscriptores:  
  
    -   **Una fila de esta tabla irá a varias suscripciones**  
  
    -   **Una fila de esta tabla irá a una sola suscripción**  
  
     Si selecciona **Una fila de esta tabla irá a una sola suscripción**, la replicación de mezcla puede optimizar el rendimiento almacenando y procesando menos metadatos. No obstante, debe asegurarse de que los datos se particionan de forma que una fila no se pueda replicar en más de un suscriptor. Para obtener más información, vea la sección sobre cómo configurar opciones de partición en el tema [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Si se encuentra en la **Propiedades de la publicación - \< publicación>** cuadro de diálogo, haga clic en **Aceptar** para guardar y cerrar el cuadro de diálogo.  
  
#### Para establecer las opciones de partición en las propiedades del artículo: \< artículo> cuadro de diálogo  
  
1.  En el **artículos** página del Asistente para nueva publicación o **Propiedades de la publicación - \< publicación>** cuadro de diálogo, seleccione una tabla y, a continuación, haga clic en **Propiedades del artículo**.  
  
2.  Haga clic en **Establecer propiedades del artículo de Tabla resaltado** o **Establecer propiedades de todos los artículos de la tabla**.  
  
3.  En el **el objeto de destino** sección de la **propiedades** ficha de la **Propiedades del artículo: \< artículo>** cuadro de diálogo, especifique uno de los siguientes valores para **Opciones de partición**:  
  
    -   **Superpuestas**  
  
    -   **Superpuestas, no permitir cambios de datos fuera de la partición**  
  
    -   **No superpuestas, una sola suscripción**  
  
    -   **No superpuestas, compartir entre suscripciones**  
  
     Para obtener más información acerca de estas opciones y cómo se relacionan con las opciones disponibles en los cuadros de diálogo **Agregar filtro** y **Editar filtro** , vea la sección sobre cómo establecer opciones de partición en el tema [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Si se encuentra en la **Propiedades de la publicación - \< publicación>** cuadro de diálogo, haga clic en **Aceptar** para guardar y cerrar el cuadro de diálogo.  
  
#### Para establecer Calcular particiones previamente  
  
1.  En el **Opciones de suscripción** página de la **Propiedades de la publicación - \< publicación>** cuadro de diálogo, seleccione un valor para el **calcular particiones previamente** opción. La propiedad es de solo lectura si:  
  
    -   La publicación no cumple los requisitos de las particiones precalculadas.  
  
    -   No se ha generado una instantánea para la publicación. En este caso, la opción muestra el valor **Establecer automáticamente cuando se crea una instantánea**.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### Para establecer Optimizar sincronización  
  
1.  En el **Opciones de suscripción** página de la **Propiedades de la publicación - \< publicación>** cuadro de diálogo, seleccione el valor **True** para el **Optimizar sincronización** opción.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Para obtener definiciones de las opciones de filtrado para **@keep_partition_changes** y **@use_partition_groups**, consulte [sp_addmergepublication](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md).  
  
#### Para especificar las optimizaciones de filtro de mezcla al crear una nueva publicación  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_addmergepublication](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md). Especifique **@publication** y un valor de **true** para uno de los siguientes parámetros:  
  
    -   **@use_partition_groups**:-la optimización de rendimiento más alto, proporcionada que los artículos cumplan los requisitos para las particiones precalculadas. Para obtener más información, consulte [optimizar el rendimiento de filtro con parámetros con particiones precalculadas](../../../relational-databases/replication/merge/optimize-parameterized-filter-performance-with-precomputed-partitions.md).  
  
    -   **@keep_partition_changes** -use esta optimización si no se pueden usar particiones precalculadas.  
  
2.  Agregue un trabajo de instantánea para la publicación. Para obtener más información, consulte [crear una publicación](../../../relational-databases/replication/publish/create-a-publication.md).  
  
3.  En el publicador de la base de datos de publicación, ejecute [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md), especifique los siguientes parámetros:  
  
    -   **@publication** -el nombre de la publicación del paso 1.  
  
    -   **@article** -un nombre para el artículo  
  
    -   **@source_object** : el objeto de base de datos que se publica.  
  
    -   **@subset_filterclause** -la cláusula de filtro con parámetros opcional utilizada para filtrar horizontalmente el artículo.  
  
    -   **@partition_options** -las opciones de partición para el artículo filtrado.  
  
4.  Repita el paso 3 para cada artículo de la publicación.  
  
5.  (Opcional) En el publicador de la base de datos de publicación, ejecute [sp_addmergefilter](../../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md) para definir un filtro de combinación entre dos artículos. Para obtener más información, consulte [Define and Modify a Join Filter Between Merge Articles](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md).  
  
#### Para ver y modificar los comportamientos de filtro de mezcla para una publicación existente  
  
1.  (Opcional) En el publicador de la base de datos de publicación, ejecute [sp_helpmergepublication](../../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md), especificando **@publication**. Tenga en cuenta el valor de **keep_partition_changes** y **use_partition_groups** conjunto de resultados.  
  
2.  (Opcional) En el publicador de la base de datos de publicación, ejecute [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md). Especifique un valor de **use_partition_groups** para **@property** y **true** o **false** para **@value**.  
  
3.  (Opcional) En el publicador de la base de datos de publicación, ejecute [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md). Especifique un valor de **keep_partition_changes** para **@property** y **true** o **false** para **@value**.  
  
    > [!NOTE]  
    >  Al habilitar **keep_partition_changes**, primero debe deshabilitar **use_partition_groups** y especifique un valor de **1** para **@force_reinit_subscription**.  
  
4.  (Opcional) En el publicador de la base de datos de publicación, ejecute [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md). Especifique un valor de **partition_options** para **@property** y el valor adecuado para **@value**. Consulte [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) para las definiciones de estas opciones de filtrado.  
  
5.  (Opcional) Inicie el Agente de instantáneas para regenerar la instantánea si es necesario. Para obtener información acerca de los cambios requieren generará una nueva instantánea, consulte [Propiedades de artículo y publicación de cambio](../../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
## Vea también  
 [Generar automáticamente un conjunto de filtros de combinación entre artículos de mezcla & #40; SQL Server Management Studio & #41;](../../../relational-databases/replication/publish/automatically generate join filters between merge articles.md)   
 [Definir y modificar un filtro de fila con parámetros para un artículo de mezcla](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)   
 [Filtros de fila con parámetros](../../../relational-databases/replication/merge/parameterized-row-filters.md)  
  
  