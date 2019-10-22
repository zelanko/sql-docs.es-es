---
title: MSSQLSERVER_137 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 137 (Database Engine error)
ms.assetid: 47fb4212-2165-4fec-bc41-6d548465d7be
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4e780d6afaddc5ac3af0e87e6b629fb39c987879
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/14/2019
ms.locfileid: "72305033"
---
# <a name="mssqlserver_137"></a>MSSQLSERVER_137
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
Este error se produce cuando una variable se utiliza en un script SQL sin declararla primero. En el ejemplo siguiente se devuelve el error 137 para las instrucciones SET y SELECT porque no se ha declarado **\@mycol**.  
  
SET @mycol = 'ContactName'  
  
SELECT @mycol  
  
Una de las causas más complicadas de este error incluye el uso de una variable que se declara fuera de la instrucción EXECUTE. Por ejemplo, la variable **\@mycol** especificada en la instrucción SELECT es local en la instrucción SELECT; por tanto, está fuera de la instrucción EXECUTE.  
  
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
[EXECUTE &#40;Transact-SQL&#41;](~/t-sql/language-elements/execute-transact-sql.md)  
[Instrucciones SET &#40;Transact-SQL&#41;](~/t-sql/statements/set-statements-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](~/t-sql/language-elements/declare-local-variable-transact-sql.md)  
  
