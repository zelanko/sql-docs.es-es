---
title: SQL Server Native Client (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLNCLI, ODBC
- SQL Server Native Client ODBC driver, about SQL Server Native Client ODBC driver
- data access [SQL Server Native Client], ODBC
- SQL Server Native Client ODBC driver
- ODBC
- SQL Server Native Client, ODBC
- ODBC, about SQL Server Native Client ODBC driver
ms.assetid: 811d5ba3-a2b8-48c0-adbc-8c91f041f458
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: ca071567d8151c2b620283c0da422e9963c7c01c
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82704287"
---
# <a name="sql-server-native-client-odbc"></a>SQL Server Native Client (ODBC)
  ODBC es una definición estándar de una interfaz de programación de aplicaciones (API) utilizada para tener acceso a los datos de bases de datos relacionales o de método de acceso secuencial indizado (ISAM). [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] admite ODBC mediante el controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, como una de las API nativas para escribir aplicaciones C y C++ que se comuniquen con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Los programas [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que se escriben utilizando el controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client se comunican con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a través de llamadas a funciones C. Las versiones específicas de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de las funciones ODBC se implementan en el controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. El controlador pasa las instrucciones SQL a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y devuelve los resultados de las instrucciones a la aplicación.  
  
 El controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client se ajusta a la especificación de Microsoft Win32 ODBC 3.51. El controlador admite las aplicaciones escritas utilizando versiones anteriores de ODBC tal y como se define en la especificación de ODBC 3.51.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Nombres de origen de datos y sistemas operativos de 64 bits](data-source-names-and-64-bit-operating-systems.md)  
  
-   [Crear una aplicación de controlador ODBC de SQL Server Native Client](creating-a-driver-application.md)  
  
-   [Comunicarse con SQL Server &#40;ODBC&#41;](../../native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
-   [Ejecutar consultas &#40;&#41;ODBC](../../native-client-odbc-queries/executing-queries-odbc.md)  
  
-   [Procesar los resultados &#40;ODBC&#41;](../../native-client-odbc-results/processing-results-odbc.md)  
  
-   [Usar cursores &#40;&#41;ODBC](../../native-client-odbc-cursors/using-cursors-odbc.md)  
  
-   [Realizar transacciones &#40;&#41;ODBC](../../../database-engine/dev-guide/performing-transactions-odbc.md)  
  
-   [Controlar errores y mensajes](../../native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
-   [Ejecutar procedimientos almacenados](../../native-client-odbc-stored-procedures/running-stored-procedures.md)  
  
-   [Utilizar funciones de catálogo](using-catalog-functions.md)  
  
-   [Realizar operaciones de copia masiva &#40;ODBC&#41;](../../native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
-   [Administrar columnas de texto e imagen](../../native-client-odbc-text-image-columns/managing-text-and-image-columns.md)  
  
-   [Generar perfiles del rendimiento del controlador ODBC](profiling-odbc-driver-performance.md)  
  
-   [Parámetros con valores de tabla &#40;ODBC&#41;](../../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
-   [Mejoras de fecha y hora &#40;ODBC&#41;](../../native-client-odbc-date-time/date-and-time-improvements-odbc.md)  
  
-   [Tipos CLR grandes definidos por el usuario &#40;ODBC&#41;](large-clr-user-defined-types-odbc.md)  
  
-   [Compatibilidad de FILESTREAM &#40;&#41;ODBC](filestream-support-odbc.md)  
  
-   [Nombres de entidad de seguridad de servicio &#40;SPNs&#41; en conexiones cliente &#40;ODBC&#41;](service-principal-names-spns-in-client-connections-odbc.md)  
  
-   [Compatibilidad con columnas dispersas &#40;&#41;ODBC](sparse-columns-support-odbc.md)  
  
-   [SQL Server Native Client &#40;referencia de&#41; ODBC](../../../database-engine/dev-guide/sql-server-native-client-odbc-reference.md)  
  
-   [Temas de procedimientos de ODBC](../../native-client-odbc-how-to/odbc-how-to-topics.md)  
  
## <a name="see-also"></a>Consulte también  
 [Programación de SQL Server Native Client](../sql-server-native-client-programming.md)   
 [Instalar SQL Server Native Client](../applications/installing-sql-server-native-client.md)  
  
  
