---
title: Especificar asignaciones de tipos de datos para un publicador de Oracle | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Oracle publishing [SQL Server replication], data type mapping
- data types [SQL Server replication], Oracle publishing
- mapping data types [SQL Server replication]
ms.assetid: f172d631-3b8c-4912-bd0f-568366cd9870
caps.latest.revision: 36
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 03a774a08e2817edd0f46e5c17f31824c38ed404
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36197914"
---
# <a name="specify-data-type-mappings-for-an-oracle-publisher"></a>Especificar asignaciones de tipos de datos para un publicador de Oracle
  En este tema se describe cómo especificar asignaciones de tipos de datos para un publicador de Oracle en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Aunque se proporciona un conjunto de asignaciones de tipo de datos predeterminado para los publicadores de Oracle, es posible que sea necesario especificar las diferentes asignaciones para una publicación determinada.  
  
 **En este tema**  
  
-   **Para especificar asignaciones de tipos de datos para un publicador de Oracle con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 Especifique asignaciones de tipos de datos en la pestaña **Asignación de datos** del cuadro de diálogo **Propiedades del artículo: \<artículo>**. Está disponible en la página **Artículos** del Asistente para nueva publicación y en el cuadro de diálogo **Propiedades de la publicación: \<publicación>**. Para más información sobre el uso del asistente y el acceso al cuadro de diálogo, vea [Crear una publicación a partir de una base de datos de Oracle](create-a-publication-from-an-oracle-database.md) y [Ver y modificar propiedades de publicación](view-and-modify-publication-properties.md).  
  
#### <a name="to-specify-a-data-type-mapping"></a>Para especificar una asignación de tipos de datos  
  
1.  En la página **Artículos** del Asistente para nueva publicación o en el cuadro de diálogo **Propiedades de la publicación: \<publicación>**, seleccione una tabla y luego haga clic en **Propiedades del artículo**.  
  
2.  Haga clic en **Establecer propiedades del artículo de tabla resaltado**.  
  
3.  En la pestaña **Asignación de datos** del cuadro de diálogo **Propiedades del artículo: \<artículo>**, seleccione las asignaciones de la columna **Tipo de datos del suscriptor**:  
  
    -   Para algunos tipos de datos, solo hay una asignación posible, en cuyo caso la columna de la cuadrícula de propiedades es de solo lectura.  
  
    -   Para algunos tipos, hay más de un tipo que puede seleccionar. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] recomienda el uso de la asignación predeterminada a menos que la aplicación requiera una asignación diferente. Para más información, consulte [Data Type Mapping for Oracle Publishers](../non-sql/data-type-mapping-for-oracle-publishers.md).  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Puede especificar asignaciones de tipo de datos personalizadas mediante programación con los procedimientos almacenados de la replicación. También puede establecer las asignaciones predeterminadas que se usan al asignar los tipos de datos entre [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y un sistema de administración de bases de datos (DBMS) que no sea de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para más información, consulte [Data Type Mapping for Oracle Publishers](../non-sql/data-type-mapping-for-oracle-publishers.md).  
  
#### <a name="to-define-custom-data-type-mappings-when-creating-an-article-belonging-to-an-oracle-publication"></a>Para definir las asignaciones de tipo de datos personalizadas al crear un artículo que pertenece a una publicación de Oracle  
  
1.  Si aún no existe ninguna, cree una publicación de Oracle.  
  
2.  En el distribuidor, ejecute [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql). Especifique un valor de **0** para **@use_default_datatypes**. Para más información, consulte [Define an Article](define-an-article.md).  
  
3.  En el distribuidor, ejecute [sp_helparticlecolumns](/sql/relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql) para ver la asignación existente de una columna en un artículo publicado.  
  
4.  En el distribuidor, ejecute [sp_changearticlecolumndatatype](/sql/relational-databases/system-stored-procedures/sp-changearticlecolumndatatype-transact-sql). Especifique el nombre del publicador de Oracle para **@publisher**, así como **@publication**, **@article**y **@column** para definir la columna publicada. Especifique el nombre del tipo de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] al que asignar para **@type**, así como **@length**, **@precision**y **@scale**, cuando corresponda.  
  
