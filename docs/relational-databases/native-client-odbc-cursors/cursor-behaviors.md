---
title: Comportamientos de cursor | Documentos de Microsoft
ms.custom: ''
ms.date: 10/24/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-odbc-cursors
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- scrollable cursors [SQL Server]
- SQL Server Native Client ODBC driver, cursors
- version-based optimistic concurrency
- cursors [ODBC], cursor behaviors
- ODBC applications, cursors
- SQL_ATTR_CURSOR_SENSITIVITY option
- SQL_ATTR_CURSOR_SCROLLABLE option
- sensitivity behavior of cursor
- ODBC cursors, cursor behaviors
ms.assetid: 742ddcd2-232b-4aa1-9212-027df120ad35
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 893a6ac846176c353585dbdcf7d917207ebea279
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="cursor-behaviors"></a>Comportamientos de cursor
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  ODBC admite las opciones ISO para especificar el comportamiento de los cursores especificando su capacidad de desplazamiento y sensibilidad. Estos comportamientos se especifican estableciendo las opciones SQL_ATTR_CURSOR_SCROLLABLE y SQL_ATTR_CURSOR_SENSITIVITY en una llamada a [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md). El controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client implementa estas opciones solicitando cursores de servidor con las siguientes características.  
  
|Valores de comportamiento de cursor|Características de cursor de servidor solicitadas|  
|------------------------------|---------------------------------------------|  
|SQL_SCROLLABLE y SQL_SENSITIVE|Cursor controlado por conjunto de claves y simultaneidad optimista basada en las versiones|  
|SQL_SCROLLABLE y SQL_INSENSITIVE|Cursor estático y simultaneidad de solo lectura|  
|SQL_SCROLLABLE y SQL_UNSPECIFIED|Cursor estático y simultaneidad de solo lectura|  
|SQL_NONSCROLLABLE y SQL_SENSITIVE|Cursor de solo avance y simultaneidad optimista basada en las versiones|  
|SQL_NONSCROLLABLE y SQL_INSENSITIVE|Conjunto de resultados predeterminado (solo avance, solo lectura)|  
|SQL_NONSCROLLABLE y SQL_UNSPECIFIED|Conjunto de resultados predeterminado (solo avance, solo lectura)|  
  
 Simultaneidad optimista basada en la versión requiere un **timestamp** columna en la tabla subyacente. Si se solicita el control de simultaneidad optimista basada en la versión en una tabla que no tiene un **timestamp** columna, el servidor usa basada en valores simultaneidad optimista.  
  
## <a name="scrollability"></a>Desplazamiento  
 Si se establece SQL_ATTR_CURSOR_SCROLLABLE como SQL_SCROLLABLE, el cursor admite todos los valores diferentes para la *FetchOrientation* parámetro de [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md). Si se establece SQL_ATTR_CURSOR_SCROLLABLE como SQL_NONSCROLLABLE, el cursor solo admite un *FetchOrientation* valor de SQL_FETCH_NEXT.  
  
## <a name="sensitivity"></a>Sensibilidad  
 Si SQL_ATTR_CURSOR_SENSITIVITY está establecido en SQL_SENSITIVE, el cursor refleja modificaciones de datos realizadas por el usuario actual o confirmadas por otros usuarios. Si SQL_ATTR_CURSOR_SENSITIVITY está establecido en SQL_INSENSITIVE, el cursor no refleja las modificaciones de datos.  
  
## <a name="see-also"></a>Vea también  
 [Uso de cursores (ODBC)](../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md) [propiedades de Cursor](properties/cursor-properties.md) 
  
  
