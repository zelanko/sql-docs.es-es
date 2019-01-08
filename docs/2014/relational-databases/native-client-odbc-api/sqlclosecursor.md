---
title: SQLCloseCursor | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLCloseCursor function
ms.assetid: e7134d65-5c1c-4ae2-b119-d9b4b9a42483
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: da7d6541f7bf31920519cc7462bdfd24a5f6dc0d
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/13/2018
ms.locfileid: "53360637"
---
# <a name="sqlclosecursor"></a>SQLCloseCursor
  **SQLCloseCursor** reemplaza [SQLFreeStmt](sqlfreestmt.md) con un *opción* valor de SQL_CLOSE. En el recibo de **SQLCloseCursor**, el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client descarta las filas del conjunto de resultados pendientes. Observe que los enlaces de parámetro y columna de la instrucción (si existen) quedan inalterados por **SQLCloseCursor**.  
  
## <a name="see-also"></a>Vea también  
 [SQLCloseCursor](https://go.microsoft.com/fwlink/?LinkId=59331)   
 [Detalles de implementación de la API de ODBC](odbc-api-implementation-details.md)  
  
  
