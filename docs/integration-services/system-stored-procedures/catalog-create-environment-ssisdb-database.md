---
title: Catalog.create_environment (base de datos de SSISDB) | Documentos de Microsoft
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 66367092-9f6e-40e6-90bd-81efb078ab70
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 2d3ff080d50545b75a416e459b73ebd8bbb44666
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="catalogcreateenvironment-ssisdb-database"></a>catalog.create_environment (base de datos de SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Crea un entorno en el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```tsql  
create_environment [ @folder_name = ] folder_name  
     , [ @environment_name = ] environment_name  
  [  , [ @environment_description = ] environment_description ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @folder_name =] *nombreDeCarpeta*  
 Nombre de la carpeta que contendrá el entorno. El *nombre_de_carpeta* es **nvarchar (128)**.  
  
 [ @environment_name =] *environment_name*  
 El nombre del entorno. El *environment_name* es **nvarchar (128)**.  
  
 [ @environment_description=] *environment_description*  
 Una descripción opcional del entorno. El *environment_description* es **nvarchar (1024)**.  
  
## <a name="return-code-value"></a>Valor de código de retorno  
 0 (correcto)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Ninguno  
  
## <a name="permissions"></a>Permissions  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
  
-   Permisos READ y MODIFY en la carpeta  
  
-   La pertenencia a la **ssis_admin** rol de base de datos  
  
-   rol de base de datos  
  
-   La pertenencia a la **sysadmin** rol de servidor  
  
## <a name="errors-and-warnings"></a>Errores y advertencias  
 En la siguiente lista se describen algunas condiciones que pueden producir un error o una advertencia:  
  
-   El nombre de la carpeta no se encuentra  
  
-   Un entorno con el mismo nombre ya existe en la carpeta especificada  
  
## <a name="remarks"></a>Comentarios  
 El nombre del entorno debe ser único en la carpeta.  
  
  
