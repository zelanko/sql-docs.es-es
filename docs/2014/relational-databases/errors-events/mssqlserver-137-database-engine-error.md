---
title: MSSQLSERVER_137 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 137 (Database Engine error)
ms.assetid: 47fb4212-2165-4fec-bc41-6d548465d7be
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e0142cd53006609e9274972e4f5964132f5982c2
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84967975"
---
# <a name="mssqlserver_137"></a>MSSQLSERVER_137
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|137|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|P_SCALAR_VAR_NOTFOUND|  
|Texto del mensaje|Debe declarar la variable escalar "%.*ls".|  
  
## <a name="explanation"></a>Explicación  
 Este error se produce cuando una variable se utiliza en un script SQL sin declararla primero. En el ejemplo siguiente se devuelve el error 137 para las instrucciones SET y SELECT porque **@mycol** no se ha declarado.  
  
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
  
## <a name="see-also"></a>Consulte también  
 [EXECUTE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/execute-transact-sql)   
 [Instrucciones SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-statements-transact-sql)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/declare-local-variable-transact-sql)  
  
  
