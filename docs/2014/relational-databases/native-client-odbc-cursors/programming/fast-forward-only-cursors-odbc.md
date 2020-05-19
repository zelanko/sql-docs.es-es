---
title: Cursores de solo avance rápido (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- fast forward-only cursors
- forward-only cursors
- cursors [ODBC], fast forward-only
- ODBC cursors, fast forward-only
ms.assetid: 0707d07e-fc95-42ed-9280-b7e508ac8c62
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 812419f7ebf9501ab2409876c4cc5c0a775492b9
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82705622"
---
# <a name="fast-forward-only-cursors-odbc"></a>Cursores de solo avance rápido (ODBC)
  Cuando se conecta a una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client admite optimizaciones de rendimiento para cursores de solo avance y de solo lectura. Los cursores de solo avance rápido se implementan internamente mediante el controlador y el servidor de un modo muy similar a los conjuntos de resultados predeterminados. Además de presentar un alto rendimiento, los cursores de solo avance rápido también presentan estas características:  
  
-   No se admite [SQLGetData](../../native-client-odbc-api/sqlgetdata.md) . Las columnas del conjunto de resultados deben estar enlazadas a variables de programa.  
  
-   El servidor cierra automáticamente el cursor cuando se detecta el final del cursor. La aplicación debe seguir llamando a [SQLCloseCursor](../../native-client-odbc-api/sqlclosecursor.md) o [SQLFreeStmt](../../native-client-odbc-api/sqlfreestmt.md)(SQL_CLOSE), pero el controlador no tiene que enviar la solicitud de cierre al servidor. De esta forma, se ahorra un viaje de ida y vuelta (round trip) de la red al servidor.  
  
 La aplicación solicita cursores de solo avance rápido mediante el atributo de instrucciones específico del controlador SQL_SOPT_SS_CURSOR_OPTIONS. Cuando se establece en SQL_CO_FFO, los cursores de solo avance rápido se habilitan sin captura automática. Cuando se establece en SQL_CO_FFO_AF, también se habilita la opción de captura automática. Para obtener más información sobre la captura automática, vea [usar la captura automática con cursores ODBC](using-autofetch-with-odbc-cursors.md).  
  
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
  
## <a name="see-also"></a>Consulte también  
 [Detalles de la programación de cursores &#40;ODBC&#41;](cursor-programming-details-odbc.md)  
  
  
