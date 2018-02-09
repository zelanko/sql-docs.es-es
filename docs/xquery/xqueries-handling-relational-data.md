---
title: Consultas XQuery controlar datos relacionales | Documentos de Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: xquery
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- relational data [XQuery]
- XQuery, relational data
ms.assetid: 9812b71a-52ec-48a0-92f3-016a93660229
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 420caf1620974293f279e72892f0da2cad6a140b
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="xqueries-handling-relational-data"></a>Funciones de XQuery para controlar datos relacionales
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Se especifica XQuery en una **xml** columna de tipo o una variable con uno de los [métodos del tipo de datos XML](../t-sql/xml/xml-data-type-methods.md). Puede tratarse de **query()**, **value()**, **exist()**, o **modify()**. La función de XQuery se ejecuta en la instancia XML identificada en la consulta que genera el XML.  
  
 EL XML generado mediante la ejecución de una XQuery puede incluir valores recuperados de otras columnas de conjunto de filas o variable de Transact-SQL. Para enlazar datos relacionales no XML con el XML resultante, SQL Server proporciona las siguientes pseudofunciones como extensiones de XQuery:  
  
-   **SQL:Column()** (función)  
  
-   **SQL:variable()** (función)  
  
 Puede usar estas extensiones de XQuery al especificar una XQuery en el **query()** método de la **xml** tipo de datos. Como resultado, el **query()** método puede generar XML que combina datos de XML y no-**xml** tipos de datos.  
  
 También puede utilizar estas funciones cuando se usa el **xml** métodos del tipo de datos **modify()**, **value()**, **query()**, y  **exist()**para exponer un valor relacional dentro de XML.  
  
 Para obtener más información, consulte [función SQL:Column() (XQuery)](../xquery/xquery-extension-functions-sql-column.md) y [:variable() (XQuery)](../xquery/xquery-extension-functions-sql-variable.md).  
  
## <a name="see-also"></a>Vea también  
 [Datos XML &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [Referencia del lenguaje XQuery &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)   
 [Construcción de XML &#40; XQuery &#41;](../xquery/xml-construction-xquery.md)  
  
  
