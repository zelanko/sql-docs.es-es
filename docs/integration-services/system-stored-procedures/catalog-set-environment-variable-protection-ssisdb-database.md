---
title: catalog.set_environment_variable_protection (base de datos de SSISDB) | Microsoft Docs
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
ms.assetid: 005b6b2f-a5d9-4ea4-8d4e-beed6ab33c0d
caps.latest.revision: "13"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ba92aca58744a652314630f786ea6783e51b1cbb
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="catalogsetenvironmentvariableprotection-ssisdb-database"></a>catalog.set_environment_variable_protection (base de datos de SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Establece el bit de sensibilidad de una variable de entorno en el catálogo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
catalog.set_environment_variable_protection [ @folder_name = ] folder_name  
    , [ @environment_name = ] environment_name  
    , [ @variable_name = ] variable_name  
    , [ @is_sensitive = ] is_sensitive  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @folder_name = ] *folder_name*  
 Nombre de la carpeta que contiene el entorno. El parámetro *folder_name* es **nvarchar(128)**.  
  
 [ @environment_name = ] *environment_name*  
 El nombre del entorno. El parámetro *environment_name* es **nvarchar(128)**.  
  
 [ @variable_name = ] *variable_name*  
 Nombre de la variable de entorno. El parámetro *variable_name* es **nvarchar(128)**.  
  
 [ @sensitive = ] *sensitive*  
 Indica si la variable contiene un valor confidencial o no. Use un valor de `1` para indicar que el valor de la variable de entorno es confidencial o un valor de `0` para indicar que no lo es. Un valor confidencial se cifra cuando se almacena. Un valor que no es confidencial se almacena como texto simple. El parámetro *sensitive* es **bit**.  
  
## <a name="return-code-value"></a>Valor de código de retorno  
 0 (Correcto)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Ninguno  
  
## <a name="permissions"></a>Permissions  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
  
-   Permisos READ y MODIFY en el entorno  
  
-   Pertenencia al rol de base de datos de **ssis_admin**  
  
-   Pertenencia al rol de servidor de **sysadmin**  
  
## <a name="errors-and-warnings"></a>Errores y advertencias  
 En la siguiente lista se describen algunas condiciones que pueden producir un error o una advertencia:  
  
-   El nombre de la carpeta no es válido  
  
-   El nombre del entorno no es válido  
  
-   El nombre de la variable de entorno no es válido  
  
-   El usuario no tiene los permisos adecuados  
  
  
