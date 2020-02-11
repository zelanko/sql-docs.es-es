---
title: SQLDriverConnect | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLDriverConnect function
ms.assetid: a1e38e2c-3a97-42d1-9c45-a0ca3282ffd1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 22d560c8a65d5b9a7cebc4062ddd2d1ce936d5a2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63067751"
---
# <a name="sqldriverconnect"></a>SQLDriverConnect
  El controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client define atributos de conexión que o reemplazan o mejoran las palabras clave de cadena de conexión. Algunas palabras clave de cadena de conexión tienen valores predeterminados que especifica el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
 Para obtener una lista de las palabras clave disponibles [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el controlador ODBC de Native Client, vea [usar palabras clave de cadena de conexión con SQL Server Native Client](../native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 Para obtener más información [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] acerca de los atributos de conexión y los comportamientos predeterminados del controlador, consulte [SQLSetConnectAttr](sqlsetconnectattr.md).  
  
 Para obtener una descripción de las palabras clave de cadena de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conexión que son válidas para Native Client, vea [usar palabras clave de cadena de conexión con SQL Server Native Client](../native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 Cuando el `SQLDriverConnect`valor del parámetro *DriverCompletion* es SQL_DRIVER_PROMPT, SQL_DRIVER_COMPLETE o SQL_DRIVER_COMPLETE_REQUIRED, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client recupera los valores de palabra clave del cuadro de diálogo que se muestra. Si el valor de palabra clave se pasa en la cadena de conexión y el usuario no modifica el valor de la palabra clave en el cuadro de diálogo, el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client utiliza el valor de la cadena de conexión. Si el valor no está establecido en la cadena de conexión y el usuario no realiza ninguna asignación en el cuadro de diálogo, el controlador utiliza el valor predeterminado.  
  
 `SQLDriverConnect`se debe proporcionar un *WindowHandle* válido cuando cualquier valor de *DriverCompletion* requiere (o podría requerir) la presentación del cuadro de diálogo de conexión del controlador. Un identificador no válido devuelve SQL_ERROR.  
  
 Especifique las palabras clave DRIVER o DSN. Si se indican ambas, ODBC especifica que un controlador utiliza la palabra clave del extremo izquierdo y omite la otra. Si se especifica el controlador, o es el extremo izquierdo de los dos, `SQLDriverConnect`y el valor del parámetro *DriverCompletion* es SQL_DRIVER_NOPROMPT, se requiere la palabra clave Server y un valor adecuado.  
  
 Cuando se especifica SQL_DRIVER_NOPROMPT, las palabras clave de autenticación de usuario deben estar presentes con valores. El controlador garantiza que la cadena "Trusted_Connection=yes" o que las palabras clave UID y PWD están presentes.  
  
 Si el valor del parámetro *DriverCompletion* es SQL_DRIVER_NOPROMPT o SQL_DRIVER_COMPLETE_REQUIRED y el lenguaje o la base de datos proceden de la cadena de `SQLDriverConnect` conexión y no son válidos, devuelve SQL_ERROR.  
  
 Si el valor del parámetro *DriverCompletion* es SQL_DRIVER_NOPROMPT o SQL_DRIVER_COMPLETE_REQUIRED y el lenguaje o la base de datos proceden de las definiciones de origen de `SQLDriverConnect` datos ODBC y no son válidos, utiliza el idioma o la base de datos predeterminados para el ID. de usuario especificado y devuelve SQL_SUCCESS_WITH_INFO.  
  
 Si el valor del parámetro *DriverCompletion* es SQL_DRIVER_COMPLETE o SQL_DRIVER_PROMPT y si el idioma o la base de `SQLDriverConnect` datos no son válidos, vuelve a mostrar el cuadro de diálogo.  
  
## <a name="sqldriverconnect-support-for-high-availability-disaster-recovery"></a>Compatibilidad de SQLDriverConnect para la alta disponibilidad con recuperación de desastres  
 Para obtener más información sobre `SQLDriverConnect` el uso de para [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] conectarse a un clúster, consulte [SQL Server Native Client compatibilidad con la alta disponibilidad y la recuperación ante desastres](../native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md).  
  
## <a name="sqldriverconnect-support-for-service-principal-names-spns"></a>Compatibilidad de SQLDriverConnect con los Nombres principales de servicio (SPN)  
 SQLDDriverConnect utilizará el cuadro de diálogo Inicio de sesión ODBC boxwhen se habilitará la solicitud. Esto permite escribir SPN tanto para el servidor principal como para su asociado de conmutación por error.  
  
 SQLDriverConnect aceptará las nuevas palabras clave `ServerSPN` de cadena `FailoverPartnerSPN`de conexión y, y reconocerá los nuevos atributos de conexión SQL_COPT_SS_SERVER_SPN y SQL_COPT_SS_FAILOVER_PARTNER_SPN.  
  
 Cuando un valor de atributo de conexión se especifica más de una vez, el valor que se establece mediante programación tiene prioridad sobre el valor de un DSN y el valor de una cadena de conexión. El valor de un DSN tiene prioridad sobre el valor de una cadena de conexión.  
  
 Cuando se abre una conexión, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client establece SQL_COPT_SS_MUTUALLY_AUTHENTICATED y SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD en el método de autenticación que se utiliza para abrir la conexión.  
  
 Para obtener más información acerca de los SPN, consulte [nombres de entidad de seguridad de servicio &#40;spn&#41; en conexiones de cliente &#40;&#41;ODBC ](../native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md).  
  
## <a name="examples"></a>Ejemplos  
 La siguiente llamada ilustra la cantidad mínima de datos necesarios para `SQLDriverConnect`:  
  
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
  
## <a name="see-also"></a>Consulte también  
 [SQLDriverConnect, función](https://go.microsoft.com/fwlink/?LinkId=59340)   
 [Detalles de implementación de la API de ODBC](odbc-api-implementation-details.md)   
 [SET ANSI_NULLS &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-nulls-transact-sql)   
 [SET ANSI_PADDING &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-padding-transact-sql)   
 [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-warnings-transact-sql)  
  
  
