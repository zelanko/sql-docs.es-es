---
title: Copia masiva de datos de texto e imagen | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- bulk copy [ODBC], text data
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [ODBC], image data
- ODBC, bulk copy operations
ms.assetid: 87155bfa-3a73-4158-9d4d-cb7435dac201
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 593f0b17ead284940d6f22b5983d284ddd37d7d4
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85760719"
---
# <a name="bulk-copying-text-and-image-data"></a>Copia masiva de datos de texto e imagen
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  Los valores **Text**, **ntext**e **Image** grandes se copian de forma masiva mediante la función [bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md) . Codifique [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) para la columna **Text**, **ntext**o **Image** con un puntero *pdata* establecido en NULL que indica que los datos se proporcionarán con **bcp_moretext**. Es importante especificar la longitud exacta de los datos proporcionados para cada columna **Text**, **ntext**o **Image** en cada fila copiada de forma masiva. Si la longitud de los datos de una columna es diferente de la especificada en [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md), use [bcp_collen](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md) para establecer la longitud en el valor adecuado. Un [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md) envía todos los datos que no son de**texto**, no**ntext**ni de**imagen** ; a continuación, llame a **bcp_moretext** para enviar los datos **Text**, **ntext**o **Image** en unidades independientes. Las funciones de copia masiva determinan que se han enviado todos los datos para la columna **Text**, **ntext**o **Image** actual cuando la suma de las longitudes de los datos enviados a través de **bcp_moretext** es igual a la longitud especificada en el **bcp_collen** o **bcp_bind**más reciente.  
  
 **bcp_moretext** no tiene ningún parámetro para identificar una columna. Cuando hay varias columnas **Text**, **ntext**o **image** en una fila, **bcp_moretext** funciona en las columnas **Text**, **ntext**o **Image** a partir de la columna que tiene el número ordinal más bajo y continúa con la columna con el número ordinal más alto. **bcp_moretext** va de una columna a la siguiente cuando la suma de las longitudes de los datos enviados es igual a la longitud especificada en el **bcp_collen** o **bcp_bind** más reciente de la columna actual.  
  
## <a name="see-also"></a>Consulte también  
 [Realizar operaciones de copia masiva &#40;ODBC&#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
  
