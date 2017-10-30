---
title: Catalog.update_master_address (base de datos de SSISDB) | Documentos de Microsoft
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e5e560d6011370b3d56ba13c86608d2be3d0dc6e
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="catalogupdatemasteraddress-ssisdb-database"></a>Catalog.update_master_address (base de datos de SSISDB)
[!INCLUDE[tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md](../../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]

Actualización de la [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] extremo escala Out Master.

## <a name="syntax"></a>Sintaxis

```sql
catalog.update_master_address [@MasterAddress = ] masterAddress
```

## <a name="arguments"></a>Argumentos
[ @MasterAddress =] *masterAddress*  
El extremo de la escala fuera Master. El *masterAddress* es **nvarchar**.  

 ## <a name="return-code-value"></a>Valor de código de retorno  
 0 (correcto)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  

## <a name="permissions"></a>Permissions  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
   
-   La pertenencia a la **ssis_admin** rol de base de datos  
  
-   La pertenencia a la **sysadmin** rol de servidor  
 

