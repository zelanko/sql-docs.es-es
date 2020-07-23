---
title: Conectarse a un origen de datos ODBC (Asistente para importación y exportación de SQL Server) | Microsoft Docs
description: Cómo configurar un DSN de ODBC o crear una cadena de conexión ODBC para utilizarla con el Asistente para importación y exportación de SQL Server
ms.custom: ''
ms.date: 06/29/2020
ms.prod: sql
ms.reviewer: vanto
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: e6318776-a188-48a7-995d-9eafd7148ff2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a4049581b36d05f178fc56fa37bf332bfc2355a2
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/22/2020
ms.locfileid: "86917101"
---
# <a name="connect-to-an-odbc-data-source-sql-server-import-and-export-wizard"></a>Conectarse a un origen de datos ODBC (Asistente para importación y exportación de SQL Server)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


En este tema se muestra cómo conectarse a un origen de datos **ODBC** desde la página **Elegir un origen de datos** o **Elegir un destino** del Asistente para importación y exportación de SQL Server.

Puede que tenga que descargar el controlador ODBC desde Microsoft o desde un tercero.

Puede que también tenga que buscar la información de conexión necesaria que debe proporcionar. Este sitio de terceros, [The Connection Strings Reference](https://www.connectionstrings.com/) (Referencia de cadenas de conexión), contiene cadenas de conexión de ejemplo y más información acerca de los proveedores de datos y la información de conexión que necesitan.

## <a name="make-sure-the-driver-you-want-is-installed"></a>Comprobar que el controlador deseado está instalado
1.  Busque o vaya al applet **Orígenes de datos ODBC (64 bits)** en el menú Inicio o el Panel de control. Si solo tiene un controlador de 32 bits o sabe que tiene que usar un controlador de 32 bits, busque o examine **Orígenes de datos ODBC (32 bits)** en su lugar.
2.  Inicie el applet. Se abre la ventana **Administrador de origen de datos ODBC**.
3.  En la pestaña **Controladores**, encontrará una lista de todos los controladores ODBC instalados en su equipo. (Los nombres de algunos de los controladores pueden mostrarse en varios idiomas).

    A continuación se muestra un ejemplo de la lista de controladores de 64 bits instalados.

    ![Controladores ODBC de 64 bits instalados](../../integration-services/import-export-data/media/installed-64-bit-odbc-drivers.png)

> [!TIP]
> Si sabe que el controlador está instalado y no lo ve en el applet de 64 bits, busque en el applet de 32 bits en su lugar. Esto también le indica si tiene que ejecutar el Asistente para importación y exportación de SQL Server de 64 bits o de 32 bits.
>
> Para usar la versión de 64 bits del asistente para importación y exportación de SQL Server, tendrá que instalar SQL Server. SQL Server Data Tools (SSDT) y SQL Server Management Studio (SSMS) son aplicaciones de 32 bits y solo instalan archivos de 32 bits, incluida la versión de 32 bits del asistente.
    
## <a name="step-1---select-the-data-source"></a>Paso 1: Seleccionar el origen de datos
Los controladores ODBC instalados en el equipo no aparecen en la lista desplegable de orígenes de datos. Para conectarse con un controlador ODBC, empiece seleccionando el **proveedor de datos de .NET Framework para ODBC** como origen de datos en la página **Elegir un origen de datos** o **Elegir un destino** del asistente. Este proveedor actúa como un contenedor para el controlador ODBC.

Esta es la pantalla genérica que se ve inmediatamente después de seleccionar el proveedor de datos de .NET Framework para ODBC.

![Conectarse antes a SQL con ODBC](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

## <a name="step-2---provide-the-connection-info"></a>Paso 2: Proporcionar la información de conexión
El siguiente paso es proporcionar la información de conexión del controlador ODBC y el origen de datos. Tiene dos opciones.
1.  Proporcione un **DSN** (nombre de origen de datos) que ya exista o que cree con el applet **Administrador de origen de datos ODBC**. Un DSN es la colección guardada de la configuración necesaria para conectarse a un origen de datos ODBC.

    Si ya conoce el nombre DSN o sabe cómo crear un nuevo DSN ahora, puede omitir el resto de esta página. Escriba el nombre DSN en el campo **Dsn** en la página **Elegir un origen de datos** o **Elegir un destino** y, a continuación, continúe con el paso siguiente del asistente.

    [Proporcionar un nombre](#odbc_dsn)
    
2.  Proporcione una **cadena de conexión**, que pueda buscar en línea, o crear y probar en el equipo con el applet **Administrador de origen de datos ODBC**.

    Si ya tiene la cadena de conexión o sabe cómo crearla, puede omitir el resto de esta página. Escriba la cadena de conexión en el campo **ConnectionString** en la página **Elegir un origen de datos** o **Elegir un destino** y, a continuación, continúe con el paso siguiente del asistente.

    [Proporcionar una cadena de conexión](#odbc_connstring)

Si proporciona una cadena de conexión, la página **Elegir un origen de datos** o **Elegir un destino** muestra toda la información de conexión que el asistente va a usar para conectarse al origen de datos, como el nombre del servidor y la base de datos, o el método de autenticación. Si proporciona un DSN, esta información no se mostrará.

## <a name="option-1---provide-a-dsn"></a><a name="odbc_dsn"></a> Opción 1: Proporcionar un DSN
Si quiere proporcionar la información de conexión con un DSN (nombre de origen de datos), use el applet **Administrador de origen de datos ODBC** para buscar el nombre del DSN existente o para crear un nuevo DSN.
1.  Busque o vaya al applet **Orígenes de datos ODBC (64 bits)** en el menú Inicio o el Panel de control. Si solo tiene un controlador de 32 bits o tiene que usar un controlador de 32 bits, busque o examine **Orígenes de datos ODBC (32 bits)** en su lugar.
2.  Inicie el applet. Se abre la ventana **Administrador de origen de datos ODBC**. El applet tiene el siguiente aspecto.

    ![Applet Administrador de ODBC del Panel de control](../../integration-services/import-export-data/media/odbc-administrator-control-panel-applet.png)
    
3.  Si quiere **usar un DSN existente** para el origen de datos, puede usar cualquier DSN que se muestre en la pestaña **DSN de usuario**, **DSN de sistema** o **DSN de archivo**. Compruebe el nombre, vuelva al asistente y escríbalo en el campo **Dsn** en la página **Elegir un origen de datos** o **Elegir un destino**. Omita el resto de esta página y continúe con el paso siguiente del asistente.
4.  Si quiere **crear un nuevo DSN**, decida si desea que sea visible solo para usted (DSN de usuario), que sea visible para todos los usuarios del equipo que incluye los servicios de Windows (DSN de sistema) o que esté guardado en un archivo (DSN de archivo). En este ejemplo se crea un nuevo DSN de sistema.
5. En la pestaña **DSN de sistema**, haga clic en **Agregar**.

    ![Agregar un nuevo DSN de sistema de ODBC](../../integration-services/import-export-data/media/add-a-new-odbc-system-dsn.png)
    
6.  En el cuadro de diálogo **Crear un nuevo origen de datos**, seleccione el controlador para el origen de datos y, a continuación, haga clic en **Finalizar**.

    ![Seleccionar el controlador para un nuevo DSN de sistema](../../integration-services/import-export-data/media/pick-driver-for-new-system-dsn.png)
    
7. El controlador muestra ahora una o más pantallas específicas del controlador, donde debe escribir la información necesaria para conectarse al origen de datos. (Para el controlador de SQL Server, por ejemplo, hay cuatro páginas de configuración personalizada). Cuando termine, el nuevo DSN de sistema aparecerá en la lista.

    ![Nuevo DSN de sistema en la lista](../../integration-services/import-export-data/media/new-system-dsn-in-list.png)
    
8.  Vuelva al asistente e introduzca el nombre DSN en el campo **Dsn** en la página **Elegir un origen de datos** o **Elegir un destino**. Continúe con el paso siguiente del asistente.

## <a name="option-2---provide-a-connection-string"></a><a name="odbc_connstring"></a> Opción 2: Proporcionar una cadena de conexión
Si quiere proporcionar la información de conexión con una cadena de conexión, el resto de este tema le ayudará a obtener la cadena de conexión que necesita.

En este ejemplo se va a usar la siguiente cadena de conexión, que se conecta a Microsoft SQL Server. El ejemplo de base de datos que se usa es **WideWorldImporters** y se va a conectar a SQL Server en la máquina local.

```console
Driver={ODBC Driver 13 for SQL Server};server=localhost;database=WideWorldImporters;trusted_connection=Yes;
```

Escriba la cadena de conexión en el campo **ConnectionString** en la página **Elegir un origen de datos** o **Elegir un destino**. Después de escribir la cadena de conexión, el asistente la analiza y muestra las propiedades individuales y sus valores en la lista.

Esta es la pantalla que verá después de escribir la cadena de conexión.

![Conectarse antes a SQL con ODBC](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-after.jpg)

> [!NOTE]
> Las opciones de conexión de un controlador ODBC son las mismas sin importar si se configura el origen o el destino. Es decir, las opciones que ve son las mismas en las páginas **Elegir un origen de datos** y **Elegir un destino** del asistente.

## <a name="get-the-connection-string-online"></a>Obtener la cadena de conexión en línea
Para buscar cadenas de conexión para el controlador ODBC en línea, consulte [The Connection Strings Reference](https://www.connectionstrings.com/) (Referencia de cadenas de conexión). Este sitio de terceros contiene cadenas de conexión de ejemplo y más información acerca de los proveedores de datos y la conexión que estos necesitan.

## <a name="get-the-connection-string-with-an-app"></a>Obtener la cadena de conexión con una aplicación
Para compilar y probar la cadena de conexión para el controlador ODBC en su propio equipo, puede usar el applet **Administrador de origen de datos ODBC** en el Panel de control. Cree un DSN de archivo para su conexión y, a continuación, copie la configuración del DSN de archivo para ensamblar la cadena de conexión. Esto requiere varios pasos, pero le ayuda a comprobar que tiene una cadena de conexión válida.

1.  Busque o vaya al applet **Orígenes de datos ODBC (64 bits)** en el menú Inicio o el Panel de control. Si solo tiene un controlador de 32 bits o tiene que usar un controlador de 32 bits, busque o examine **Orígenes de datos ODBC (32 bits)** en su lugar.
2.  Inicie el applet. Se abre la ventana **Administrador de origen de datos ODBC**.
3.  Ahora, vaya a la pestaña **DSN de archivo** del applet. Haga clic en **Agregar**.

    Para este ejemplo, cree un DSN de archivo en lugar de un DSN de usuario o un DSN de sistema, ya que el DSN de archivo guarda los pares nombre-valor en el formato específico necesario para la cadena de conexión.

    ![Agregar un nuevo DSN de archivo de ODBC](../../integration-services/import-export-data/media/add-a-new-odbc-file-dsn.png)

4.  En el cuadro de diálogo **Crear nuevo origen de datos**, seleccione el controlador en la lista y, a continuación, haga clic en **Siguiente**. En este ejemplo se va a crear un DSN que contiene los argumentos de la cadena de conexión que se necesitan para conectarse a Microsoft SQL Server.

    ![Crear un origen de datos ODBC](../../integration-services/import-export-data/media/create-new-odbc-data-source.png)
    
5.  Seleccione una ubicación, escriba un nombre de archivo para el nuevo DSN de archivo y, a continuación, haga clic en **Siguiente**. Recuerde dónde guarda el archivo para poder encontrarlo y abrirlo en un paso posterior.

    ![Guardar el DSN de archivo nuevo](../../integration-services/import-export-data/media/save-new-file-dsn.png)

6.  Revise el resumen de las selecciones y, a continuación, haga clic en **Finalizar**.

7.  Tras hacer clic en **Finalizar**, el controlador que seleccionó muestra una o más pantallas de propiedad para recopilar la información que necesita para conectarse. Normalmente, esta información incluye el servidor, información de inicio de sesión y la base de datos de orígenes de datos basados en servidor, así como el archivo, el formato y la versión de los orígenes de datos basados en archivos.

8. Después de configurar el origen de datos y hacer clic en **Finalizar**, normalmente se muestra un resumen de las selecciones y tiene la oportunidad de probarlas.

    ![Probar el DSN de archivo nuevo](../../integration-services/import-export-data/media/test-new-file-dsn.png)

9. Después de probar el origen de datos y cerrar los cuadros de diálogo, busque el DSN de archivo donde lo guardó en el sistema de archivos. Si no cambió la extensión del archivo, la extensión predeterminada es .dsn.

10. Abra el archivo guardado con el Bloc de notas u otro editor de texto. Este es el contenido de nuestro ejemplo de SQL Server.

    ```console
    [ODBC]  
    DRIVER=ODBC Driver 13 for SQL Server  
    TrustServerCertificate=No  
    DATABASE=WideWorldImporters    
    WSID=<local computer name>  
    APP=MicrosoftÂ® WindowsÂ® Operating System  
    Trusted_Connection=Yes  
    SERVER=localhost   
    ```
        
11. Copie y pegue los valores necesarios en una cadena de conexión donde los pares nombre-valor estén separados por punto y coma.

    Después de ensamblar los valores necesarios del DSN de archivo de ejemplo, tendrá la cadena de conexión siguiente.
    
    ```console
    DRIVER=ODBC Driver 13 for SQL Server;SERVER=localhost;DATABASE=WideWorldImporters;Trusted_Connection=Yes
    ```

    Normalmente, no necesita todas las configuraciones de un DSN creado con el Administrador de origen de datos ODBC para crear una cadena de conexión que funcione.  
    -   Siempre tiene que especificar el controlador ODBC.
    -   Para un origen de datos basado en servidor, como SQL Server, normalmente se necesita el servidor, la base de datos y la información de inicio de sesión. En el DSN de ejemplo, no necesita TrustServerCertificate, WSID ni APP.
    -   Para un origen de datos basado en archivos, se necesitan al menos el nombre de archivo y la ubicación.
    
12. Pegue la cadena de conexión en el campo **ConnectionString** en la página **Elegir un origen de datos** o **Elegir un destino** del asistente. El asistente analiza la cadena y ya puede continuar.

    ![Conectarse antes a SQL con ODBC](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-after.jpg)

## <a name="see-also"></a>Consulte también
[Choose a Data Source](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md) (Selección de un origen de datos)  
[Choose a Destination](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md) (Selección de un destino)


