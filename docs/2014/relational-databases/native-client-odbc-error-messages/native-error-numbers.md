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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b9612fbd7dd50ffeec812532e25a63eecca26571
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82705362"
---
# <a name="native-error-numbers"></a>Números de errores nativos
  En el caso de los errores que se producen en el origen de datos (devuelto por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ), el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client devuelve el número de error nativo que devuelve [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . En el caso de los errores detectados por el controlador, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client devuelve un número de error nativo de 0. Para obtener más información acerca de una lista de números de error nativos, vea la columna error de la tabla del sistema **sysmessages** en la base de datos **maestra** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Para obtener información acerca de los códigos de error de estado, consulte [SQLSTATE &#40;códigos de error ODBC&#41;](sqlstate-odbc-error-codes.md). Para los errores devueltos por la Biblioteca de red, el número de error nativo es del software de red subyacente.  
  
## <a name="see-also"></a>Consulte también  
 [Controlar errores y mensajes](handling-errors-and-messages.md)  
  
  
