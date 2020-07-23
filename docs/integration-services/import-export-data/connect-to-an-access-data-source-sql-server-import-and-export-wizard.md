---
title: Conectarse a un origen de datos de Acces (Asistente para importación y exportación de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/20/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: b44c159a-c33d-4f3c-bdb8-9832f35317c8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 79c994357b7d57f138bc022b6f4b3cdf3963111b
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/22/2020
ms.locfileid: "86913191"
---
# <a name="connect-to-an-access-data-source-sql-server-import-and-export-wizard"></a>Conectarse a un origen de datos de Access (Asistente para importación y exportación de SQL Server)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


En este tema se muestra cómo conectarse a un origen de datos de **Microsoft Access** desde la página **Elegir un origen de datos** o **Elegir un destino** del Asistente para importación y exportación de SQL Server.

En la siguiente captura de pantalla se muestra una conexión de ejemplo a una base de datos de Microsoft Access. En este ejemplo, no tiene que escribir un nombre de usuario y una contraseña, ya que la base de datos de destino no usa un archivo de información de grupo de trabajo.

![Conectarse a Access](../../integration-services/import-export-data/media/connect-to-access.jpg)

## <a name="options-to-specify"></a>Opciones que hay que especificar

> [!NOTE]
> Las opciones de conexión de este proveedor de datos son las mismas sin importar que Access sea el origen o el destino. Es decir, las opciones que ve son las mismas en las páginas **Elegir un origen de datos** y **Elegir un destino** del asistente.

**Origen de datos**  
La lista de proveedores de datos puede contener varias entradas para Microsoft Access. Seleccione la última versión instalada o la versión que corresponda a la versión de Access que creó el archivo de base de datos.

|Origen de datos|Versión de Office|
|-------|-------|
|Microsoft Access (Microsoft.ACE.OLEDB.16.0)|Office 2016|
|Microsoft Access (Microsoft.ACE.OLEDB.15.0)|Office 2013|
|Microsoft Access (Microsoft Access Database Engine)|Office 2010 y Office 2007|
|Microsoft Access (Microsoft Jet Database Engine)|Versiones de Office anteriores a Office 2007|

> [!IMPORTANT]
> Es posible que tenga que descargar e instalar archivos adicionales para conectarse a archivos de Access. Para obtener más información, vea [Get the files you need to connect to Access](#officeDownloads) (Obtener los archivos que necesita para conectarse a Access) en esta página.

 **Nombre de archivo**  
Especifique la ruta de acceso y el nombre del archivo de Access. Por ejemplo, **C:\\MisDatos.mdb** para un archivo en el equipo local, o bien **\\\\Ventas\\BaseDeDatos\\Northwind.mdb** para un archivo en un recurso compartido de red. O bien, haga clic en **Examinar**. 

> [!NOTE]
> Si hace clic en **Examinar** para buscar el archivo de Access, el cuadro de diálogo **Abrir** filtra los archivos con el formato y la extensión de archivo .mdb anteriores de forma predeterminada. Sin embargo, el proveedor de datos también puede abrir archivos con el formato y la extensión de archivo .accdb más recientes.
  
 **Browse**  
 Busque el archivo de base de datos desde el cuadro de diálogo **Abrir**.  
  
 **Nombre de usuario**  
Proporcione un nombre de usuario válido si existe un archivo de información de grupo de trabajo asociado a la base de datos.  
  
 **Contraseña**  
Proporcione la contraseña del usuario si existe un archivo de información de grupo de trabajo asociado a la base de datos.
 
Si la base de datos está protegida con una contraseña para todos los usuarios, consulte [¿El archivo de base de datos está protegido con contraseña?](#database_password).
  
 **Avanzadas**  
Especifique las opciones avanzadas, como la contraseña de la base de datos o un archivo de información del grupo de trabajo no predeterminado, mediante el cuadro de diálogo **Propiedades de vínculo de datos**.  

## <a name="i-dont-see-access-in-the-list-of-data-sources"></a>No veo Access en la lista de orígenes de datos
Si no ve Access en la lista de orígenes de datos, ¿está ejecutando el asistente de 64 bits? Los proveedores para Excel y Access son normalmente de 32 bits y no son visibles en el asistente de 64 bits. Ejecute al asistente de 32 bits en su lugar.

> [!NOTE]
> Para usar la versión de 64 bits del asistente para importación y exportación de SQL Server, tendrá que instalar SQL Server. SQL Server Data Tools (SSDT) y SQL Server Management Studio (SSMS) son aplicaciones de 32 bits y solo instalan archivos de 32 bits, incluida la versión de 32 bits del asistente.

## <a name="get-the-files-you-need-to-connect-to-access"></a><a name="officeDownloads"></a>Obtener los archivos que necesita para conectarse a Access  
Es posible que tenga que descargar los componentes de conectividad para orígenes de datos de Microsoft Office, incluidos Access y Excel, si aún no están instalados. Descargue la versión más reciente de los componentes de conectividad para los archivos de Access y Excel aquí: [Microsoft Access Database Engine 2016 Redistributable](https://www.microsoft.com/download/details.aspx?id=54920).
  
La versión más reciente de los componentes puede abrir los archivos creados con versiones anteriores de los programas de Access.

Si el equipo tiene una versión de Office de 32 bits, tendrá que instalar la versión de 32 bits de los componentes, y también debe asegurarse de que ejecuta el paquete en el modo de 32 bits.

Si tiene una suscripción de Office 365, asegúrese de descargar Access Database Engine 2016 Redistributable y no Microsoft Access 2016 Runtime. Al ejecutar el instalador, es posible que vea un mensaje de error que indica que no se puede instalar la descarga en paralelo con componentes para hacer clic y ejecutar de Office. Para omitir este mensaje de error, ejecute la instalación en modo silencioso abriendo una ventana del símbolo del sistema y ejecutando el archivo .EXE que descargó con el modificador `/quiet`. Por ejemplo:

`C:\Users\<user name>\Downloads\AccessDatabaseEngine.exe /quiet`

## <a name="is-the-database-file-password-protected"></a><a name="database_password"></a> ¿El archivo de base de datos está protegido con contraseña?
En algunos casos, una base de datos de Access está protegida con contraseña, pero no usa un archivo de información de grupo de trabajo. Todos los usuarios deben proporcionar la misma contraseña, pero no tienen que especificar un nombre de usuario. Para proporcionar una contraseña de base de datos, haga lo siguiente:

1.  En la página **Elegir un origen de datos** o **Elegir un destino**, haga clic en el botón **Avanzadas** para abrir el cuadro de diálogo **Propiedades de vínculo de datos**.  
2.  En el cuadro de diálogo **Propiedades de vínculo de datos**, seleccione la pestaña **Todas**.  
3.  En la lista de propiedades y valores, seleccione **Jet OLEDB:Database Password**.   
    
    ![Especificar la contraseña de Access, pantalla 1](../../integration-services/import-export-data/media/specify-access-password-screen-1.jpg) 
4.  Haga clic en **Editar valor** para abrir el cuadro de diálogo **Modificar valor de la propiedad**.  
    
    ![Especificar la contraseña de Access, pantalla 2](../../integration-services/import-export-data/media/specify-access-password-screen-2.jpg)
5.  En el cuadro de diálogo **Modificar valor de la propiedad**, escriba la contraseña de la base de datos.
6.  Haga clic en **Aceptar** en cada cuadro de diálogo para volver a la página **Elegir un origen de datos** o **Elegir un destino** del asistente y continúe.

## <a name="keep-your-autonumber-values-when-you-export-from-access"></a>Mantener los valores de autonumeración al realizar la exportación desde Access
Para permitir que los valores de identidad existentes en los datos de origen se inserten en una columna de identidad en la tabla de destino, elija la opción **Habilitar la inserción de identidad** en el cuadro de diálogo **Asignaciones de columnas**. De manera predeterminada, la columna de identidad de destino no suele permitir la inserción de valores existentes. Para mostrar el cuadro de diálogo **Asignaciones de columnas**, seleccione **Editar asignaciones** cuando llegue a la página **Seleccionar tablas y vistas de origen** del asistente. Para poder echar un vistazo a estas páginas, vea [Seleccionar tablas y vistas de origen](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md) y [Asignaciones de columnas](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md).

Si las claves principales existentes están en una columna de identidad, una columna autonumérica o su equivalente, normalmente es necesario seleccionar esta opción para mantener los valores de clave principales existentes. De lo contrario, la columna de identidad de destino normalmente asigna nuevos valores.

## <a name="see-also"></a>Consulte también
[Choose a Data Source](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md) (Selección de un origen de datos)  
[Choose a Destination](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md) (Selección de un destino)

