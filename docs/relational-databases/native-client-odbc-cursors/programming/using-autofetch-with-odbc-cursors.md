---
title: Uso de la captura automática con cursores ODBC Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC cursors, autofetch
- autofetch option
- cursors [ODBC], autofetch
ms.assetid: 57bd55f4-8945-4d8d-9f58-d30c81d2a514
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 812f4742dfe8273c4e96fc5205626fe1f6c07347
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298421"
---
# <a name="using-autofetch-with-odbc-cursors"></a>Usar la captura automática con cursores ODBC
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Cuando se conecta [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] una instancia de , el controlador ODBC de Native Client admite una opción de captura automática cuando se utiliza cualquier tipo de cursor de servidor. Con autofetch, la función **SQLExecute** o **SQLExecDirect** que abre el cursor también tiene una función [IMPLÍCITA SQLFetchScroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)(SQL_FIRST). Las filas que componen el primer conjunto de filas se devuelven a las variables de aplicación enlazadas como parte de la ejecución de la instrucción y se ahorra un viaje de ida y vuelta (round trip) de la red al servidor. [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) no se admite cuando la opción de captura automática está habilitada; las columnas del conjunto de resultados deben estar enlazadas a variables de programa.  
  
 Las aplicaciones solicitan la captura automática estableciendo el atributo de la instrucción SQL_SOPT_SS_CURSOR_OPTIONS específica del controlador en SQL_CO_AF.  
  
## <a name="see-also"></a>Consulte también  
 [Detalles de programación del cursor &#40;&#41;ODBC](../../../relational-databases/native-client-odbc-cursors/programming/cursor-programming-details-odbc.md)  
  
  
