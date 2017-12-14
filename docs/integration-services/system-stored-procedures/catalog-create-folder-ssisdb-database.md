---
title: catalog.create_folder (base de datos de SSISDB) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 06fb3549-e970-4ca2-a61f-59affb9c6dcc
caps.latest.revision: "12"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d909a3596dd260065904f0d4e8413978288cc9fd
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="catalogcreatefolder-ssisdb-database"></a>catalog.create_folder (base de datos de SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Crea una carpeta en el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
catalog.create_folder [@folder_name =] folder_name, [@folder_id =] folder_id OUTPUT  
```  
  
## <a name="arguments"></a>Argumentos  
 [@folder_name =] *folder_name*  
 El nombre de la nueva carpeta. *folder_name* es **nvarchar(128)**.  
  
 [@folder_name =] *folder_id*  
 El identificador único (ID) de la carpeta. *folder_id* es **bigint**.  
  
## <a name="return-code-value"></a>Valor de código de retorno  
 Se devuelve el identificador de carpeta.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Ninguno  
  
## <a name="permissions"></a>Permissions  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
  
-   Pertenencia al rol de base de datos **ssis_admin**  
  
-   Pertenencia al rol de servidor **sysadmin**  
  
## <a name="errors-and-warnings"></a>Errores y advertencias  
El procedimiento almacenado devuelve un error si ya existe una carpeta con el mismo nombre.  
  
  
