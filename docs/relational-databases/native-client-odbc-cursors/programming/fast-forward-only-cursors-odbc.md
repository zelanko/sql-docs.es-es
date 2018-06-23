---
title: Cursores de solo avance rápido (ODBC) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- fast forward-only cursors
- forward-only cursors
- cursors [ODBC], fast forward-only
- ODBC cursors, fast forward-only
ms.assetid: 0707d07e-fc95-42ed-9280-b7e508ac8c62
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 20b721adca163021f87c490cc7c8bc8b42e53da0
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2018
ms.locfileid: "35703726"
---
# <a name="fast-forward-only-cursors-odbc"></a>Cursores de solo avance rápido (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Cuando se conecta a una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC Native Client admite optimizaciones de rendimiento para los cursores de solo avance y solo lectura. Los cursores de solo avance rápido se implementan internamente mediante el controlador y el servidor de un modo muy similar a los conjuntos de resultados predeterminados. Además de presentar un alto rendimiento, los cursores de solo avance rápido también presentan estas características:  
  
-   [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) no se admite. Las columnas del conjunto de resultados deben estar enlazadas a variables de programa.  
  
-   El servidor cierra automáticamente el cursor cuando se detecta el final del cursor. La aplicación debe seguir llamando a [SQLCloseCursor](../../../relational-databases/native-client-odbc-api/sqlclosecursor.md) o [SQLFreeStmt](../../../relational-databases/native-client-odbc-api/sqlfreestmt.md)(SQL_CLOSE), pero el controlador no tiene que enviar la solicitud de cierre al servidor. De esta forma, se ahorra un viaje de ida y vuelta (round trip) de la red al servidor.  
  
 La aplicación solicita cursores de solo avance rápido mediante el atributo de instrucciones específico del controlador SQL_SOPT_SS_CURSOR_OPTIONS. Cuando se establece en SQL_CO_FFO, los cursores de solo avance rápido se habilitan sin captura automática. Cuando se establece en SQL_CO_FFO_AF, también se habilita la opción de captura automática. Para obtener más información acerca de la captura automática, consulte [utilizar la captura automática con cursores ODBC](../../../relational-databases/native-client-odbc-cursors/programming/using-autofetch-with-odbc-cursors.md).  
  
 Los cursores de solo avance rápido con captura automática pueden usarse para recuperar un pequeño conjunto de resultados con solo un viaje de ida y vuelta (round trip) al servidor. En estos pasos, *n* es el número de filas que se devuelven:  
  
1.  Establezca SQL_SOPT_SS_CURSOR_OPTIONS en SQL_CO_FFO_AF.  
  
2.  Establezca SQL_ATTR_ROW_ARRAY_SIZE en *n* + 1.  
  
3.  Enlazar las columnas de resultados a las matrices de *n* + 1 elementos (que es seguro si *n* + realmente se recopila la fila 1).  
  
4.  Abra el cursor con cualquiera **SQLExecDirect** o **SQLExecute**.  
  
5.  Si el estado de retorno es SQL_SUCCESS, a continuación, llame a **SQLFreeStmt** o **SQLCloseCursor** para cerrar el cursor. Todos los datos de las filas estarán en las variables de programa enlazadas.  
  
 Con estos pasos, el **SQLExecDirect** o **SQLExecute** envía una solicitud de apertura del cursor con la opción de recopilación automática habilitada. En esa única solicitud del cliente, el servidor:  
  
-   Abre el cursor.  
  
-   Genera el conjunto de resultados y envía las filas al cliente.  
  
-   Dado que el tamaño del conjunto de filas se estableció en 1 más el número de filas del conjunto de resultados, el servidor detecta el final del cursor y cierra el cursor.  
  
## <a name="see-also"></a>Vea también  
 [Detalles de la programación de cursor &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-cursors/programming/cursor-programming-details-odbc.md)  
  
  
