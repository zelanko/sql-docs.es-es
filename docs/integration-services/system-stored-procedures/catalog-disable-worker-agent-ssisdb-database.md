---
title: Catalog.disable_worker_agent (base de datos de SSISDB) | Documentos de Microsoft
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3f19dc4c-a000-4318-8fe1-e80d56720e66
caps.latest.revision: 3
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: 8f4a8cd24278742ffb13d16791ce5f1f3a95f301
ms.contentlocale: es-es
ms.lasthandoff: 10/20/2017

---
# <a name="catalogdisableworkeragent-ssisdb-database"></a>Catalog.disable_worker_agent (base de datos de SSISDB)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Deshabilitar un trabajo de salida de escala para trabajar con esta escala Out maestro [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] catálogo.

## <a name="syntax"></a>Sintaxis

```sql
catalog.disable_worker_agent [@WorkerAgentId =] WorkerAgentId
```
## <a name="arguments"></a>Argumentos
[@WorkerAgentId =] *WorkerAgentId* el agente de trabajo del Id. de escala Out trabajo. El *WorkerAgentId* es **uniqueidentifier**.

## <a name="example"></a>Ejemplo
Este ejemplo deshabilita a la escala fuera Worker en MachineA.

```sql
SELECT WorkerAgentId, MachineName FROM [catalog].[worker_agents]
GO
-- Result: --
-- WorkerAgentId                           MachineName --
-- 6583054A-E915-4C2A-80E4-C765E79EF61D    MachineA    --

EXEC [catalog].[disable_worker_agent] '6583054A-E915-4C2A-80E4-C765E79EF61D'
GO 
```

## <a name="return-code-value"></a>Valor de código de retorno  
 0 (correcto)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Ninguno  

## <a name="permissions"></a>Permissions  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
  
-   La pertenencia a la **ssis_admin** rol de base de datos  
  
-   La pertenencia a la **sysadmin** rol de servidor 

## <a name="errors-and-warnings"></a>Errores y advertencias
Si el identificador de agente de trabajo no es válido, el procedimiento almacenado devuelve un error.

