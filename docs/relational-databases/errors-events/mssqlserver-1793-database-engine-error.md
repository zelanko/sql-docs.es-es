---
title: MSSQLSERVER_1793 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 808db1d0-acc1-41d0-9287-8a5455001a02
caps.latest.revision: "6"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e55735177ed8f7afe1177aa9d32255d8f19be3fe
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver1793"></a>MSSQLSERVER_1793
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|1793|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|FILESTREAM_BASEDATA_NEED_SAME_PARTITION|  
|Texto del mensaje|No se puede quitar el índice '%.*ls' porque no se ha especificado un esquema de partición para datos de FILESTREAM.|  
  
## <a name="explanation"></a>Explicación  
Este mensaje aparece cuando intenta quitar un índice agrupado en una tabla que contiene datos FILESTREAM y especifica una cláusula **MOVE TO** para los datos básicos pero no especifica una cláusula **FILESTREAM_ON** para los datos FILESTREAM.  
  
## <a name="user-action"></a>Acción del usuario  
Al quitar un índice clúster en una tabla que contiene datos FILESTREAM, use una de las siguientes opciones:  
  
-   Especifique tanto una cláusula **MOVE TO** para los datos base como una cláusula **FILESTREAM_ON** para los datos FILESTREAM.  
  
-   No especifique una cláusula **MOVE TO** para los datos base ni una cláusula **FILESTREAM_ON** para los datos FILESTREAM.  
  
En el siguiente ejemplo se produce un error porque un esquema de partición se especifica en los datos básicos, pero no se especifica en los datos FILESTREAM.  
  
```Transact-SQL  
DROP INDEX [<clustered_index_name>] ON [<table_name>]   
WITH ( ONLINE = OFF, MOVE TO [PRIMARY] )  
GO  
```  
  
El siguiente ejemplo funciona correctamente debido a que se especifican tanto una cláusula **MOVE TO** para los datos base como una cláusula **FILESTREAM_ON** para los datos FILESTREAM.  
  
```Transact-SQL  
DROP INDEX [<clustered_index_name>] ON [<table_name>]   
WITH ( ONLINE = OFF, MOVE TO [PRIMARY], filestream_on 'default' )  
GO  
```  
  
El siguiente ejemplo también funciona correctamente debido a que no se especifican ni una cláusula **MOVE TO** para los datos base ni una cláusula **FILESTREAM_ON** para los datos FILESTREAM.  
  
```Transact-SQL  
DROP INDEX [<clustered_index_name>] ON [<table_name>]   
WITH ( ONLINE = OFF )  
GO  
```  
  
