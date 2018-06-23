---
title: Recuperar información del conjunto de resultados (ODBC) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- result sets [ODBC]
- result sets [ODBC], fetching
ms.assetid: 34f235e4-f80b-4123-8764-9deb18506f14
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: a87f490742bc3dad279d0aeed99bf61e7b14dcef
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2018
ms.locfileid: "35700536"
---
# <a name="processing-results---retrieve-result-set-information"></a>Procesar resultados - recuperar información del conjunto de resultados
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

    
### <a name="to-get-information-about-a-result-set"></a>Para obtener información sobre un conjunto de resultados  
  
1.  Llame a [SQLNumResultCols](../../relational-databases/native-client-odbc-api/sqlnumresultcols.md) para obtener el número de columnas del conjunto de resultados.  
  
2.  Para cada columna del conjunto de resultados:  
  
    -   Llame a [SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md) para obtener información acerca de la columna de resultados.  
  
     o bien  
  
    -   Llame a [SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md) para obtener información específica del descriptor acerca de la columna de resultados.  
  
## <a name="see-also"></a>Vea también  
[Procesar resultados &#40;ODBC&#41;](../../relational-databases/native-client-odbc-how-to/processing-results-process-results.md)

[Determinar las características de un conjunto de resultados &#40;ODBC&#41;](../../relational-databases/native-client-odbc-results/determining-the-characteristics-of-a-result-set-odbc.md)  
  
  
