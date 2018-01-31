---
title: catalog.set_execution_property_override_value | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 37cb3c01-f4c0-4978-8e40-a975456def5a
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2b127fe80d88d05c3f1f56e7c355d7a24f3abd6a
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="catalogsetexecutionpropertyoverridevalue"></a>catalog.set_execution_property_override_value
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Establece el valor de una propiedad para una instancia de ejecución en el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
catalog.set_execution_property_override_value [ @execution_id = execution_id  
    , [ @property_path = ] property_path  
    , [ @property_value = ] property_value  
    , [ @sensitive = ] sensitive  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @execution_id = ] *execution_id*  
 Identificador único de la instancia de ejecución. El parámetro *execution_id* es de tipo **bigint**.  
  
 [ @property_path = ] *property_path*  
 Ruta de acceso a la propiedad en el paquete. El parámetro *property_path* es **nvarchar(4000)**.  
  
 [ @property_value = ] *property_value*  
 El valor de invalidación que se va a asignar a la propiedad. El parámetro *property_value* es **nvarchar(max)**.  
  
 [ @sensitive = ] *sensitive*  
 Cuando el valor es 1, la propiedad es confidencial y se cifra cuando se almacena. Cuando el valor es 0, la propiedad no es confidencial y el valor se almacena como texto simple. El argumento *sensitive* es **bit**.  
  
## <a name="remarks"></a>Notas  
 Este procedimiento realiza la misma función que la sección **Invalidaciones de propiedad** de la pestaña **Avanzadas** del diálogo **Ejecutar paquete**. La ruta de acceso a la propiedad se deriva de la propiedad **Ruta de acceso del paquete** de la tarea del paquete.  
  
## <a name="return-code-value"></a>Valor de código de retorno  
 0 (correcto)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="errors-and-warnings"></a>Errores y advertencias  
 En la siguiente lista se describen algunas condiciones que pueden producir un error o una advertencia:  
  
-   El usuario no tiene los permisos adecuados.  
  
-   El identificador de ejecución no es válido  
  
-   La ruta de acceso a la propiedad no es válida  
  
-   El tipo de datos del valor de propiedad no coincide con el tipo de datos de la propiedad.  
  
## <a name="see-also"></a>Ver también  
 [catalog.set_execution_parameter_value &#40;SSISDB Database&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md) (catalog.set_execution_parameter_value [base de datos de SSISDB];)  
  
  
