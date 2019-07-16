---
title: Los mensajes de error | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, errors
- messages [ODBC], types
- ODBC error handling, message types
- errors [ODBC], types
ms.assetid: 46c0c22e-d105-4d5b-bb9d-5694472e8651
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d6d41ee2d59e30c2e892f442f680930e535ccba1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68062349"
---
# <a name="error-messages"></a>mensajes de error
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  El texto de los mensajes devueltos por la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client se coloca en el *MessageText* parámetro de **SQLGetDiagRec**. El encabezado del mensaje indica el origen de un error:  
  
 [Microsoft][ODBC Driver Manager]  
 El Administrador de controladores ODBC produce estos errores.  
  
 [Microsoft][ODBC Cursor Library]  
 La biblioteca de cursores ODBC produce estos errores.  
  
 [Microsoft][SQL Server Native Client]  
 Estos errores se producen por la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client. Si no hay ningún otro nodo con el nombre de una biblioteca de red o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el error se produjo en el controlador.  
  
 [Microsoft] [SQL Server Native Client] [*Nombredetransportedered*]  
 Estos errores se producen por la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Net-Library, donde *Nombredetransportedered* es el nombre para mostrar de un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] transporte de red de cliente (por ejemplo, canalizaciones con nombre, memoria compartida, Sockets de TCP/IP o VIA). El resto del mensaje de error contiene la función de biblioteca de red a la que se ha llamado y la función a la que se ha llamado en la API de red subyacente mediante la función TDS. El *pfNative* código de error devuelto con estos errores es el código de error de la pila de protocolo de red subyacente.  
  
 [Microsoft] [SQL Server Native Client] [ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]]  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] produce estos errores. El resto del mensaje de error es el texto del mensaje de error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El *pfNative* código devuelto con estos errores es el número de error [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información acerca de una lista de los mensajes de error (y sus números) que puede devolver [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte las columnas de error y la descripción de la **sysmessages** tabla del sistema en el **maestro** en la base de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Controlar errores y mensajes](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
