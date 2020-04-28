---
title: Números de error nativos | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0b5572ee784f47b0444e1d825de1b6dd53db8066
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81291615"
---
# <a name="native-error-numbers"></a>Números de errores nativos
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  En el caso de los errores que se producen en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]origen de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (devuelto por), el controlador ODBC de Native Client devuelve [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]el número de error nativo que devuelve. En el caso de los errores detectados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por el controlador, el controlador ODBC de Native Client devuelve un número de error nativo de 0. Para obtener más información acerca de una lista de números de error nativos, vea la columna error de la tabla del sistema **sysmessages** en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]la base de datos **maestra** de.  
  
 Para obtener información acerca de los códigos de error de estado, consulte [SQLSTATE &#40;códigos de error ODBC&#41;](../../relational-databases/native-client-odbc-error-messages/sqlstate-odbc-error-codes.md). Para los errores devueltos por la Biblioteca de red, el número de error nativo es del software de red subyacente.  
  
## <a name="see-also"></a>Consulte también  
 [Controlar errores y mensajes](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
