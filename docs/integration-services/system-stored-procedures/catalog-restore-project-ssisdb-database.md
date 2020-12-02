---
description: catalog.restore_project (base de datos de SSISDB)
title: catalog.restore_project (base de datos de SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 8adee525-579b-4d2f-b807-e2ecc07fb2e9
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6ad50f86bc3c4f6f52262df591c1504139590cab
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/25/2020
ms.locfileid: "96129743"
---
# <a name="catalogrestore_project-ssisdb-database"></a>catalog.restore_project (base de datos de SSISDB)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Restaura un proyecto del catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] a una versión anterior.  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
catalog.restore_project [ @folder_name = ] folder_name  
    , [ @project_name = ] project _name  
    , [ @object_version_lsn = ] object_version_lsn  
  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @folder_name = ] *folder_name*  
 Nombre de la carpeta que contiene el proyecto. *folder_name* es **nvarchar(128)** .  
  
 [ @project _name = ] *project_name*  
 Nombre del proyecto. *project_name* es **nvarchar(128)** .  
  
 [ @object_version_lsn = ] *object_version_lsn*  
 Versión del proyecto. El parámetro *object_version_lsn* es **bigint**.  
  
## <a name="return-code-value"></a>Valor de código de retorno  
 0 (correcto)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Los detalles del proyecto se devuelven como valores **varbinary(MAX)** como parte del conjunto de resultados si se encuentra el parámetro *project_name*.  
  
 Se devuelve **NO RESULT SET** si el proyecto no se puede restaurar en la carpeta especificada.  
  
## <a name="permissions"></a>Permisos  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
  
-   Permisos READ y MODIFY en el proyecto  
  
-   Pertenencia al rol de base de datos de **ssis_admin**  
  
-   Pertenencia al rol de servidor de **sysadmin**  
  
## <a name="errors-and-warnings"></a>Errores y advertencias  
 En la siguiente lista se describen algunas condiciones que pueden producir un error o una advertencia:  
  
-   La versión del proyecto no existe o no coincide con el nombre del proyecto  
  
-   El proyecto no existe  
  
-   El usuario no tiene los permisos adecuados.  
  
## <a name="remarks"></a>Observaciones  
 Cuando se restaura un proyecto, se asignan los valores predeterminados a todos los parámetros y todas las referencias de entorno quedan sin modificar. El número máximo de versiones de proyecto que se conservan en el catálogo está determinado por la propiedad de catálogo **MAX_VERSIONS_PER_PROJECT**, tal como se muestra en la vista [catalog_property](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md).  
  
> [!WARNING]  
>  Puede que las referencias de entorno ya no sean válidas una vez restaurado un proyecto.  
  
  
