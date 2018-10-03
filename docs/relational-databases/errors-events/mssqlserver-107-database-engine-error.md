---
title: MSSQLSERVER_107 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 107 (Database Engine error)
ms.assetid: f33f514c-56aa-42e2-841b-e91244da90e2
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c57610443c17d7e198dae7d6bf524c6a0bdb6d62
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47715433"
---
# <a name="mssqlserver107"></a>MSSQLSERVER_107
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|107|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|P_NOCORRMATCH|  
|Texto del mensaje|El prefijo de columna '%.*ls' no coincide con un nombre de tabla o un nombre de alias utilizado en la consulta.|  
  
## <a name="explanation"></a>Explicación  
La lista de selección de la consulta contiene un asterisco (*) que se califica incorrectamente con un prefijo de columna. Este error se puede devolver en las condiciones siguientes:  
  
-   El prefijo de columna no se corresponde con ningún nombre de tabla o de alias utilizado en la consulta. Por ejemplo, la instrucción siguiente utiliza un nombre de alias (`T1`) como prefijo de columna, pero el alias no está definido en la cláusula FROM.  
  
    ```  
    SELECT T1.* FROM dbo.ErrorLog;  
    ```  
  
-   Se especifica un nombre de tabla como prefijo de columna cuando se proporciona un nombre de alias para la tabla en la cláusula FROM. Por ejemplo, la instrucción siguiente utiliza el nombre de tabla `ErrorLog` como prefijo de columna; sin embargo, la tabla tiene definido un alias (`T1`) en la cláusula FROM.  
  
    ```  
    SELECT ErrorLog.* FROM dbo.ErrorLog AS T1;  
    ```  
  
    Si se ha proporcionado un alias para un nombre de tabla en la cláusula FROM, solo puede utilizar el alias como prefijo de las columnas de la tabla.  
  
## <a name="user-action"></a>Acción del usuario  
Haga coincidir los prefijos de columna con los nombres de tabla o con los nombres de alias especificados en la cláusula FROM de la consulta. Por ejemplo, las instrucciones anteriores se pueden corregir de la forma siguiente:  
  
```  
SELECT T1.* FROM dbo.ErrorLog AS T1;  
```  
  
o Administrador de configuración de  
  
```  
SELECT ErrorLog.* FROM dbo.ErrorLog;  
```  
  
## <a name="see-also"></a>Ver también  
[MSSQLSERVER_4104](~/relational-databases/errors-events/mssqlserver-4104-database-engine-error.md)  
  
