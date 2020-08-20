---
description: MSSQLSERVER_7711
title: MSSQLSERVER_7711 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 7711 (Database Engine error)
ms.assetid: a5c7cd6e-18d6-47ef-902b-db9dd64bba34
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7b31daec8051ea8bd4a4ea8a73d6754e2014edbf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88460937"
---
# <a name="mssqlserver_7711"></a>MSSQLSERVER_7711
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalles  
  
| Atributo | Value |  
| :-------- | :---- |  
|Nombre de producto|SQL Server|  
|Id. de evento|7711|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|PRT_RANGE_OVERLAP|  
|Texto del mensaje|La opción DATA_COMPRESSION se especificó más de una vez para la tabla o índice, o una de sus particiones.|  
  
## <a name="explanation"></a>Explicación  
Error en la opción DATA_COMPRESSION en una de las instrucciones siguientes:  
  
-   CREATE TABLE  
  
-   ALTER TABLE  
  
-   CREATE INDEX  
  
-   ALTER INDEX  
  
Si la tabla o índice mencionado tiene particiones, la opción DATA_COMPRESSION se enumeró más de una vez para al menos una de las particiones. Si la tabla o índice no tiene particiones, la opción DATA_COMPRESSION se mencionó más de una vez.  
  
## <a name="user-action"></a>Acción del usuario  
Para una tabla o índice con particiones, asegúrese de que la opción DATA_COMPRESSION se especifica solo una vez para cada partición. Para una tabla o índice sin particiones, utilice la opción DATA_COMPRESSION solo una vez en la instrucción.  
  
