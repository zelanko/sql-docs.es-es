---
title: MSSQLSERVER_137 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 137 (Database Engine error)
ms.assetid: 47fb4212-2165-4fec-bc41-6d548465d7be
caps.latest.revision: 12
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 443418b5b01af527dd93b31625ca1fee9284836c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36110947"
---
# <a name="mssqlserver137"></a>MSSQLSERVER_137
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|137|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|P_SCALAR_VAR_NOTFOUND|  
|Texto del mensaje|Debe declarar la variable escalar "%.*ls".|  
  
## <a name="explanation"></a>Explicación  
 Este error se produce cuando una variable se utiliza en un script SQL sin declararla primero. En el siguiente ejemplo, se devuelve el error 137 para las instrucciones SET y SELECT porque no se ha declarado **@mycol**.  
  
 SET @mycol = 'ContactName'  
  
 SELECT @mycol  
  
 Una de las causas más complicadas de este error incluye el uso de una variable que se declara fuera de la instrucción EXECUTE. Por ejemplo, la variable **@mycol** especificada en la instrucción SELECT es local para la instrucción SELECT; por tanto, está fuera de la instrucción EXECUTE.  
  
 USE AdventureWorks2012;  
  
 GO  
  
 DECLARE @mycol nvarchar(20);  
  
 SET @mycol = 'Name'  
  
 EXECUTE ('SELECT @mycol FROM Production.Product;')  
  
## <a name="user-action"></a>Acción del usuario  
 Compruebe que cualquier variable que se use en un script SQL se declara antes de utilizarse en otra parte del script.  
  
 Vuelva a escribir el script para que no haga referencia a las variables de la instrucción EXECUTE que se declaran fuera de ella. Por ejemplo:  
  
 USE AdventureWorks2012;  
  
 GO  
  
 DECLARE @mycol nvarchar(20)  
  
 SET @mycol = 'Name'  
  
 EXECUTE ('SELECT ' + @mycol + ' FROM Production.Product';)  
  
## <a name="see-also"></a>Vea también  
 [EXECUTE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/execute-transact-sql)   
 [Instrucciones SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-statements-transact-sql)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/declare-local-variable-transact-sql)  
  
  
