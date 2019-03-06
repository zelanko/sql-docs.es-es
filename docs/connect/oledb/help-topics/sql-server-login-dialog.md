---
title: Cuadro de diálogo de inicio de sesión SQL Server (OLE DB) | Microsoft Docs
description: Uso del cuadro de diálogo de inicio de sesión de SQL Server
ms.custom: ''
ms.date: 01/21/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.author: v-beaziz
author: bazizi
ms.openlocfilehash: 4735ead33dc7c3a6d633e3b23ff1da97eeae4962
ms.sourcegitcommit: 958cffe9288cfe281280544b763c542ca4025684
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 02/23/2019
ms.locfileid: "56744877"
---
# <a name="sql-server-login-dialog-box"></a>Cuadro de diálogo de inicio de sesión de SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

Cuando intenta conectarse sin especificar suficiente información, el controlador OLE DB muestra el **el inicio de sesión de SQL Server** cuadro de diálogo.

> [!NOTE]  
> Diálogo de inicio de sesión de SQL Server comportamiento se controla mediante el `DBPROP_INIT_PROMPT` propiedad de inicialización. Para obtener más información, vea:
> - [Propiedades de inicialización y autorización](../ole-db-data-source-objects/initialization-and-authorization-properties.md)
> - [Guía del programador OLE DB](https://go.microsoft.com/fwlink/?linkid=2067702)

![Captura de pantalla del cuadro de diálogo de inicio de sesión SQL Server](../media/sql-server-login-dialog.png)

## <a name="options"></a>Opciones
|Opción|Descripción|
|---   |---        |
|Servidor|El nombre de una instancia de SQL Server en la red. Seleccione un nombre de servidor\instancia de la lista, o escriba el nombre de servidor\instancia en el cuadro **Servidor**. Opcionalmente, se puede crear un alias de servidor en el equipo cliente mediante el **Administrador de configuración de SQL Server** y escribir ese nombre en el cuadro **Servidor**. <br/><br/>Puede escribir "(local)" si está utilizando el mismo equipo que SQL Server. Después puede establecer conexión con una instancia local de SQL Server, incluso si ejecuta una versión que no está en red de SQL Server.<br/><br/>Para obtener más información acerca de los nombres de servidor para los distintos tipos de redes, consulte [instalación de SQL Server](https://go.microsoft.com/fwlink/?linkid=2067541).|
|Modo de autenticación|Puede seleccionar las opciones de autenticación siguientes en la lista desplegable:<br/><ul><li>`Windows Authentication:` Autenticación de SQL Server con las credenciales de cuenta de Windows del usuario que ha iniciado sesión actualmente.</li><li>`SQL Server Authentication:` Autenticación de SQL Server mediante el identificador de inicio de sesión y la contraseña.</li><li>`Active Directory - Integrated:` Autenticación integrada con las credenciales de cuenta de Windows del usuario que ha iniciado sesión actualmente.</li><li>`Active Directory - Password:` Autenticación de Active Directory con Id. de inicio de sesión y la contraseña.</li></ul>|
|Dirección SPN del servidor|Si utiliza una conexión de confianza, puede especificar un nombre principal de servicio (SPN) para el servidor.|
|Id. de inicio de sesión|Especifica el identificador de inicio de sesión que se usará para la conexión. El cuadro de texto Id. de inicio de sesión está habilitado sólo si `Authentication Mode` está establecido en `SQL Server Authentication` o `Active Directory - Password`.|
|Contraseña|Especifica la contraseña utilizada para la conexión. El cuadro de texto de contraseña solo está habilitado si `Authentication Mode` está establecido en `SQL Server Authentication` o `Active Directory - Password`.|
|Opciones|Muestra u oculta el grupo **Opciones**. El botón **Opciones** está habilitado si hay un valor en **Servidor**.|
|Cambio de contraseñas|Cuando está activada, permite **nueva contraseña** y **Confirmar nueva contraseña** cuadros de texto.|
|Contraseña nueva|Especifica la nueva contraseña.|
|Confirmar nueva contraseña|Especifica la nueva contraseña por segunda vez para la confirmación.|
|Base de datos|Seleccione o escriba la base de datos predeterminada que se va a utilizar en la conexión. Este valor invalida la base de datos predeterminada especificada para el inicio de sesión en el servidor. Si no se especifica ninguna base de datos, la conexión utiliza la base de datos predeterminada especificada para el inicio de sesión en el servidor.|
|Servidor reflejado|Especifica el nombre del asociado de conmutación por error de la base de datos que se va a reflejar.|
|SPN del servidor reflejado|Opcionalmente, puede especificar un SPN para el servidor reflejado. El SPN para el servidor reflejado se utiliza para la autenticación mutua entre cliente y servidor.|
|Idioma|Especifica el idioma nacional que se va a utilizar para los mensajes de sistema de SQL Server. El equipo que ejecuta SQL Server debe tener instalado el idioma. Este valor invalida el idioma predeterminado especificado para el inicio de sesión en el servidor. Si no se especifica ningún idioma, la conexión utiliza el idioma predeterminado especificado para el inicio de sesión en el servidor.|
|Application Name|Especifica el nombre de aplicación que se va a almacenar en la columna **program_name** de la fila para esta conexión en **sys.sysprocesses**.|
|Id. de estación de trabajo|Especifica el identificador de la estación de trabajo que se va a almacenar en la columna **hostname** de la fila para esta conexión en **sys.sysprocesses**.|
|Utilizar cifrado de alta seguridad para los datos|Cuando está activada, se cifrarán los datos que se pasan a través de la conexión.|
|Certificado de servidor de confianza|Cuando está activada, se validará el certificado del servidor. Certificado del servidor debe tener el nombre de host correcto del servidor y emitido por una entidad de certificación de confianza.|

> [!NOTE]  
> Cuando se usa `Windows Authentication` o `SQL Server Authentication` modos, **certificado de servidor de confianza** se considera solamente cuando el **utilizar cifrado de alta seguridad para datos** está habilitada.

## <a name="next-steps"></a>Pasos siguientes
- [Autenticarse en Azure Active Directory](../features/using-azure-active-directory.md) con el controlador de OLE DB.
- Información de conexión de conjunto con [Universal Data Link (UDL)](data-link-pages.md).