---
title: 'Creación de un conjunto de recopilación: tipo de recopilador de consultas T-SQL genérico'
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- T-SQL Query collector type
- collection sets [SQL Server], creating custom
ms.assetid: 6b06db5b-cfdc-4ce0-addd-ec643460605b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b27dda40294185f923d74b61dfd1b10ce7301ba9
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "74055576"
---
# <a name="create-custom-collection-set---generic-t-sql-query-collector-type"></a>Creación de un conjunto de recopilación: tipo de recopilador de consultas T-SQL genérico
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Puede crear un conjunto de recopilación personalizado con elementos de recopilación que utilicen el tipo de recopilador de consultas T-SQL genérico mediante los procedimientos almacenados que se proporcionan con el recopilador de datos. Para realizar esta tarea debe usar el Editor de consultas de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para llevar a cabo los siguientes procedimientos:  
  
-   Configurar programaciones de carga.  
  
-   Definir y crear el conjunto de recopilación.  
  
-   Definir y crear un elemento de recopilación.  
  
-   Comprobar la existencia del conjunto de recopilación y de los elementos de recopilación.  
  
> [!NOTE]  
>  Antes de crear un conjunto de recopilación personalizada, debe configurar los parámetros de recopilación de datos. Para obtener más información, vea [Configurar parámetros para la recopilación de datos &#40;Transact-SQL&#41;](../../relational-databases/data-collection/configure-data-collection-parameters-transact-sql.md).  
  
### <a name="define-and-create-the-collection-set"></a>Definir y crear el conjunto de recopilación  
  
1.  Defina un nuevo conjunto de recopilación mediante el procedimiento almacenado sp_syscollector_create_collection_set.  
  
    ```  
    USE msdb;  
    DECLARE @collection_set_id int;  
    DECLARE @collection_set_uid uniqueidentifier;  
    EXEC sp_syscollector_create_collection_set   
        @name=N'DMV Test 1',   
        @collection_mode=0,   
        @description=N'This is a test collection set',   
        @logging_level=1,   
        @days_until_expiration=14,   
        @schedule_name=N'CollectorSchedule_Every_15min',   
        @collection_set_id=@collection_set_id OUTPUT,   
        @collection_set_uid=@collection_set_uid OUTPUT;  
    SELECT @collection_set_id, @collection_set_uid;  
    ```  
  
     El modo de recopilación se puede establecer en 0 (almacenamiento en caché) o en 1 (sin almacenamiento en caché).  
  
     El nivel de registro se puede establecer en 0, 1 o 2.  
  
     Se proporcionan las siguientes programaciones preconfiguradas con el recopilador de datos:  
  
    -   CollectorSchedule_Every_5min  
  
    -   CollectorSchedule_Every_10min  
  
    -   CollectorSchedule_Every_15min  
  
    -   CollectorSchedule_Every_30min  
  
    -   CollectorSchedule_Every_60min  
  
    -   CollectorSchedule_Every_6h  
  
     Si no desea usar una de las programaciones que se proporcionan, puede crear una nueva programación y usarla para el conjunto de recopilación. Para obtener más información, vea [Crear y adjuntar programaciones a trabajos](../../ssms/agent/create-and-attach-schedules-to-jobs.md).  
  
### <a name="define-and-create-a-collection-item"></a>Definir y crear un elemento de recopilación  
  
1.  Dado que el nuevo elemento de recopilación está basado en un tipo de recopilador genérico que ya se ha instalado, puede ejecutar el siguiente código para establecer el GUID de forma que corresponda al tipo de recopilador de consultas T-SQL genérico.  
  
    ```sql  
    DECLARE @collector_type_uid uniqueidentifier;  
    SELECT @collector_type_uid = collector_type_uid FROM [msdb].[dbo].[syscollector_collector_types]   
    WHERE name = N'Generic T-SQL Query Collector Type';  
    DECLARE @collection_item_id int;  
    ```  
  
2.  Use el procedimiento almacenado sp_syscollector_create_collection_item para crear el elemento de recopilación. Declare el esquema para el elemento de recopilación para que se asigne al esquema necesario para el tipo de recopilador de consultas T-SQL genérico.  
  
    ```sql  
    EXEC sp_syscollector_create_collection_item   
        @name=N'Query Stats - Test 1',   
        @parameters=N'  
            <ns:TSQLQueryCollector xmlns:ns="DataCollectorType">  
            <Query>  
            <Value>SELECT * FROM sys.dm_exec_query_stats</Value>  
            <OutputTable>dm_exec_query_stats</OutputTable>  
            </Query>  
            </ns:TSQLQueryCollector>',   
        @collection_item_id=@collection_item_id OUTPUT,   
        @frequency=5,   
        @collection_set_id=@collection_set_id,   
        @collector_type_uid=@collector_type_uid;  
    SELECT @collection_item_id;  
    ```  
  
### <a name="verify-that-the-new-collection-set-and-collection-item-exist"></a>Compruebe que el nuevo conjunto de recopilación y el elemento de recopilación existan.  
  
1.  Antes de iniciar el nuevo conjunto de recopilación, ejecute la consulta siguiente para comprobar que se han creado el nuevo conjunto de recopilación y su elemento de recopilación.  
  
    ```sql  
    USE msdb;  
    SELECT * FROM syscollector_collection_sets;  
    SELECT * FROM syscollector_collection_items;  
    GO  
    ```  
  
     También puede hacer una comprobación visual en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. En el Explorador de objetos, expanda el nodo **Administración** y, a continuación, expanda **Recopilación de datos**. Se mostrará el nuevo conjunto de recopilación. El icono de círculo rojo para el conjunto de recopilación indica que se ha detenido el conjunto de recopilación.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo de código siguiente combina los ejemplos documentados en los pasos anteriores. Tenga en cuenta que la frecuencia de recopilación establecida para el elemento de recopilación (5 segundos) se omite porque el modo recopilación del conjunto de recopilación se ha establecido en 0, que es el modo de almacenamiento en caché. Para obtener más información, consulte [Data Collection](../../relational-databases/data-collection/data-collection.md).  
  
```sql  
USE msdb;  
  
DECLARE @collection_set_id int;  
DECLARE @collection_set_uid uniqueidentifier  
  
EXEC dbo.sp_syscollector_create_collection_set  
    @name = N'DMV Stats Test 1',  
    @collection_mode = 0,  
    @description = N'This is a test collection set',  
    @logging_level=1,  
    @days_until_expiration = 14,  
    @schedule_name=N'CollectorSchedule_Every_15min',  
    @collection_set_id = @collection_set_id OUTPUT,  
    @collection_set_uid = @collection_set_uid OUTPUT;  
SELECT @collection_set_id,@collection_set_uid;  
  
DECLARE @collector_type_uid uniqueidentifier;  
SELECT @collector_type_uid = collector_type_uid FROM syscollector_collector_types   
WHERE name = N'Generic T-SQL Query Collector Type';  
  
DECLARE @collection_item_id int;  
EXEC sp_syscollector_create_collection_item  
@name= N'Query Stats - Test 1',  
@parameters=N'  
<ns:TSQLQueryCollector xmlns:ns="DataCollectorType">  
<Query>  
  <Value>select * from sys.dm_exec_query_stats</Value>  
  <OutputTable>dm_exec_query_stats</OutputTable>  
</Query>  
 </ns:TSQLQueryCollector>',  
    @collection_item_id = @collection_item_id OUTPUT,  
    @frequency = 5, -- This parameter is ignored in cached mode  
    @collection_set_id = @collection_set_id,  
    @collector_type_uid = @collector_type_uid;  
SELECT @collection_item_id;  
  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [Procedimientos almacenados del recopilador de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [Administrar programaciones](../../ssms/agent/manage-schedules.md)   
 [Iniciar o detener un conjunto de recopilación](../../relational-databases/data-collection/start-or-stop-a-collection-set.md)  
  
  
