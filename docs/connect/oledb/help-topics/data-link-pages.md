---
title: Configuración de vínculo de datos universal (UDL) | Microsoft Docs
description: Configuración de vínculo de datos universal (UDL) mediante Microsoft OLE DB driver for SQL Server
ms.custom: ''
ms.date: 10/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.author: v-beaziz
author: bazizi
ms.openlocfilehash: d92555fba1d9e0a380ffdc9051817ddfae9ca4b7
ms.sourcegitcommit: 4c75b49599018124f05f91c1df3271d473827e4d
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/16/2019
ms.locfileid: "72381759"
---
# <a name="universal-data-link-udl-configuration"></a>Configuración de vínculo de datos universal (UDL)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

## <a name="connection-tab"></a>Pestaña conexión
Use la pestaña conexión para especificar cómo conectarse a los datos mediante el controlador de Microsoft OLE DB para SQL Server.

![Captura de pantalla de páginas de vínculo de datos OLE DB: pestaña conexión](../media/data-link-pages-connection-tab.png)

La pestaña Conexión es específica del proveedor y solo muestra las propiedades de conexión que requiere el controlador OLE DB de Microsoft para SQL Server.

|Opción|Descripción|
|---   |---        |
|Seleccionar o especificar un nombre de servidor|Seleccione un nombre de servidor en la lista desplegable o escriba la ubicación del servidor donde se encuentra la base de datos a la que desea obtener acceso. La selección de la base de datos en el servidor es una acción independiente. Actualice la lista haciendo clic en "Actualizar".
|Escriba la información para iniciar sesión en el servidor|Puede seleccionar las siguientes opciones de autenticación en esta lista desplegable: <ul><li>`Windows Authentication:` la autenticación en SQL Server mediante las credenciales de la cuenta de Windows del usuario que ha iniciado sesión actualmente.</li><li>`SQL Server Authentication:` la autenticación mediante el identificador de inicio de sesión y la contraseña.</li><li>`Active Directory - Integrated:` la autenticación integrada con una identidad de Azure Active Directory. Este modo también se puede usar para la autenticación de Windows en SQL Server.</li><li>`Active Directory - Password:` la autenticación de ID. de usuario y contraseña con una identidad de Azure Active Directory.</li><li>`Active Directory - Universal with MFA support:` la autenticación interactiva con una identidad de Azure Active Directory. Este modo es compatible con Azure multi-factor Authentication (MFA).</li></ul>|
|Dirección SPN del servidor|Si utiliza una conexión de confianza, puede especificar un nombre principal de servicio (SPN) para el servidor.|
|Nombre de usuario|Escriba el ID. de usuario que se usará para la autenticación al iniciar sesión en el origen de datos.|
|Contraseña|Escriba la contraseña que se utilizará para la autenticación al iniciar sesión en el origen de datos.|
|Contraseña en blanco|Cuando esta opción está activada, permite que el proveedor especificado use una contraseña en blanco en la cadena de conexión.|
|Permitir guardar la contraseña|Cuando esta opción está activada, permite guardar la contraseña con la cadena de conexión. La inclusión o no de la contraseña en la cadena de conexión depende de la funcionalidad de la aplicación que hace la llamada. <br/><br/>**NOTA:** La contraseña se devuelve y se guarda sin enmascarar ni cifrar.|
|Utilizar cifrado de alta seguridad para los datos|Cuando esta opción está activada, se cifrarán los datos que se pasan a través de la conexión.|
|Certificado de servidor de confianza|Cuando esta opción está activada, se validará el certificado del servidor. El certificado del servidor debe tener el nombre de host correcto del servidor y emitido por una entidad de certificación de confianza.|
|Seleccionar la base de datos|Seleccione o escriba el nombre de la base de datos a la que desea obtener acceso.|
|Adjuntar un archivo de base de datos como nombre de base de datos|Especifica el nombre del archivo principal de una base de datos que se puede adjuntar. Esta base de datos se adjunta y se utiliza como predeterminada para el origen de datos. En el primer cuadro de texto de esta sección, escriba el nombre de la base de datos que se utilizará para el archivo de base de datos adjunto.<br/><br/>Escriba la ruta de acceso completa al archivo de base de datos que se va a adjuntar en el cuadro de texto con la etiqueta `Using the filename`, o haga clic en el botón `...` para buscar el archivo de base de datos.|
|Cambio de contraseñas|Muestra el cuadro de diálogo Cambiar contraseña de SQL Server. |
|Probar conexión|Haga clic para intentar una conexión con el origen de datos especificado. Si se produce un error en la conexión, asegúrese de que la configuración es correcta. Por ejemplo, los errores ortográficos y la distinción entre mayúsculas y minúsculas pueden provocar que las conexiones no se puedan establecer.|

## <a name="advanced-tab"></a>Ficha Opciones avanzadas
Use la pestaña avanzadas para ver y establecer propiedades de inicialización adicionales.

![Captura de pantalla de páginas de vínculo de datos de OLE DB: pestaña avanzadas](../media/data-link-pages-advanced-tab.png)

|Opción|Descripción|
|---   |---        |
| Tiempo de espera de conexión | Especifica la cantidad de tiempo (en segundos) que el controlador de Microsoft OLE DB para SQL Server espera a que se complete la inicialización. Si se supera el tiempo de espera de la inicialización, se devuelve un error y no se crea la conexión.|


> [!NOTE]  
>  Para obtener más información general sobre la conexión de vínculos de datos, consulte [información general sobre la API de vínculo de datos](https://go.microsoft.com/fwlink/?linkid=2067432).

## <a name="next-steps"></a>Pasos siguientes
- [Autentique en Azure Active Directory](../features/using-azure-active-directory.md) mediante el controlador de OLE DB.

- [Solicite al usuario credenciales de autenticación](../help-topics/sql-server-login-dialog.md) mediante el controlador de OLE DB.