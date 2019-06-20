---
title: Recuperar información del conjunto de resultados (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- result sets [ODBC]
- result sets [ODBC], fetching
ms.assetid: 34f235e4-f80b-4123-8764-9deb18506f14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a39a6715a9ba8ab08d846aabb96e5b0665a2aa43
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63200296"
---
# <a name="retrieve-result-set-information-odbc"></a>Recuperar información del conjunto de resultados (ODBC)
    
### <a name="to-get-information-about-a-result-set"></a>Para obtener información sobre un conjunto de resultados  
  
1.  Llame a [SQLNumResultCols](../native-client-odbc-api/sqlnumresultcols.md) para obtener el número de columnas del conjunto de resultados.  
  
2.  Para cada columna del conjunto de resultados:  
  
    -   Llame a [SQLDescribeCol](../native-client-odbc-api/sqldescribecol.md) para obtener información acerca de la columna de resultados.  
  
     o bien  
  
    -   Llame a [SQLColAttribute](../native-client-odbc-api/sqlcolattribute.md) para obtener información específica de descriptor acerca de la columna de resultados.  
  
## <a name="see-also"></a>Vea también  
 [Temas de procedimientos de los resultados de procesamiento &#40;ODBC&#41;](../../database-engine/dev-guide/processing-results-how-to-topics-odbc.md)   
 [Determinar las características de un conjunto de resultados &#40;ODBC&#41;](../native-client-odbc-results/determining-the-characteristics-of-a-result-set-odbc.md)  
  
  
