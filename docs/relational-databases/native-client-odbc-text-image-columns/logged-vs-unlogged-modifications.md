---
title: Modificaciones registradas frente a No registradas modificaciones | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-text-image-columns
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- text columns [ODBC]
- SQL Server Native Client ODBC driver, image columns
- SQL Server Native Client ODBC driver, text columns
- data types [ODBC], image
- data types [ODBC], text
- logged vs. nonlogged modifications [SQL Server Native Client]
- columns [ODBC]
- ODBC data types, image columns
- nonlogged vs. logged modifications
- ODBC data types, text columns
- image columns [ODBC]
ms.assetid: 20aa5b27-4a2c-46e7-8356-beb0eebf4b7e
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: b84160c6f054c5ff24230df3bb84a213f2d31919
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39536765"
---
# <a name="logged-vs-unlogged-modifications"></a>Modificaciones registradas frente a modificaciones no registradas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Una aplicación puede solicitar que el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client no registro **texto**, **ntext**, y **imagen** modificaciones. Sin embargo, se debe tener cautela con esta opción. Debe usarse solo en aquellas situaciones donde la **texto**, **ntext**, o **imagen** datos no son fundamentales y propietarios de los datos están dispuestos a compensar la capacidad para recuperar datos un mayor rendimiento.  
  
 El registro de **texto**, **ntext**, y **imagen** modificaciones se controla mediante una llamada a [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) con el  *Atributo* parámetro establecido en SQL_SOPT_SS_ TEXTPTR_LOGGING y *ValuePtr* establecido en SQL_TL_ON o SQL_TL_OFF.  
  
## <a name="see-also"></a>Vea también  
 [Administrar columnas de texto e imagen](../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)  
  
  
