---
title: Copiando datos Text e Image de forma masiva | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- bulk copy [ODBC], text data
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [ODBC], image data
- ODBC, bulk copy operations
ms.assetid: 87155bfa-3a73-4158-9d4d-cb7435dac201
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: c674c24b4000ada4651dfb44ed2d49e9fd5bde83
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36105145"
---
# <a name="bulk-copying-text-and-image-data"></a>Copia masiva de datos de texto e imagen
  Grandes **texto**, **ntext**, y **imagen** valores son masiva copiada mediante el [bcp_moretext](../native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md) función. Codifica [bcp_bind](../native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) para el **texto**, **ntext**, o **imagen** columna con un *pData* puntero establecido en NULL indicando que los datos se proporcionarán con **bcp_moretext**. Es importante especificar la longitud exacta de los datos proporcionados para cada **texto**, **ntext**, o **imagen** columna en cada fila de una copia masiva. Si la longitud de los datos de una columna es diferente de la longitud de la columna especificada en [bcp_bind](../native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md), use [bcp_collen](../native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md) para establecer la longitud en el valor adecuado. A [bcp_sendrow](../native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md) envía todas las no -**texto**, no-**ntext**y no-**imagen** datos; a continuación, llame a **bcp_moretext** para enviar la **texto**, **ntext**, o **imagen** datos en unidades independientes. Funciones de copia masiva determinan que se han enviado todos los datos actuales **texto**, **ntext**, o **imagen** columna cuando la suma de las longitudes de datos enviados a través de **bcp_moretext** es igual a la longitud especificada en la versión más reciente **bcp_collen** o **bcp_bind**.  
  
 **bcp_moretext** no tiene ningún parámetro para identificar una columna. Si hay varios **texto**, **ntext**, o **imagen** columnas de una fila, **bcp_moretext** opera en el **texto**, **ntext**, o **imagen** columnas a partir de la columna que tiene el número ordinal más bajo y se procede a la columna con el mayor número ordinal. **bcp_moretext** va de una columna a la siguiente cuando la suma de las longitudes de los datos enviados es igual a la longitud especificada en la versión más reciente **bcp_collen** o **bcp_bind** para la columna actual.  
  
## <a name="see-also"></a>Vea también  
 [Realizar operaciones de copia masiva &#40;ODBC&#41;](performing-bulk-copy-operations-odbc.md)  
  
  