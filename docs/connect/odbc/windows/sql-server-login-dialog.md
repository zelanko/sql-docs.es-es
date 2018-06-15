---
title: Cuadro de diálogo de inicio de sesión SQL Server (ODBC) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/21/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
caps.latest.revision: 22
author: MightyPen
ms.author: v-jizho2
manager: craigg
ms.openlocfilehash: 3dcd7f9d5d3807858ae13a9ded3a2164eca20b45
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32855360"
---
# <a name="sql-server-login-dialog-box-odbc"></a>Cuadro de diálogo Inicio de sesión de SQL Server (ODBC)

Cuando se llama a una conexión ODBC sin especificar suficiente información para que el controlador para conectarse a SQL Server, el controlador ODBC se muestra la **el inicio de sesión de SQL Server** cuadro de diálogo.

## <a name="options"></a>Opciones

### <a name="server"></a>Server

El nombre de una instancia de SQL Server en la red. Seleccione un servidor o nombre de la lista o escriba el nombre del servidor en el **Server** cuadro. Si lo desea, puede crear un alias de servidor en el equipo cliente con **Administrador de configuración de SQL Server**y escriba ese nombre en el **Server** cuadro.

Puede escribir "(local)" cuando se usa el mismo equipo que SQL Server. A continuación, puede conectarse a una instancia local de SQL Server, incluso cuando se ejecuta una versión de SQL Server no está en la red.

Para obtener más información acerca de los nombres de servidor para diferentes tipos de redes, consulte la documentación de instalación de SQL Server en los libros en pantalla de SQL Server.

### <a name="authentication-mode"></a>Modo de autenticación

Selecciona el modo de autenticación de uno de los siguientes:
- **SQL Server** con Id. de inicio de sesión y contraseña
- **Integrada de Windows** autenticación mediante la cuenta de usuario que ha iniciado la sesión actual
- **Contraseña de Active Directory** con Id. de inicio de sesión y contraseña
- **Active Directory integrado** autenticación mediante la cuenta de usuario que ha iniciado la sesión actual
- **Active Directory interactivo** autenticación con el Id. de inicio de sesión

Vea [Asistente pantalla 2 de origen de datos](../../../connect/odbc/windows/dsn-wizard-2.md) para obtener más información sobre los modos de autenticación.

### <a name="server-spn"></a>Dirección SPN del servidor

Si utiliza una conexión de confianza, puede especificar un nombre principal de servicio (SPN) para el servidor.

### <a name="login-id"></a>Id. de inicio de sesión

Especifica el identificador de inicio de sesión de SQL Server o Azure Active Directory que se usará para la conexión si **modo de autenticación** está establecido en **SQL Server** o **contraseña de Active Directory** o **Interactivo de active Directory**. En caso contrario, el **Id. de inicio de sesión** casilla está deshabilitada.

### <a name="password"></a>Contraseña

Especifica la contraseña para el identificador de inicio de sesión de SQL Server o Azure Active Directory utilizado para la conexión si **modo de autenticación** está establecido en **SQL Server** o **decontraseñadeActiveDirectory**. En caso contrario, el **contraseña** casilla está deshabilitada.

### <a name="options"></a>Opciones

Muestra u oculta el **opciones** grupo. El **opciones** botón se habilita si **Server** tiene un valor.

### <a name="change-password"></a>Cambio de contraseñas

Cuando esta casilla está activada, se muestra la **nueva contraseña** y **Confirmar nueva contraseña** cuadros.

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

### <a name="language"></a>Lenguaje

Especifica el idioma nacional que se utilizará para los mensajes de sistema de SQL Server. El equipo que ejecuta SQL Server debe tener el idioma instalado. Este valor invalida el idioma predeterminado especificado para el inicio de sesión en el servidor. Si no se especifica ningún idioma, la conexión utiliza el idioma predeterminado especificado para el inicio de sesión en el servidor.

### <a name="application-name"></a>Application Name

(Opcional) Especifica el nombre de la aplicación que se almacenará en la **program_name** columna en la fila para esta conexión en **sys.sysprocesses**.

### <a name="workstation-id"></a>Id. de estación de trabajo

(Opcional) Especifica el identificador de estación de trabajo que se almacenará en la **hostname** columna en la fila para esta conexión en **sys.sysprocesses**.

### <a name="use-strong-encryption-for-data"></a>Utilizar cifrado de alta seguridad para los datos

Cuando se selecciona, se cifrarán los datos que se pasan a través de la conexión. De forma predeterminada los inicios de sesión se cifran, aun cuando la casilla esté desactivada.

### <a name="trust-server-certificate"></a>Confiar en certificado de servidor

Esta opción solo es aplicable cuando **utilizar cifrado de alta seguridad para los datos** está habilitado. Cuando se selecciona, no se validará el certificado del servidor para que el nombre del host correcto del servidor y ser emitido por una entidad de certificación de confianza.

## <a name="see-also"></a>Vea también

[Microsoft ODBC Driver for SQL Server en Windows](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)
