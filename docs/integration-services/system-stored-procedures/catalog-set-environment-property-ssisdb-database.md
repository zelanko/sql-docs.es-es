---
title: catalog.set_environment_property (base de datos de SSISDB) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: a345675b-d32e-4624-96cf-ec656730b114
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 463a904a6c9e049074cb76ead1faea1be47f5a5d
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="catalogsetenvironmentproperty-ssisdb-database"></a>catalog.set_environment_property (base de datos de SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Establece la propiedad de un entorno del catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
catalog.set_environment_property [ @folder_name = ] folder_name  
    , [ @environment_name = ] environment_name  
    , [ @property_name = ] property_name  
    , [ @property_value = ] property_value  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @folder_name = ] *folder_name*  
 Nombre de la carpeta que contiene el entorno. *folder_name* es **nvarchar(128)**.  
  
 [ @environment_name = ] *environment_name*  
 El nombre del entorno. *environment_name* es **nvarchar(128)**.  
  
 [ @property_name = ] *property_name*  
 Nombre de una propiedad del entorno. *property_name* es **nvarchar(128)**.  
  
 [ @property_value = ] *property_value*  
 Valor de la propiedad del entorno. *property_value* es **nvarchar(1024)**.  
  
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
  
-   El nombre de la propiedad no es válido  
  
-   El nombre del entorno no es válido  
  
## <a name="remarks"></a>Notas  
 En esta versión, solo se puede establecer la propiedad `Description`. El valor de la propiedad `Description` no puede superar los 4.000 caracteres.  
  
  
