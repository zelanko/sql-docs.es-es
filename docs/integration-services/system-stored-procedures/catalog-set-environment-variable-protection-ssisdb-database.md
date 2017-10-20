---
title: Catalog.set_environment_variable_protection (base de datos de SSISDB) | Documentos de Microsoft
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 005b6b2f-a5d9-4ea4-8d4e-beed6ab33c0d
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 6d282ca675a35e84f2d283d3ad85b15039a15e52
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="catalogsetenvironmentvariableprotection-ssisdb-database"></a>catalog.set_environment_variable_protection (base de datos de SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Establece el bit de sensibilidad de una variable de entorno en el catálogo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
set_environment_variable_protection [ @folder_name = ] folder_name  
    , [ @environment_name = ] environment_name  
    , [ @variable_name = ] variable_name  
    , [ @is_sensitive = ] is_sensitive  
  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @folder_name =] *nombreDeCarpeta*  
 Nombre de la carpeta que contiene el entorno. El *nombre_de_carpeta* es **nvarchar (128)**.  
  
 [ @environment_name =] *environment_name*  
 El nombre del entorno. El *environment_name* es **nvarchar (128)**.  
  
 [ @variable_name =] *variable_name*  
 Nombre de la variable de entorno. El *variable_name* es **nvarchar (128)**.  
  
 [ @sensitive =] *confidencial*  
 Indica si la variable contiene un valor confidencial o no. Use un valor de `1` para indicar que el valor de la variable de entorno es confidencial o un valor de `0` para indicar que no lo es. Un valor confidencial se cifra cuando se almacena. Un valor que no es confidencial se almacena como texto simple. El *confidencial* parámetro es **bits**.  
  
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
  
-   El nombre de la carpeta no es válido  
  
-   El nombre del entorno no es válido  
  
-   El nombre de la variable de entorno no es válido  
  
-   El usuario no tiene los permisos adecuados  
  
  
