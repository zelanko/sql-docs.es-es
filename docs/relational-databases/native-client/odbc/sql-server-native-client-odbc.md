---
title: SQL Server Native Client (ODBC) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client|ODBC
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
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
caps.latest.revision: 46
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 82a923e22e3954529685eb35832fe7e211ca18b3
ms.sourcegitcommit: 2d93cd115f52bf3eff3069f28ea866232b4f9f9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/01/2018
ms.locfileid: "34708373"
---
# <a name="sql-server-native-client-odbc"></a>SQL Server Native Client (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  ODBC es una definición estándar de una interfaz de programación de aplicaciones (API) utilizada para tener acceso a los datos de bases de datos relacionales o de método de acceso secuencial indizado (ISAM). [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] admite ODBC mediante el controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, como una de las API nativas para escribir aplicaciones C y C++ que se comuniquen con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Los programas [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que se escriben utilizando el controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client se comunican con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a través de llamadas a funciones C. Las versiones específicas de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de las funciones ODBC se implementan en el controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. El controlador pasa las instrucciones SQL a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y devuelve los resultados de las instrucciones a la aplicación.  
  
 El controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client se ajusta a la especificación de Microsoft Win32 ODBC 3.51. El controlador admite las aplicaciones escritas utilizando versiones anteriores de ODBC tal y como se define en la especificación de ODBC 3.51.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Nombres de origen de datos y sistemas operativos de 64 bits](../../../relational-databases/native-client/odbc/data-source-names-and-64-bit-operating-systems.md)  
  
-   [Crear una aplicación de controlador ODBC de SQL Server Native Client](../../../relational-databases/native-client/odbc/creating-a-driver-application.md)  
  
-   [Comunicar con SQL Server &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
-   [Ejecutar consultas &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
-   [Procesar resultados &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
-   [Uso de cursores &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md)  
  
-   [Realizar transacciones &#40;ODBC&#41;](http://msdn.microsoft.com/library/f431191a-5762-4f0b-85bb-ac99aff29724)  
  
-   [Controlar errores y mensajes](../../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
-   [Ejecutar procedimientos almacenados](../../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)  
  
-   [Utilizar funciones de catálogo](../../../relational-databases/native-client/odbc/using-catalog-functions.md)  
  
-   [Realizar operaciones de copia masiva &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
-   [Administrar columnas de texto e imagen](../../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)  
  
-   [Generar perfiles del rendimiento del controlador ODBC](../../../relational-databases/native-client/odbc/profiling-odbc-driver-performance.md)  
  
-   [Parámetros con valores de tabla &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
-   [Fecha y hora mejoras &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)  
  
-   [Tipos definidos por el usuario CLR grandes &#40;ODBC&#41;](../../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)  
  
-   [Compatibilidad con FILESTREAM &#40;ODBC&#41;](../../../relational-databases/native-client/odbc/filestream-support-odbc.md)  
  
-   [Nombres principales de servicio &#40;SPN&#41; en las conexiones de cliente &#40;ODBC&#41;](../../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md)  
  
-   [Compatibilidad con columnas dispersas &#40;ODBC&#41;](../../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md)  
  
-   [SQL Server Native Client &#40;ODBC&#41; referencia](http://msdn.microsoft.com/library/06b7edee-8636-49d9-9b5c-2c710bf4fa2d)  
  
-   [Temas de procedimientos de ODBC](../../../relational-databases/native-client-odbc-how-to/odbc-how-to-topics.md)  
  
## <a name="see-also"></a>Vea también  
 [Programación de SQL Server Native Client](../../../relational-databases/native-client/sql-server-native-client-programming.md)   
 [Instalar SQL Server Native Client](../../../relational-databases/native-client/applications/installing-sql-server-native-client.md)  
  
  
