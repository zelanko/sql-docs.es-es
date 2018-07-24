---
title: catalog.update_logdb_info (base de datos de SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: language-reference
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: craigg
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: be9feb6fc6e1b027b739fdb3afc4cbf3c37ff2d9
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38063783"
---
# <a name="catalogupdatelogdbinfo-ssisdb-database"></a>catalog.update_logdb_info (base de datos de SSISDB)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Actualice la información de registro de escalabilidad horizontal de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].

## <a name="syntax"></a>Sintaxis

```sql
catalog.update_logdb_info [@server_name = ] server_name, [@connection_string = ] connection_string
```

## <a name="arguments"></a>Argumentos
[ @server_name = ] *server_name*  
 Servidor SQL Server que se usa para el registro de la escalabilidad horizontal. El valor de *server_name* es **nvarchar**.  

 [ @connection_string = ] *connection_string*  
 Cadena de conexión que se usa para el registro de la escalabilidad horizontal. El valor de *connection_string* es **nvarchar**.

 ## <a name="return-code-value"></a>Valor de código de retorno  
 0 (correcto)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  

## <a name="permissions"></a>Permisos  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
   
-   Pertenencia al rol de base de datos de **ssis_admin**  
  
-   Pertenencia al rol de servidor de **sysadmin**  
 
