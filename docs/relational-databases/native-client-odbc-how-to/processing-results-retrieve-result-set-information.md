---
title: Recuperar información del conjunto de resultados (ODBC) Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- result sets [ODBC]
- result sets [ODBC], fetching
ms.assetid: 34f235e4-f80b-4123-8764-9deb18506f14
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f1c65841db0fdfd386891cfbd03bdee483ce25f6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300395"
---
# <a name="processing-results---retrieve-result-set-information"></a>Procesar resultados: recuperar información del conjunto de resultados
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

    
### <a name="to-get-information-about-a-result-set"></a>Para obtener información sobre un conjunto de resultados  
  
1.  Llame a [SQLNumResultCols](../../relational-databases/native-client-odbc-api/sqlnumresultcols.md) para obtener el número de columnas del conjunto de resultados.  
  
2.  Para cada columna del conjunto de resultados:  
  
    -   Llame a [SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md) para obtener información sobre la columna de resultados.  
  
     Or  
  
    -   Llame a [SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md) para obtener información de descriptor específica sobre la columna de resultados.  
  
## <a name="see-also"></a>Consulte también  
[Resultados del proceso &#40;&#41;ODBC](../../relational-databases/native-client-odbc-how-to/processing-results-process-results.md)

[Determinar las características de un conjunto de resultados &#40;&#41;ODBC](../../relational-databases/native-client-odbc-results/determining-the-characteristics-of-a-result-set-odbc.md)  
  
  
