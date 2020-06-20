---
title: MSSQLSERVER_17065 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17065 (Database Engine error)
ms.assetid: 63c2ba5a-be34-461e-bee1-03c25b396cd2
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 47aebfa29b60a1c2ae50c6699946312996d26e6f
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84967925"
---
# <a name="mssqlserver_17065"></a>MSSQLSERVER_17065
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|17065|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SQLASSERT_BOTH|  
|Texto del mensaje|SQL Server Assertion: archivo: \<%s> , línea =% d error de aserción = '% s '% s. Puede que este error esté relacionado con el tiempo de espera. Si el error persiste después de volver a ejecutar la instrucción, utilice DBCC CHECKDB para comprobar la integridad estructural de la base de datos, o bien reinicie el servidor para asegurarse de que las estructuras de datos en memoria no están dañadas.|  
  
## <a name="explanation"></a>Explicación  
 Este error puede deberse a errores transitorios relacionados con el control de tiempo, o a que los datos en memoria o en disco estén dañados.  
  
## <a name="user-action"></a>Acción del usuario  
 Vuelva a ejecutar la instrucción que hizo que se desencadenara la excepción. Si el error se debe a un evento relacionado con el control de tiempo, puede que el error no se repita. Si el problema persiste, ejecute DBCC CHECKDB para comprobar si el disco está dañado. Reinicie el servidor para asegurarse de que las estructuras de datos en memoria no están dañadas.  
  
## <a name="see-also"></a>Consulte también  
 [DBCC CHECKDB &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql)  
  
  
