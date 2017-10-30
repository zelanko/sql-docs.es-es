---
title: Catalog.create_folder (base de datos de SSISDB) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 06fb3549-e970-4ca2-a61f-59affb9c6dcc
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: 43d128f9dcc4cea632c810a13d21eb5e1ddb61df
ms.contentlocale: es-es
ms.lasthandoff: 10/20/2017

---
# <a name="catalogcreatefolder-ssisdb-database"></a>catalog.create_folder (base de datos de SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Crea una carpeta en el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
catalog.create_folder [@folder_name =] folder_name, [@folder_id =] folder_id OUTPUT  
```  
  
## <a name="arguments"></a>Argumentos  
 [@folder_name =] *nombreDeCarpeta*  
 El nombre de la nueva carpeta. El *nombre_de_carpeta* es **nvarchar (128)**.  
  
 [@folder_name =] *folder_id*  
 El identificador único (ID) de la carpeta. El *folder_id* es **bigint**.  
  
## <a name="return-code-value"></a>Valor de código de retorno  
 Se devuelve el identificador de carpeta.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Ninguno  
  
## <a name="permissions"></a>Permissions  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
  
-   La pertenencia a la **ssis_admin** rol de base de datos  
  
-   La pertenencia a la **sysadmin** rol de servidor  
  
## <a name="errors-and-warnings"></a>Errores y advertencias  
Si ya existe una carpeta con el mismo nombre, el procedimiento almacenado devuelve un error.  
  
  

