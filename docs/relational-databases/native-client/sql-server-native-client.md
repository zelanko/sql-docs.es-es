---
title: SQL Server Native Client | Microsoft Docs
ms.date: 04/14/2017
ms.prod: sql
ms.reviewer: ''
ms.custom: ''
ms.technology: native-client
ms.topic: conceptual
ms.assetid: e4d4fe39-0090-42a7-8405-6378370d11cb
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4e11bc1094f7bab993eb67542c16360e874db87f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68031779"
---
# <a name="sql-server-native-client"></a>SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

SNAC o SQL Server Native Client es un término que se ha usado de forma intercambiable para hacer referencia a los controladores ODBC y OLE DB para SQL Server.

> [!IMPORTANT] 
> El SQL Server Native Client (SQLNCLI) permanece en desuso y no se recomienda usarla en nuevos trabajos de desarrollo. En su lugar, use la nueva [controlador OLE DB de Microsoft para SQL Server](../../connect/oledb/oledb-driver-for-sql-server.md) (MSOLEDBSQL) que se actualizará con las características más recientes del servidor.

> [!NOTE]
> Para obtener más información y descargar el SNAC o los controladores ODBC, consulte el [entrada de blog explica el ciclo de vida de SNAC](https://blogs.msdn.microsoft.com/sqlreleaseservices/snac-lifecycle-explained/).
> Para obtener más información sobre el controlador ODBC para SQL Server, vea [Microsoft ODBC Driver para SQL Server](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md).  

 Información sobre la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publican características de cliente nativo con [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], la última versión disponible de SQL Server native Client:

-   [Compatibilidad de SQL Server Native Client con LocalDB](../../relational-databases/native-client/features/sql-server-native-client-support-for-localdb.md)  

-   [Detección de metadatos](../../relational-databases/native-client/features/metadata-discovery.md)  

-   [Compatibilidad con UTF-16 en SQL Server Native Client 11.0](../../relational-databases/native-client/features/utf-16-support-in-sql-server-native-client-11-0.md)  

-   [Compatibilidad de SQL Server Native Client para la alta disponibilidad con recuperación de desastres](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  

-   [Obtener acceso a información de diagnóstico en el registro de eventos extendidos](../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)  

ODBC en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client admite tres características que se agregaron a ODBC estándar en el SDK de Windows 7:  

-   Ejecución asincrónica en operaciones relacionadas con conexión. Para obtener más información, vea el tema que trata sobre [ejecución asincrónica](https://go.microsoft.com/fwlink/?LinkID=191493).  

-   Extensibilidad del tipo de datos C. Para obtener más información, vea el tema sobre [tipos de datos C en ODBC](https://go.microsoft.com/fwlink/?LinkID=191495).  

     Para admitir esta característica en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, que puede devolver SQLGetDescField **SQL_C_SS_TIME2** (para **tiempo** tipos) o **SQL_C_SS_TIMESTAMPOFFSET** (para **datetimeoffset**) en lugar de **SQL_C_BINARY**, si su aplicación utiliza ODBC 3.8. Para obtener más información, consulte [compatibilidad con tipos de datos de ODBC mejoras de fecha y hora](../../relational-databases/native-client-odbc-date-time/data-type-support-for-odbc-date-and-time-improvements.md).  

-   Llamada varias veces a **SQLGetData** con un búfer pequeño para recuperar un valor de parámetro grande. Para obtener más información, vea el tema que trata sobre [recuperar parámetros de salida mediante SQLGetData](https://go.microsoft.com/fwlink/?LinkID=191494).  

 En los siguientes temas se describen los cambios de comportamiento de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  

-   Al llamar a **ICommandWithParameters::SetParameterInfo**, el valor pasado al parámetro *pwszName* debe ser un identificador válido. Para obtener más información, vea [ICommandWithParameters](../../relational-databases/native-client-ole-db-interfaces/icommandwithparameters.md).  

-   **SQLDescribeParam** devolverá de forma coherente un valor que cumplen las especificaciones de especificación de ODBC. Para obtener más información, vea [SQLDescribeParam](../../relational-databases/native-client-odbc-api/sqldescribeparam.md).  

-   [Cambio de comportamiento del controlador ODBC al administrar las conversiones de caracteres](../../relational-databases/native-client/features/odbc-driver-behavior-change-when-handling-character-conversions.md)  

## <a name="see-also"></a>Vea también  
[Instale SQL Server Native Client](../../relational-databases/native-client/applications/installing-sql-server-native-client.md)  
 [Características de SQL Server Native Client](../../relational-databases/native-client/features/sql-server-native-client-features.md)  
