---
title: MSSQLSERVER_107 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 107 (Database Engine error)
ms.assetid: f33f514c-56aa-42e2-841b-e91244da90e2
caps.latest.revision: 9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3faf08fe9c4e31667a46bbf669d0984b4aa6557e
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37412673"
---
# <a name="mssqlserver107"></a>MSSQLSERVER_107
    
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
  
## <a name="see-also"></a>Vea también  
 [MSSQLSERVER_4104](mssqlserver-4104-database-engine-error.md)  
  
  
