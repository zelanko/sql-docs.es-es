---
title: MSSQLSERVER_2596 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 2596 (Database Engine error)
ms.assetid: 49ab892f-8ba3-4ba1-b562-ddf205019802
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d0c54732eabe0289f7b8389c26b6f27a80e3b8ea
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47767173"
---
# <a name="mssqlserver2596"></a>MSSQLSERVER_2596
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
  
## <a name="see-also"></a>Ver también  
[ALTER DATABASE &#40;Transact-SQL&#41;](~/t-sql/statements/alter-database-transact-sql-set-options.md)  
  
