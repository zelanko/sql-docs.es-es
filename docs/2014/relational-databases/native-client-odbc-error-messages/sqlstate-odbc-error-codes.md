---
title: SQLSTATE (códigos de error ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 253841e26ab7ecbeafb2cfeeed8c090c91650d14
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62805869"
---
# <a name="sqlstate-odbc-error-codes"></a>SQLSTATE (códigos de error ODBC)
  SQLSTATE proporciona información detallada sobre la causa de una advertencia o error. En el caso de los errores que se producen en el origen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] detectado y devuelto por, el controlador ODBC de Native Client asigna el número de error nativo devuelto al SQLSTATE adecuado. Si un número de error nativo no tiene un código de error ODBC al que asignar, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el controlador ODBC de Native Client devuelve SQLSTATE 42000 ("error de sintaxis o infracción de acceso"). En el caso de los errores detectados por el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador, el controlador ODBC de Native Client genera el SQLSTATE adecuado.  
  
 Para obtener más información sobre los códigos de error de estado, vea los temas siguientes:  
  
-   [Apéndice A: Códigos de error de ADO](https://go.microsoft.com/fwlink/?LinkId=89356)  
  
-   [Asignaciones SQLSTATE](https://go.microsoft.com/fwlink/?LinkId=89355)  
  
## <a name="see-also"></a>Consulte también  
 [Controlar errores y mensajes](handling-errors-and-messages.md)  
  
  
