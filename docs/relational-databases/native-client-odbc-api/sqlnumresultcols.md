---
title: SQLNumResultCols | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLNumResultCols function
ms.assetid: f79d8b3c-521e-4e50-a564-21d73ae5767b
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8fec604f795aacc9a65f6ebce97afec1a784c755
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "86009201"
---
# <a name="sqlnumresultcols"></a>SQLNumResultCols
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Para las instrucciones ejecutadas, el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client no tiene acceso al servidor para notificar el número de columnas de un conjunto de resultados. En este caso, **SQLNumResultCols** no produce un ciclo de ida y vuelta del servidor. Como ocurre con [SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md) y [SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md), al llamar a **SQLNumResultCols** en instrucciones preparadas pero no ejecutadas se genera un ciclo de ida y vuelta del servidor.  
  
 Cuando una instrucción o un lote de instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] devuelve varios conjuntos de filas de resultados, es posible que el número de columnas del conjunto de resultados cambie de un conjunto a otro. Se debe llamar a**a SQLNumResultCols** para cada conjunto. Cuando el número de columnas cambia, la aplicación debe volver a enlazar los valores de datos antes de capturar los resultados de la fila. Para obtener más información sobre cómo administrar la devolución de varios conjuntos de resultados, vea [SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md).  
  
 Las mejoras en el motor de base de datos a partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] permiten a SQLNumResultCols obtener descripciones más precisas de los resultados esperados. Estos resultados más precisos pueden diferir de los valores devueltos por SQLNumResultCols en versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obtener más información, vea [Detección de metadatos](../../relational-databases/native-client/features/metadata-discovery.md).  
  
## <a name="see-also"></a>Consulte también  
 [SQLNumResultCols función)](https://go.microsoft.com/fwlink/?LinkId=59359)   
 [ODBC API Implementation Details](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
