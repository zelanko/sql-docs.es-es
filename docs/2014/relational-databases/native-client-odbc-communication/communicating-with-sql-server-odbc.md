---
title: Comunicación con SQL Server (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, communicating with SQL Server
- ODBC applications, communicating with SQL Server
- ODBC, communicating with SQL Server
ms.assetid: cca3dcf0-2a7e-465a-84de-7ce055360eb6
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 015cec73c97a3a02179bb65735aaed4dd4f0da6c
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82702061"
---
# <a name="communicating-with-sql-server-odbc"></a>Comunicar con SQL Server (ODBC)
  Para que una aplicación ODBC se comunique con una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , debe asignar el entorno y los identificadores de conexión y conectarse al origen de datos. Una vez establecida una conexión, la aplicación puede enviar consultas al servidor y procesar cualquier conjunto de resultados. Cuando la aplicación ha terminado de usar el origen de datos, se desconecta del origen de datos y libera el identificador de conexión. Cuando la aplicación ha liberado todos sus identificadores de conexión, libera el identificador del entorno.  
  
 Una aplicación puede conectarse a cualquier número de orígenes de datos. La aplicación puede usar una combinación de controladores y orígenes de datos, el mismo controlador y una combinación de orígenes de datos o incluso el mismo controlador y varias conexiones al mismo origen de datos.  
  
 Puede descargar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los ejemplos de ODBC de Native Client en la página de [descargas de SQL Server](https://go.microsoft.com/fwlink/?LinkId=62796) en MSDN.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Asignar un identificador de entorno](allocating-an-environment-handle.md)  
  
-   [Asignar un identificador de conexión](allocating-a-connection-handle.md)  
  
-   [Orígenes de datos de ODBC para SQL Server Native Client](../../integration-services/connection-manager/data-sources.md)  
  
-   [Conectar con un origen de datos &#40;ODBC&#41;](connecting-to-a-data-source-odbc.md)  
  
-   [Desconectarse de un origen de datos](disconnecting-from-a-data-source.md)  
  
## <a name="see-also"></a>Consulte también  
 [SQL Server Native Client &#40;ODBC&#41;](../native-client/odbc/sql-server-native-client-odbc.md)   
 [SQLSetEnvAttr](../native-client-odbc-api/sqlsetenvattr.md)  
  
  
