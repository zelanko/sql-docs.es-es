---
title: Modificaciones registradas frente a modificaciones sin registrar ? Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: dc7fb913bef4083b045a0c1c010bdedbc43135c5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297703"
---
# <a name="logged-vs-unlogged-modifications"></a>Modificaciones registradas frente a modificaciones no registradas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Una aplicación puede [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solicitar que el controlador ODBC de Native Client no registre **el texto,** **ntext**y las modificaciones de **imagen.** Sin embargo, se debe tener cautela con esta opción. Debe utilizarse solo para aquellas situaciones en las que los datos de **texto,** **ntext**o **imagen** no son críticos y los propietarios de datos están dispuestos a intercambiar la capacidad de recuperar datos para obtener un mayor rendimiento.  
  
 El registro de **text**, **ntext**y las modificaciones de **imagen** se controla llamando a [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) con el *parámetro Attribute* establecido en SQL_SOPT_SS_ TEXTPTR_LOGGING y *ValuePtr* establecido en SQL_TL_ON o SQL_TL_OFF.  
  
## <a name="see-also"></a>Consulte también  
 [Administrar columnas de texto e imagen](../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)  
  
  
