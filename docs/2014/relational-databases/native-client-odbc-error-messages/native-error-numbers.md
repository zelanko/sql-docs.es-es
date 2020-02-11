---
title: Números de error nativos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC error handling, native error numbers
- SQL Server Native Client ODBC driver, errors
- native error numbers [SQL Server Native Client]
- messages [ODBC], native error numbers
- errors [ODBC], native error numbers
ms.assetid: 77cbc826-f47f-4803-8e7a-223d6df069b1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7e7cd24a3eb1ccdeea1b6e6cbb97e2d0f222193f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63223500"
---
# <a name="native-error-numbers"></a>Números de errores nativos
  En el caso de los errores que se producen en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]origen de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (devuelto por), el controlador ODBC de Native Client devuelve [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]el número de error nativo que devuelve. En el caso de los errores detectados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por el controlador, el controlador ODBC de Native Client devuelve un número de error nativo de 0. Para obtener más información acerca de una lista de números de error nativos, vea la columna error de la tabla del sistema **sysmessages** en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]la base de datos **maestra** de.  
  
 Para obtener información acerca de los códigos de error de estado, consulte [SQLSTATE &#40;códigos de error ODBC&#41;](sqlstate-odbc-error-codes.md). Para los errores devueltos por la Biblioteca de red, el número de error nativo es del software de red subyacente.  
  
## <a name="see-also"></a>Consulte también  
 [Controlar errores y mensajes](handling-errors-and-messages.md)  
  
  
