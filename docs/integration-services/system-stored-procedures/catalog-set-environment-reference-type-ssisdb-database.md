---
title: Catalog.set_environment_reference_type (base de datos de SSISDB) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
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
ms.assetid: b79e3a06-22c0-40e5-8933-1b3414db3329
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: e83d9979ee4736528efb4851848ea3eac717fab8
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="catalogsetenvironmentreferencetype-ssisdb-database"></a>catalog.set_environment_reference_type (base de datos SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Establece el tipo de referencia y el nombre del entorno asociados con una referencia de entorno existente para un proyecto en el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
catalog.set_environment_reference_location [ @reference_id = reference_id  
    , [ @reference_type = ] reference_type  
 [  , [ @environment_folder_name = ] environment_folder_name ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @reference_id =] *reference_id*  
 Identificador único de la referencia de entorno que se va a actualizar. El *reference_id* es **bigint**.  
  
 [ @reference_type =] *reference_type*  
 Indica si el entorno se puede encontrar en la misma carpeta que el proyecto (referencia relativa) o en una carpeta diferente (referencia absoluta). Utilice el valor `R` para indicar una referencia relativa. Utilice el valor `A` para indicar una referencia absoluta. El *reference_type* es **char (1)**.  
  
 [ @environment_folder_name =] *environment_folder_name*  
 La carpeta en que se encuentra el entorno. Este valor se requiere para las referencias absolutas. El *environment_folder_name* es **nvarchar (128)**.  
  
## <a name="return-code-value"></a>Valor de código de retorno  
 0 (correcto)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Ninguno  
  
## <a name="permissions"></a>Permissions  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
  
-   Los permisos de lectura y modificación en el proyecto, y el permiso de lectura en el entorno  
  
-   La pertenencia a la **ssis_admin** rol de base de datos  
  
-   La pertenencia a la **sysadmin** rol de servidor  
  
## <a name="errors-and-warnings"></a>Errores y advertencias  
 En la siguiente lista se describen algunas condiciones que pueden producir un error o una advertencia:  
  
-   El nombre de la carpeta, el nombre del entorno o el identificador de referencia no es válido  
  
-   El usuario no los permisos adecuados  
  
-   Una referencia absoluta se especifica mediante la `A` caracteres en el *reference_location* parámetro, pero el nombre de la carpeta no se especificó con el *environment_folder_name* parámetro.  
  
## <a name="remarks"></a>Comentarios  
 Un proyecto puede tener referencias de entorno absolutas o relativas. Las referencias relativas se refieren al entorno por nombre y requieren que resida en la misma carpeta que el proyecto. Las referencias absolutas hacen referencia al entorno por nombre y carpeta, y pueden hacer referencia a los entornos que residen en una carpeta diferente que el proyecto. Un proyecto puede hacer referencia a varios entornos.  
  
> [!IMPORTANT]  
>  Si se especifica una referencia relativa, la *environment_folder_name* no se utiliza el valor del parámetro y el nombre de la carpeta de entorno se establece automáticamente en **NULL**. Si se especifica una referencia absoluta, se debe proporcionar el nombre de la carpeta de entorno en el *environment_folder_name* parámetro.  
  
  

