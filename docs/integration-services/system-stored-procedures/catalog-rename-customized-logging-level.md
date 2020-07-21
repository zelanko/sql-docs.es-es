---
title: catalog.rename_customized_logging_level | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: b1a57d5e-3f03-4901-8b2b-bb8b371b595b
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7e73f5f38ea1253a933d0f27221c41136b1a6315
ms.sourcegitcommit: 703968b86a111111a82ef66bb7467dbf68126051
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/07/2020
ms.locfileid: "86053667"
---
# <a name="catalogrename_customized_logging_level"></a>catalog.rename_customized_logging_level 

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

  Cambia el nombre de un nivel de registro personalizado existente. Para obtener más información sobre los niveles de registro personalizados, consulte [Registro de Integration Services &#40;SSIS&#41;](../../integration-services/performance/integration-services-ssis-logging.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
catalog.rename_customized_logging_level [ @old_name = ] old_name  
    , [ @new_name = ] new_name  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @old_name = ] *old_name*  
 Nombre de un nivel de registro personalizado existente que va a cambiar.  
  
 *old_name* es **nvarchar(128)** .  
  
 [ @new_name = ] *new_name*  
 Nuevo nombre del nivel de registro personalizado especificado.  
  
 *new_name* es **nvarchar(128)** .  
  
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
  
  
