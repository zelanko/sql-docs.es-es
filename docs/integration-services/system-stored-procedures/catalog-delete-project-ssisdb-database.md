---
title: catalog.delete_project (base de datos de SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: f3431445-8dd2-443b-813e-b99db893977e
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7cbad7736ea76560cd5db800ca5e2c488545c2d8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="catalogdeleteproject-ssisdb-database"></a>catalog.delete_project (base de datos de SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Elimina un proyecto existente de una carpeta del catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
catalog.delete_project [ @folder_name = ] folder_name , [ @project_name = ] project_name  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @folder_name = ] *folder_name*  
 Nombre de la carpeta que contiene el proyecto. *folder_name* es **nvarchar(128)**.  
  
 [ @project_name = ] *project_name*  
 Nombre del proyecto que se va a eliminar. *project_name* es **nvarchar(128)**.  
  
## <a name="return-code-value"></a>Valor de código de retorno  
 0 (correcto)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="permissions"></a>Permisos  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
  
-   Permisos READ y MODIFY en el proyecto  
  
-   Pertenencia al rol de base de datos de **ssis_admin**  
  
-   Pertenencia al rol de servidor de **sysadmin**  
  
## <a name="errors-and-warnings"></a>Errores y advertencias  
 En la lista siguiente se describen algunas condiciones que pueden hacer que el procedimiento almacenado delete_project produzca un error:  
  
-   El proyecto no existe  
  
-   La carpeta no existe  
  
-   El usuario no tiene los permisos adecuados.  
  
## <a name="remarks"></a>Notas  
 Todos los objetos y las referencias de entorno del proyecto correspondiente se eliminarán junto con el proyecto. Sin embargo, las versiones del proyecto y de los registros correspondientes de las operaciones se conservarán hasta la próxima vez que se ejecute el trabajo de limpieza de operaciones.  
  
  
