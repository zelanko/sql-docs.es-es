---
title: ALTER EXTERNAL DATA SOURCE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER EXTERNAL DATA SOURCE
- ALTER_EXTERNAL_DATA_SOURCE
dev_langs:
- TSQL
helpviewer_keywords:
- polybase, alter external data source statement
- ALTER EXTERNAL DATA SOURCE statement
ms.assetid: a34b9e90-199d-46d0-817a-a7e69387bf5f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a28f86d1e5a87f41a8894dad22f4cf887602af02
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/17/2020
ms.locfileid: "81628199"
---
# <a name="alter-external-data-source-transact-sql"></a>ALTER EXTERNAL DATA SOURCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Modifica un origen de datos externo usado para crear una tabla externa. El origen de datos externo puede ser Hadoop o Azure Blob Storage (WASBS) para SQL SERVER, y Azure Blob Storage (WASBS) o Azure Data Lake Storage (ABFSS/ADL) para Azure SQL Data Warehouse. 

## <a name="syntax"></a>Sintaxis  

```syntaxsql
-- Modify an external data source
-- Applies to: SQL Server (2016 or later) and APS
ALTER EXTERNAL DATA SOURCE data_source_name SET
    {   
        LOCATION = 'server_name_or_IP' [,] |
        RESOURCE_MANAGER_LOCATION = <'IP address;Port'> [,] |
        CREDENTIAL = credential_name
    }  
    [;]  

-- Modify an external data source pointing to Azure Blob storage
-- Applies to: SQL Server (starting with 2017)
ALTER EXTERNAL DATA SOURCE data_source_name
    SET
        LOCATION = 'https://storage_account_name.blob.core.windows.net'
        [, CREDENTIAL = credential_name ] 

-- Modify an external data source pointing to Azure Blob storage or Azure Data Lake storage
-- Applies to: Azure SQL Data Warehouse
ALTER EXTERNAL DATA SOURCE data_source_name
    SET
        [LOCATION = '<location prefix>://<location path>']
        [, CREDENTIAL = credential_name ] 
```

## <a name="arguments"></a>Argumentos  
 data_source_name especifica el nombre definido por el usuario para el origen de datos. El nombre debe ser único.

 LOCATION = "nombre_del_servidor_o_dirección_IP" Proporciona el protocolo de conectividad y la ruta de acceso al origen de datos externo.

 RESOURCE_MANAGER_LOCATION = "\<dirección IP;Puerto>" (No se aplica a Azure SQL Data Warehouse) Especifica la ubicación del Administrador de recursos de Hadoop. Cuando se especifica, el optimizador de consultas podría preprocesar los datos de una consulta de PolyBase mediante el uso de las funciones de cálculo de Hadoop. Esta es una decisión basada en el costo. Esta técnica, denominada aplicación de predicado, puede reducir significativamente el volumen de datos transferidos entre Hadoop y SQL y, por tanto, mejorar el rendimiento de las consultas.

 CREDENTIAL = Credential_Name especifica la credencial con nombre. Vea [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md).

TYPE = [HADOOP | BLOB_STORAGE]   
**Se aplica a:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)].
Solo para operaciones masivas, `LOCATION` debe ser la dirección URL válida en Azure Blob Storage. No coloque **/** , el nombre de archivo o parámetros de firma de acceso compartido al final de la dirección URL de `LOCATION`.
La credencial usada debe crearse mediante el uso de `SHARED ACCESS SIGNATURE` como identidad. Para más información sobre las firmas de acceso compartido, vea [Uso de Firmas de acceso compartido (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).

  

## <a name="remarks"></a>Observaciones
 Solo puede modificarse un único origen de cada vez. Las solicitudes simultáneas para modificar el mismo origen hacen que una instrucción tenga que esperar. Aun así, es posible modificar varios orígenes al mismo tiempo. Esta instrucción se puede ejecutar simultáneamente con otras instrucciones.

## <a name="permissions"></a>Permisos  
 Requiere el permiso ALTER ANY EXTERNAL DATA SOURCE.
 > [!IMPORTANT]  
 > El permiso ALTER ANY EXTERNAL DATA SOURCE concede a cualquier entidad de seguridad la capacidad de crear y modificar cualquier objeto de origen de datos externo y, por lo tanto, también permite acceder a todas las credenciales con ámbito de base de datos de la base de datos. Debe considerarse como un permiso con muchos privilegios, por lo que solo debe concederse a las entidades de seguridad de confianza del sistema.


## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se modifica la ubicación y la ubicación del administrador de recursos de un origen de datos existente.

```  
ALTER EXTERNAL DATA SOURCE hadoop_eds SET
     LOCATION = 'hdfs://10.10.10.10:8020',
     RESOURCE_MANAGER_LOCATION = '10.10.10.10:8032'
    ;
  
```

 En el ejemplo siguiente se modifica la credencial para conectar con un origen de datos existente.

```  
ALTER EXTERNAL DATA SOURCE hadoop_eds SET
   CREDENTIAL = new_hadoop_user
    ;
```

 En el ejemplo siguiente se modifica la credencial a una nueva ubicación. Este ejemplo es un origen de datos externo creado para Azure SQL Data Warehouse. 

```  
ALTER EXTERNAL DATA SOURCE AzureStorage_west SET
   LOCATION = 'wasbs://loadingdemodataset@updatedproductioncontainer.blob.core.windows.net',
   CREDENTIAL = AzureStorageCredential
```
