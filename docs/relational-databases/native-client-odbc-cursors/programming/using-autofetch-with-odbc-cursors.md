---
description: Usar la captura automática con cursores ODBC
title: Usar la captura automática con cursores ODBC | Microsoft Docs
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: abb1bb038273bfd2d1e9e4bdd2d6f130285361e1
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97473746"
---
# <a name="using-autofetch-with-odbc-cursors"></a>Usar la captura automática con cursores ODBC
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Cuando se conecta a una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client admite una opción de captura automática cuando se usa cualquier tipo de cursor de servidor. Con la captura automática, la función **SQLExecute** o **SQLExecDirect** que abre el cursor también tiene una función [SQLFetchScroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)(SQL_FIRST) implícita. Las filas que componen el primer conjunto de filas se devuelven a las variables de aplicación enlazadas como parte de la ejecución de la instrucción y se ahorra un viaje de ida y vuelta (round trip) de la red al servidor. No se admite [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) cuando está habilitada la opción de captura automática; las columnas del conjunto de resultados se deben enlazar a las variables de programa.  
  
 Las aplicaciones solicitan la captura automática estableciendo el atributo de la instrucción SQL_SOPT_SS_CURSOR_OPTIONS específica del controlador en SQL_CO_AF.  
  
## <a name="see-also"></a>Consulte también  
 [Detalles de la programación de cursores &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-cursors/programming/cursor-programming-details-odbc.md)  
  
  
