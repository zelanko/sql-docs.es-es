---
title: MSSQLSERVER_2596 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 2596 (Database Engine error)
ms.assetid: 49ab892f-8ba3-4ba1-b562-ddf205019802
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 21209de55bc010c2c85285f4cbed7305c6755f4c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48118505"
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
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)  
  
  
