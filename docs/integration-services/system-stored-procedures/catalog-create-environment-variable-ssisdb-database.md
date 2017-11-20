---
title: Catalog.create_environment_variable (base de datos de SSISDB) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
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
ms.assetid: 91ed017b-6567-4bf2-b9f1-e2b5c70a5343
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: 5636651cccbb43c6c1627d1f28eccd9b3f9b5b0d
ms.contentlocale: es-es
ms.lasthandoff: 10/20/2017

---
# <a name="catalogcreateenvironmentvariable-ssisdb-database"></a>catalog.create_environment_variable (base de datos de SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Cree una variable de entorno en el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
catalog.create_environment_variable [@folder_name =] folder_name  
    , [@environment_name =] environment_name  
    , [@variable_name =] variable_name  
    , [@data_type =] data_type  
    , [@sensitive =] sensitive  
    , [@value =] value  
    , [@description =] description  
```  
  
## <a name="arguments"></a>Argumentos  
 [@folder_name =] *nombreDeCarpeta*  
 Nombre de la carpeta que contiene el entorno. El *nombre_de_carpeta* es **nvarchar (128)**.  
  
 [@environment_name =] *environment_name*  
 El nombre del entorno. El *environment_name* es **nvarchar (128)**.  
  
 [@variable_name =] *variable_name*  
 Nombre de la variable de entorno. El *variable_name* es **nvarchar (128)**.  
  
 [@data_type =] *data_type*  
 Tipo de datos de la variable. Admite datos de variable de entorno tipos incluyen **booleano**, **bytes**, **DateTime**, **doble**, **Int16**, **Int32**, **Int64**, **único**, **cadena**, **UInt32**y  **UInt64**. Tipos de datos de la variable de entorno no admitidos incluyen **Char**, **DBNull**, **objeto**, y **Sbyte**. Tipo de datos de la *data_type* parámetro es **nvarchar (128)**.  
  
 [@sensitive =] *confidencial*  
 Indica si la variable contiene un valor confidencial o no. Use un valor de `1` para indicar que el valor de la variable de entorno es confidencial o un valor de `0` para indicar que no lo es. Un valor confidencial se cifra cuando se almacena. Un valor que no es confidencial se almacena en texto sin formato. *Confidencial* es **bits**.  
  
 [@value =] *valor*  
 Valor de la variable de entorno. El *valor* es **sql_variant**.  
  
 [@description =] *descripción*  
 Descripción de la variable de entorno. El *valor* es **nvarchar (1024)**.  
  
## <a name="return-code-value"></a>Valor de código de retorno  
 0 (correcto)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Ninguno  
  
## <a name="permissions"></a>Permissions  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
  
-   Permisos READ y MODIFY en el entorno  
  
-   La pertenencia a la **ssis_admin** rol de base de datos  
  
-   La pertenencia a la **sysadmin** rol de servidor  
  
## <a name="errors-and-warnings"></a>Errores y advertencias  
 En la siguiente lista se describen algunas condiciones que pueden producir un error o una advertencia:  
  
-   El nombre de la carpeta, del entorno o de la variable de entorno no es válido  
  
-   El nombre de la variable ya existe en el entorno  
  
-   El usuario no tiene los permisos adecuados  
  
## <a name="remarks"></a>Comentarios  
 Se puede usar una variable de entorno para asignar eficazmente un valor a un parámetro de proyecto o parámetro de paquete para su uso en la ejecución de un paquete. Las variables de entorno permiten organizar los valores de parámetro. Los nombres de variable deben ser únicos dentro de un entorno.  
  
 El procedimiento almacenado valida el tipo de datos de la variable para garantizar que es compatible con el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
> [!TIP]  
>  Considere el uso de la **Int16** tipo de datos en [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en lugar de no admitida **Sbyte** tipo de datos.  
  
 El valor pasado a este procedimiento almacenado con el *valor* parámetro se convierte de un [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] tipo de datos que un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos según la tabla siguiente:  
  
|Tipo de datos de Integration Services|Tipo de datos de SQL Server|  
|------------------------------------|--------------------------|  
|**Boolean**|**bit**|  
|**Bytes**|**binario**, **varbinary**|  
|**DateTime**|**fecha y hora**, **datetime2**, **datetimeoffset**, **smalldatetime**|  
|**Doble**|Valor numérico exacto: **decimal**, **numérico**; Numérico aproximado: **float**, **real**|  
|**Int16**|**smallint**|  
|**Int32**|**int**|  
|**Int64**|**bigint**|  
|**Único**|Valor numérico exacto: **decimal**, **numérico**; Numérico aproximado: **float**, **real**|  
|**String**|**varchar**, **nvarchar**, **char**|  
|**UInt32**|**int** (**int** es la asignación disponible más cercana a **Uint32**.)|  
|**UInt64**|**bigint** (**int** es la asignación disponible más cercana a **Uint64**.)|  
  
  

