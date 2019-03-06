---
title: Vínculo de datos universal (UDL) configuración | Microsoft Docs
description: Configuración de Universal Data Link (UDL) mediante el controlador OLE DB de Microsoft para SQL Server
ms.custom: ''
ms.date: 01/21/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.author: v-beaziz
author: bazizi
ms.openlocfilehash: e198f561fd4f6bcec390ef8632c1cdc96f2810d6
ms.sourcegitcommit: 958cffe9288cfe281280544b763c542ca4025684
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 02/23/2019
ms.locfileid: "56744852"
---
# <a name="universal-data-link-udl-configuration"></a>Configuración de Universal Data Link (UDL)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

## <a name="connection-tab"></a>Pestaña conexión
Utilice la ficha conexión para especificar cómo conectarse a los datos mediante el controlador OLE DB de Microsoft para SQL Server.

![Captura de pantalla de páginas de vínculo de datos OLE DB - ficha conexión](../media/data-link-pages-connection-tab.png)

La pestaña Conexión es específica del proveedor y solo muestra las propiedades de conexión que requiere el controlador OLE DB de Microsoft para SQL Server.

|Opción|Descripción|
|---   |---        |
|Seleccionar o especificar un nombre de servidor|Seleccione un nombre de servidor en la lista desplegable o escriba la ubicación del servidor donde se encuentra la base de datos a la que desea obtener acceso. La selección de la base de datos en el servidor es una acción independiente. Actualice la lista haciendo clic en "Actualizar".
|Escriba la información para iniciar sesión en el servidor|Puede seleccionar las siguientes opciones de autenticación de la lista desplegable: <ul><li>`Windows Authentication:` Autenticación de SQL Server con las credenciales de cuenta de Windows del usuario que ha iniciado sesión actualmente.</li><li>`SQL Server Authentication:` Autenticación de SQL Server mediante el identificador de inicio de sesión y la contraseña.</li><li>`Active Directory - Integrated:` Autenticación integrada con las credenciales de cuenta de Windows del usuario que ha iniciado sesión actualmente.</li><li>`Active Directory - Password:` Autenticación de Active Directory con Id. de inicio de sesión y la contraseña.</li></ul>|
|Dirección SPN del servidor|Si utiliza una conexión de confianza, puede especificar un nombre principal de servicio (SPN) para el servidor.|
|Nombre de usuario|Escriba el identificador de usuario que se usará para la autenticación al iniciar sesión en el origen de datos.|
|Contraseña|Escriba la contraseña que se utilizará para la autenticación al iniciar sesión el origen de datos.|
|Contraseña en blanco|Cuando está activada, permite que el proveedor especificado usar una contraseña en blanco en la cadena de conexión.|
|Permitir guardar la contraseña|Cuando está activada, permite que la contraseña se guardará con la cadena de conexión. La inclusión o no de la contraseña en la cadena de conexión depende de la funcionalidad de la aplicación que hace la llamada. <br/><br/>**NOTA:** La contraseña se devuelve y se guarda sin enmascarar ni cifrar.|
|Utilizar cifrado de alta seguridad para los datos|Cuando está activada, se cifrarán los datos que se pasan a través de la conexión.|
|Certificado de servidor de confianza|Cuando está activada, se validará el certificado del servidor. Certificado del servidor debe tener el nombre de host correcto del servidor y emitido por una entidad de certificación de confianza.|
|Seleccionar la base de datos|Seleccione o escriba el nombre de base de datos que desea obtener acceso.|
|Adjuntar un archivo de base de datos como nombre de base de datos|Especifica el nombre del archivo principal de una base de datos que se puede adjuntar. Esta base de datos se adjunta y se utiliza como predeterminada para el origen de datos. En el primer cuadro de texto en esta sección, escriba el nombre de la base de datos que se usará para el archivo de base de datos adjunta.<br/><br/>Escriba la ruta de acceso completa al archivo de base de datos va a adjuntar en el cuadro de texto denominado `Using the filename`, o haga clic en el `...` botón para buscar el archivo de base de datos.|
|Cambio de contraseñas|Muestra el cuadro de diálogo Cambiar contraseña de SQL Server. |
|Probar conexión|Haga clic aquí para intentar establecer una conexión al origen de datos especificado. Si se produce un error en la conexión, asegúrese de que la configuración es correcta. Por ejemplo, los errores ortográficos y la distinción entre mayúsculas y minúsculas pueden provocar que las conexiones no se puedan establecer.|

## <a name="advanced-tab"></a>Ficha Opciones avanzadas
Use la ficha Opciones avanzadas para ver y establecer propiedades de inicialización adicionales.

![Captura de pantalla de páginas de vínculo de datos OLE DB - ficha Opciones avanzadas](../media/data-link-pages-advanced-tab.png)

|Opción|Descripción|
|---   |---        |
| Tiempo de espera de conexión | Especifica la cantidad de tiempo (en segundos) que el controlador OLE DB de Microsoft para SQL Server espera que finalice la inicialización. Si se supera el tiempo de espera de la inicialización, se devuelve un error y no se crea la conexión.|


> [!NOTE]  
>  Para obtener más información de conexión de vínculo de datos, vea el [Introducción a la API de vínculo de datos](https://go.microsoft.com/fwlink/?linkid=2067432).

## <a name="next-steps"></a>Pasos siguientes
- [Autenticarse en Azure Active Directory](../features/using-azure-active-directory.md) con el controlador de OLE DB.

- [Solicitar al usuario las credenciales de autenticación](../help-topics/sql-server-login-dialog.md) con el controlador de OLE DB.