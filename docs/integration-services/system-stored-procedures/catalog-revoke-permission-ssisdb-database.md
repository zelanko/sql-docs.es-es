---
title: Catalog.revoke_permission (base de datos de SSISDB) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- revoke_permission stored procedure [Integration Services]
- catalog.revoke_permission stored procedure [Integration Services]
ms.assetid: 850b9c26-5c7c-47b9-a61c-5cf9bb5948cf
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f058368bdd39b31a569d8810cccfc4d03d9f875e
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="catalogrevokepermission-ssisdb-database"></a>catalog.revoke_permission (base de datos de SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Revoca un permiso de un objeto protegible en el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```sql
catalog.revoke_permission [ @object_type = ] object_type  
    , [ @object_id = ] object_id  
    , [ @principal_id = ] principal_id  
    , [ @permission_type = ] permission_type  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @object_type =] *object_type*  
 Tipo del objeto protegible. Tipos de objetos protegibles incluyen carpeta (`1`), proyecto (`2`), entorno (`3`) y la operación (`4`). El *object_type* es **smallint***.*  
  
 [ @object_id =] *object_id*  
 Identitifier único (Id.) del objeto protegible. El *object_id* es **bigint**.  
  
 [ @principal_id =] *principal_id*  
 Identificador de la entidad de seguridad cuyo permiso se va a revocar. El *principal_id* es **int**.  
  
 [ @permission_type =] *permission_type*  
 Tipo de permiso. El *permission_type* es **smallint**.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto)  
  
 1 (object_class no es válido)  
  
 2 (object_id no existe)  
  
 3 (entidad de seguridad no existe)  
  
 4 (permiso no es válido)  
  
 5 (otro error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Ninguno  
  
## <a name="remarks"></a>Comentarios  
 Ninguno  
  
## <a name="permissions"></a>Permissions  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
  
-   Permisos ASSIGN_PERMISSIONS en el objeto  
  
-   La pertenencia a la **ssis_admin** rol de base de datos  
  
-   La pertenencia a la **sysadmin** rol de servidor  
  
## <a name="remarks"></a>Comentarios  
 Si se especifica permission_type, el procedimiento almacenado quita el permiso que se asigna explícitamente a la entidad de seguridad para el objeto. Aunque cuando no haya ninguna de esas instancias, el procedimiento devuelve un valor de código correcto (`0`). Si se omite permission_type, el procedimiento almacenado quita todos los permisos de la entidad de seguridad para el objeto.  
  
> [!NOTE]  
>  La entidad de seguridad todavía puede tener el permiso especificado en el objeto si es miembro de un rol que tiene el permiso especificado.  
  
 Este procedimiento almacenado le permite revocar los tipos de permiso descritos en la tabla siguiente:  
  
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
  
  
