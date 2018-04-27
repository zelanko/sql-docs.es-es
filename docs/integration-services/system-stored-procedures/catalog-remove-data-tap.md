---
title: catalog.remove_data_tap | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: b77db3e6-478c-441a-a838-82c4de750275
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b763a9817faeceecf1334af0a89f18613f149bfd
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="catalogremovedatatap"></a>catalog.remove_data_tap
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Quita una derivación de datos de la salida de un componente que está en una ejecución. El identificador único de la derivación de datos está asociado a una instancia de la ejecución.  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
catalog.remove_data_tap [ @data_tap_id = ] data_tap_id  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @data_tap_id = ] *data_tap_id*  
 Identificador único de la derivación de datos que se crea usando el procedimiento almacenado catalog.add_data_tap. *data_tap_id* es **bigint**.  
  
## <a name="remarks"></a>Notas  
 Si un paquete contiene varias tareas Flujo de datos con el mismo nombre, la derivación de datos se agrega a la primera tarea Flujo de datos con el nombre especificado.  
  
## <a name="return-codes"></a>Códigos de retorno  
 0 (correcto)  
  
 Cuando se produce un error en el procedimiento almacenado, se genera un error.  
  
## <a name="result-set"></a>Conjunto de resultados  
 None  
  
## <a name="remarks"></a>Notas  
 Para quitar derivaciones de datos, la instancia de la ejecución debe estar en el estado creado (un valor 1 en la columna **status** de la vista [catalog.operations &#40;Base de datos SSISDB&#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md)).  
  
## <a name="permissions"></a>Permisos  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
  
-   Permisos MODIFY en la instancia de ejecución  
  
-   Pertenencia al rol de base de datos de **ssis_admin**  
  
-   Pertenencia al rol de servidor de **sysadmin**  
  
## <a name="errors-and-warnings"></a>Errores y advertencias  
 En la lista siguiente se describen las condiciones que hacen que el procedimiento almacenado genere un error.  
  
-   El usuario no tiene permisos MODIFY.  
  
## <a name="see-also"></a>Ver también  
 [catalog.add_data_tap](../../integration-services/system-stored-procedures/catalog-add-data-tap.md)   
 [catalog.add_data_tap_by_guid](../../integration-services/system-stored-procedures/catalog-add-data-tap-by-guid.md)  
  
  
