---
title: Efectos de las opciones ISO | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ISO options (ODBC)
- ODBC applications, ISO options
- ODBC applications, statements
- SQL Server Native Client ODBC driver, ISO options
- statements [ODBC], ISO options
ms.assetid: 813f1397-fa0b-45ec-a718-e13fe2fb88ac
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 00b05935b12c52ef655fc2587c8b016c2434f25f
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43058738"
---
# <a name="effects-of-iso-options"></a>Efectos de las opciones ISO
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  La norma ODBC está estrechamente relacionada con la norma ISO, y las aplicaciones ODBC esperan de los controladores ODBC un comportamiento estándar. Para que su comportamiento se ajuste más estrechamente con que se define en el estándar ODBC, el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client utiliza siempre las opciones ISO disponibles en la versión de SQL Server con la que se conecta.  
  
 Cuando el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client se conecta a una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], el servidor detecta que el cliente está utilizando el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client y activa varias opciones.  
  
 El propio controlador emite estas instrucciones; la aplicación ODBC no hace nada para solicitarlas. Cuando se establecen estas opciones, las aplicaciones ODBC que usan el controlador pueden ser más portables porque el comportamiento del servidor se ajusta a la norma ISO.  
  
 Las aplicaciones basadas en DB-Library no suelen activar estas opciones. Observar diferentes sitios de comportamiento entre los clientes ODBC o DB-Library al ejecutar la misma instrucción SQL esto no debería suponer apunta a un problema con el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client. Debe primero volver a ejecutar la instrucción en el entorno de DB-Library con las mismas opciones SET que utilizaría el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client.  
  
 Puesto que los usuarios y las aplicaciones pueden activar y desactivar las opciones SET en cualquier momento, los programadores de procedimientos almacenados y desencadenadores también deben tomar la precaución de probar sus procedimientos y desencadenadores con las opciones SET anteriormente indicadas tanto activadas como desactivadas. De esta forma se garantiza que los procedimientos y los desencadenadores funcionan correctamente, independientemente de las opciones que pueda tener configuradas una conexión concreta al llamar al procedimiento o el desencadenador. Los desencadenadores o procedimientos almacenados que requieren un valor determinado para una de estas opciones deben emitir una instrucción SET al comienzo del desencadenador o procedimiento almacenado. Esta instrucción SET solo permanece vigente durante la ejecución del desencadenador o del procedimiento almacenado; cuando se complete la acción del procedimiento o del desencadenador, se restablecerá la configuración original.  
  
 Al conectar a una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], también se activa una cuarta opción SET, CONCAT_NULL_YIELDS_NULL. El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client no establece estas opciones si AnsiNPW = NO se especifica en el origen de datos o en [SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md) o [SQLBrowseConnect](../../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md).  
  
 Al igual que las opciones ISO mencionadas anteriormente, el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client no activa la opción QUOTED_IDENTIFIER si QuotedID = NO se especifica en el origen de datos o en **SQLDriverConnect** o  **SQLBrowseConnect**.  
  
 Para que al controlador pueda conocer el estado actual de las opciones SET, las aplicaciones ODBC no deben utilizar la instrucción SET de [!INCLUDE[tsql](../../../includes/tsql-md.md)] para establecer estas opciones. Solo deben establecerlas usando el origen de datos o las opciones de conexión. Si la aplicación emite instrucciones SET, el controlador puede generar instrucciones SQL incorrectas.  
  
## <a name="see-also"></a>Vea también  
 [Ejecución de instrucciones &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)   
 [SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md)   
 [SQLBrowseConnect](../../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md)  
  
  
