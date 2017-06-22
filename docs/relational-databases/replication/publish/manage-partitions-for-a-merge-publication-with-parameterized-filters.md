---
title: "Administración de particiones para una publicación de mezcla mediante filtros con parámetros | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- partitions [SQL Server replication]
- merge replication partitions [SQL Server replication], SQL Server Management Studio
- parameterized filters [SQL Server replication], partition management
ms.assetid: fb5566fe-58c5-48f7-8464-814ea78e6221
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 5718198b2cbfc99a1658a703199bb943fcd73aeb
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="manage-partitions-for-a-merge-publication-with-parameterized-filters"></a>Administrar particiones para una publicación de mezcla mediante filtros con parámetros
  En este tema se describe cómo administrar particiones para una publicación de mezcla con filtros con parámetros en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]o Replication Management Objects (RMO). Los filtros de fila con parámetros se puede utilizar para generar particiones no superpuestas. Estas particiones pueden estar restringidas para que solo una suscripción reciba una partición determinada. En estos casos, un número grande de suscriptores producirá un número de particiones grande, las cuales a su vez requieren un número igual de instantánea con particiones. Para más información, consulte [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Recomendaciones](#Recommendations)  
  
-   **Para administrar particiones para una publicación de mezcla mediante filtros con parámetros con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Recommendations"></a> Recomendaciones  
  
-   Si genera un script para una topología de replicación (opción recomendada), los scripts de la publicación contienen las llamadas al procedimiento almacenado para crear particiones de datos. El script proporciona una referencia para las particiones creadas y una forma de volver a crear una o más divisiones en caso necesario. Para más información, consulte [Scripting Replication](../../../relational-databases/replication/scripting-replication.md).  
  
-   Cuando una publicación ha parametrizado filtros que producen suscripciones con particiones no superpuestas, y si una suscripción determinada se pierde y necesita volverse a crear, debe realizar las siguientes acciones: quitar la partición a la que se suscribió, volver a crear la suscripción y, a continuación, volver a crear la partición. Para más información, consulte [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md). La replicación genera scripts de creación para particiones del suscriptor existentes cuando se genera un script de creación de publicación. Para más información, consulte [Scripting Replication](../../../relational-databases/replication/scripting-replication.md).  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 Administre las particiones en la página **Particiones de datos** del cuadro de diálogo **Propiedades de la publicación: \<publicación>**. Para obtener más información sobre el acceso a este cuadro de diálogo, vea [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md). En esta página puede crear y eliminar particiones, permitir a los suscriptores iniciar la generación y distribución de instantáneas, generar instantáneas para una o más particiones, y limpiar instantáneas.  
  
#### <a name="to-create-a-partition"></a>Para crear una partición  
  
1.  En la página **Particiones de datos** del cuadro de diálogo **Propiedades de la publicación: \<publicación>**, haga clic en **Agregar**.  
  
2.  En el cuadro de diálogo **Agregar partición de datos** , escriba valores para **HOST_NAME()** y/o **SUSER_SNAME()** asociados con la partición que desea crear.  
  
3.  También puede especificar una programación para actualizar las instantáneas:  
  
    1.  Seleccione **Programar el Agente de instantáneas para que esta partición se ejecute a las horas siguientes**.  
  
    2.  Acepte la programación predeterminada para actualizar instantáneas o haga clic en **Cambiar** para especificar una programación diferente.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-delete-a-partition"></a>Para eliminar una partición  
  
1.  En la página **Particiones de datos** , seleccione una partición en la cuadrícula.  
  
2.  Haga clic en **Eliminar**.  
  
#### <a name="to-allow-subscribers-to-initiate-snapshot-generation-and-delivery"></a>Para permitir a los suscriptores inicializar la generación y distribución de instantáneas  
  
1.  En la página **Particiones de datos** , seleccione **Definir automáticamente una partición y generar una instantánea si es necesario cuando un suscriptor nuevo intente sincronizarse**.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-generate-a-snapshot-for-a-partition"></a>Para generar una instantánea para una partición  
  
1.  En la página **Particiones de datos** , seleccione una partición en la cuadrícula.  
  
2.  Haga clic en **Generar instantáneas seleccionadas ahora**.  
  
#### <a name="to-clean-up-a-snapshot-for-a-partition"></a>Para limpiar una instantánea de una partición  
  
1.  En la página **Particiones de datos** , seleccione una partición en la cuadrícula.  
  
2.  Haga clic en **Limpiar instantáneas existentes**.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Para administrar mejor una publicación con filtros parametrizados, puede enumerar mediante programación las particiones existentes utilizando los procedimientos almacenados de replicación. También puede crear y eliminar particiones existentes. Se puede obtener la información siguiente sobre las particiones existentes:  
  
-   Filtrado de una partición (mediante [SUSER_SNAME &#40;Transact-SQL&#41;](../../../t-sql/functions/suser-sname-transact-sql.md) o [HOST_NAME &#40;Transact-SQL&#41;](../../../t-sql/functions/host-name-transact-sql.md)).  
  
-   El nombre del trabajo que genera una instantánea con particiones.  
  
-   La última vez que se ejecutó un trabajo de instantánea con particiones.  
  
 Mientras la segunda parte de la instantánea de dos partes se puede generar a petición cuando se inicializa una nueva suscripción, los procedimientos siguientes le permiten controlar cómo se genera esta instantánea y pre-generar dicha instantánea cuando sea más conveniente. Para más información, consulte [Snapshots for Merge Publications with Parameterized Filters](../../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md).  
  
#### <a name="to-view-information-on-existing-partitions"></a>Para ver información sobre particiones existentes  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_helpmergepartition &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpmergepartition-transact-sql.md). Especifique el nombre de la publicación para **@publication**. (Opcional) Especifique **@suser_sname** o **@host_name** para devolver únicamente información basada en un criterio del filtrado único.  
  
#### <a name="to-define-a-new-partition-and-generate-a-new-partitioned-snapshot"></a>Para definir una nueva partición y generar una nueva instantánea con particiones  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_addmergepartition &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepartition-transact-sql.md). Especifique el nombre de la publicación para **@publication**y el valor con parámetros que define la partición para uno de los siguientes:  
  
    -   **@suser_sname**: cuando el filtro con parámetros se define con el valor devuelto por [SUSER_SNAME &#40;Transact-SQL&#41;](../../../t-sql/functions/suser-sname-transact-sql.md).  
  
    -   **@host_name**: cuando el filtro con parámetros se define con el valor devuelto por [HOST_NAME &#40;Transact-SQL&#41;](../../../t-sql/functions/host-name-transact-sql.md).  
  
2.  Cree e inicialice la instantánea parametrizada para esta nueva partición. Para más información, consulte [Crear una instantánea para una publicación de mezcla con filtros con parámetros](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
#### <a name="to-delete-a-partition"></a>Para eliminar una partición  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_dropmergepartition &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-dropmergepartition-transact-sql.md). Especifique el nombre de la publicación para **@publication** y el valor con parámetros que define la partición para uno de los siguientes:  
  
    -   **@suser_sname**: cuando el filtro con parámetros se define con el valor devuelto por [SUSER_SNAME &#40;Transact-SQL&#41;](../../../t-sql/functions/suser-sname-transact-sql.md).  
  
    -   **@host_name**: cuando el filtro con parámetros se define con el valor devuelto por [HOST_NAME &#40;Transact-SQL&#41;](../../../t-sql/functions/host-name-transact-sql.md).  
  
     Este procedimiento quita también el trabajo de instantáneas y los archivos de instantáneas de la partición.  
  
##  <a name="RMOProcedure"></a> Usar Replication Management Objects (RMO)  
 Para administrar mejor una publicación con filtros parametrizados, puede crear mediante programación nuevas particiones del suscriptor, enumerar las particiones del suscriptor existentes y eliminar las particiones del suscriptor utilizando Replication Management Objects (RMO). Para obtener más información acerca de cómo particiones del suscriptor, vea [Crear una instantánea para una publicación de mezcla con filtros con parámetros](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md). Se puede obtener la información siguiente sobre las particiones existentes:  
  
-   El valor y la función de filtrado en los que se basa la partición.  
  
-   El nombre del trabajo que genera una instantánea con parámetros para el suscriptor.  
  
-   La última vez que se ejecutó un trabajo de instantánea con parámetros.  
  
#### <a name="to-view-information-on-existing-partitions"></a>Para ver información sobre particiones existentes  
  
1.  Cree una conexión al publicador mediante la clase <xref:Microsoft.SqlServer.Management.Common.ServerConnection>.  
  
2.  Cree una instancia de la clase <xref:Microsoft.SqlServer.Replication.MergePublication>. Establezca las propiedades <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> y <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> para la publicación y establezca la propiedad <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> en la conexión creada en el elemento <xref:Microsoft.SqlServer.Management.Common.ServerConnection> creado en el paso 1.  
  
3.  Llame al método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obtener las propiedades del objeto. Si este método devuelve **false**, significa que las propiedades de publicación del paso 2 se definieron incorrectamente, o bien que la publicación no existe.  
  
4.  Llame al método <xref:Microsoft.SqlServer.Replication.MergePublication.EnumMergePartitions%2A> y pase el resultado a una matriz de objetos <xref:Microsoft.SqlServer.Replication.MergePartition>.  
  
5.  Para cada objeto <xref:Microsoft.SqlServer.Replication.MergePartition> de la matriz, obtenga cualquier propiedad de interés.  
  
#### <a name="to-delete-existing-partitions"></a>Para eliminar particiones existentes  
  
1.  Cree una conexión al publicador mediante la clase <xref:Microsoft.SqlServer.Management.Common.ServerConnection>.  
  
2.  Cree una instancia de la clase <xref:Microsoft.SqlServer.Replication.MergePublication>. Establezca las propiedades <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> y <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> para la publicación y establezca la propiedad <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> en la conexión creada en el elemento <xref:Microsoft.SqlServer.Management.Common.ServerConnection> creado en el paso 1.  
  
3.  Llame al método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obtener las propiedades del objeto. Si este método devuelve **false**, significa que las propiedades de publicación del paso 2 se definieron incorrectamente, o bien que la publicación no existe.  
  
4.  Llame al método <xref:Microsoft.SqlServer.Replication.MergePublication.EnumMergePartitions%2A> y pase el resultado a una matriz de objetos <xref:Microsoft.SqlServer.Replication.MergePartition>.  
  
5.  Para cada objeto <xref:Microsoft.SqlServer.Replication.MergePartition> de la matriz, determine si se debería eliminar la partición. Esta decisión normalmente se basa en el valor de la propiedad <xref:Microsoft.SqlServer.Replication.MergePartition.DynamicFilterLogin%2A> o la propiedad <xref:Microsoft.SqlServer.Replication.MergePartition.DynamicFilterHostName%2A>.  
  
6.  Llame al método <xref:Microsoft.SqlServer.Replication.MergePublication.RemoveMergePartition%2A> del objeto <xref:Microsoft.SqlServer.Replication.MergePublication> del paso 2. Pase el objeto <xref:Microsoft.SqlServer.Replication.MergePartition> del paso 5.  
  
7.  Repita el paso 6 para cada partición que se elimina.  
  
## <a name="see-also"></a>Vea también  
 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [Snapshots for Merge Publications with Parameterized Filters](../../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)  
  
  
