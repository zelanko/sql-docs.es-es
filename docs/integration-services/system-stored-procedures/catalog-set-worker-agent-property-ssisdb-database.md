---
title: catalog.set_worker_agent_property (base de datos de SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: ddd2a534-6925-4d66-90e7-541c14f41de7
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 121c39ddc217cbdc178ca8ea8221081ce33eee4b
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/22/2020
ms.locfileid: "86912801"
---
# <a name="catalogset_worker_agent_property-ssisdb-database"></a>catalog.set_worker_agent_property (base de datos de SSISDB)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Establece la propiedad de un trabajo de escalabilidad horizontal de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].

## <a name="syntax"></a>Sintaxis

```sql
catalog.set_worker_agent_property [ @WorkerAgentId = ] WorkerAgentId
    , [ @PropertyName = ] PropertyName
    , [ @PropertyValue = ] PropertyValue 
```

## <a name="arguments"></a>Argumentos
[@WorkerAgentId =] *WorkerAgentId*  
Id. de agente de trabajo del trabajo de escalabilidad horizontal. *WorkerAgentId* es **uniqueidentifier**.

[@PropertyName =] *PropertyName*  
El nombre de la propiedad. *PropertyName* es **nvarchar(256)** .

[@PropertyValue =] *PropertyValue*  
El valor de la propiedad. *PropertyValue* es **nvarchar(max)** .

## <a name="remarks"></a>Observaciones
Los nombres de propiedad válidos son **DisplayName**, **Descriptio0n** y **Tags**.

## <a name="return-code-value"></a>Valor de código de retorno  
 0 (correcto)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  

## <a name="permissions"></a>Permisos  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
  
-   Pertenencia al rol de base de datos de **ssis_admin**  
  
-   Pertenencia al rol de servidor de **sysadmin**

## <a name="errors-and-warnings"></a>Errores y advertencias
  En la siguiente lista se describen algunas condiciones que pueden producir un error o una advertencia:  
  
-   El usuario no tiene los permisos adecuados. 

-   El identificador del agente de trabajo no es válido.

-   El nombre de la propiedad no es válido.

-   El valor de la propiedad no es válido.  
