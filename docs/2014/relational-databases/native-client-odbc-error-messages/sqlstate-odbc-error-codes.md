---
title: SQLSTATE (códigos de Error ODBC) | Documentos de Microsoft
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
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/13/2018
ms.locfileid: "53350090"
---
# <a name="sqlstate-odbc-error-codes"></a>SQLSTATE (códigos de error ODBC)
  SQLSTATE proporciona información detallada sobre la causa de una advertencia o error. Errores que se producen en los datos de origen que detecta y devuelve [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client asigna el número de error nativo devuelto al SQLSTATE correspondiente. Si un número de error nativo no tiene un código de error ODBC para asignar a, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client devuelve SQLSTATE 42000 ("sintaxis o infracción de acceso"). Para los errores detectados por el controlador, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client genera el SQLSTATE correspondiente.  
  
 Para obtener más información sobre los códigos de error de estado, vea los temas siguientes:  
  
-   [Apéndice A: Códigos de Error ODBC](https://go.microsoft.com/fwlink/?LinkId=89356)  
  
-   [Asignaciones SQLSTATE](https://go.microsoft.com/fwlink/?LinkId=89355)  
  
## <a name="see-also"></a>Vea también  
 [Controlar errores y mensajes](handling-errors-and-messages.md)  
  
  
