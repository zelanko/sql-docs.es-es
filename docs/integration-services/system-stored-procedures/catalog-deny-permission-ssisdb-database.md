---
title: Catalog.deny_permission (base de datos de SSISDB) | Documentos de Microsoft
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: de310bac-2ddc-4ef9-8783-43dcb02a94f1
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 689a59e92286881fa3be7ee3754a786ccb54ae6c
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="catalogdenypermission-ssisdb-database"></a>catalog.deny_permission (base de datos de SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Deniega un permiso en un objeto protegible del catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```sql
catalog.deny_permission [ @object_type = ] object_type  
    , [ @object_id = ] object_id  
    , [ @principal_id = ] principal_id  
    , [ @permission_type = ] permission_type  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @object_type =] *object_type*  
 Tipo del objeto protegible. Tipos de objetos protegibles incluyen carpeta (`1`), proyecto (`2`), entorno (`3`) y la operación (`4`). El *object_type* es **smallint***.*  
  
 [ @object_id =] *object_id*  
 Identificador único (Id.) o clave principal del objeto protegible. El *object_id* es **bigint**.  
  
 [ @principal_id =] *principal_id*  
 El identificador de la entidad de seguridad que será denegado. El *principal_id* es **int**.  
  
 [ @permission_type =] *permission_type*  
 El tipo de permiso que será denegado. El *permission_type* es **smallint**.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto)  
  
 1 (object_class no es válido)  
  
 2 (object_id no existe)  
  
 3 (entidad de seguridad no existe)  
  
 4 (permiso no es válido)  
  
 5 (otro error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Ninguno  
  
## <a name="permissions"></a>Permissions  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
  
-   Permiso MANAGE_PERMISSIONS en el objeto  
  
-   La pertenencia a la **ssis_admin** rol de base de datos  
  
-   La pertenencia a la **sysadmin** rol de servidor  
  
## <a name="remarks"></a>Comentarios  
 Este procedimiento almacenado le permite denegar los tipos de permiso descritos en la tabla siguiente:  
  
|Valor de permission_type|Nombre del permiso|Descripción del permiso|Tipos de objetos aplicables|  
|----------------------------|---------------------|----------------------------|-----------------------------|  
|`1`|READ|Permite a la entidad de seguridad leer información que se considera parte del objeto, como las propiedades. No permite a la entidad de seguridad enumerar o leer el contenido de otros objetos contenidos dentro del objeto.|Carpeta, proyecto, entorno, operación|  
|`2`|MODIFY|Permite a la entidad de seguridad modificar información que se considera parte del objeto, como las propiedades. No permite a la entidad de seguridad modificar otros objetos contenidos dentro del objeto.|Carpeta, proyecto, entorno, operación|  
|`3`|Ejecute|Permite a la entidad de seguridad ejecutar todos los paquetes del proyecto.|Proyecto|  
|`4`|MANAGE_PERMISSIONS|Permite a la entidad de seguridad asignar permisos a los objetos.|Carpeta, proyecto, entorno, operación|  
|`100`|CREATE_OBJECTS|Permite a la entidad de seguridad crear objetos en la carpeta.|Carpeta|  
|`101`|READ_OBJECTS|Permite a la entidad de seguridad leer todos los objetos de la carpeta.|Carpeta|  
|`102`|MODIFY_OBJECTS|Permite a la entidad de seguridad modificar todos los objetos de la carpeta.|Carpeta|  
|`103`|EXECUTE_OBJECTS|Permite a la entidad de seguridad ejecutar todos los paquetes de todos los proyectos de la carpeta.|Carpeta|  
|`104`|MANAGE_OBJECT_PERMISSIONS|Permite a la entidad de seguridad administrar los permisos de todos los objetos de la carpeta.|Carpeta|  
  
## <a name="errors-and-warnings"></a>Errores y advertencias  
 En la siguiente lista se describen algunas condiciones que pueden producir un error o una advertencia:  
  
-   Si se especifica permission_type, el procedimiento deniega el permiso especificado que se asigna explícitamente a la entidad de seguridad especificada para el objeto especificado. Aun cuando no haya ninguna de esas instancias, el procedimiento devuelve todavía un valor de código correcto (`0`).  
  
-   Si se omite permission_type, el procedimiento deniega todos los permisos de la entidad de seguridad especificada en el objeto especificado.  
  
  

