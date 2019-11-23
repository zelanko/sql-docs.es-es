---
title: SQLDriverConnect | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLDriverConnect function
ms.assetid: a1e38e2c-3a97-42d1-9c45-a0ca3282ffd1
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9a76a653277b7f99ecf88c3b0277617eb053a41c
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/07/2019
ms.locfileid: "73787096"
---
# <a name="sqldriverconnect"></a>SQLDriverConnect
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  El controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client define atributos de conexión que o reemplazan o mejoran las palabras clave de cadena de conexión. Algunas palabras clave de cadena de conexión tienen valores predeterminados que especifica el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
 Para obtener una lista de las palabras clave disponibles en el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, vea [usar palabras clave de cadena de conexión con SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 Para obtener más información acerca de los atributos de conexión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y los comportamientos predeterminados del controlador, consulte [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md).  
  
 Para obtener una descripción de las palabras clave de cadena de conexión válidas para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, vea [usar palabras clave de cadena de conexión con SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 Cuando el valor del parámetro **SQLDriverConnect**_DriverCompletion_ es SQL_DRIVER_PROMPT, SQL_DRIVER_COMPLETE o SQL_DRIVER_COMPLETE_REQUIRED, el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client recupera los valores de palabra clave del cuadro de diálogo que se muestra. Si el valor de palabra clave se pasa en la cadena de conexión y el usuario no modifica el valor de la palabra clave en el cuadro de diálogo, el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client utiliza el valor de la cadena de conexión. Si el valor no está establecido en la cadena de conexión y el usuario no realiza ninguna asignación en el cuadro de diálogo, el controlador utiliza el valor predeterminado.  
  
 Se debe proporcionar un *WindowHandle* válido a **SQLDriverConnect** cuando algún valor de *DriverCompletion* requiera (o podría requerir) la presentación del cuadro de diálogo de conexión del controlador. Un identificador no válido devuelve SQL_ERROR.  
  
 Especifique las palabras clave DRIVER o DSN. Si se indican ambas, ODBC especifica que un controlador utiliza la palabra clave del extremo izquierdo y omite la otra. Si se especifica el controlador, o es el izquierdo de los dos, y el valor del parámetro **SQLDriverConnect**_DriverCompletion_ es SQL_DRIVER_NOPROMPT, se requiere la palabra clave Server y un valor adecuado.  
  
 Cuando se especifica SQL_DRIVER_NOPROMPT, las palabras clave de autenticación de usuario deben estar presentes con valores. El controlador garantiza que la cadena "Trusted_Connection=yes" o que las palabras clave UID y PWD están presentes.  
  
 Si el valor del parámetro *DriverCompletion* es SQL_DRIVER_NOPROMPT o SQL_DRIVER_COMPLETE_REQUIRED y el lenguaje o la base de datos proceden de la cadena de conexión y no son válidos, **SQLDriverConnect** devuelve SQL_ERROR.  
  
 Si el valor del parámetro *DriverCompletion* es SQL_DRIVER_NOPROMPT o SQL_DRIVER_COMPLETE_REQUIRED y el lenguaje o la base de datos proceden de las definiciones de origen de datos ODBC y no son válidos, **SQLDriverConnect** utiliza el idioma o la base de datos predeterminados para el ID. de usuario especificado y devuelve SQL_SUCCESS_WITH_INFO.  
  
 Si el valor del parámetro *DriverCompletion* es SQL_DRIVER_COMPLETE o SQL_DRIVER_PROMPT y si el idioma o la base de datos no son válidos, **SQLDriverConnect** vuelve a mostrar el cuadro de diálogo.  
  
## <a name="sqldriverconnect-support-for-high-availability-disaster-recovery"></a>Compatibilidad de SQLDriverConnect para la alta disponibilidad con recuperación de desastres  
 Para obtener más información sobre el uso de **SQLDriverConnect** para conectarse a un [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] del clúster, consulte [Compatibilidad de SQL Server Native Client para la alta disponibilidad con recuperación de desastres](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md).  
  
## <a name="sqldriverconnect-support-for-service-principal-names-spns"></a>Compatibilidad de SQLDriverConnect con los Nombres principales de servicio (SPN)  
 SQLDDriverConnect utilizará el cuadro de diálogo Inicio de sesión ODBC boxwhen se habilitará la solicitud. Esto permite escribir SPN tanto para el servidor principal como para su asociado de conmutación por error.  
  
 SQLDriverConnect aceptará las nuevas palabras clave de cadena de conexión **ServerSPN** y **FailoverPartnerSPN**, y reconocerá los nuevos atributos de conexión SQL_COPT_SS_SERVER_SPN y SQL_COPT_SS_FAILOVER_PARTNER_SPN.  
  
 Cuando un valor de atributo de conexión se especifica más de una vez, el valor que se establece mediante programación tiene prioridad sobre el valor de un DSN y el valor de una cadena de conexión. El valor de un DSN tiene prioridad sobre el valor de una cadena de conexión.  
  
 Cuando se abre una conexión, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client establece SQL_COPT_SS_MUTUALLY_AUTHENTICATED y SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD en el método de autenticación que se utiliza para abrir la conexión.  
  
 Para obtener más información acerca de los SPN, consulte [ &#40;nombres&#41; de entidad de &#40;seguridad&#41;de servicio en conexiones de cliente ODBC](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md).  
  
## <a name="examples"></a>Ejemplos  
 La siguiente llamada ilustra la cantidad mínima de datos necesarios para **SQLDriverConnect**:  
  
```  
SQLDriverConnect(hdbc, hwnd,  
    (SQLTCHAR*) TEXT("DRIVER={SQL Server Native Client 10};"), SQL_NTS, szOutConn,  
    MAX_CONN_OUT, &cbOutConn, SQL_DRIVER_COMPLETE);  
```  
  
 Las cadenas de conexión siguientes ilustran los datos mínimos necesarios cuando el valor del parámetro *DriverCompletion* es SQL_DRIVER_NOPROMPT:  
  
```  
"DSN=Human Resources;Trusted_Connection=yes"  
  
"FILEDSN=HR_FDSN;Trusted_Connection=yes"  
  
"DRIVER={SQL Server Native Client 10};SERVER=(local);Trusted_Connection=yes"  
```  
  
## <a name="see-also"></a>Vea también  
 [SQLDriverConnect (función](https://go.microsoft.com/fwlink/?LinkId=59340) )   
 [Detalles de implementación](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md) de la API de ODBC   
 [SET ANSI_NULLS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md)   
 [SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)   
 [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md)  
  
  
