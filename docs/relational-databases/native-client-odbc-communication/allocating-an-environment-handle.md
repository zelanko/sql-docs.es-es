---
title: Asignación de un identificador de entorno | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, environment handles
- ODBC applications, connections
- handles [SQL Server Native Client]
- environment handles [SQLNCLI]
ms.assetid: 15c1b428-ea6d-4672-894c-f0e289e2da3f
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d36f0f2c1f2b98ef70f3a7460c5565307cc0a3d7
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "86007132"
---
# <a name="allocating-an-environment-handle"></a>Asignar un identificador de entorno
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Para que una aplicación pueda llamar a cualquier función ODBC, debe inicializar el entorno ODBC y asignar un identificador de entorno. Se trata del identificador de contexto global y marcador de posición del resto de los identificadores de ODBC. Para ello, debe llamar a **SQLAllocHandle** con el parámetro *HandleType* establecido en SQL_HANDLE_ENV y *InputHandle* establecido en SQL_NULL_HANDLE.  
  
 Después de asignar el identificador de entorno, la aplicación debe establecer atributos de entorno para indicar qué versión de las llamadas a funciones de ODBC va a utilizar. Para usar ODBC 3. funciones *x* , llame a [SQLSetEnvAttr](../../relational-databases/native-client-odbc-api/sqlsetenvattr.md) con el parámetro de *atributo* establecido en SQL_ATTR_ODBC_VERSION y *ValuePtr* establecido en SQL_OV_ODBC3.  
  
## <a name="see-also"></a>Consulte también  
 [Comunicarse con SQL Server &#40;ODBC&#41;](../../relational-databases/native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
  
