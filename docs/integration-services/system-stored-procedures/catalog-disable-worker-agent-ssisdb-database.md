---
title: catalog.disable_worker_agent (base de datos SSISDB) | Microsoft Docs
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3f19dc4c-a000-4318-8fe1-e80d56720e66
caps.latest.revision: "3"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3695d9a06c6de6e42409b7dba1e8e63e25925b73
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="catalogdisableworkeragent-ssisdb-database"></a>catalog.disable_worker_agent (base de datos SSISDB)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Deshabilite un trabajo de escalabilidad horizontal para el patrón de escalabilidad horizontal mediante este catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].

## <a name="syntax"></a>Sintaxis

```sql
catalog.disable_worker_agent [@WorkerAgentId =] WorkerAgentId
```
## <a name="arguments"></a>Argumentos
[@WorkerAgentId =] *WorkerAgentId* Id. de agente de trabajo del trabajo de escalabilidad horizontal. *WorkerAgentId* es **uniqueidentifier**.

## <a name="example"></a>Ejemplo
En este ejemplo se deshabilita el trabajo de escalabilidad horizontal en MachineA.

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
  
-   Pertenencia al rol de base de datos **ssis_admin**  
  
-   Pertenencia al rol de servidor **sysadmin** 

## <a name="errors-and-warnings"></a>Errores y advertencias
Si el identificador de agente de trabajo no es válido, el procedimiento almacenado devuelve un error.
