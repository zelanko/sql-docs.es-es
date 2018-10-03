---
title: SQLFetchScroll | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLFetchScroll function
ms.assetid: 524a3985-a08d-4445-99e0-bb551a666615
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2be98b82689763aeae0de1b53037d48e7e50167f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47766114"
---
# <a name="sqlfetchscroll"></a>SQLFetchScroll
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **SQLFetchScroll** devuelve un conjunto de filas de datos a la aplicación. El tamaño del conjunto de filas se establece mediante [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md). El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client admite todas las instrucciones de captura definidas (por ejemplo, SQL_FETCH_RELATIVE) con las siguientes limitaciones:  
  
-   Si se define un cursor de solo avance para la instrucción, se requiere SQL_FETCH_NEXT y los intentos de capturar de cualquier otro modo producirán un retorno incorrecto.  
  
-   SQL_FETCH_BOOKMARK solamente se admite en cursores estáticos y controlados por conjunto de claves.  
  
## <a name="sqlfetchscroll-support-for-enhanced-date-and-time-features"></a>SQLFetchScroll admite las características mejoradas de fecha y hora  
 Los valores de columna de resultados de tipos de fecha y hora se convierten como se describe en [conversiones de SQL a C](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md).  
  
 Para obtener más información, consulte [mejoras de fecha y hora &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlfetchscroll-support-for-large-clr-udts"></a>SQLFetchScroll admite UDT CLR grandes  
 **SQLFetchScroll** admite los tipos definidos por el usuario (UDT) CLR grandes. Para obtener más información, consulte [Large CLR User-Defined tipos &#40;ODBC&#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Vea también  
 [Función SQLFetchScroll](http://go.microsoft.com/fwlink/?LinkId=59343)   
 [Detalles de implementación de la API de ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
