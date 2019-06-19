---
title: catalog.set_environment_variable_property (base de datos de SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: c1deb31e-b8d1-44ca-b355-570959bc6478
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4b57a3ca1893d44cc2ed3fd60e20a39c4e43f473
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65715935"
---
# <a name="catalogsetenvironmentvariableproperty-ssisdb-database"></a>catalog.set_environment_variable_property (base de datos de SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Establece la propiedad de una variable de entorno en el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
catalog.set_environment_variable_property [ @folder_name = ] folder_name  
    , [ @environment_name = ] environment_name  
    , [ @variable_name = ] variable_name  
    , [ @property_name = ] property_name  
    , [ @property_value = ] property_value  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @folder_name = ] *folder_name*  
 Nombre de la carpeta que contiene el entorno. *folder_name* es **nvarchar(128)** .  
  
 [ @environment_name = ] *environment_name*  
 El nombre del entorno. *environment_name* es **nvarchar(128)** .  
  
 [ @variable_name = ] *variable_name*  
 Nombre de la variable de entorno. El parámetro *variable_name* es de tipo **nvarchar(128)** .  
  
 [ @property_name = ] *property_name*  
 Nombre de la propiedad de variable de entorno. *property_name* es **nvarchar(128)** .  
  
 [ @property_value = ] *property_value*  
 Valor de la propiedad de variable de entorno. El parámetro *property_value* es de tipo **nvarchar(4000)** .  
  
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
  
-   El nombre de la carpeta no es válido  
  
-   El nombre del entorno no es válido  
  
-   El nombre de la variable de entorno no es válido  
  
-   El nombre de propiedad de la variable de entorno no es válido  
  
-   El usuario no tiene los permisos adecuados.  
  
## <a name="remarks"></a>Notas  
 En esta versión, solo se puede establecer la propiedad `Description`. El valor de la propiedad `Description` no puede superar los 4.000 caracteres.  
  
  
