---
description: catalog.set_worker_agent_property (base de datos de SSISDB)
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
ms.openlocfilehash: b5981431210ba98c950b56b7621f3f9cc50586c5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88422119"
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
Nombre de la propiedad. *PropertyName* es **nvarchar(256)**.

[@PropertyValue =] *PropertyValue*  
Valor de la propiedad. *PropertyValue* es **nvarchar(max)** .

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
