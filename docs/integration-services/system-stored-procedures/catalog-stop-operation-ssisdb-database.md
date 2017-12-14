---
title: catalog.stop_operation (base de datos de SSISDB) | Microsoft Docs
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
ms.assetid: 97fd9d22-03dd-4eda-8f6c-ba8b67acec68
caps.latest.revision: "11"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bf33675e591fbb16417bc3b251a1a47693b59673
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="catalogstopoperation-ssisdb-database"></a>catalog.stop_operation (base de datos de SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Detiene una validación o instancia de ejecución en el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
catalog.stop_operation [ @operation_id = ] operation_id  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @operation_id = ] *operation_id*  
 Identificador único de la validación o la instancia de ejecución. *operation_id* es **bigint**.  
  
## <a name="return-code-value"></a>Valor de código de retorno  
 0 (correcto)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Ninguno  
  
## <a name="permissions"></a>Permissions  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
  
-   Permisos READ y MODIFY en la validación o instancia de ejecución  
  
-   Pertenencia al rol de base de datos **ssis_admin**  
  
-   Pertenencia al rol de servidor **sysadmin**  
  
## <a name="errors-and-warnings"></a>Errores y advertencias  
 En la siguiente lista se describen algunas condiciones que pueden producir un error o una advertencia:  
  
-   El usuario no tiene los permisos adecuados.  
  
-   El identificador de la operación no es válido.  
  
-   La operación ya se ha detenido  
  
## <a name="remarks"></a>Comentarios  
 Solo un usuario, y no más de uno a la vez, debe detener una operación en el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Si varios usuarios intentan detener la operación, el procedimiento almacenado indicará que se ha realizado correctamente (valor `0`) en el primer intento, pero los intentos subsiguientes producirán un error.  
  
  
