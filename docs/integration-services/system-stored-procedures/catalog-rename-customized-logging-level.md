---
title: Catalog.rename_customized_logging_level | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: b1a57d5e-3f03-4901-8b2b-bb8b371b595b
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 00c2cd8fa5f8423a7791d663d02aecbf27b8ab41
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="catalogrenamecustomizedlogginglevel"></a>Catalog.rename_customized_logging_level
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Cambia el nombre de un nivel de registro personalizado existente. Para obtener más información acerca de los niveles de registro personalizados, consulte [Integration Services &#40; SSIS &#41; Registro](../../integration-services/performance/integration-services-ssis-logging.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
rename_customized_logging_level [ @old_name = ] old_name  
    , [ @new_name = ] new_name  
  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @old_name =] *Nombre_antiguo*  
 El nombre de la existente Personalizar nivel de registro para cambiar el nombre.  
  
 El *Nombre_antiguo* es **nvarchar (128)**.  
  
 [ @new_name =] *new_name*  
 El nuevo nombre para el elemento especificado el nivel de registro personalizado.  
  
 El *new_name* es **nvarchar (128)**.  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="return-codes"></a>Códigos de retorno  
 0 (correcto)  
  
 Cuando se produce un error en el procedimiento almacenado, se genera un error.  
  
## <a name="result-set"></a>Conjunto de resultados  
 Ninguno  
  
## <a name="permissions"></a>Permissions  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
  
-   Pertenencia al rol de base de datos **ssis_admin**  
  
-   Pertenencia al rol de servidor **sysadmin**  
  
## <a name="errors-and-warnings"></a>Errores y advertencias  
 En la lista siguiente se describen las condiciones que hacen que el procedimiento almacenado genere un error.  
  
-   El usuario no tiene los permisos necesarios.  
  
  
