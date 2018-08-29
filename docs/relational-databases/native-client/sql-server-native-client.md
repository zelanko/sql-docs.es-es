---
title: SQL Server Native Client | Microsoft Docs
ms.date: 04/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e4d4fe39-0090-42a7-8405-6378370d11cb
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a1f60dff72b14e29572a4d255ad8473d6ed1672d
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43081957"
---
# <a name="sql-server-native-client"></a>SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

SNAC o SQL Server Native Client es un término que se ha usado de forma intercambiable para hacer referencia a los controladores ODBC y OLE DB para SQL Server.

**Nota:** no se recomienda utilizar este controlador para el nuevo desarrollo. El nuevo proveedor de OLE DB se llama a la [controlador OLE DB de Microsoft para SQL Server](../../connect/oledb/oledb-driver-for-sql-server.md) (MSOLEDBSQL) que se actualizará con las características más recientes del servidor en el futuro.


**Para obtener más información y descargar los controladores de ODBC o SNAC, visite [ciclo de vida SNAC explicado](https://blogs.msdn.microsoft.com/sqlreleaseservices/snac-lifecycle-explained/).**

Para obtener más información sobre el controlador ODBC para SQL Server, vea [Microsoft ODBC Driver for SQL Server en Windows](https://msdn.microsoft.com/library/jj730314(v=sql.110).aspx).  Consulte también, [presentación de los nuevos controladores ODBC de Microsoft para SQL Server](https://blogs.msdn.microsoft.com/sqlnativeclient/2013/01/23/introducing-the-new-microsoft-odbc-drivers-for-sql-server/), y [ODBC Driver 13.1 para SQL Server lanzó](https://blogs.technet.microsoft.com/dataplatforminsider/2016/08/03/odbc-driver-13-1-for-sql-server-released/).  

 Información sobre la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publican características de cliente nativo con [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], la última versión disponible de SQL Server native Client:

-   [Compatibilidad de SQL Server Native Client con LocalDB](../../relational-databases/native-client/features/sql-server-native-client-support-for-localdb.md)  

-   [Detección de metadatos](../../relational-databases/native-client/features/metadata-discovery.md)  

-   [Compatibilidad con UTF-16 en SQL Server Native Client 11.0](../../relational-databases/native-client/features/utf-16-support-in-sql-server-native-client-11-0.md)  

-   [Compatibilidad de SQL Server Native Client para la alta disponibilidad con recuperación de desastres](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  

-   [Obtener acceso a información de diagnóstico en el registro de eventos extendidos](../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)  

ODBC en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client admite tres características que se agregaron a ODBC estándar en el SDK de Windows 7:  

-   Ejecución asincrónica en operaciones relacionadas con conexión. Para obtener más información, vea el tema que trata sobre [ejecución asincrónica](http://go.microsoft.com/fwlink/?LinkID=191493).  

-   Extensibilidad del tipo de datos C. Para obtener más información, vea el tema sobre [tipos de datos C en ODBC](http://go.microsoft.com/fwlink/?LinkID=191495).  

     Para admitir esta característica en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, que puede devolver SQLGetDescField **SQL_C_SS_TIME2** (para **tiempo** tipos) o **SQL_C_SS_TIMESTAMPOFFSET** (para **datetimeoffset**) en lugar de **SQL_C_BINARY**, si su aplicación utiliza ODBC 3.8. Para obtener más información, consulte [compatibilidad con tipos de datos de ODBC mejoras de fecha y hora](../../relational-databases/native-client-odbc-date-time/data-type-support-for-odbc-date-and-time-improvements.md).  

-   Llamada varias veces a **SQLGetData** con un búfer pequeño para recuperar un valor de parámetro grande. Para obtener más información, vea el tema que trata sobre [recuperar parámetros de salida mediante SQLGetData](http://go.microsoft.com/fwlink/?LinkID=191494).  

 En los siguientes temas se describen los cambios de comportamiento de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  

-   Al llamar a **ICommandWithParameters::SetParameterInfo**, el valor pasado al parámetro *pwszName* debe ser un identificador válido. Para obtener más información, consulte [ICommandWithParameters](../../relational-databases/native-client-ole-db-interfaces/icommandwithparameters.md).  

-   **SQLDescribeParam** devolverá de forma coherente un valor que cumplen las especificaciones de especificación de ODBC. Para obtener más información, consulte [SQLDescribeParam](../../relational-databases/native-client-odbc-api/sqldescribeparam.md).  

-   [Cambio de comportamiento del controlador ODBC al administrar las conversiones de caracteres](../../relational-databases/native-client/features/odbc-driver-behavior-change-when-handling-character-conversions.md)  

## <a name="see-also"></a>Vea también  
[Instale SQL Server Native Client](../../relational-databases/native-client/applications/installing-sql-server-native-client.md)  
 [Características de SQL Server Native Client](../../relational-databases/native-client/features/sql-server-native-client-features.md)  
