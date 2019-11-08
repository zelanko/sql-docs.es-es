---
title: SQLSTATE (códigos de error ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, errors
- ODBC error handling, cause information
- messages [ODBC], cause information
- SQLSTATEs
- errors [ODBC], cause information
ms.assetid: 84cce528-edb0-473f-a85f-3eb87fbe2cf3
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 162f6ff15a95c1839ef59b10c659935b687aeb59
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/07/2019
ms.locfileid: "73783211"
---
# <a name="sqlstate-odbc-error-codes"></a>SQLSTATE (códigos de error ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  SQLSTATE proporciona información detallada sobre la causa de una advertencia o error. En el caso de los errores que se producen en el origen de datos detectado y devuelto por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client asigna el número de error nativo devuelto al SQLSTATE adecuado. Si un número de error nativo no tiene un código de error ODBC al que asignar, el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client devuelve SQLSTATE 42000 ("error de sintaxis o infracción de acceso"). En el caso de los errores detectados por el controlador, el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client genera el SQLSTATE adecuado.  
  
 Para obtener más información sobre los códigos de error de estado, vea los temas siguientes:  
  
-   [Apéndice A: Códigos de error ODBC ](https://go.microsoft.com/fwlink/?LinkId=89356)  
  
-   [Asignaciones SQLSTATE](https://go.microsoft.com/fwlink/?LinkId=89355)  
  
## <a name="see-also"></a>Vea también  
 [Controlar errores y mensajes](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
