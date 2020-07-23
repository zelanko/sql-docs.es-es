---
title: catalog.add_execution_worker (base de datos de SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: d587cedd-6402-4d5c-9526-7cd25627a037
author: chugugrace
ms.author: chugu
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: ffcd20f1895252cc09eca1fc87a055bd5c964a38
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/22/2020
ms.locfileid: "86917653"
---
# <a name="catalogadd_execution_worker-ssisdb-database"></a>catalog.add_execution_worker (base de datos de SSISDB)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE[sqlserver2017](../../includes/applies-to-version/sqlserver2017.md)]

Agrega un trabajo de escalabilidad horizontal [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] a una instancia de ejecución en la escalabilidad horizontal.

## <a name="syntax"></a>Sintaxis

```sql
catalog.add_execution_worker [ @execution_id = ] execution_id, [ @workeragent_id = ] workeragent_id
```

## <a name="arguments"></a>Argumentos
[ @execution_id = ] *execution_id*  
 Identificador único de la instancia de ejecución. El parámetro *execution_id* es de tipo **bigint**.  
 
[@workeragent_id = ] *workeragent_id*  
Id. de agente de trabajo del trabajo de escalabilidad horizontal. *workeragent_id* es **uniqueIdentifier**.

## <a name="return-code-value"></a>Valor de código de retorno  
 0 (correcto)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  

## <a name="permissions"></a>Permisos  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
  
-   Permisos READ y MODIFY en la instancia de ejecución  
  
-   Pertenencia al rol de base de datos de **ssis_admin**  
  
-   Pertenencia al rol de servidor de **sysadmin**  
 
## <a name="errors-and-warnings"></a>Errores y advertencias  
 En la siguiente lista se describen algunas condiciones que pueden producir un error o una advertencia:  
 
- El usuario no tiene los permisos adecuados.

- El identificador de ejecución no es válido.

- El identificador del agente de trabajo no es válido.

- La ejecución no está en escalabilidad horizontal.

## <a name="see-also"></a>Consulte también
[Ejecutar paquetes en la escalabilidad horizontal](~/integration-services/scale-out/run-packages-in-integration-services-ssis-scale-out.md).

