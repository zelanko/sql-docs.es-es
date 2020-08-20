---
description: MSSQLSERVER_2546
title: MSSQLSERVER_2546 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 2546 (Database Engine error)
ms.assetid: c8f0e1b4-c7c4-45f2-9221-746714172313
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d955e5e7a0ab7ec1bc8c34306bc983683275f05c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482823"
---
# <a name="mssqlserver_2546"></a>MSSQLSERVER_2546
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalles  
  
| Atributo | Value |  
| :-------- | :---- |  
|Nombre de producto|SQL Server|  
|Id. de evento|2546|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBCC_INDEX_MARKED_DISABLED|  
|Texto del mensaje|El índice 'INDEX_NAME' de la tabla 'OBJECT_NAME' está marcado como deshabilitado. Genere de nuevo el índice para ponerlo en línea.|  
  
## <a name="explanation"></a>Explicación  
El índice especificado está marcado como sin conexión o está deshabilitado. Por tanto, este índice no se puede comprobar.  
  
## <a name="user-action"></a>Acción del usuario  
Vuelva a generar el índice usando ALTER INDEX.  
  
## <a name="see-also"></a>Consulte también  
[ALTER INDEX &#40;Transact-SQL&#41;](~/t-sql/statements/alter-index-transact-sql.md)  
[Reorganizar y volver a generar índices](~/relational-databases/indexes/reorganize-and-rebuild-indexes.md)  
  
