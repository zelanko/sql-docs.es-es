---
title: Desconectarse de un origen de datos | Documentos de Microsoft
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-odbc-communication
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ODBC data sources, connections
- data sources [SQL Server Native Client]
- disconnecting [ODBC]
- ODBC applications, disconnecting
- SQLDisconnect function
- ODBC applications, data sources
- connections [SQL Server Native Client]
- SQLFreeHandle function
- ODBC data sources, disconnecting
- SQL Server Native Client ODBC driver, data sources
- ODBC functions
- SQL Server Native Client ODBC driver, connections
ms.assetid: 65b0267d-b2ab-4a59-83f2-436d90cfbf79
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 1b511f9e5435658d470c1e97a2ef71e97bb80ec2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="disconnecting-from-a-data-source"></a>Desconectarse de un origen de datos
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Cuando una aplicación ha terminado de usar un origen de datos, se llama a **SQLDisconnect**. **SQLDisconnect** libera las instrucciones que se asignan en la conexión y desconecta el controlador del origen de datos. Después de desconectarse, la aplicación puede llamar a [SQLFreeHandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md) para liberar el identificador de conexión. Antes de salir, una aplicación llama también **SQLFreeHandle** para liberar el identificador de entorno.  
  
 Después de desconectarse, una aplicación puede reutilizar el identificador de conexión asignado, conectarse a un origen de datos diferente o volver a conectarse al mismo origen de datos. La decisión de seguir conectado en lugar de desconectarse y volver a conectarse después requiere que el sistema de escritura de la aplicación considere los costes relativos de cada opción. Conectarse a un origen de datos y seguir conectado puede ser relativamente costoso, dependiendo del medio de conexión. Para realizar un intercambio, la aplicación debe hacer también suposiciones sobre la probabilidad y el control de tiempo de operaciones adicionales en el mismo origen de datos. Puede que una aplicación tenga que utilizar además más de una conexión.  
  
## <a name="see-also"></a>Vea también  
 [Comunicar con SQL Server &#40;ODBC&#41;](../../relational-databases/native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
  
