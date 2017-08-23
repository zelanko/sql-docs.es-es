---
title: Catalog.update_logdb_info (base de datos de SSISDB) | Documentos de Microsoft
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: a898be08859230ab873fd8e358b892789aaed043
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="catalogupdatelogdbinfo-ssisdb-database"></a>Catalog.update_logdb_info (base de datos de SSISDB)
[!INCLUDE[tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md](../../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]

Actualización de la [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] escala espera registrar información.

## <a name="syntax"></a>Sintaxis

```tsql
update_logdb_info [@server_name = ] server_name, [@connection_string = ] connection_string
```

## <a name="arguments"></a>Argumentos
[ @server_name =] *nombre_servidor*  
 El servidor de Sql Server usa para el registro horizontalmente. El *nombre_servidor* es **nvarchar**.  

 [ @connection_string =] *conexión*  
 La cadena de conexión que se usa para el registro horizontalmente. El *conexión* es **nvarchar**.

 ## <a name="return-code-value"></a>Valor de código de retorno  
 0 (correcto)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  

## <a name="permissions"></a>Permissions  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
   
-   La pertenencia a la **ssis_admin** rol de base de datos  
  
-   La pertenencia a la **sysadmin** rol de servidor  
 
