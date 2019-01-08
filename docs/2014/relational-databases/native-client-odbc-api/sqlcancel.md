---
title: SQLCancel | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLCancel function
ms.assetid: d4c965ae-c1ac-4e9d-b4b9-32b561401106
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8bad2cc35a30f5c6f5855292ff73635cef6072b2
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/13/2018
ms.locfileid: "53364267"
---
# <a name="sqlcancel"></a>SQLCancel
  El [SQLCancel](https://go.microsoft.com/fwlink/?LinkId=203516) tema dice que en ODBC 2.x, si una aplicación llama a `SQLCancel` cuando no se realiza ningún procesamiento en la instrucción, `SQLCancel` tiene el mismo efecto que `SQLFreeStmt` con el `SQL_CLOSE` opción; esto comportamiento se define únicamente por integridad y las aplicaciones deben llamar a `SQLFreeStmt` o `SQLCloseCursor` para cerrar los cursores. Pero aunque la aplicación [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client establezca que la versión de la API de ODBC ha de ser 3.5.x o posterior, la función `SQLCancel` utilizará el comportamiento de ODBC 2.x.  
  
## <a name="see-also"></a>Vea también  
 [SQLCancel](https://go.microsoft.com/fwlink/?LinkId=203516)   
 [Detalles de implementación de la API de ODBC](odbc-api-implementation-details.md)  
  
  
