---
title: Recuperar información del conjunto de resultados (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- result sets [ODBC]
- result sets [ODBC], fetching
ms.assetid: 34f235e4-f80b-4123-8764-9deb18506f14
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a814a65419026dfb6e7901f2b49db2096c5da423
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37409645"
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
  
  
