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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3017f74b12eb18624f8a34e8a1289da18b70c93a
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82712693"
---
# <a name="retrieve-result-set-information-odbc"></a>Recuperar información del conjunto de resultados (ODBC)
    
### <a name="to-get-information-about-a-result-set"></a>Para obtener información sobre un conjunto de resultados  
  
1.  Llame a [SQLNumResultCols](../native-client-odbc-api/sqlnumresultcols.md) para obtener el número de columnas del conjunto de resultados.  
  
2.  Para cada columna del conjunto de resultados:  
  
    -   Llame a [SQLDescribeCol](../native-client-odbc-api/sqldescribecol.md) para obtener información sobre la columna de resultados.  
  
     O bien  
  
    -   Llame a [SQLColAttribute](../native-client-odbc-api/sqlcolattribute.md) para obtener información específica del descriptor sobre la columna de resultados.  
  
## <a name="see-also"></a>Consulte también  
 [Temas de procedimientos de procesamiento de resultados &#40;ODBC&#41;](../../database-engine/dev-guide/processing-results-how-to-topics-odbc.md)   
 [Determinar las características de un conjunto de resultados &#40;ODBC&#41;](../native-client-odbc-results/determining-the-characteristics-of-a-result-set-odbc.md)  
  
  
