---
title: SQLNumResultCols | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-api
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apitype: DLLExport
helpviewer_keywords: SQLNumResultCols function
ms.assetid: f79d8b3c-521e-4e50-a564-21d73ae5767b
caps.latest.revision: "33"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a29d2ac6e21b6e8fe5ecd46ee75f11264901e582
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sqlnumresultcols"></a>SQLNumResultCols
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Las instrucciones ejecutadas, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC Native Client no tiene acceso al servidor para notificar el número de columnas en un conjunto de resultados. En este caso, **SQLNumResultCols** no produce un ciclo de ida y vuelta del servidor. Al igual que [SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md) y [SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md), si se llama **SQLNumResultCols** en preparado, pero las instrucciones ejecutadas no genera un ida y vuelta del servidor.  
  
 Cuando una instrucción o un lote de instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] devuelve varios conjuntos de filas de resultados, es posible que el número de columnas del conjunto de resultados cambie de un conjunto a otro. Se debe llamar a**a SQLNumResultCols** para cada conjunto. Cuando el número de columnas cambia, la aplicación debe volver a enlazar los valores de datos antes de capturar los resultados de la fila. Para obtener más información sobre el control de resultados múltiples conjuntos devuelve, vea [SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md).  
  
 Mejoras en el motor de base de datos a partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] permitir SQLNumResultCols obtener descripciones más precisas de los resultados esperados. Estos resultados más precisos pueden diferir de los valores devueltos por SQLNumResultCols en versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, consulte [de detección de metadatos](../../relational-databases/native-client/features/metadata-discovery.md).  
  
## <a name="see-also"></a>Vea también  
 [SQLNumResultCols (función)](http://go.microsoft.com/fwlink/?LinkId=59359)   
 [Detalles de implementación de la API de ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
