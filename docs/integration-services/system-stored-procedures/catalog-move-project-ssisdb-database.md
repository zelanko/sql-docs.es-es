---
title: catalog.move_project (base de datos de SSISDB) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: ef3b0325-d8e9-472b-bf11-7d3efa6312ff
caps.latest.revision: "15"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0a7cc5e2b529f503c0a4182f43e1436fc355ab4c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="catalogmoveproject---ssisdb-database"></a>catalog.move_project - base de datos de SSISDB
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Mueve un proyecto desde una carpeta a otra del catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
catalog.move_project [ @source_folder = ] source_folder  
    , [ @project_name = ] project_name  
    , [ @destination_folder = ] destination_folder  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @source_folder = ] *source_folder*  
 Nombre de la carpeta de origen en la que está ubicado el proyecto antes de moverlo. El parámetro *source_folder* es **nvarchar(128)**.  
  
 [ @project_name = ] *project_name*  
 Nombre del proyecto que se va a mover. El parámetro *project_name* es **nvarchar(128)**.  
  
 [ @destination_folder = ] *destination_folder*  
 Nombre de la carpeta de destino en la que está ubicado el proyecto después de moverlo. El parámetro *destination_folder* es **nvarchar(128)**.  
  
## <a name="return-code-value"></a>Valor de código de retorno  
 0 (Correcto)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Ninguno  
  
## <a name="permissions"></a>Permissions  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
  
-   Los permisos READ y MODIFY del proyecto que se desea mover y el permiso CREATE_OBJECTS de la carpeta de destino  
  
-   Pertenencia al rol de base de datos de **ssis_admin**  
  
-   Pertenencia al rol de servidor de **sysadmin**  
  
## <a name="errors-and-warnings"></a>Errores y advertencias  
 La siguiente lista describe algunas condiciones que pueden hacer que este procedimiento almacenado produzca un error:  
  
-   El proyecto no existe  
  
-   La carpeta de origen no existe  
  
-   La carpeta de destino no existe o ya contiene un proyecto con el mismo nombre  
  
-   El usuario no tiene los permisos adecuados  
  
## <a name="remarks"></a>Comentarios  
 Cuando un proyecto se mueve de una carpeta de origen a una carpeta de destino, el proyecto de la carpeta de origen y las referencias de entorno correspondientes se eliminan. En la carpeta de destino, se crea un proyecto idéntico y unas referencias de entorno. Las referencias de entorno relativas se resolverán en otra carpeta después de la operación de traslado. Las referencias absolutas se resolverán en la misma carpeta después de la operación de traslado.  
  
> [!NOTE]  
>  Un proyecto puede tener referencias de entorno absolutas o relativas. Las referencias relativas hacen referencia al entorno por nombre y requieren que el entorno resida en la misma carpeta que el proyecto. Las referencias absolutas hacen referencia al entorno por nombre y carpeta y hacen referencia a los entornos que residen en una carpeta diferente a la del proyecto.  
  
  
