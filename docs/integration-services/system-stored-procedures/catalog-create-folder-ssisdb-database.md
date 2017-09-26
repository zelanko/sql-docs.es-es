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
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: df7b4750e813601b7e4d2a02c8f1f277f1000d9c
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="catalogcreatefolder-ssisdb-database"></a>catalog.create_folder (base de datos de SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Crea una carpeta en el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```tsql  
create_folder [ @folder_name = ] folder_name, [ @folder_id = ] folder_id OUTPUT  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @folder_name =] *nombreDeCarpeta*  
 El nombre de la nueva carpeta. El *nombre_de_carpeta* es **nvarchar (128)**.  
  
 [ @folder_name =] *folder_id*  
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
 El procedimiento almacenado devuelve un error si ya existe una carpeta con el mismo nombre.  
  
  
