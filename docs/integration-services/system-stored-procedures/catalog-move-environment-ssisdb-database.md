---
title: catalog.move_environment (base de datos de SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: b3fb5242-3c4c-4a87-b3e5-beb22fbab053
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 4a6d69ef7cc1a10b31cdb03f2dd43e20687a3f96
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68007822"
---
# <a name="catalogmoveenvironment-ssisdb-database"></a>catalog.move_environment (base de datos de SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Mueve un entorno desde una carpeta a otra en el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
catalog.move_environment [ @source_folder = ] source_folder  
    , [ @environment_name = ] environment_name  
    , [ @destination_folder = ] destination_folder  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @source_folder = ] *source_folder*  
 Nombre de la carpeta de origen en la que está ubicado el entorno antes de moverlo. *source_folder* es **nvarchar(128)** .  
  
 [ @environment_name = ] *environment_name*  
 Nombre del entorno que se va a mover. *environment_name* es **nvarchar(128)** .  
  
 [ @destination_folder = ] *destination_folder*  
 Nombre de la carpeta de destino en la que está ubicado el entorno después de moverlo. *destination_folder* es **nvarchar(128)** .  
  
## <a name="return-code-value"></a>Valor de código de retorno  
 0 (correcto)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="permissions"></a>Permisos  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
  
-   Permisos READ y MODIFY en el entorno  
  
-   Pertenencia al rol de base de datos de **ssis_admin**  
  
-   Pertenencia al rol de servidor de **sysadmin**  
  
## <a name="errors-and-warnings"></a>Errores y advertencias  
 En la siguiente lista se describen algunas condiciones que pueden producir un error o una advertencia:  
  
-   El entorno no existe en la carpeta de origen  
  
-   La carpeta de destino tiene un entorno con el mismo nombre  
  
-   El usuario no tiene los permisos adecuados.  
  
## <a name="remarks"></a>Notas  
 Las referencias de entorno de los proyectos no siguen el entorno durante el desplazamiento. Las referencias del entorno deben actualizadas como corresponda. Este procedimiento almacenado funcionará correctamente aunque las referencias del entorno se interrumpan al mover el entorno. Las referencias del entorno se deben actualizar después de que se completa este procedimiento almacenado.  
  
> [!NOTE]  
>  Un proyecto puede tener referencias de entorno absolutas o relativas. Las referencias relativas hacen referencia al entorno por nombre y requieren que el entorno resida en la misma carpeta que el proyecto. Las referencias absolutas hacen referencia al entorno por nombre y carpeta y hacen referencia a los entornos que residen en una carpeta diferente a la del proyecto.  
  
  
