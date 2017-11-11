---
title: MODIFICAR el origen de datos externo (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 11/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 8
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: c2a0a43aefe59bc11f16445b5ee0c781179a33fa
ms.openlocfilehash: f74a105226f1ae113287f1c337c1c33e81bb09ae
ms.contentlocale: es-es
ms.lasthandoff: 09/06/2017

---
# <a name="alter-external-data-source-transact-sql"></a>MODIFICAR el origen de datos externo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Modifica un origen de datos externo que se utiliza para crear una tabla externa. El origen de datos externo puede ser almacenamiento de blobs de Azure o Hadoop (WASB).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Modify an external data source
-- Applies to: SQL Server (2016 or later), Azure SQL Data Warehouse,
               Parallel Data Warehouse    
ALTER EXTERNAL DATA SOURCE data_source_name SET  
    {   
        LOCATION = 'server_name_or_IP' [,] |  
        RESOURCE_MANAGER_LOCATION = <'IP address;Port'> [,] |  
        CREDENTIAL = credential_name  
    }  
    [;]  

-- Modify an external data source pointing to Azure Blob storage
-- Applies to: SQL Server (starting with 2017), Azure SQL Database,
               Azure SQL Data Warehouse, Parallel Data Warehouse
ALTER EXTERNAL DATA SOURCE data_source_name  
    WITH (   
        TYPE = BLOB_STORAGE,  
        LOCATION = 'https://storage_account_name.blob.core.windows.net'
        [, CREDENTIAL = credential_name ]
    )  
```  
  
## <a name="arguments"></a>Argumentos  
 data_source_name  
 Especifica el nombre del origen de datos definido por el usuario. El nombre debe ser único.  
  
 UBICACIÓN = 'server_name_or_IP'  
 Especifica el nombre del servidor o una dirección IP.  
  
 RESOURCE_MANAGER_LOCATION = '\<dirección IP. Puerto >'  
 Especifica la ubicación del Administrador de recursos de Hadoop. Cuando se especifica, el optimizador de consultas puede procesar previamente los datos de una consulta de PolyBase mediante el uso de las capacidades de cálculo de Hadoop. Esta es una decisión basada en costos. Llama a la aplicación del predicado, esto puede reducir significativamente el volumen de datos transferidos entre Hadoop y SQL y, por tanto, mejorar el rendimiento de las consultas.  
  
 CREDENCIAL = Credential_Name  
 Especifica la credencial con nombre. Vea [CREATE DATABASE SCOPED CREDENTIAL &#40; Transact-SQL &#41; ](../../t-sql/statements/create-database-scoped-credential-transact-sql.md).  

TIPO = BLOB_STORAGE   
**Se aplica a:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)].   
Para operaciones masivas, `LOCATION` debe ser válido la dirección URL al almacenamiento de blobs de Azure. No coloque  **/** , nombre de archivo o compartido parámetros de la firma de acceso al final de la `LOCATION` dirección URL.   
La credencial usada, debe crearse con `SHARED ACCESS SIGNATURE` como la identidad. Para más información sobre las firmas de acceso compartido, vea [Uso de Firmas de acceso compartido (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).

  
  
## <a name="remarks"></a>Comentarios  
 Origen único solo puede modificarse a la vez. Solicitudes simultáneas para modificar el mismo origen de hacen que una instrucción de espera. Sin embargo, pueden modificarse orígenes diferentes al mismo tiempo. Además, esto esta instrucción puede ejecutar simultáneamente con otras instrucciones.  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso ALTER ANY EXTERNAL DATA SOURCE.  
 > [!IMPORTANT]  
 >  El permiso ALTER ANY EXTERNAL DATA SOURCE concede a cualquier entidad de seguridad de la capacidad de crear y modificar cualquier objeto de origen de datos externo y, por lo tanto, también concede la capacidad de tener acceso a todas las credenciales de ámbito de la base de datos en la base de datos. Este permiso debe considerarse como con altos privilegios y, por tanto, se debe conceder únicamente a las entidades de confianza en el sistema.

  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se modifica la ubicación y la ubicación del Administrador de recursos de un origen de datos existente.  
  
```  
ALTER EXTERNAL DATA SOURCE hadoop_eds SET  
     LOCATION = 'hdfs://10.10.10.10:8020',  
     RESOURCE_MANAGER_LOCATION = '10.10.10.10:8032'  
    ;  
  
```  
  
 En el ejemplo siguiente se modifica la credencial que se va a conectar a un origen de datos existente.  
  
```  
ALTER EXTERNAL DATA SOURCE hadoop_eds SET  
   CREDENTIAL = new_hadoop_user  
    ;  
```  
  
  

