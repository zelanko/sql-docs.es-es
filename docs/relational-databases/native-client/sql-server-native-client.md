---
title: Información
ms.date: 04/14/2017
ms.prod: sql
ms.reviewer: ''
ms.custom: ''
ms.technology: native-client
ms.topic: conceptual
ms.assetid: e4d4fe39-0090-42a7-8405-6378370d11cb
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d175942c9d636221868ca12743e6dac79bb2ddcb
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388712"
---
# <a name="sql-server-native-client"></a>SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

SNAC, o SQL ServerSQL Server Native Client, es un término que se ha utilizado indistintamente para hacer referencia a controladores ODBC y OLE DB para SQL Server.

> [!IMPORTANT] 
> SQL ServerSQL Server Native Client (SQLNCLI) permanece en desuso y no se recomienda usarlo para el nuevo trabajo de desarrollo. En su lugar, use el nuevo [Microsoft OLE DB Driver for SQL Server](../../connect/oledb/oledb-driver-for-sql-server.md) (MSOLEDBSQL), que se actualizará con las características de servidor más recientes.

> [!NOTE]
> Para obtener más información y descargar los controladores SNAC u ODBC, consulte la entrada de blog explicada por el ciclo de vida de [SNAC.](https://blogs.msdn.microsoft.com/sqlreleaseservices/snac-lifecycle-explained/)
> Para obtener más información sobre el controlador ODBC para SQL Server, vea Controlador ODBC de [Microsoft para SQL Server](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md).  

 Información sobre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] las características [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]de Native Client publicadas con , la última versión disponible de SQL ServerSQL Server Native Client:

-   [Compatibilidad de SQL Server Native Client con LocalDB](../../relational-databases/native-client/features/sql-server-native-client-support-for-localdb.md)  

-   [Detección de metadatos](../../relational-databases/native-client/features/metadata-discovery.md)  

-   [Compatibilidad con UTF-16 en SQL Server Native Client 11.0](../../relational-databases/native-client/features/utf-16-support-in-sql-server-native-client-11-0.md)  

-   [Compatibilidad de SQL Server Native Client para la alta disponibilidad con recuperación de desastres](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  

-   [Acceso a la información de diagnóstico en el registro de eventos extendidos](../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)  

ODBC [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en Native Client admite tres características que se agregaron a ODBC estándar en el SDK de Windows 7:  

-   Ejecución asincrónica en operaciones relacionadas con conexión. Para obtener más información, vea el tema que trata sobre [ejecución asincrónica](https://go.microsoft.com/fwlink/?LinkID=191493).  

-   Extensibilidad del tipo de datos C. Para obtener más información, vea el tema sobre [tipos de datos C en ODBC](https://go.microsoft.com/fwlink/?LinkID=191495).  

     Para admitir esta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] característica en Native Client, SQLGetDescField puede devolver **SQL_C_SS_TIME2** (para tipos de **hora)** o **SQL_C_SS_TIMESTAMPOFFSET** (para **datetimeoffset**) en lugar de **SQL_C_BINARY**, si la aplicación usa ODBC 3.8. Para obtener más información, vea Compatibilidad con tipos de datos para mejoras de [fecha y hora ODBC](../../relational-databases/native-client-odbc-date-time/data-type-support-for-odbc-date-and-time-improvements.md).  

-   Llamada varias veces a **SQLGetData** con un búfer pequeño para recuperar un valor de parámetro grande. Para obtener más información, vea el tema que trata sobre [recuperar parámetros de salida mediante SQLGetData](https://go.microsoft.com/fwlink/?LinkID=191494).  

 En los siguientes temas se describen los cambios de comportamiento de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  

-   Al llamar a **ICommandWithParameters::SetParameterInfo**, el valor pasado al parámetro *pwszName* debe ser un identificador válido. Para obtener más información, vea [ICommandWithParameters](../../relational-databases/native-client-ole-db-interfaces/icommandwithparameters.md).  

-   **SQLDescribeParam** devolverá constantemente un valor conforme a la especificación ODBC. Para obtener más información, vea [SQLDescribeParam](../../relational-databases/native-client-odbc-api/sqldescribeparam.md).  

-   [Cambio de comportamiento del controlador ODBC al administrar las conversiones de caracteres](../../relational-databases/native-client/features/odbc-driver-behavior-change-when-handling-character-conversions.md)  

## <a name="see-also"></a>Consulte también  
[Instalar SQL Server Native Client](../../relational-databases/native-client/applications/installing-sql-server-native-client.md)  
 [Características de SQL Server Native Client](../../relational-databases/native-client/features/sql-server-native-client-features.md)  
