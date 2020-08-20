---
description: MSSQLSERVER_1793
title: MSSQLSERVER_1793 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
ms.assetid: 808db1d0-acc1-41d0-9287-8a5455001a02
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: aa2ba67308273dc70de17cb2812b752421559bfe
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456395"
---
# <a name="mssqlserver_1793"></a>MSSQLSERVER_1793
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalles  
  
| Atributo | Value |  
| :-------- | :---- |  
|Nombre de producto|SQL Server|  
|Id. de evento|1793|  
|Origen de eventos|MSSQLSERVER|  
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
  
