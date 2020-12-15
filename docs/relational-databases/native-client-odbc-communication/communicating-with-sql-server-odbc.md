---
title: Comunicación con SQL Server (ODBC) | Microsoft Docs
description: Obtenga información sobre cómo una aplicación ODBC se comunica con una instancia de SQL Server mediante conexiones y recursos de conexión.
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, communicating with SQL Server
- ODBC applications, communicating with SQL Server
- ODBC, communicating with SQL Server
ms.assetid: cca3dcf0-2a7e-465a-84de-7ce055360eb6
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 179e9fa7d6c89a5d575d764b7bcfba22c072dca2
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97464966"
---
# <a name="communicating-with-sql-server-odbc"></a>Comunicar con SQL Server (ODBC)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Para que una aplicación ODBC se comunique con una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , debe asignar el entorno y los identificadores de conexión y conectarse al origen de datos. Una vez establecida una conexión, la aplicación puede enviar consultas al servidor y procesar cualquier conjunto de resultados. Cuando la aplicación ha terminado de usar el origen de datos, se desconecta del origen de datos y libera el identificador de conexión. Cuando la aplicación ha liberado todos sus identificadores de conexión, libera el identificador del entorno.  
  
 Una aplicación puede conectarse a cualquier número de orígenes de datos. La aplicación puede usar una combinación de controladores y orígenes de datos, el mismo controlador y una combinación de orígenes de datos o incluso el mismo controlador y varias conexiones al mismo origen de datos.  
  
 Puede descargar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los ejemplos de ODBC de Native Client en la página de [descargas de SQL Server](https://go.microsoft.com/fwlink/?LinkId=62796) en MSDN.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Asignar un identificador de entorno](../../relational-databases/native-client-odbc-communication/allocating-an-environment-handle.md)  
  
-   [Asignar un identificador de conexión](../../relational-databases/native-client-odbc-communication/allocating-a-connection-handle.md)  
  
-   [Orígenes de datos de ODBC para SQL Server Native Client](../../relational-databases/native-client-odbc-communication/sql-server-native-client-odbc-data-sources.md)  
  
-   [Conectar con un origen de datos &#40;ODBC&#41;](../../relational-databases/native-client-odbc-communication/connecting-to-a-data-source-odbc.md)  
  
-   [Desconectarse de un origen de datos](../../relational-databases/native-client-odbc-communication/disconnecting-from-a-data-source.md)  
  
## <a name="see-also"></a>Consulte también  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)   
 [SQLSetEnvAttr](../../relational-databases/native-client-odbc-api/sqlsetenvattr.md)  
  
  
