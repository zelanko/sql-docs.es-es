---
title: MSSQLSERVER_17065 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 17065 (Database Engine error)
ms.assetid: 63c2ba5a-be34-461e-bee1-03c25b396cd2
caps.latest.revision: "16"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: df4a27deaedcf5a9cc0102ba97147b650aca0e10
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver17065"></a>MSSQLSERVER_17065
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|17065|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SQLASSERT_BOTH|  
|Texto del mensaje|Aserción de SQL Server: archivo: \<%s>, línea = %d error de aserción = '%s' % s. Puede que este error esté relacionado con el tiempo de espera. Si el error persiste después de volver a ejecutar la instrucción, utilice DBCC CHECKDB para comprobar la integridad estructural de la base de datos, o bien reinicie el servidor para asegurarse de que las estructuras de datos en memoria no están dañadas.|  
  
## <a name="explanation"></a>Explicación  
Este error puede deberse a errores transitorios relacionados con el control de tiempo, o a que los datos en memoria o en disco estén dañados.  
  
## <a name="user-action"></a>Acción del usuario  
Vuelva a ejecutar la instrucción que hizo que se desencadenara la excepción. Si el error se debe a un evento relacionado con el control de tiempo, puede que el error no se repita. Si el problema persiste, ejecute DBCC CHECKDB para comprobar si el disco está dañado. Reinicie el servidor para asegurarse de que las estructuras de datos en memoria no están dañadas.  
  
## <a name="see-also"></a>Vea también  
[DBCC CHECKDB &#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)  
  
