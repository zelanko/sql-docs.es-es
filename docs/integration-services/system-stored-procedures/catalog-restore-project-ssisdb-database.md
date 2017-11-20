---
title: Catalog.restore_project (base de datos de SSISDB) | Documentos de Microsoft
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
ms.assetid: 8adee525-579b-4d2f-b807-e2ecc07fb2e9
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 23074fc664591411666315036e3493e1b7b26134
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="catalogrestoreproject-ssisdb-database"></a>catalog.restore_project (base de datos de SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Restaura un proyecto del catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] a una versión anterior.  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
catalog.restore_project [ @folder_name = ] folder_name  
    , [ @project_name = ] project _name  
    , [ @object_version_lsn = ] object_version_lsn  
  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @folder_name =] *nombreDeCarpeta*  
 Nombre de la carpeta que contiene el proyecto. El *nombre_de_carpeta* es **nvarchar (128)**.  
  
 [ @project _name =] *Nombre_proyecto*  
 Nombre del proyecto. El *Nombre_proyecto* es **nvarchar (128)**.  
  
 [ @object_version_lsn =] *object_version_lsn*  
 Versión del proyecto. El *object_version_lsn* es **bigint**.  
  
## <a name="return-code-value"></a>Valor de código de retorno  
 0 (correcto)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Detalles del proyecto se devuelven como **varbinary (max)** como parte del conjunto de resultados si la *Nombre_proyecto* se encuentra.  
  
 **NINGÚN conjunto de resultados** se devuelve si el proyecto no se puede restaurar en la carpeta especificada.  
  
## <a name="permissions"></a>Permissions  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
  
-   Permisos READ y MODIFY en el proyecto  
  
-   La pertenencia a la **ssis_admin** rol de base de datos  
  
-   La pertenencia a la **sysadmin** rol de servidor  
  
## <a name="errors-and-warnings"></a>Errores y advertencias  
 En la siguiente lista se describen algunas condiciones que pueden producir un error o una advertencia:  
  
-   La versión del proyecto no existe o no coincide con el nombre del proyecto  
  
-   El proyecto no existe  
  
-   El usuario no tiene los permisos adecuados  
  
## <a name="remarks"></a>Comentarios  
 Cuando se restaura un proyecto, se asignan los valores predeterminados a todos los parámetros y todas las referencias de entorno quedan sin modificar. El número máximo de versiones del proyecto que se conservan en el catálogo está determinado por la propiedad de catálogo **MAX_VERSIONS_PER_PROJECT**, tal y como se muestra en el [catalog_property](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md) vista.  
  
> [!WARNING]  
>  Puede que las referencias de entorno ya no sean válidas una vez restaurado un proyecto.  
  
  

