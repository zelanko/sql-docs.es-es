---
title: Copiando datos Text e Image de forma masiva | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-bulk-copy-operations
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
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
ms.openlocfilehash: f647e9dae0a54bfb35ff9b0868891e74cfd7d125
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37416714"
---
# <a name="bulk-copying-text-and-image-data"></a>Copia masiva de datos de texto e imagen
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Grandes **texto**, **ntext**, y **imagen** los valores son masiva copiado mediante el [bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md) función. El código [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) para el **texto**, **ntext**, o **imagen** columna con un *pData* puntero establecido en NULL indicando que le proporcionará los datos **bcp_moretext**. Es importante especificar la longitud exacta de los datos proporcionados para cada **texto**, **ntext**, o **imagen** columna en cada fila de la copia masiva. Si la longitud de los datos de una columna es diferente de la longitud de la columna especificada en [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md), utilice [bcp_collen](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md) para establecer la longitud en el valor apropiado. Un [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md) envía todos los que no sean de**texto**, no-**ntext**y no-**imagen** datos; a continuación, llame a **bcp_moretext** para enviar el **texto**, **ntext**, o **imagen** datos en unidades independientes. Funciones de copia masiva determinan que se han enviado todos los datos para el actual **texto**, **ntext**, o **imagen** columna cuando la suma de las longitudes de datos se envía a través de **bcp_moretext** es igual a la longitud especificada en la versión más reciente **bcp_collen** o **bcp_bind**.  
  
 **bcp_moretext** no tiene ningún parámetro para identificar una columna. Si hay varios **texto**, **ntext**, o **imagen** columnas de una fila, **bcp_moretext** opera en el **texto**, **ntext**, o **imagen** columnas a partir de la columna tiene el número ordinal más bajo y continuando hasta la columna con el mayor número ordinal. **bcp_moretext** va de una columna a la siguiente cuando la suma de las longitudes de los datos enviados es igual a la longitud especificada en la versión más reciente **bcp_collen** o **bcp_bind** para la columna actual.  
  
## <a name="see-also"></a>Vea también  
 [Realizar operaciones de copia masiva &#40;ODBC&#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
  
