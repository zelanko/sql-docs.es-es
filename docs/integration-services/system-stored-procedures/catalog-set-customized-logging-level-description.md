---
title: catalog.set_customized_logging_level_description | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 6ceaa39f-2439-457b-b99f-f12d88a1be32
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b836c5b2ef056e630a5ff6bf00848fa5bb3a5e31
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "71295350"
---
# <a name="catalogset_customized_logging_level_description"></a>catalog.set_customized_logging_level_description 

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Cambia la descripción de un nivel de registro personalizado existente. Para obtener más información sobre los niveles de registro personalizados, consulte [Registro de Integration Services &#40;SSIS&#41;](../../integration-services/performance/integration-services-ssis-logging.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
catalog.set_customized_logging_level_description [ @level_name = ] level_name  
    , [ @level_description = ] level_description  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @level_name = ] *level_name*  
 Es el nombre de un nivel de registro personalizado existente.  
  
 *level_name* es **nvarchar(128)** .  
  
 [ @level_description = ] *level_description*  
 Es la descripción del nivel de registro personalizado especificado.  
  
 El parámetro *level_description* es de tipo **nvarchar(1024)** .  
  
## <a name="remarks"></a>Observaciones  
  
## <a name="return-codes"></a>Códigos de retorno  
 0 (correcto)  
  
 Cuando se produce un error en el procedimiento almacenado, se genera un error.  
  
## <a name="result-set"></a>Tipo de cursor  
 None  
  
## <a name="permissions"></a>Permisos  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
  
-   Pertenencia al rol de base de datos **ssis_admin**  
  
-   Pertenencia al rol de servidor **sysadmin**  
  
## <a name="errors-and-warnings"></a>Errores y advertencias  
 En la lista siguiente se describen las condiciones que hacen que el procedimiento almacenado genere un error.  
  
-   El usuario no tiene los permisos requeridos.  
  
  
