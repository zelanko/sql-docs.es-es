---
title: Números de errores nativos | Documentos de Microsoft
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
- ODBC error handling, native error numbers
- SQL Server Native Client ODBC driver, errors
- native error numbers [SQL Server Native Client]
- messages [ODBC], native error numbers
- errors [ODBC], native error numbers
ms.assetid: 77cbc826-f47f-4803-8e7a-223d6df069b1
caps.latest.revision: 34
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: faee9067ccf8f60a4b7dade849a0a987b5c07bd0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36196675"
---
# <a name="native-error-numbers"></a>Números de errores nativos
  Para los errores que se producen en el origen de datos (devuelto por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]), el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC Native Client devuelve el número de error nativo devuelto por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para los errores detectados por el controlador, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC Native Client devuelve un número de error nativo de 0. Para obtener más información acerca de una lista de números de errores nativos, vea la columna de error de la **sysmessages** tabla del sistema en el **maestro** en la base de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para obtener información sobre los códigos de error de estado, consulte [SQLSTATE &#40;códigos de Error de ODBC&#41;](sqlstate-odbc-error-codes.md). Para los errores devueltos por la Biblioteca de red, el número de error nativo es del software de red subyacente.  
  
## <a name="see-also"></a>Vea también  
 [Controlar errores y mensajes](handling-errors-and-messages.md)  
  
  