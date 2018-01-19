---
title: GO (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/27/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server (starting with 2008)
f1_keywords:
- GO
- GO_TSQL
dev_langs: TSQL
helpviewer_keywords:
- batches [SQL Server], ending
- ending batches [SQL Server]
- GO command
ms.assetid: b2ca6791-3a07-4209-ba8e-2248a92dd738
caps.latest.revision: "39"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: c6c23d90905f0250da74037fcf64082dd87360f7
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/19/2018
---
# <a name="sql-server-utilities-statements---go"></a>Instrucciones de utilidades SQL Server - GO
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Proporciona los comandos que no son [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucciones, pero son reconocidos por el **sqlcmd** y **osql** utilidades y [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] Editor de código. Estos comandos se pueden usar para facilitar la legibilidad y la ejecución de lotes y scripts.  
  
  GO marca el final de un lote de [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucciones para el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilidades.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
GO [count]  
```  
  
## <a name="arguments"></a>Argumentos  
 *Recuento*  
 Es un entero positivo. El lote que precede a GO se ejecutará el número especificado de veces.  
  
## <a name="remarks"></a>Comentarios  
 GO no es una [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción, sino un comando reconocido por el **sqlcmd** y **osql** utilidades y [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] editor de código.  
  
 Las utilidades de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interpretan GO como una señal de que deben enviar el lote actual de instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El lote actual de instrucciones está formado por todas las instrucciones especificadas desde el último comando GO o desde el comienzo de la sesión o script ad hoc si se trata del primer comando GO.  
  
 Una instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] no puede ocupar la misma línea que un comando GO. Sin embargo, la línea sí puede contener comentarios.  
  
 Los usuarios deben seguir las reglas de los lotes. Por ejemplo, la ejecución de un procedimiento almacenado después de la primera instrucción de un lote debe incluir la palabra clave EXECUTE. El ámbito de las variables locales (definidas por el usuario) está limitado a un lote y no es posible referirse a ellas después del comando GO.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @MyMsg VARCHAR(50)  
SELECT @MyMsg = 'Hello, World.'  
GO -- @MyMsg is not valid after this GO ends the batch.  
  
-- Yields an error because @MyMsg not declared in this batch.  
PRINT @MyMsg  
GO  
  
SELECT @@VERSION;  
-- Yields an error: Must be EXEC sp_who if not first statement in   
-- batch.  
sp_who  
GO  
```  
  
 Las aplicaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueden enviar varias instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para su ejecución como un lote. En ese momento, las instrucciones del lote se compilan en un único plan de ejecución. Los programadores que ejecutan instrucciones ad hoc en las utilidades de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o que generan Scripts de instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] para ejecutarlas a través de las utilidades de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizan el comando GO para indicar el final de un lote.  
  
 Las aplicaciones basadas en las API de ODBC u OLE DB reciben un error de sintaxis al intentar ejecutar un comando GO. Las utilidades de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nunca envían un comando GO al servidor.  
  
 No use un punto y coma como terminador de instrucción después de GO.  
  
## <a name="permissions"></a>Permissions  
 GO es un comando de utilidad que no requiere permisos. Cualquier usuario puede ejecutarlo.  
  
```  
-- Yields an error because ; is not permitted after GO  
SELECT @@VERSION;  
GO;  
```  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se crean dos lotes. El primer lote solo contiene un `USE``AdventureWorks2012` instrucción para establecer el contexto de base de datos. Las instrucciones restantes utilizan una variable local. Por lo tanto, es necesario agrupar todas las declaraciones de variable locales en un único lote. Esto se logra al no usar el comando `GO` hasta después de la última instrucción que hace referencia a la variable.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @NmbrPeople int  
SELECT @NmbrPeople = COUNT(*)  
FROM Person.Person;  
PRINT 'The number of people as of ' +  
      CAST(GETDATE() AS char(20)) + ' is ' +  
      CAST(@NmbrPeople AS char (10));  
GO  
```  
  
 En el siguiente ejemplo ejecutan las instrucciones del lote dos veces.  
  
```  
SELECT DB_NAME();  
SELECT USER_NAME();  
GO 2  
```  
  
  
