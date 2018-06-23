---
title: Comunicar con SQL Server (ODBC) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, communicating with SQL Server
- ODBC applications, communicating with SQL Server
- ODBC, communicating with SQL Server
ms.assetid: cca3dcf0-2a7e-465a-84de-7ce055360eb6
caps.latest.revision: 33
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 3434d20f7b2eca20db0f94155f0922580e4f2546
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36202938"
---
# <a name="communicating-with-sql-server-odbc"></a>Comunicar con SQL Server (ODBC)
  Para una aplicación ODBC para comunicarse con una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], debe asignar el entorno y conexión controla y conectarse al origen de datos. Una vez establecida una conexión, la aplicación puede enviar consultas al servidor y procesar cualquier conjunto de resultados. Cuando la aplicación ha terminado de usar el origen de datos, se desconecta del origen de datos y libera el identificador de conexión. Cuando la aplicación ha liberado todos sus identificadores de conexión, libera el identificador del entorno.  
  
 Una aplicación puede conectarse a cualquier número de orígenes de datos. La aplicación puede usar una combinación de controladores y orígenes de datos, el mismo controlador y una combinación de orígenes de datos o incluso el mismo controlador y varias conexiones al mismo origen de datos.  
  
 Puede descargar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ejemplos de ODBC de Native Client desde el [descargas de SQL Server](http://go.microsoft.com/fwlink/?LinkId=62796) página en MSDN.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Asignar un identificador de entorno](allocating-an-environment-handle.md)  
  
-   [Asignar un identificador de conexión](allocating-a-connection-handle.md)  
  
-   [Orígenes de datos de ODBC para SQL Server Native Client](../../integration-services/connection-manager/data-sources.md)  
  
-   [Conectarse a un origen de datos &#40;ODBC&#41;](connecting-to-a-data-source-odbc.md)  
  
-   [Desconectarse de un origen de datos](disconnecting-from-a-data-source.md)  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Native Client &#40;ODBC&#41;](../native-client/odbc/sql-server-native-client-odbc.md)   
 [SQLSetEnvAttr](../native-client-odbc-api/sqlsetenvattr.md)  
  
  