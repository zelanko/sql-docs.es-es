---
title: Catalog.clear_object_parameter_value (base de datos de SSISDB) | Documentos de Microsoft
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: dcbbb714-a051-4805-9e2b-2c2fb647c890
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 5d0d89081a31341a8d813d9985940c0e3ce0160a
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="catalogclearobjectparametervalue-ssisdb-database"></a>catalog.clear_object_parameter_value (base de datos de SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Borra el valor de un parámetro para un paquete o proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] existente almacenado en el servidor.  
  
## <a name="syntax"></a>Sintaxis  
  
```tsql  
clear_object_parameter [ @folder_name = ] folder_name   
    , [ @project_name = ] project_name   
    , [ @object_type = ] object_type   
    , [ @object_name = ] object_name   
    , [ @parameter_ name = ] parameter_name  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @folder_name =] *nombreDeCarpeta*  
 Nombre de la carpeta que contiene el proyecto. El *nombre_de_carpeta* es **nvarchar (128)**.  
  
 [ @project_name =] *Nombre_proyecto*  
 El nombre del proyecto. El *Nombre_proyecto* es **nvarchar (128)**.  
  
 [ @object_type =] *object_type*  
 Tipo de objeto. Los valores válidos incluyen `20` para un proyecto y `30` para un paquete. El *object_type* es **smallInt**.  
  
 [@ objeto _name =] *objeto _name*  
 Nombre del paquete. El *objeto _name* es **nvarchar (260)**.  
  
 [ @parameter_ nombre =] *parameter_name*  
 Nombre del parámetro. El *parameter_ nombre* es **nvarchar (128)**.  
  
## <a name="return-code-value"></a>Valor de código de retorno  
 0 (correcto)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Ninguno  
  
## <a name="permissions"></a>Permissions  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
  
-   Permisos READ y MODIFY en el proyecto  
  
-   La pertenencia a la **ssis_admin** rol de base de datos  
  
-   La pertenencia a la **sysadmin** rol de servidor  
  
## <a name="errors-and-warnings"></a>Errores y advertencias  
 En la lista siguiente se describe algunas condiciones que pueden hacer que el procedimiento clear_object_parameter almacenado genere un error:  
  
-   Se ha especificado un tipo de objeto no válido o no se ha podido encontrar el nombre de objeto en el proyecto.  
  
-   El proyecto no existe o no es accesible, o bien, el nombre del proyecto no es válido.  
  
-   Se ha especificado un nombre de parámetro no válido.  
  
-   El usuario no tiene los permisos adecuados.  
  
  
