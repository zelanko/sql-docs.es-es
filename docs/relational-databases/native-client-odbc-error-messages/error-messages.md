---
title: Mensajes de error | Microsoft Docs
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
ms.openlocfilehash: 10308509004493ba68d23870a70bf878ae05b4a1
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/07/2019
ms.locfileid: "73783458"
---
# <a name="error-messages"></a>mensajes de error
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  El texto de los mensajes devueltos por el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client se coloca en el parámetro *MessageText* de **SQLGetDiagRec**. El encabezado del mensaje indica el origen de un error:  
  
 [Microsoft][ODBC Driver Manager]  
 El Administrador de controladores ODBC produce estos errores.  
  
 [Microsoft][ODBC Cursor Library]  
 La biblioteca de cursores ODBC produce estos errores.  
  
 [Microsoft][SQL Server Native Client]  
 Estos errores los genera el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Si no hay ningún otro nodo con el nombre de una biblioteca de red o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el error se produjo en el controlador.  
  
 Microsoft [SQL Server Native Client] [*Net-nombredetransportedered*]  
 Estos errores los genera el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] net-Library, donde *net-nombredetransportedered* es el nombre para mostrar de un transporte de red de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cliente (por ejemplo, canalizaciones con nombre, memoria compartida, Sockets TCP/IP o Via). El resto del mensaje de error contiene la función de biblioteca de red a la que se ha llamado y la función a la que se ha llamado en la API de red subyacente mediante la función TDS. El código de error *pfNative* devuelto con estos errores es el código de error de la pila del Protocolo de red subyacente.  
  
 Microsoft [SQL Server Native Client] [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]]  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] produce estos errores. El resto del mensaje de error es el texto del mensaje de error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El código *pfNative* devuelto con estos errores es el número de error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información acerca de una lista de mensajes de error (y sus números) que pueden ser devueltos por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea la descripción y las columnas de error de la tabla del sistema **sysmessages** en la base de datos **maestra** en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Controlar errores y mensajes](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
