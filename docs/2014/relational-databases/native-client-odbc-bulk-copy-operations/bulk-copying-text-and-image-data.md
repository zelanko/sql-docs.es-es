---
title: Copia masiva de datos de texto e imagen | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- bulk copy [ODBC], text data
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [ODBC], image data
- ODBC, bulk copy operations
ms.assetid: 87155bfa-3a73-4158-9d4d-cb7435dac201
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 03d77ce1a4526cee78431def0251329111433aac
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82705826"
---
# <a name="bulk-copying-text-and-image-data"></a>Copia masiva de datos de texto e imagen
  Los valores **Text**, **ntext**e **Image** grandes se copian de forma masiva mediante la función [bcp_moretext](../native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md) . Codifique [bcp_bind](../native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) para la columna **Text**, **ntext**o **Image** con un puntero *pdata* establecido en NULL que indica que los datos se proporcionarán con **bcp_moretext**. Es importante especificar la longitud exacta de los datos proporcionados para cada columna **Text**, **ntext**o **Image** en cada fila copiada de forma masiva. Si la longitud de los datos de una columna es diferente de la especificada en [bcp_bind](../native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md), use [bcp_collen](../native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md) para establecer la longitud en el valor adecuado. Un [bcp_sendrow](../native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md) envía todos los datos que no son de**texto**, no**ntext**ni de**imagen** ; a continuación, llame a **bcp_moretext** para enviar los datos **Text**, **ntext**o **Image** en unidades independientes. Las funciones de copia masiva determinan que se han enviado todos los datos para la columna **Text**, **ntext**o **Image** actual cuando la suma de las longitudes de los datos enviados a través de **bcp_moretext** es igual a la longitud especificada en el **bcp_collen** o **bcp_bind**más reciente.  
  
 **bcp_moretext** no tiene ningún parámetro para identificar una columna. Cuando hay varias columnas **Text**, **ntext**o **image** en una fila, **bcp_moretext** funciona en las columnas **Text**, **ntext**o **Image** a partir de la columna que tiene el número ordinal más bajo y continúa con la columna con el número ordinal más alto. **bcp_moretext** va de una columna a la siguiente cuando la suma de las longitudes de los datos enviados es igual a la longitud especificada en el **bcp_collen** o **bcp_bind** más reciente de la columna actual.  
  
## <a name="see-also"></a>Consulte también  
 [Realizar operaciones de copia masiva &#40;ODBC&#41;](performing-bulk-copy-operations-odbc.md)  
  
  
