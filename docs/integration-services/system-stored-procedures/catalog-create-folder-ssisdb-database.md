---
title: catalog.create_folder (base de datos de SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 06fb3549-e970-4ca2-a61f-59affb9c6dcc
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 24ff352e3504b07a231b300c4b68378c19fae868
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47784933"
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
 None  
  
## <a name="permissions"></a>Permisos  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
  
-   Pertenencia al rol de base de datos de **ssis_admin**  
  
-   Pertenencia al rol de servidor de **sysadmin**  
  
## <a name="errors-and-warnings"></a>Errores y advertencias  
El procedimiento almacenado devuelve un error si ya existe una carpeta con el mismo nombre.  
  
  
