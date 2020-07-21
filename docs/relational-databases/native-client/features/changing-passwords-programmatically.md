---
title: Cambio de las contraseñas mediante programación | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.reviewer: ''
ms.prod: sql
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- data access [SQL Server Native Client], password expiration
- SQL Server Native Client ODBC driver, passwords
- SQL Server Native Client OLE DB provider, passwords
- passwords [SQL Server], expiration
- SQLNCLI, password expiration
- expiration [SQL Server Native Client]
- passwords [SQL Server], modifying
- expired passwords [SQL Server Native Client]
- SQL Server Native Client, password expiration
- modifying passwords
ms.assetid: 624ad949-5fed-4ce5-b319-878549f9487b
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0648fda674a0dba83ae4560fa3744e3c1b1430dc
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "86009082"
---
# <a name="changing-passwords-programmatically"></a>Cambiar las contraseñas mediante programación
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  En versiones anteriores de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], cuando expiraba una contraseña de usuario, solo el administrador podía restablecerla. A partir de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] , [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client admite la administración de la expiración de contraseña mediante programación a través del [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client y del [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client, y a través de los cambios en los cuadros de diálogo **SQL Server inicio de sesión** .  
  
> [!NOTE]  
>  Cuando sea posible, solicite a los usuarios que escriban las credenciales en tiempo de ejecución y eviten almacenarlas en un formato guardado. Si tiene que conservar las credenciales, debe cifrarlas con la [API de cifrado de Win32](https://go.microsoft.com/fwlink/?LinkId=64532). Para obtener más información sobre el uso de contraseñas seguras, vea [Contraseñas seguras](../../../relational-databases/security/strong-passwords.md).  
  
## <a name="sql-server-login-error-codes"></a>Códigos de error de inicio de sesión de SQL Server  
 Cuando no se puede realizar una conexión debido a problemas de autenticación, uno de los códigos de error de SQL Server siguientes estará disponible para la aplicación para ayudar en el diagnóstico y recuperación.  
  
|Código de error de SQL Server|Mensaje de error|  
|---------------------------|-------------------|  
|15113|Error de inicio de sesión del usuario '%. * ls'. Motivo: error de validación de contraseña. Se ha bloqueado la cuenta.|  
|18463|Error de inicio de sesión del usuario '%.*ls'. Motivo: error de cambio de contraseña. La contraseña no se puede utilizar en este momento.|  
|18464|Error de inicio de sesión del usuario '%.*ls'. Motivo: error de cambio de contraseña. La contraseña no cumple los requisitos de directiva porque es demasiado larga.|  
|18465|Error de inicio de sesión del usuario '%.*ls'. Motivo: error de cambio de contraseña. La contraseña no cumple los requisitos de directiva porque es demasiado larga.|  
|18466|Error de inicio de sesión del usuario '%.*ls'. Motivo: error de cambio de contraseña. La contraseña no cumple los requisitos de directiva porque no es bastante compleja.|  
|18467|Error de inicio de sesión del usuario '%.*ls'. Motivo: error de cambio de contraseña. La contraseña no cumple los requisitos de la DLL de filtro de contraseña.|  
|18468|Error de inicio de sesión del usuario '%.*ls'. Motivo: error de cambio de contraseña. Error inesperado durante la validación de la contraseña.|  
|18487|Error de inicio de sesión del usuario '%.*ls'. Motivo: la contraseña de la cuenta expiró.|  
|18488|Error de inicio de sesión del usuario '%.*ls'. Motivo: se debe cambiar la contraseña de la cuenta. |  
  
## <a name="sql-server-native-client-ole-db-provider"></a>Proveedor OLE DB de SQL Server Native Client  
 El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client admite la expiración de la contraseña a través de una interfaz de usuario y mediante programación.  
  
### <a name="ole-db-user-interface-password-expiration"></a>Expiración de contraseñas de la interfaz de usuario de OLE DB  
 El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client admite la expiración de la contraseña a través de los cambios realizados en los cuadros de diálogo **SQL Server inicio de sesión** . Si el valor de DBPROP_INIT_PROMPT está establecido en DBPROMPT_NOPROMPT, se producirá un error en el intento de conexión inicial si la contraseña ha expirado.  
  
 Si DBPROP_INIT_PROMPT se ha establecido en cualquier otro valor, el usuario ve el cuadro de diálogo **Inicio de sesión de SQL Server**, independientemente de que la contraseña haya expirado o no. El usuario puede hacer clic en el botón **Opciones** y seleccionar **Cambiar contraseña** para cambiar la contraseña.  
  
 Si el usuario hace clic en Aceptar y la contraseña ha expirado, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pedirá al usuario que escriba y confirme una nueva contraseña mediante el cuadro de diálogo **Cambiar contraseña de SQL Server**.  
  
#### <a name="ole-db-prompt-behavior-and-locked-accounts"></a>Comportamiento de las solicitudes de OLE DB y cuentas bloqueadas  
 Los intentos de conexión pueden producir un error debido a que la cuenta está bloqueada. Si se produce esto después de la presentación del cuadro de diálogo **Inicio de sesión de SQL Server**, se muestra un mensaje de error del servidor al usuario y se anula el intento de conexión. Se puede producir también después de la presentación del cuadro de diálogo **Cambiar contraseña de SQL Server** si el usuario especifica un valor incorrecto de la contraseña anterior. En este caso se muestra el mismo mensaje de error y se anula el intento de conexión.  
  
#### <a name="ole-db-connection-pooling-password-expiration-and-locked-accounts"></a>Agrupación de conexiones de OLE DB, expiración de contraseña y cuentas bloqueadas  
 Se puede bloquear una cuenta o puede expirar la contraseña cuando la conexión está activa todavía en un grupo de conexiones. El servidor comprueba las contraseñas expiradas y las cuentas bloqueadas en dos ocasiones. La primera vez es cuando se crea una conexión. La segunda ocasión es al restablecer una conexión, cuando se toma la conexión del grupo.  
  
 Cuando se produce un error en el intento de reinicio, la conexión se quita del grupo y se devuelve un error.  
  
### <a name="ole-db-programmatic-password-expiration"></a>Expiración de contraseña mediante programación de OLE DB  
 El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client admite la expiración de la contraseña mediante la adición de la propiedad SSPROP_AUTH_OLD_PASSWORD (tipo VT_BSTR) que se ha agregado al conjunto de propiedades DBPROPSET_SQLSERVERDBINIT.  
  
 La propiedad "Contraseña" existente hace referencia a DBPROP_AUTH_PASSWORD y se utiliza para almacenar la nueva contraseña.  
  
> [!NOTE]  
>  En la cadena de conexión, la propiedad "Contraseña anterior" establece SSPROP_AUTH_OLD_PASSWORD, que es la contraseña actual (posiblemente expirada) que no está disponible a través de una propiedad de cadena del proveedor.  
  
 El proveedor no conserva el valor de esta propiedad. Cuando se establece esta propiedad, el proveedor no utiliza el grupo de conexiones para la primera conexión porque se producirá una nueva conexión. Si el cambio de contraseña se realiza correctamente, no se puede reutilizar la conexión actual dado que todavía contiene la contraseña anterior, que no será válida después del cambio de contraseña. Además, si el inicio de sesión tiene éxito, el proveedor borra esta propiedad. Los intentos subsiguientes de recuperar la contraseña anterior devuelven VT_EMPTY.  
  
> [!NOTE]  
>  No se debe conservar SSPROP_AUTH_OLD_PASSWORD nunca porque solo se utiliza cuando una contraseña ha expirado.  
  
 Recuerde que siempre que se establece la propiedad "Contraseña anterior", el proveedor asume que intenta cambiar la contraseña, a menos que se especifique también la Autenticación de Windows, en cuyo caso tiene siempre prioridad.  
  
 Si se usa la autenticación de Windows, especificar la contraseña anterior da como resultado DB_E_ERRORSOCCURRED o DB_S_ERRORSOCCURRED en función de que la contraseña anterior se haya especificado como REQUIRED u OPTIONAL respectivamente, y se devuelve el valor de estado de DBPROPSTATUS_CONFLICTINGBADVALUE en *dwStatus*. Esto se detecta cuando se llama a **IDBInitialize::Initialize**.  
  
 Si el intento de cambiar la contraseña produce un error inesperadamente, el servidor devuelve el código de error 18468. Se devuelve un error OLEDB estándar del intento de conexión.  
  
 Para más información sobre el conjunto de propiedades DBPROPSET_SQLSERVERDBINIT, consulte [Propiedades de inicialización y autorización](../../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md).  
  
## <a name="sql-server-native-client-odbc-driver"></a>Controlador ODBC de SQL Server Native Client  
 El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client admite la expiración de la contraseña a través de una interfaz de usuario y mediante programación.  
  
### <a name="odbc-user-interface-password-expiration"></a>Expiración de contraseñas de la interfaz de usuario de ODBC  
 El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client admite la expiración de la contraseña a través de los cambios realizados en los cuadros de diálogo de **Inicio de sesión SQL Server** .  
  
 Si se llama a [SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md) y el valor de **DriverCompletion** se establece en SQL_DRIVER_NOPROMPT, se produce un error en el intento de conexión inicial si la contraseña ha expirado. Las llamadas posteriores a **SQLError** o **SQLGetDiagRec**devuelven el valor de SQLSTATE 28000 y el valor de código de error nativo 18487.  
  
 Si **DriverCompletion** se ha establecido en cualquier otro valor, el usuario verá el **SQL Server** cuadro de diálogo de inicio de sesión, independientemente de si la contraseña ha expirado o no. El usuario puede hacer clic en el botón **Opciones** y seleccionar **Cambiar contraseña** para cambiar la contraseña.  
  
 Si el usuario hace clic en aceptar y la contraseña ha expirado, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] le pedirá que escriba y confirme una nueva contraseña mediante el cuadro de diálogo **Cambiar contraseña de SQL Server** .  
  
#### <a name="odbc-prompt-behavior-and-locked-accounts"></a>Comportamiento de las solicitudes de ODBC y cuentas bloqueadas  
 Los intentos de conexión pueden producir un error debido a que la cuenta está bloqueada. Si se produce esto después de la presentación del cuadro de diálogo **Inicio de sesión de SQL Server**, se muestra un mensaje de error del servidor al usuario y se anula el intento de conexión. Se puede producir también después de la presentación del cuadro de diálogo **Cambiar contraseña de SQL Server** si el usuario especifica un valor incorrecto de la contraseña anterior. En este caso se muestra el mismo mensaje de error y se anula el intento de conexión.  
  
#### <a name="odbc-connection-pooling-password-expiry-and-locked-accounts"></a>Expiración de la agrupación de conexiones de ODBC y cuentas bloqueadas  
 Se puede bloquear una cuenta o puede expirar la contraseña cuando la conexión está activa todavía en un grupo de conexiones. El servidor comprueba las contraseñas expiradas y las cuentas bloqueadas en dos ocasiones. La primera vez es cuando se crea una conexión. La segunda ocasión es al restablecer una conexión, cuando se toma la conexión del grupo.  
  
 Cuando se produce un error en el intento de reinicio, la conexión se quita del grupo y se devuelve un error.  
  
### <a name="odbc-programmatic-password-expiration"></a>Expiración de contraseña mediante programación de ODBC  
 El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client admite la expiración de la contraseña mediante la adición del atributo SQL_COPT_SS_OLDPWD que se establece antes de conectarse al servidor mediante la función [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) .  
  
 El atributo SQL_COPT_SS_OLDPWD del identificador de conexión hace referencia a la contraseña expirada. No hay ningún atributo de cadena de conexión para este atributo, porque esto interferiría con la agrupación de conexiones. Si el inicio de sesión tiene éxito, el controlador borra este atributo.  
  
 El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client devuelve SQL_ERROR en cuatro casos para esta característica: la expiración de contraseñas, el conflicto de la Directiva de contraseñas, el bloqueo de cuentas y el momento en que se establece la propiedad contraseña antigua mientras se usa la autenticación de Windows. El controlador devuelve los mensajes de error correspondientes al usuario cuando se invoca [SQLGetDiagField](../../../relational-databases/native-client-odbc-api/sqlgetdiagfield.md) .  
  
## <a name="see-also"></a>Consulte también  
 [Características de SQL Server Native Client](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
