---
title: MSSQLSERVER_1793 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
ms.assetid: 808db1d0-acc1-41d0-9287-8a5455001a02
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fdddf626aa081138d58387b9562327964d600074
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58530047"
---
# <a name="mssqlserver1793"></a>MSSQLSERVER_1793
    
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
  
```sql  
DROP INDEX [<clustered_index_name>] ON [<table_name>]   
WITH ( ONLINE = OFF, MOVE TO [PRIMARY] )  
GO  
```  
  
 El siguiente ejemplo funciona correctamente debido a que se especifican tanto una cláusula **MOVE TO** para los datos base como una cláusula **FILESTREAM_ON** para los datos FILESTREAM.  
  
```sql  
DROP INDEX [<clustered_index_name>] ON [<table_name>]   
WITH ( ONLINE = OFF, MOVE TO [PRIMARY], filestream_on 'default' )  
GO  
```  
  
 El siguiente ejemplo también funciona correctamente debido a que no se especifican ni una cláusula **MOVE TO** para los datos base ni una cláusula **FILESTREAM_ON** para los datos FILESTREAM.  
  
```sql  
DROP INDEX [<clustered_index_name>] ON [<table_name>]   
WITH ( ONLINE = OFF )  
GO  
```  
  
  
