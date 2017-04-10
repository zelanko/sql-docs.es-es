---
title: "Especificar asignaciones de tipos de datos para un publicador de Oracle | Microsoft Docs"
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
  - "publicación de Oracle [replicación de SQL Server], asignación de tipos de datos"
  - "tipos de datos [replicación de SQL Server], publicación de Oracle"
  - "asignar tipos de datos [replicación de SQL Server]"
ms.assetid: f172d631-3b8c-4912-bd0f-568366cd9870
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 37
---
# Especificar asignaciones de tipos de datos para un publicador de Oracle
  En este tema se describe cómo especificar asignaciones de tipos de datos para un publicador de Oracle en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Aunque se proporciona un conjunto de asignaciones de tipo de datos predeterminado para los publicadores de Oracle, es posible que sea necesario especificar las diferentes asignaciones para una publicación determinada.  
  
 **En este tema**  
  
-   **Para especificar asignaciones de tipos de datos para un publicador de Oracle con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 Especificar asignaciones de tipos de datos en el **datos asignación** ficha de la **Propiedades del artículo: \< artículo>** cuadro de diálogo. Está disponible en la **artículos** página del Asistente para nueva publicación y **Propiedades de la publicación - \< publicación>** cuadro de diálogo. Para obtener más información sobre cómo usar el asistente y acceso al cuadro de diálogo, vea [crear una publicación de una base de datos de Oracle](../../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md) y [Ver y modificar propiedades de publicación](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### Para especificar una asignación de tipos de datos  
  
1.  En el **artículos** página del Asistente para nueva publicación o **Propiedades de la publicación - \< publicación>** cuadro de diálogo, seleccione una tabla y, a continuación, haga clic en **Propiedades del artículo**.  
  
2.  Haga clic en **Establecer propiedades del artículo de tabla resaltado**.  
  
3.  En el **asignación de datos** ficha de la **Propiedades del artículo: \< artículo>** cuadro de diálogo, seleccione las asignaciones en el **tipo de datos de suscriptor** columna:  
  
    -   Para algunos tipos de datos, solo hay una asignación posible, en cuyo caso la columna de la cuadrícula de propiedades es de solo lectura.  
  
    -   Para algunos tipos, hay más de un tipo que puede seleccionar. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] recomienda el uso de la asignación predeterminada a menos que la aplicación requiera una asignación diferente. Para más información, consulte [Data Type Mapping for Oracle Publishers](../../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md).  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Puede especificar asignaciones de tipo de datos personalizadas mediante programación con los procedimientos almacenados de la replicación. También puede establecer las asignaciones predeterminadas que se utilizan cuando los tipos de datos de asignación entre [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y no[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] la base de datos (DBMS) del sistema de administración. Para más información, consulte [Data Type Mapping for Oracle Publishers](../../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md).  
  
#### Para definir las asignaciones de tipo de datos personalizadas al crear un artículo que pertenece a una publicación de Oracle  
  
1.  Si aún no existe ninguna, cree una publicación de Oracle.  
  
2.  En el distribuidor, ejecute [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Especifique un valor de **0** para **@use_default_datatypes**. Para más información, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
3.  En el distribuidor, ejecute [sp_helparticlecolumns](../../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md) para ver la asignación existente para una columna en un artículo publicado.  
  
4.  En el distribuidor, ejecute [sp_changearticlecolumndatatype](../../../relational-databases/system-stored-procedures/sp-changearticlecolumndatatype-transact-sql.md). Especifique el nombre del publicador de Oracle para **@publisher**, así como **@publication**, **@article**y **@column** para definir la columna publicada. Especifique el nombre del tipo de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] al que asignar para **@type**, así como **@length**, **@precision**y **@scale**, cuando corresponda.  
  
5.  En el distribuidor, ejecute [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md). Esto crea la vista usada para generar la instantánea de la publicación de Oracle.  
  
#### Para especificar una asignación como la asignación predeterminada de un tipo de datos  
  
1.  (Opcional) En el distribuidor de cualquier base de datos, ejecutar [sp_getdefaultdatatypemapping](../../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md). Especifique **@source_dbms**, **@source_type**, **@destination_dbms**, **@destination_version**, y otros parámetros necesarios para identificar el DBMS de origen. Se devuelve información acerca del tipo de datos asignado actualmente en el DBMS de destino mediante los parámetros de salida.  
  
2.  (Opcional) En el distribuidor de cualquier base de datos, ejecutar [sp_helpdatatypemap](../../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md). Especifique **@source_dbms** y cualquier otro parámetro necesario para filtrar el conjunto de resultados. Tenga en cuenta el valor de **mapping_id** para la asignación en el resultado deseada.  
  
3.  En el distribuidor de cualquier base de datos, ejecutar [sp_setdefaultdatatypemapping](../../../relational-databases/system-stored-procedures/sp-setdefaultdatatypemapping-transact-sql.md).  
  
    -   Si conoce el valor deseado de **mapping_id** obtenido en el paso 2, especifíquelo para **@mapping_id**.  
  
    -   Si no conoce el **mapping_id**, especifique los parámetros **@source_dbms**, **@source_type**, **@destination_dbms**, **@destination_type**, y otros parámetros necesarios para identificar una asignación existente.  
  
#### Para buscar los tipos de datos válidos para un tipo de datos de Oracle determinado  
  
1.  En el distribuidor de cualquier base de datos, ejecutar [sp_helpdatatypemap](../../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md). Especifique un valor de **ORACLE** para **@source_dbms** y cualquier otro parámetro necesario para filtrar el conjunto de resultados.  
  
###  <a name="TsqlExample"></a> Ejemplos (Transact-SQL)  
 Este ejemplo cambia una columna con un tipo de datos de Oracle del número de modo que se asigna a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipo de datos **numérico**(38,38), en lugar del tipo de datos predeterminado **float**.  
  
 [!code-sql[HowTo#sp_changecolumndatatype](../../../relational-databases/replication/codesnippet/tsql/specify-data-type-mappin_1.sql)]  
  
 Esta consulta de ejemplo devuelve las asignaciones predeterminadas y alternativas para el tipo de datos de Oracle 9 **CHAR**.  
  
 [!code-sql[HowTo#sp_helpcolumndatatype_char](../../../relational-databases/replication/codesnippet/tsql/specify-data-type-mappin_2.sql)]  
  
 Esta consulta de ejemplo devuelve las asignaciones predeterminadas para el tipo de datos de Oracle 9 **NUMBER** cuando se especifica sin escala o precisión.  
  
 [!code-sql[HowTo#sp_helpcolumndatatype_number](../../../relational-databases/replication/codesnippet/tsql/specify-data-type-mappin_3.sql)]  
  
## Vea también  
 [Asignar tipos de datos para publicadores de Oracle](../../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)   
 [Replicación de bases de datos heterogéneas](../../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Conceptos sobre los procedimientos almacenados del sistema de replicación](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Configurar un publicador de Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)  
  
  