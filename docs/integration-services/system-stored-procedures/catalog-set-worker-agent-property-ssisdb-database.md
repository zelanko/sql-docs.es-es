---
title: Catalog.set_worker_agent_property (base de datos de SSISDB) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ddd2a534-6925-4d66-90e7-541c14f41de7
caps.latest.revision: 2
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: cd1366409f9fb0af271b26fad3b8b911f99acc06
ms.openlocfilehash: d0476bbb67cff44a05aed1441a31d679882b4cb3
ms.contentlocale: es-es
ms.lasthandoff: 09/08/2017

---
# <a name="catalogsetworkeragentproperty-ssisdb-database"></a>Catalog.set_worker_agent_property (base de datos de SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

Establece la propiedad de un [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] escala Out trabajo.

## <a name="syntax"></a>Sintaxis

```tsql
set_worker_agent_property [ @WorkerAgentId = ] WorkerAgentId, [ @PropertyName = ] PropertyName, [ @PropertyValue = ] PropertyValue 
```

## <a name="arguments"></a>Argumentos
[ @WorkerAgentId =] *WorkerAgentId*  
Id. de agente de trabajo del trabajador Out en escala. El *WorkerAgentId* es **uniqueidentifier**.

[ @PropertyName =] *PropertyName*  
El nombre de la propiedad. El *PropertyName* es **nvarchar (256)**.

[ @PropertyValue =] *PropertyValue*  
El valor de la propiedad. El *PropertyValue* es **nvarchar (max)**.

## <a name="remarks"></a>Comentarios
Los nombres de propiedades válidos son **DisplayName**, **descripción**, **etiquetas**.

## <a name="return-code-value"></a>Valor de código de retorno  
 0 (correcto)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Ninguno  

## <a name="permissions"></a>Permissions  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
  
-   La pertenencia a la **ssis_admin** rol de base de datos  
  
-   La pertenencia a la **sysadmin** rol de servidor

## <a name="erros-and-warnings"></a>Errores y advertencias
  En la siguiente lista se describen algunas condiciones que pueden producir un error o una advertencia:  
  
-   El usuario no tiene los permisos adecuados 

-   El identificador del agente de trabajo no es válido.

-   El nombre de propiedad no es válido.

-   El valor de propiedad no es vilid.  
