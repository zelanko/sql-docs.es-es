---
title: catalog.update_master_address (base de datos SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: language-reference
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: craigg
ms.workload: Inactive
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: ee47c3bbd6d0e8f29152ca0869b3315855180a0f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="catalogupdatemasteraddress-ssisdb-database"></a>catalog.update_master_address (base de datos SSISDB)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Actualice el punto de conexión de patrón de escalabilidad horizontal de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].

## <a name="syntax"></a>Sintaxis

```sql
catalog.update_master_address [@MasterAddress = ] masterAddress
```

## <a name="arguments"></a>Argumentos
[ @MasterAddress = ] *masterAddress*  
Punto de conexión de patrón de escalabilidad horizontal. *masterAddress* es **nvarchar**.  

 ## <a name="return-code-value"></a>Valor de código de retorno  
 0 (correcto)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  

## <a name="permissions"></a>Permisos  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
   
-   Pertenencia al rol de base de datos de **ssis_admin**  
  
-   Pertenencia al rol de servidor de **sysadmin**  
 
