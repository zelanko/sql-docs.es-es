---
title: SQLCancel | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQLCancel function
ms.assetid: d4c965ae-c1ac-4e9d-b4b9-32b561401106
caps.latest.revision: 5
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 6aff7aea0040e2fd7f86a3ad668b4e4438148497
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36202285"
---
# <a name="sqlcancel"></a>SQLCancel
  El [SQLCancel](http://go.microsoft.com/fwlink/?LinkId=203516) tema indica que en ODBC 2.x, si una aplicación llama `SQLCancel` cuando no se realiza ningún procesamiento en la instrucción, `SQLCancel` tiene el mismo efecto que `SQLFreeStmt` con el `SQL_CLOSE` opción; esto comportamiento se define únicamente por integridad y las aplicaciones deben llamar a `SQLFreeStmt` o `SQLCloseCursor` para cerrar los cursores. Pero aunque la aplicación [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client establezca que la versión de la API de ODBC ha de ser 3.5.x o posterior, la función `SQLCancel` utilizará el comportamiento de ODBC 2.x.  
  
## <a name="see-also"></a>Vea también  
 [SQLCancel](http://go.microsoft.com/fwlink/?LinkId=203516)   
 [Detalles de implementación de la API de ODBC](odbc-api-implementation-details.md)  
  
  