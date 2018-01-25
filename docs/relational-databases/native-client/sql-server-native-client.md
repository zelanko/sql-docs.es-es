---
title: SQL Server Native Client | Documentos de Microsoft
ms.date: 04/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client
ms.reviewer: 
ms.suite: sql
ms.custom: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e4d4fe39-0090-42a7-8405-6378370d11cb
caps.latest.revision: "43"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Active
ms.openlocfilehash: 7474d620d96880396e8fe7dc44e55b4cdcf7f440
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="sql-server-native-client"></a>SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

SNAC o SQL Server Native Client es un término que se ha utilizado indistintamente para hacer referencia a los controladores ODBC y OLE DB para SQL Server. 

**Para obtener más información y descargar los controladores de ODBC o SNAC, visite [ciclo de vida SNAC explicada](https://blogs.msdn.microsoft.com/sqlreleaseservices/snac-lifecycle-explained/).**

Para obtener más información sobre el controlador ODBC para SQL Server, vea [Microsoft ODBC Driver for SQL Server en Windows](https://msdn.microsoft.com/library/jj730314(v=sql.110).aspx).  Vea también, [presentación de los nuevos controladores ODBC de Microsoft para SQL Server](https://blogs.msdn.microsoft.com/sqlnativeclient/2013/01/23/introducing-the-new-microsoft-odbc-drivers-for-sql-server/), y [ODBC Driver 13.1 para SQL Server libera](https://blogs.technet.microsoft.com/dataplatforminsider/2016/08/03/odbc-driver-13-1-for-sql-server-released/).  
  
 Obtener información sobre la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] características Native Client se lanzó con [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], la última versión disponible de SQL Server native Client: 
  
-   [Compatibilidad de SQL Server Native Client con LocalDB](../../relational-databases/native-client/features/sql-server-native-client-support-for-localdb.md)  
  
-   [Detección de metadatos](../../relational-databases/native-client/features/metadata-discovery.md)  
  
-   [Compatibilidad con UTF-16 en SQL Server Native Client 11.0](../../relational-databases/native-client/features/utf-16-support-in-sql-server-native-client-11-0.md)  
  
-   [SQL Server Native Client Support for High Availability, Disaster Recovery](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  
  
-   [Obtener acceso a información de diagnóstico en el registro de eventos extendidos](../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)  
  
ODBC en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client admite tres características que se agregaron a ODBC estándar en el SDK de Windows 7:  
  
-   Ejecución asincrónica en operaciones relacionadas con conexión. Para obtener más información, vea el tema que trata sobre [ejecución asincrónica](http://go.microsoft.com/fwlink/?LinkID=191493).  
  
-   Extensibilidad del tipo de datos C. Para obtener más información, vea el tema sobre [tipos de datos C en ODBC](http://go.microsoft.com/fwlink/?LinkID=191495).  
  
     Para admitir esta característica en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, que puede devolver SQLGetDescField **SQL_C_SS_TIME2** (para **tiempo** tipos) o **SQL_C_SS_TIMESTAMPOFFSET** (para **datetimeoffset**) en lugar de **SQL_C_BINARY**, si su aplicación utiliza ODBC 3.8. Para obtener más información, consulte [compatibilidad de tipos de datos ODBC de fecha y hora mejoras](../../relational-databases/native-client-odbc-date-time/data-type-support-for-odbc-date-and-time-improvements.md).  
  
-   Llamada varias veces a **SQLGetData** con un búfer pequeño para recuperar un valor de parámetro grande. Para obtener más información, vea el tema que trata sobre [recuperar parámetros de salida mediante SQLGetData](http://go.microsoft.com/fwlink/?LinkID=191494).  
  
 En los siguientes temas se describen los cambios de comportamiento de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
-   Al llamar a **ICommandWithParameters::SetParameterInfo**, el valor pasado al parámetro *pwszName* debe ser un identificador válido. Para obtener más información, consulte [ICommandWithParameters](../../relational-databases/native-client-ole-db-interfaces/icommandwithparameters.md).  
  
-   **SQLDescribeParam** devolverá de forma coherente un valor que cumplan el estándar de especificación de ODBC. Para obtener más información, consulte [SQLDescribeParam](../../relational-databases/native-client-odbc-api/sqldescribeparam.md).  
  
-   [Cambio de comportamiento del controlador ODBC al administrar las conversiones de caracteres](../../relational-databases/native-client/features/odbc-driver-behavior-change-when-handling-character-conversions.md)  
  
## <a name="see-also"></a>Vea también  
[Instale SQL Server Native Client](../../relational-databases/native-client/applications/installing-sql-server-native-client.md)  
 [Características de SQL Server Native Client](../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
