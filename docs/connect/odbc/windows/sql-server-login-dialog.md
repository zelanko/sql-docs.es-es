---
title: Cuadro de diálogo de inicio de sesión SQL Server (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/21/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
author: MightyPen
ms.author: v-jizho2
manager: craigg
ms.openlocfilehash: 58248a2772377ccecba0c701d03276025785c964
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47698063"
---
# <a name="sql-server-login-dialog-box-odbc"></a>Cuadro de diálogo Inicio de sesión de SQL Server (ODBC)

Al llamar a una conexión ODBC sin especificar suficiente información para que el controlador se conecte a un servidor SQL Server, el controlador ODBC muestra el cuadro de diálogo **Inicio de sesión de SQL Server**.

## <a name="options"></a>Opciones

### <a name="server"></a>Servidor

El nombre de una instancia de SQL Server en la red. Seleccione un nombre de servidor\instancia de la lista, o escriba el nombre de servidor\instancia en el cuadro **Servidor**. Opcionalmente, se puede crear un alias de servidor en el equipo cliente mediante el **Administrador de configuración de SQL Server** y escribir ese nombre en el cuadro **Servidor**.

Puede escribir "(local)" si está utilizando el mismo equipo que SQL Server. Después puede establecer conexión con una instancia local de SQL Server, incluso si ejecuta una versión que no está en red de SQL Server.

Para más información acerca de los nombres de servidor para diferentes tipos de redes, vea la documentación de la instalación de SQL Server en los Libros en pantalla de SQL Server.

### <a name="authentication-mode"></a>Modo de autenticación

Selecciona el modo de autenticación de uno de los siguientes:
- **SQL Server** con Id. de inicio de sesión y contraseña
- **Integrada de Windows** autenticación mediante la cuenta de usuario que ha iniciado sesión actualmente
- **Contraseña de Active Directory** con Id. de inicio de sesión y contraseña
- **Integrada en Active Directory** autenticación mediante la cuenta de usuario que ha iniciado sesión actualmente
- Autenticación **interactiva de Active Directory** con identificador de inicio de sesión

Consulte [Asistente pantalla 2 de origen de datos](../../../connect/odbc/windows/dsn-wizard-2.md) para obtener más información sobre los modos de autenticación.

### <a name="server-spn"></a>Dirección SPN del servidor

Si utiliza una conexión de confianza, puede especificar un nombre principal de servicio (SPN) para el servidor.

### <a name="login-id"></a>Id. de inicio de sesión

Especifica el identificador de inicio de sesión de SQL Server o Azure Active Directory que se usará para la conexión si **modo de autenticación** está establecido en **SQL Server** o **contraseña de Active Directory** o **Interactiva de active Directory**. En caso contrario, el **Id. de inicio de sesión** casilla está deshabilitada.

### <a name="password"></a>Contraseña

Especifica la contraseña para el identificador de inicio de sesión de SQL Server o Azure Active Directory utilizado para la conexión si **modo de autenticación** está establecido en **SQL Server** o **decontraseñadeActiveDirectory**. En caso contrario, el **contraseña** casilla está deshabilitada.

### <a name="options"></a>Opciones

Muestra u oculta el grupo **Opciones**. El botón **Opciones** está habilitado si hay un valor en **Servidor**.

### <a name="change-password"></a>Cambio de contraseñas

Cuando este cuadro está activado, se muestran los cuadros **Nueva contraseña** y **Confirmar nueva contraseña**.

### <a name="new-password"></a>Contraseña nueva

Especifica la nueva contraseña.

### <a name="confirm-new-password"></a>Confirmar nueva contraseña

Especifica la nueva contraseña por segunda vez para la confirmación.

### <a name="database"></a>Base de datos

Especifica la base de datos predeterminada que se va a utilizar en la conexión. Este valor invalida la base de datos predeterminada especificada para el inicio de sesión en el servidor. Si no se especifica ninguna base de datos, la conexión utiliza la base de datos predeterminada especificada para el inicio de sesión en el servidor.

### <a name="mirror-server"></a>Servidor reflejado

Especifica el nombre del asociado de conmutación por error de la base de datos que se va a reflejar.

### <a name="mirror-spn"></a>SPN del servidor reflejado

Opcionalmente, puede especificar un SPN para el servidor reflejado. El SPN para el servidor reflejado se utiliza para la autenticación mutua entre cliente y servidor.

### <a name="language"></a>Idioma

Especifica el idioma nacional que se va a utilizar para los mensajes de sistema de SQL Server. El equipo que ejecuta SQL Server debe tener instalado el idioma. Este valor invalida el idioma predeterminado especificado para el inicio de sesión en el servidor. Si no se especifica ningún idioma, la conexión utiliza el idioma predeterminado especificado para el inicio de sesión en el servidor.

### <a name="application-name"></a>Application Name

(Opcional) Especifica el nombre de aplicación que se va a almacenar en la columna **program_name** de la fila para esta conexión en **sys.sysprocesses**.

### <a name="workstation-id"></a>Id. de estación de trabajo

(Opcional) Especifica el identificador de la estación de trabajo que se va a almacenar en la columna **hostname** de la fila para esta conexión en **sys.sysprocesses**.

### <a name="use-strong-encryption-for-data"></a>Utilizar cifrado de alta seguridad para los datos

Cuando se selecciona, se cifrarán los datos que se pasan a través de la conexión. De forma predeterminada los inicios de sesión se cifran, aun cuando la casilla esté desactivada.

### <a name="trust-server-certificate"></a>Certificado de servidor de confianza

Esta opción solo es aplicable cuando **utilizar cifrado de alta seguridad para datos** está habilitado. Cuando se selecciona, no se validará el certificado del servidor para que el nombre de host correcto del servidor y ser emitido por una entidad de certificación de confianza.

## <a name="see-also"></a>Ver también

[Microsoft ODBC Driver for SQL Server en Windows](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)
