---
title: catalog.set_worker_agent_property (base de datos de SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ddd2a534-6925-4d66-90e7-541c14f41de7
caps.latest.revision: 2
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 71deccd2ebb6ce3ad422cbc8e0501bb828980a4b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="catalogsetworkeragentproperty-ssisdb-database"></a>catalog.set_worker_agent_property (base de datos de SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

Establece la propiedad de un trabajo de escalabilidad horizontal de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].

## <a name="syntax"></a>Sintaxis

```sql
catalog.set_worker_agent_property [@WorkerAgentId =] WorkerAgentId, [@PropertyName =] PropertyName, [@PropertyValue =] PropertyValue 
```

## <a name="arguments"></a>Argumentos
[@WorkerAgentId =] *WorkerAgentId*  
Id. de agente de trabajo del trabajo de escalabilidad horizontal. *WorkerAgentId* es **uniqueidentifier**.

[@PropertyName =] *PropertyName*  
El nombre de la propiedad. *PropertyName* es **nvarchar(256)**.

[@PropertyValue =] *PropertyValue*  
Valor de la propiedad. *PropertyValue* es **nvarchar(max)**.

## <a name="remarks"></a>Notas
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