5.  En el distribuidor, ejecute [sp_articleview](/sql/relational-databases/system-stored-procedures/sp-articleview-transact-sql). Esto crea la vista usada para generar la instantánea de la publicación de Oracle.  
  
#### <a name="to-specify-a-mapping-as-the-default-mapping-for-a-data-type"></a>Para especificar una asignación como la asignación predeterminada de un tipo de datos  
  
1.  (Opcional) En cualquier base de datos del distribuidor, ejecute [sp_getdefaultdatatypemapping](/sql/relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql). Especifique **@source_dbms**, **@source_type**, **@destination_dbms**, **@destination_version**y cualquier otro parámetro necesario para identificar el DBMS de origen. Se devuelve información acerca del tipo de datos asignado actualmente en el DBMS de destino mediante los parámetros de salida.  
  
2.  (Opcional) En cualquier base de datos del distribuidor, ejecute [sp_helpdatatypemap](/sql/relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql). Especifique **@source_dbms** y cualquier otro parámetro necesario para filtrar el conjunto de resultados. Tenga en cuenta el valor de **mapping_id** para la asignación deseada en el conjunto de resultados.  
  
3.  En cualquier base de datos del distribuidor, ejecute [sp_setdefaultdatatypemapping](/sql/relational-databases/system-stored-procedures/sp-setdefaultdatatypemapping-transact-sql).  
  
    -   Si conoce el valor deseado de **mapping_id** obtenido en el paso 2, especifíquelo para **@mapping_id**.  
  
    -   Si no conoce **mapping_id**, especifique los parámetros **@source_dbms**, **@source_type**, **@destination_dbms**, **@destination_type**y cualquier otro parámetro necesario para identificar una asignación existente.  
  
#### <a name="to-find-valid-data-types-for-a-given-oracle-data-type"></a>Para buscar los tipos de datos válidos para un tipo de datos de Oracle determinado  
  
1.  En cualquier base de datos del distribuidor, ejecute [sp_helpdatatypemap](/sql/relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql). Especifique un valor de **ORACLE** para **@source_dbms** y cualquier otro parámetro necesario para filtrar el conjunto de resultados.  
  
###  <a name="TsqlExample"></a> Ejemplos (Transact-SQL)  
 En este ejemplo se cambia una columna con un tipo de datos de Oracle NUMBER, de modo que se asigna al tipo de datos `numeric`(38,38) de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], en lugar del tipo de datos predeterminado `float`.  
  
 [!code-sql[HowTo#sp_changecolumndatatype](../../../snippets/tsql/SQL15/replication/howto/tsql/datatypemapping.sql#sp_changecolumndatatype)]  
  
 Esta consulta de ejemplo devuelve las asignaciones predeterminadas y alternativas para el tipo de datos de Oracle 9 `CHAR`.  
  
 [!code-sql[HowTo#sp_helpcolumndatatype_char](../../../snippets/tsql/SQL15/replication/howto/tsql/datatypemapping.sql#sp_helpcolumndatatype_char)]  
  
 Esta consulta de ejemplo devuelve las asignaciones predeterminadas para el tipo de datos de Oracle 9 `NUMBER` cuando se especifica sin escala o precisión.  
  
 [!code-sql[HowTo#sp_helpcolumndatatype_number](../../../snippets/tsql/SQL15/replication/howto/tsql/datatypemapping.sql#sp_helpcolumndatatype_number)]  
  
## <a name="see-also"></a>Vea también  
 [Data Type Mapping for Oracle Publishers](../non-sql/data-type-mapping-for-oracle-publishers.md)   
 [Replicación de bases de datos heterogéneas](../non-sql/heterogeneous-database-replication.md)   
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)   
 [Configurar un publicador de Oracle](../non-sql/configure-an-oracle-publisher.md)  
  
  
