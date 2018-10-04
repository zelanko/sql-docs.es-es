---
title: ¿Qué&#39;s nuevo en SQL Server Native Client | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: e4d4fe39-0090-42a7-8405-6378370d11cb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 68acf1991e3d1b5af44f6335f59635fcc1eacefc
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48144525"
---
# <a name="what39s-new-in-sql-server-native-client"></a>¿Qué&#39;s nuevo en SQL Server Native Client
  [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] instala [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Native Client. No hay ningún [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Native Client.  
  
 No habrá más actualizaciones para el controlador ODBC en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. El sucesor para el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, que se denomina Controlador ODBC 11 de [!INCLUDE[msCoName](../../includes/msconame-md.md)] para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de Windows, se instala con [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]. Para obtener más información sobre la [!INCLUDE[msCoName](../../includes/msconame-md.md)] ODBC Driver 11 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en Windows, consulte [Microsoft ODBC Driver 11 for SQL Server: Windows](http://www.microsoft.com/download/details.aspx?id=36434).  
  
 El proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client se actualizó por última vez en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Native Client. Los desarrolladores que deseen usar un proveedor OLE DB para conectarse a la versión más reciente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deben usar el proveedor OLE DB incluido en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Native Client.  
  
 En los temas siguientes se describen las características nuevas más importantes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
-   [Compatibilidad de SQL Server Native Client con LocalDB](features/sql-server-native-client-support-for-localdb.md)  
  
-   [Detección de metadatos](features/metadata-discovery.md)  
  
-   [Compatibilidad con UTF-16 en SQL Server Native Client 11.0](features/utf-16-support-in-sql-server-native-client-11-0.md)  
  
-   [Compatibilidad de SQL Server Native Client para la alta disponibilidad con recuperación de desastres](features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  
  
-   [Obtener acceso a información de diagnóstico en el registro de eventos extendidos](features/accessing-diagnostic-information-in-the-extended-events-log.md)  
  
 Además, ODBC en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client admite ahora tres características que se agregaron a ODBC estándar en el SDK de Windows 7:  
  
-   Ejecución asincrónica en operaciones relacionadas con conexión. Para obtener más información, vea el tema que trata sobre [ejecución asincrónica](http://go.microsoft.com/fwlink/?LinkID=191493).  
  
-   Extensibilidad del tipo de datos C. Para obtener más información, vea el tema sobre [tipos de datos C en ODBC](http://go.microsoft.com/fwlink/?LinkID=191495).  
  
     Para admitir esta característica en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, que puede devolver SQLGetDescField `SQL_C_SS_TIME2` (para `time` tipos) o `SQL_C_SS_TIMESTAMPOFFSET` (para `datetimeoffset`) en lugar de `SQL_C_BINARY`, si su aplicación utiliza ODBC 3.8. Para obtener más información, consulte [compatibilidad con tipos de datos de ODBC mejoras de fecha y hora](features/date-and-time-improvements.md).  
  
-   Llamada varias veces a `SQLGetData` con un búfer pequeño para recuperar un valor de parámetro grande. Para obtener más información, vea el tema que trata sobre [recuperar parámetros de salida mediante SQLGetData](http://go.microsoft.com/fwlink/?LinkID=191494).  
  
 En los siguientes temas se describen los cambios de comportamiento de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
-   Al llamar a `ICommandWithParameters::SetParameterInfo`, el valor pasado a la *pwszName* parámetro debe ser un identificador válido. Para obtener más información, consulte [ICommandWithParameters](../native-client-ole-db-interfaces/icommandwithparameters.md).  
  
-   `SQLDescribeParam` devolverá ahora de forma coherente un valor que cumple con la especificación de ODBC. Para obtener más información, consulte [SQLDescribeParam](../native-client-odbc-api/sqldescribeparam.md).  
  
-   [Cambio de comportamiento del controlador ODBC al administrar las conversiones de caracteres](features/odbc-driver-behavior-change-when-handling-character-conversions.md)  
  
## <a name="see-also"></a>Vea también  
 [Características de SQL Server Native Client](features/sql-server-native-client-features.md)  
  
  
