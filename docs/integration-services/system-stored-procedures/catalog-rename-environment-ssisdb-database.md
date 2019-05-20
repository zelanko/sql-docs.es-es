---
title: catalog.rename_environment (base de datos de SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: c73d7452-31c5-4f4e-afcc-e9eca760c826
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 42d83c5adf9afa268bb7ec6e069731d6f8a05219
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/16/2019
ms.locfileid: "65716001"
---
# <a name="catalogrenameenvironment-ssisdb-database"></a>catalog.rename_environment (base de datos de SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Cambia el nombre de un entorno en el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
catalog.rename_environment [ @folder_name = ] folder_name  
    , [ @environment_name = ] environment_name  
    , [ @new_environment_name= ] new_environment_name  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @folder_name = ] *folder_name*  
 Nombre de la carpeta que contiene el entorno. *folder_name* es **nvarchar(128)**.  
  
 [ @environment_name = ] *environment_name*  
 Nombre original del entorno. *environment_name* es **nvarchar(128)**.  
  
 [ @new_environment_name = ] *new_environment_name*  
 Nuevo nombre del entorno. *new_environment_name* es **nvarchar(128)**.  
  
## <a name="return-code-value"></a>Valor de código de retorno  
 0 (correcto)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="permissions"></a>Permisos  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
  
-   Permisos MODIFY en el entorno  
  
-   Pertenencia al rol de base de datos de **ssis_admin**  
  
-   Pertenencia al rol de servidor de **sysadmin**  
  
## <a name="errors-and-warnings"></a>Errores y advertencias  
 En la siguiente lista se describen algunas condiciones que pueden producir un error o una advertencia:  
  
-   El nombre del entorno original no es válido  
  
-   El nuevo nombre ya se ha utilizado en un entorno existente  
  
## <a name="remarks"></a>Notas  
 Las referencias de entorno de los proyectos no se actualizan automáticamente al cambiar el nombre del entorno. Las referencias del entorno deben actualizadas como corresponda. Este procedimiento almacenado tendrá éxito aunque las referencias del entorno se interrumpan cambiando el nombre del entorno. Las referencias del entorno se deben actualizar después de que se completa este procedimiento almacenado.  
  
> [!NOTE]  
>  Cuando una referencia de entorno no es válida, la validación y ejecución de los paquetes correspondientes que utilizan esas referencias no se ejecutarán correctamente.  
  
  
