---
title: MSSQLSERVER_17066 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17066 (Database Engine error)
ms.assetid: 7d650bbf-c583-4af8-9e22-993ee2880d95
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1b8600d83f09504d43778ad0b349ae71b653374e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62915400"
---
# <a name="mssqlserver_17066"></a>MSSQLSERVER_17066
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|17066|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SQLASSERT_ONLY|  
|Texto del mensaje|Aserción de SQL Server: archivo: \<%s>, línea =%d error de aserción = '%s'. Puede que este error esté relacionado con el tiempo de espera. Si el error persiste después de volver a ejecutar la instrucción, utilice DBCC CHECKDB para comprobar la integridad estructural de la base de datos, o bien reinicie el servidor para asegurarse de que las estructuras de datos en memoria no están dañadas.|  
  
## <a name="explanation"></a>Explicación  
 Este error puede deberse a errores transitorios relacionados con el control de tiempo, o a que los datos en memoria o en disco estén dañados.  
  
## <a name="user-action"></a>Acción del usuario  
 Vuelva a ejecutar la instrucción que hizo que se desencadenara la excepción. Si el error se debe a un evento relacionado con el control de tiempo, puede que el error no se repita. Si el problema persiste, ejecute DBCC CHECKDB para comprobar si el disco está dañado. Reinicie el servidor para asegurarse de que las estructuras de datos en memoria no están dañadas.  
  
## <a name="see-also"></a>Consulte también  
 [DBCC CHECKDB &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql)  
  
  
