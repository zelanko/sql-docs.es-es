---
title: Agregar un elemento de recopilación a un conjunto de recopilación (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- collection items [SQL Server]
- collection sets [SQL Server], adding items
ms.assetid: 9fe6454e-8c0e-4b50-937b-d9871b20fd13
caps.latest.revision: 20
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b2e5ce955af2f073009a662f8bc4d844c82f6218
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2018
ms.locfileid: "43811252"
---
# <a name="add-a-collection-item-to-a-collection-set-transact-sql"></a>Agregar un elemento de recopilación a un conjunto de recopilación (Transact-SQL)
  Puede agregar un elemento de recopilación a una conjunto de recopilación existente mediante los procedimientos almacenados que se proporcionan con el recopilador de datos.  
  
 Lleve a cabo los pasos siguientes utilizando Editor de consultas de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
### <a name="add-a-collection-item-to-a-collection-set"></a>Agregar un elemento de recopilación a un conjunto de recopilación  
  
1.  Detenga el conjunto de recopilación al que quiere agregar el elemento; para ello, ejecute el procedimiento almacenado **sp_syscollector_stop_collection_set** . Por ejemplo, para detener un conjunto de recopilación denominado "Test Collection Set", ejecute las instrucciones siguientes:  
  
    ```tsql  
    USE msdb  
    DECLARE @csid int  
    SELECT @csid = collection_set_id  
    FROM syscollector_collection_sets  
    WHERE name = 'Test Collection Set'  
    SELECT @csid  
    EXEC dbo.sp_syscollector_stop_collection_set @collection_set_id = @csid  
    ```  
  
    > [!NOTE]  
    >  Para detener el conjunto de recopilación, también puede usar el Explorador de objetos en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obtener más información, vea [Iniciar o detener un conjunto de recopilación](start-or-stop-a-collection-set.md).  
  
2.  Declare el conjunto de recopilación al que desea agregar el elemento de recopilación. El código siguiente es un ejemplo de cómo se declara el identificador del conjunto de recopilación.  
  
    ```tsql  
    DECLARE @collection_set_id_1 int  
    SELECT @collection_set_id_1 = collection_set_id FROM [msdb].[dbo].[syscollector_collection_sets]  
    WHERE name = N'Test Collection Set'; -- name of collection set  
    ```  
  
3.  Declare el tipo de recopilador. El código siguiente es un ejemplo de cómo se declara el tipo de recopilador de consultas T-SQL genérico.  
  
    ```tsql  
    DECLARE @collector_type_uid_1 uniqueidentifier  
    SELECT @collector_type_uid_1 = collector_type_uid FROM [msdb].[dbo].[syscollector_collector_types]   
       WHERE name = N'Generic T-SQL Query Collector Type';  
    ```  
  
     Puede ejecutar el código siguiente para obtener una lista de los tipos de recopilador instalados:  
  
    ```tsql  
    USE msdb  
    SELECT * from syscollector_collector_types  
    GO  
    ```  
  
4.  Ejecute el procedimiento almacenado **sp_syscollector_create_collection_item** para crear el elemento de recopilación. Debe declarar el esquema del elemento de recopilación para que se asigne al esquema que corresponde al tipo de recopilador deseado. En el ejemplo siguiente se usa el esquema de entrada de consultas T-SQL genérico.  
  
    ```tsql  
    DECLARE @collection_item_id int;  
    EXEC [msdb].[dbo].[sp_syscollector_create_collection_item]   
    @name=N'OS Wait Stats', --name of collection item  
    @parameters=N'  
    <ns:TSQLQueryCollector xmlns:ns="DataCollectorType">  
     <Query>  
      <Value>select * from sys.dm_os_wait_stats</Value>  
      <OutputTable>os_wait_stats</OutputTable>  
    </Query>  
    </ns:TSQLQueryCollector>',  
    @collection_item_id = @collection_item_id OUTPUT,  
    @frequency = 60,  
    @collection_set_id = @collection_set_id_1, --- Provides the collection set ID number  
    @collector_type_uid = @collector_type_uid_1 -- Provides the collector type UID  
    SELECT @collection_item_id     
    ```  
  
5.  Antes de iniciar el conjunto de recopilación actualizado, ejecute la consulta siguiente para comprobar que se ha creado el nuevo elemento de recopilación:  
  
    ```xaml  
    USE msdb  
    SELECT * from syscollector_collection_sets  
    SELECT * from syscollector_collection_items  
    GO  
    ```  
  
     Los conjuntos de recopilación y sus elementos de recopilación se muestran en la pestaña **Resultados** .  
  
## <a name="see-also"></a>Vea también  
 [Crear un conjunto de recopilación personalizado que use el tipo de recopilador de consultas T-SQL genérico &#40;Transact-SQL&#41;](create-custom-collection-set-generic-t-sql-query-collector-type.md)   
 [Procedimientos almacenados del recopilador de datos &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql)  
  
  
