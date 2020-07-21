---
title: Configuración de vínculo de datos universal (UDL) | Microsoft Docs
description: Configuración de vínculo de datos universal (UDL) mediante Microsoft OLE DB Driver for SQL Server
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
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "72381759"
---
# <a name="universal-data-link-udl-configuration"></a>Configuración de vínculo de datos universal (UDL)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

## <a name="connection-tab"></a>Pestaña Connection (Conexión)
Use la pestaña Conexión para especificar cómo conectarse a los datos mediante Microsoft OLE DB Driver for SQL Server.

![Captura de pantalla de páginas de vínculo de datos OLE DB: pestaña Conexión](../media/data-link-pages-connection-tab.png)

La pestaña Conexión es específica del proveedor y solo muestra las propiedades de conexión que requiere el controlador OLE DB de Microsoft para SQL Server.

|Opción|Descripción|
|---   |---        |
|Seleccionar o especificar un nombre de servidor|Seleccione un nombre de servidor en la lista desplegable o escriba la ubicación del servidor donde se encuentra la base de datos a la que desea obtener acceso. La selección de la base de datos en el servidor es una acción independiente. Actualice la lista haciendo clic en "Actualizar".
|Especificación de información para iniciar sesión en el servidor|Puede seleccionar las siguientes opciones de autenticación en esta lista desplegable: <ul><li>`Windows Authentication:` autenticación en SQL Server con las credenciales de la cuenta de Windows del usuario que ha iniciado sesión actualmente.</li><li>`SQL Server Authentication:` autenticación con el identificador y la contraseña de inicio de sesión.</li><li>`Active Directory - Integrated:` autenticación integrada con una identidad de Azure Active Directory. Este modo también se puede usar para la autenticación de Windows en SQL Server.</li><li>`Active Directory - Password:` autenticación de identificador de usuario y contraseña con una identidad de Azure Active Directory.</li><li>`Active Directory - Universal with MFA support:` autenticación interactiva con una identidad de Azure Active Directory. Este modo admite Microsoft Azure Multi-Factor Authentication (MFA).</li></ul>|
|Dirección SPN del servidor|Si utiliza una conexión de confianza, puede especificar un nombre principal de servicio (SPN) para el servidor.|
|Nombre de usuario|Escriba el identificador de usuario que se usará en la autenticación al iniciar sesión en el origen de datos.|
|Contraseña|Escriba la contraseña que se utilizará en la autenticación al iniciar sesión en el origen de datos.|
|Contraseña en blanco|Cuando se activa, permite que el proveedor especificado use una contraseña en blanco en la cadena de conexión.|
|Permitir guardar la contraseña|Cuando se activa, permite guardar la contraseña con la cadena de conexión. La inclusión o no de la contraseña en la cadena de conexión depende de la funcionalidad de la aplicación que hace la llamada. <br/><br/>**NOTA:** La contraseña se devuelve y se guarda sin enmascarar ni cifrar.|
|Utilizar cifrado de alta seguridad para los datos|Cuando se activa, se cifrarán los datos que se pasen a través de la conexión.|
|Certificado de servidor de confianza|Cuando se activa, se validará el certificado del servidor. El certificado del servidor debe tener el nombre de host correcto del servidor y haber sido emitido por una entidad de certificación de confianza.|
|Seleccione la base de datos|Seleccione o escriba el nombre de la base de datos a la que quiere acceder.|
|Adjuntar un archivo de base de datos como nombre de base de datos|Especifica el nombre del archivo principal de una base de datos que se puede adjuntar. Esta base de datos se adjunta y se utiliza como predeterminada para el origen de datos. En el primer cuadro de texto de esta sección, escriba el nombre de la base de datos que se utilizará para el archivo de base de datos adjunto.<br/><br/>Escriba la ruta de acceso completa al archivo de base de datos que se va a adjuntar en el cuadro de texto con la etiqueta `Using the filename`, o bien, haga clic en el botón `...` para buscar el archivo de base de datos.|
|Cambio de contraseñas|Muestra el cuadro de diálogo Cambiar contraseña de SQL Server. |
|Probar la conexión|Haga clic para intentar establecer una conexión con el origen de datos especificado. Si se produce un error en la conexión, asegúrese de que la configuración es correcta. Por ejemplo, los errores ortográficos y la distinción entre mayúsculas y minúsculas pueden provocar que las conexiones no se puedan establecer.|

## <a name="advanced-tab"></a>Ficha Opciones avanzadas
Use esta pestaña para ver y establecer otras propiedades de inicialización.

![Captura de pantalla de páginas de vínculo de datos de OLE DB: pestaña Opciones Avanzadas](../media/data-link-pages-advanced-tab.png)

|Opción|Descripción|
|---   |---        |
| Tiempo de espera de conexión | Especifica la cantidad de tiempo (en segundos) que Microsoft OLE DB Driver for SQL Server espera hasta que se completa la inicialización. Si se supera el tiempo de espera de la inicialización, se devuelve un error y no se crea la conexión.|


> [!NOTE]  
>  Para obtener más información general sobre la conexión de vínculos de datos, consulte la [introducción a la API de vínculo de datos](https://go.microsoft.com/fwlink/?linkid=2067432).

## <a name="next-steps"></a>Pasos siguientes
- [Autenticación en Azure Active Directory](../features/using-azure-active-directory.md) mediante el controlador OLE DB.

- [Solicitud de las credenciales de autenticación al usuario](../help-topics/sql-server-login-dialog.md) mediante el controlador OLE DB.