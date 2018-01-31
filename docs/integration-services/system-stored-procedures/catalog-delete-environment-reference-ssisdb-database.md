---
title: catalog.delete_environment_reference (base de datos de SSISDB) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
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
ms.assetid: 1f68f157-c4e9-412c-92b3-53a2faaba29b
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8e747fdbac0cd60733edbf0f639108df849b391d
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="catalogdeleteenvironmentreference-ssisdb-database"></a>catalog.delete_environment_reference (base de datos de SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Elimina una referencia de entorno de un proyecto en el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
delete_environment_reference [ @reference_id = ] reference_id  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @reference_id = ] *reference_id*  
 Identificador único de la referencia de entorno. *reference_id* es **bigint**.  
  
## <a name="return-code-value"></a>Valor de código de retorno  
 0 (correcto)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="permissions"></a>Permisos  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
  
-   Permiso MODIFY en el proyecto  
  
-   Pertenencia al rol de base de datos de **ssis_admin**  
  
-   Pertenencia al rol de servidor de **sysadmin**  
  
## <a name="errors-and-warnings"></a>Errores y advertencias  
 En la siguiente lista se describen algunas condiciones que pueden producir un error o una advertencia:  
  
-   El identificador de referencia de entorno no es válido  
  
-   El usuario no tiene los permisos adecuados.  
  
  
