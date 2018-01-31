---
title: catalog.update_master_address (base de datos SSISDB) | Microsoft Docs
ms.custom: 
ms.date: 07/18/2017
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
caps.latest.revision: 
author: haoqian
ms.author: haoqian
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dd052bb7b75c3ea8002a40db3e37ca1e2a0b2788
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
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
 
