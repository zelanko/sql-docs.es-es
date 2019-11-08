---
title: Cursores de solo avance rápido (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- fast forward-only cursors
- forward-only cursors
- cursors [ODBC], fast forward-only
- ODBC cursors, fast forward-only
ms.assetid: 0707d07e-fc95-42ed-9280-b7e508ac8c62
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8d61ef2d8b3f4efa29bdf5fffa653c210207f25c
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/07/2019
ms.locfileid: "73784500"
---
# <a name="fast-forward-only-cursors-odbc"></a>Cursores de solo avance rápido (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Cuando se conecta a una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], el controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client admite optimizaciones de rendimiento para cursores de solo avance y de solo lectura. Los cursores de solo avance rápido se implementan internamente mediante el controlador y el servidor de un modo muy similar a los conjuntos de resultados predeterminados. Además de presentar un alto rendimiento, los cursores de solo avance rápido también presentan estas características:  
  
-   No se admite [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) . Las columnas del conjunto de resultados deben estar enlazadas a variables de programa.  
  
-   El servidor cierra automáticamente el cursor cuando se detecta el final del cursor. La aplicación debe seguir llamando a [SQLCloseCursor](../../../relational-databases/native-client-odbc-api/sqlclosecursor.md) o [SQLFreeStmt](../../../relational-databases/native-client-odbc-api/sqlfreestmt.md)(SQL_CLOSE), pero el controlador no tiene que enviar la solicitud de cierre al servidor. De esta forma, se ahorra un viaje de ida y vuelta (round trip) de la red al servidor.  
  
 La aplicación solicita cursores de solo avance rápido mediante el atributo de instrucciones específico del controlador SQL_SOPT_SS_CURSOR_OPTIONS. Cuando se establece en SQL_CO_FFO, los cursores de solo avance rápido se habilitan sin captura automática. Cuando se establece en SQL_CO_FFO_AF, también se habilita la opción de captura automática. Para obtener más información sobre la captura automática, vea [usar la captura automática con cursores ODBC](../../../relational-databases/native-client-odbc-cursors/programming/using-autofetch-with-odbc-cursors.md).  
  
 Los cursores de solo avance rápido con captura automática pueden usarse para recuperar un pequeño conjunto de resultados con solo un viaje de ida y vuelta (round trip) al servidor. En estos pasos, *n* es el número de filas que se devolverán:  
  
1.  Establezca SQL_SOPT_SS_CURSOR_OPTIONS en SQL_CO_FFO_AF.  
  
2.  Establezca SQL_ATTR_ROW_ARRAY_SIZE en *n* + 1.  
  
3.  Enlazar las columnas de resultados a matrices de *n* + 1 elementos (para que sea seguro si se capturan *n* + 1 filas realmente).  
  
4.  Abra el cursor con **SQLExecDirect** o **SQLExecute**.  
  
5.  Si el estado de retorno es SQL_SUCCESS, llame a **SQLFreeStmt** o **SQLCloseCursor** para cerrar el cursor. Todos los datos de las filas estarán en las variables de programa enlazadas.  
  
 Con estos pasos, **SQLExecDirect** o **SQLExecute** envía una solicitud de cursor Open con la opción de captura automática habilitada. En esa única solicitud del cliente, el servidor:  
  
-   Abre el cursor.  
  
-   Genera el conjunto de resultados y envía las filas al cliente.  
  
-   Dado que el tamaño del conjunto de filas se estableció en 1 más el número de filas del conjunto de resultados, el servidor detecta el final del cursor y cierra el cursor.  
  
## <a name="see-also"></a>Vea también  
 [Detalles &#40;de programación de cursores ODBC&#41;](../../../relational-databases/native-client-odbc-cursors/programming/cursor-programming-details-odbc.md)  
  
  
