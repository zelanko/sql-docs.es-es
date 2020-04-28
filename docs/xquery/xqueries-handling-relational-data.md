---
title: Consultas XQuery controlar datos relacionales | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- relational data [XQuery]
- XQuery, relational data
ms.assetid: 9812b71a-52ec-48a0-92f3-016a93660229
author: rothja
ms.author: jroth
ms.openlocfilehash: ed4583b30ed1e4538a36079f9f7794704b819cda
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67946168"
---
# <a name="xqueries-handling-relational-data"></a>Funciones de XQuery para controlar datos relacionales
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Se especifica XQuery en una columna o variable de tipo **XML** mediante uno de los [métodos de tipo de datos XML](../t-sql/xml/xml-data-type-methods.md). Estos incluyen **query ()**, **Value ()**, **exist ()** o **Modify ()**. La función de XQuery se ejecuta en la instancia XML identificada en la consulta que genera el XML.  
  
 EL XML generado mediante la ejecución de una XQuery puede incluir valores recuperados de otras columnas de conjunto de filas o variable de Transact-SQL. Para enlazar datos relacionales no XML con el XML resultante, SQL Server proporciona las siguientes pseudofunciones como extensiones de XQuery:  
  
-   **SQL: column () (función)**  
  
-   **SQL: variable () (función)**  
  
 Puede utilizar estas extensiones XQuery al especificar una expresión XQuery en el método **query ()** del tipo de datos **XML** . Como resultado, el método **query ()** puede generar XML que combina datos de tipos de datos XML y no**XML** .  
  
 También puede usar estas funciones cuando utilice los métodos de **xml** tipo de datos XML **Modify ()**, **Value ()**, **query ()** y **exist ()** para exponer un valor relacional dentro de XML.  
  
 Para obtener más información, vea [SQL: column () (función de XQuery)](../xquery/xquery-extension-functions-sql-column.md) y [SQL: variable () (función de XQuery)](../xquery/xquery-extension-functions-sql-variable.md).  
  
## <a name="see-also"></a>Consulte también  
 [&#40;de datos XML SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [&#40;de referencia del lenguaje XQuery SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)   
 [Construcción XML &#40;XQuery&#41;](../xquery/xml-construction-xquery.md)  
  
  
