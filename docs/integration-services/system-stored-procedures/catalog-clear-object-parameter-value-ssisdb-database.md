---
title: catalog.clear_object_parameter_value (base de datos de SSISDB) | Microsoft Docs
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
ms.assetid: dcbbb714-a051-4805-9e2b-2c2fb647c890
caps.latest.revision: "19"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9c079f4c5ce9809d1624992601213f6d5fafc8e3
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="catalogclearobjectparametervalue-ssisdb-database"></a>catalog.clear_object_parameter_value (base de datos de SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Borra el valor de un parámetro para un paquete o proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] existente almacenado en el servidor.  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
catalog.clear_object_parameter [ @folder_name = ] folder_name   
    , [ @project_name = ] project_name   
    , [ @object_type = ] object_type   
    , [ @object_name = ] object_name   
    , [ @parameter_ name = ] parameter_name  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @folder_name = ] *folder_name*  
 Nombre de la carpeta que contiene el proyecto. *folder_name* es **nvarchar(128)**.  
  
 [ @project_name = ] *project_name*  
 Nombre del proyecto. *project_name* es **nvarchar(128)**.  
  
 [ @object_type = ] *object_type*  
 Tipo de objeto. Los valores válidos incluyen `20` para un proyecto y `30` para un paquete. *object_type* es **smallInt**.  
  
 [ @ object _name = ] *object _name*  
 Nombre del paquete. *object _name* es **nvarchar(260)**.  
  
 [ @parameter_ name = ] *parameter_name*  
 Nombre del parámetro. *parameter_ name* es **nvarchar(128)**.  
  
## <a name="return-code-value"></a>Valor de código de retorno  
 0 (correcto)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Ninguno  
  
## <a name="permissions"></a>Permissions  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
  
-   Permisos READ y MODIFY en el proyecto  
  
-   Pertenencia al rol de base de datos de **ssis_admin**  
  
-   Pertenencia al rol de servidor **sysadmin**  
  
## <a name="errors-and-warnings"></a>Errores y advertencias  
 En la lista siguiente se describen algunas condiciones que pueden hacer que el procedimiento almacenado clear_object_parameter produzca un error:  
  
-   Se ha especificado un tipo de objeto no válido o no se ha podido encontrar el nombre de objeto en el proyecto.  
  
-   El proyecto no existe o no es accesible, o bien, el nombre del proyecto no es válido.  
  
-   Se ha especificado un nombre de parámetro no válido.  
  
-   El usuario no tiene los permisos adecuados.  
  
  
