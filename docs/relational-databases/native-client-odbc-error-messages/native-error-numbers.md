---
title: "Números de errores nativos | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-error-messages
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- ODBC error handling, native error numbers
- SQL Server Native Client ODBC driver, errors
- native error numbers [SQL Server Native Client]
- messages [ODBC], native error numbers
- errors [ODBC], native error numbers
ms.assetid: 77cbc826-f47f-4803-8e7a-223d6df069b1
caps.latest.revision: "35"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e5ff5f12b824a53b1804e90e653ec9dd2718bb5e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="native-error-numbers"></a>Números de errores nativos
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Para los errores que se producen en el origen de datos (devuelto por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]), el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC Native Client devuelve el número de error nativo devuelto por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para los errores detectados por el controlador, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC Native Client devuelve un número de error nativo de 0. Para obtener más información acerca de una lista de números de errores nativos, vea la columna de error de la **sysmessages** tabla del sistema en el **maestro** en la base de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para obtener información sobre los códigos de error de estado, consulte [SQLSTATE &#40; códigos de Error de ODBC &#41;](../../relational-databases/native-client-odbc-error-messages/sqlstate-odbc-error-codes.md). Para los errores devueltos por la Biblioteca de red, el número de error nativo es del software de red subyacente.  
  
## <a name="see-also"></a>Vea también  
 [Controlar errores y mensajes](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
