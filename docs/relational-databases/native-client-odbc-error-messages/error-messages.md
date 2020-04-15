---
title: Mensajes de error ? Microsoft Docs
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7d632d1d22cd8439a3d787e22301ec06ec4e0d93
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81291795"
---
# <a name="error-messages"></a>mensajes de error
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  El texto de los [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mensajes devueltos por el controlador ODBC de Native Client se coloca en el parámetro *MessageText* de **SQLGetDiagRec**. El encabezado del mensaje indica el origen de un error:  
  
 [Microsoft][ODBC Driver Manager]  
 El Administrador de controladores ODBC produce estos errores.  
  
 [Microsoft][ODBC Cursor Library]  
 La biblioteca de cursores ODBC produce estos errores.  
  
 [Microsoft][SQL Server Native Client]  
 Estos errores se generan [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante el controlador ODBC de Native Client. Si no hay ningún otro nodo con el nombre de una biblioteca de red o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el error se produjo en el controlador.  
  
 [Microsoft] [SQL Server Native Client] [*Net-Transportname*]  
 Estos errores se generan [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante la biblioteca de red, donde *Net-Transportname* es el nombre para mostrar de un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] transporte de red cliente (por ejemplo, canalizaciones con nombre, memoria compartida, sockets TCP/IP o VIA). El resto del mensaje de error contiene la función de biblioteca de red a la que se ha llamado y la función a la que se ha llamado en la API de red subyacente mediante la función TDS. El código de error *pfNative* devuelto con estos errores es el código de error de la pila de protocolos de red subyacente.  
  
 [Microsoft] [SQL Server Native Client] [ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]]  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] produce estos errores. El resto del mensaje de error es el texto del mensaje de error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El código *pfNative* devuelto con estos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]errores es el número de error de . Para obtener más información acerca de una lista de mensajes [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]de error (y sus números) que puede devolver [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea las columnas de descripción y error de la tabla del sistema **sysmessages** en la base de datos **maestra** en .  
  
## <a name="see-also"></a>Consulte también  
 [Controlar errores y mensajes](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
