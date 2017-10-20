---
title: Catalog.set_execution_property_override_value | Documentos de Microsoft
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 37cb3c01-f4c0-4978-8e40-a975456def5a
caps.latest.revision: 4
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 20f2c882a78f5e60931b0152d5877898e1972d0a
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="catalogsetexecutionpropertyoverridevalue"></a>catalog.set_execution_property_override_value
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Establece el valor de una propiedad para una instancia de ejecución en el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
catalog.set_execution_property_override_value [ @execution_id = execution_id  
    , [ @property_path = ] property_path  
    , [ @property_value = ] property_value  
    , [ @sensitive = ] sensitive  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @execution_id =] *execution_id*  
 Identificador único de la instancia de ejecución. El *execution_id* es **bigint**.  
  
 [ @property_path =] *rutaDeAccesoAPropiedad*  
 Ruta de acceso a la propiedad en el paquete. El *rutaDeAccesoAPropiedad* es **nvarchar (4000)**.  
  
 [ @property_value =] *property_value*  
 El valor de invalidación que se va a asignar a la propiedad. El *property_value* es **nvarchar (max)**.  
  
 [ @sensitive =] *confidencial*  
 Cuando el valor es 1, la propiedad es confidencial y se cifra cuando se almacena. Cuando el valor es 0, la propiedad no es confidencial y el valor se almacena como texto simple. El *confidencial* argumento es **bits**.  
  
## <a name="remarks"></a>Comentarios  
 Este procedimiento realiza la misma función que la **invalidaciones de propiedad** sección la **avanzadas** pestaña de la **Ejecutar paquete** cuadro de diálogo. La ruta de acceso a la propiedad se deriva de la **ruta de acceso del paquete** propiedad de la tarea de paquete.  
  
## <a name="return-code-value"></a>Valor de código de retorno  
 0 (correcto)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Ninguno  
  
## <a name="errors-and-warnings"></a>Errores y advertencias  
 En la siguiente lista se describen algunas condiciones que pueden producir un error o una advertencia:  
  
-   El usuario no tiene los permisos adecuados  
  
-   El identificador de ejecución no es válido  
  
-   La ruta de acceso a la propiedad no es válida  
  
-   El tipo de datos del valor de propiedad no coincide con el tipo de datos de la propiedad.  
  
## <a name="see-also"></a>Vea también  
 [catalog.set_execution_parameter_value &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)  
  
  
