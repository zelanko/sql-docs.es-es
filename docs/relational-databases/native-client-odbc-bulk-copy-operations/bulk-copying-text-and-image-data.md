---
title: Copiando datos Text e Image de forma masiva | Documentos de Microsoft
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-bulk-copy-operations
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- bulk copy [ODBC], text data
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [ODBC], image data
- ODBC, bulk copy operations
ms.assetid: 87155bfa-3a73-4158-9d4d-cb7435dac201
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 5a8c6a70a4d1682117fff68cefe38f5d40a1e5d3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="bulk-copying-text-and-image-data"></a>Copia masiva de datos de texto e imagen
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Grandes **texto**, **ntext**, y **imagen** valores son masiva copiada mediante el [bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md) función. Codifica [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) para el **texto**, **ntext**, o **imagen** columna con un *pData* puntero establecido en NULL indicando que los datos se proporcionarán con **bcp_moretext**. Es importante especificar la longitud exacta de los datos proporcionados para cada **texto**, **ntext**, o **imagen** columna en cada fila de una copia masiva. Si la longitud de los datos de una columna es diferente de la longitud de la columna especificada en [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md), use [bcp_collen](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md) para establecer la longitud en el valor adecuado. A [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md) envía todas las no -**texto**, no-**ntext**y no-**imagen** datos; a continuación, llame a **bcp_moretext** para enviar la **texto**, **ntext**, o **imagen** datos en unidades independientes. Funciones de copia masiva determinan que se han enviado todos los datos actuales **texto**, **ntext**, o **imagen** columna cuando la suma de las longitudes de datos enviados a través de **bcp_moretext** es igual a la longitud especificada en la versión más reciente **bcp_collen** o **bcp_bind**.  
  
 **bcp_moretext** no tiene ningún parámetro para identificar una columna. Si hay varios **texto**, **ntext**, o **imagen** columnas de una fila, **bcp_moretext** opera en el **texto**, **ntext**, o **imagen** columnas a partir de la columna que tiene el número ordinal más bajo y se procede a la columna con el mayor número ordinal. **bcp_moretext** va de una columna a la siguiente cuando la suma de las longitudes de los datos enviados es igual a la longitud especificada en la versión más reciente **bcp_collen** o **bcp_bind** para la columna actual.  
  
## <a name="see-also"></a>Vea también  
 [Realizar operaciones de copia masiva &#40;ODBC&#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
  
