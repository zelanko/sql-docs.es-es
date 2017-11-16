---
title: MSSQLSERVER_2596 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 2596 (Database Engine error)
ms.assetid: 49ab892f-8ba3-4ba1-b562-ddf205019802
caps.latest.revision: "18"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 8eb8b851b589c916a449b527c8037e932d683472
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver2596"></a>MSSQLSERVER_2596
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|2596|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBCC_DATABASE_IN_READ_ONLY_MODE|  
|Texto del mensaje|Instrucción de reparación no procesada. La base de datos no puede estar en modo de solo lectura.|  
  
## <a name="explanation"></a>Explicación  
Este mensaje indica que la base de datos está en modo de solo lectura. No es posible llevar a cabo reparaciones cuando una base de datos está en modo de solo lectura.  
  
## <a name="user-action"></a>Acción del usuario  
Establezca la base de datos en modo de lectura y escritura mediante el uso de ALTER DATABASE y después vuelva a ejecutar el comando DBCC.  
  
## <a name="see-also"></a>Vea también  
[ALTER DATABASE &#40;Transact-SQL&#41;](~/t-sql/statements/alter-database-transact-sql-set-options.md)  
  
