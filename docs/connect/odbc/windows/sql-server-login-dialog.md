---
title: Cuadro de diálogo SQL Server inicio de sesión (ODBC) | Microsoft Docs
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
ms.openlocfilehash: fcfde122b978fa1e77baa690a1f3e09417dab1c0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67989420"
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
- **SQL Server** con el identificador de inicio de sesión y la contraseña
- Autenticación **integrada de Windows** con la cuenta de usuario que ha iniciado sesión actualmente
- **Active Directory contraseña** con el identificador de inicio de sesión y la contraseña
- **Active Directory** la autenticación integrada mediante la cuenta de usuario que ha iniciado sesión actualmente
- Autenticación **interactiva de Active Directory** con identificador de inicio de sesión

Consulte la [pantalla del Asistente para orígenes de datos 2](../../../connect/odbc/windows/dsn-wizard-2.md) para obtener más información sobre los modos de autenticación.

### <a name="server-spn"></a>Dirección SPN del servidor

Si utiliza una conexión de confianza, puede especificar un nombre principal de servicio (SPN) para el servidor.

### <a name="login-id"></a>Id. de inicio de sesión

Especifica el SQL Server o Azure Active Directory identificador de inicio de sesión que se usará para la conexión si el **modo de autenticación** está establecido en **SQL Server** o **Active Directory contraseña** o **Active Directory Interactive**. De lo contrario, el cuadro ID. de **Inicio de sesión** está deshabilitado.

### <a name="password"></a>Contraseña

Especifica la contraseña para el SQL Server o Azure Active Directory identificador de inicio de sesión usado para la conexión si el **modo de autenticación** está establecido en **SQL Server** o **Active Directory contraseña**. De lo contrario, el cuadro **contraseña** estará deshabilitado.

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

Esta opción solo es aplicable cuando está habilitado el **uso de cifrado seguro para datos** . Cuando se selecciona, el certificado del servidor no se validará para tener el nombre de host correcto del servidor y debe ser emitido por una entidad de certificación de confianza.

## <a name="see-also"></a>Consulte también

[Microsoft ODBC Driver for SQL Server en Windows](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)
