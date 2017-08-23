---
title: Conectarse a un origen de datos ODBC (SQL Server importar y exportar) | Documentos de Microsoft
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e6318776-a188-48a7-995d-9eafd7148ff2
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 4d1a2374d480f2d6b886425a02cb590b00b3564a
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="connect-to-an-odbc-data-source-sql-server-import-and-export-wizard"></a>Conectarse a un origen de datos ODBC (importación de SQL Server y Asistente para exportación)
Este tema muestra cómo conectarse a un **ODBC** del origen de datos de la **elegir un origen de datos** o **elegir un destino** página de la importación de SQL Server y el Asistente para exportación.

Tendrá que descargar el controlador ODBC de Microsoft o de un tercero.

También tendrá que buscar la información de conexión requiere que se deben proporcionar. Este sitio de terceros: [la referencia de las cadenas de conexión](https://www.connectionstrings.com/) -contiene las cadenas de conexión de ejemplo y obtener más información acerca de los proveedores de datos y la información de conexión que se necesiten.

## <a name="make-sure-the-driver-you-want-is-installed"></a>Asegúrese de que el controlador que desea está instalado
1.  Buscar o desplazarse a la **orígenes de datos ODBC (64 bits)** applet del Panel de Control. Si solo tiene un controlador de 32 bits, o sabe que tiene que usar un controlador de 32 bits, busque o vaya a **orígenes de datos ODBC (32 bits)** en su lugar.
2.  Inicie el applet del sistema. El **Administrador de orígenes de datos ODBC** abre la ventana.
3.  En el **controladores** ficha, encontrará una lista de todos los controladores ODBC instalados en su equipo. (Los nombres de algunos de los controladores pueden mostrarse en varios idiomas.)

    Este es un ejemplo de la lista de controladores de 64 bits instalados.

    ![Instala a controladores ODBC de 64 bits](../../integration-services/import-export-data/media/installed-64-bit-odbc-drivers.png)

> [!TIP]
> Si sabe que el controlador instalado y no lo ve en el applet de 64 bits, busque en el applet de 32 bits en su lugar. Esto también indica si tiene que ejecutar el Asistente para exportar y SQL Server Import 64 bits o de 32 bits.
    
## <a name="step-1---select-the-data-source"></a>Paso 1: seleccione el origen de datos
Los controladores ODBC instalados en el equipo no aparezcan en la lista desplegable de orígenes de datos. Para conectar con un controlador ODBC, empiece seleccionando la **proveedor de datos de .NET Framework para ODBC** como el origen de datos en el **elegir un origen de datos** o **elegir un destino** página del asistente. Este proveedor actúa como un contenedor para el controlador ODBC.

Esta es la pantalla genérica que se ve inmediatamente después de seleccionar el proveedor de datos de .NET Framework para ODBC.

![Conectarse a SQL con ODBC antes de](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

## <a name="step-2---provide-the-connection-info"></a>Paso 2: proporcionar la información de conexión
El siguiente paso es proporcionar la información de conexión para el controlador ODBC y el origen de datos. Tiene dos opciones.
1.  Proporcionar un **DSN** (nombre de origen de datos) que ya exista o que cree con la **Administrador de orígenes de datos ODBC** applet del Panel de Control. Un DSN es la colección guardada de la configuración necesaria para conectarse a un origen de datos ODBC.

    Si ya conoce el nombre DSN, o sabe cómo crear un nuevo DSN ahora, puede omitir el resto de esta página. Escriba el nombre DSN en el **Dsn** campo el **elegir un origen de datos** o **elegir un destino** página, a continuación, continúe con el paso siguiente del asistente.

    [Proporcionar un DSN](#odbc_dsn)
    
2.  Proporcionar un **cadena de conexión**, que puede buscar en línea, o crear y probar en el equipo con el **Administrador de orígenes de datos ODBC** applet.

    Si ya tiene la cadena de conexión o sabe cómo crearla, puede omitir el resto de esta página. Escriba la cadena de conexión en el **ConnectionString** campo el **elegir un origen de datos** o **elegir un destino** página, a continuación, continúe con el paso siguiente del asistente.

    [Proporcionar una cadena de conexión](#odbc_connstring)

Si proporciona una cadena de conexión, el **elegir un origen de datos** o **elegir un destino** página muestra toda la información de conexión que el asistente va a usar para conectarse al origen de datos, como método de autenticación y nombre de servidor y base de datos. Si proporciona un DSN, esta información no está visible.

## <a name="odbc_dsn"></a>Opción 1: proporcionar un DSN
Si desea proporcionar la información de conexión con un DSN (nombre de origen de datos), use la **Administrador de orígenes de datos ODBC** applet para buscar el nombre del DSN existente o para crear un nuevo DSN.
1.  Buscar o desplazarse a la **orígenes de datos ODBC (64 bits)** applet del Panel de Control. Si sólo dispone de un controlador de 32 bits o tenga que utilizar un controlador de 32 bits, busque o vaya a **orígenes de datos ODBC (32 bits)** en su lugar.
2.  Inicie el applet del sistema. El **Administrador de orígenes de datos ODBC** abre la ventana. Este es el aspecto de la aplicación.

    ![Applet del panel de control de administrador de ODBC](../../integration-services/import-export-data/media/odbc-administrator-control-panel-applet.png)
    
3.  Si desea **utilizar un DSN existente** para el origen de datos, puede usar cualquier DSN que se ve en el **DSN de usuario**, **DSN de sistema**, o **DSN de archivo** ficha. Compruebe el nombre, a continuación, volver al asistente y escríbala de nuevo en el **Dsn** campo el **elegir un origen de datos** o **elegir un destino** página. Omita el resto de esta página y continúe con el paso siguiente del asistente.
4.  Si desea **crear un nuevo DSN**, decida si desea que esté visible solo a usted (DSN de usuario), es visible para todos los usuarios del equipo incluido servicios de Windows (DSN de sistema), o se guardan en un archivo (DSN de archivo). Este ejemplo crea un nuevo DSN de sistema.
5. En el **DSN de sistema** , haga clic en **agregar**.

    ![Agregar un nuevo sistema DSN de ODBC](../../integration-services/import-export-data/media/add-a-new-odbc-system-dsn.png)
    
6.  En el **crear un nuevo origen de datos** cuadro de diálogo, seleccione el controlador para el origen de datos, a continuación, haga clic en **finalizar**.

    ![Seleccionar controladores para nuevo DSN de sistema](../../integration-services/import-export-data/media/pick-driver-for-new-system-dsn.png)
    
7. El controlador ahora muestra uno o más pantallas específicas del controlador que escriba la información necesaria para conectarse al origen de datos. (Para el controlador de SQL Server, por ejemplo, hay cuatro páginas de configuración personalizada.) Cuando termine, el nuevo sistema DSN aparece en la lista.

    ![Nuevo DSN de sistema en la lista](../../integration-services/import-export-data/media/new-system-dsn-in-list.png)
    
8.  Volver al asistente y escriba el nombre DSN en el **Dsn** campo el **elegir un origen de datos** o **elegir un destino** página. Vaya al paso siguiente del asistente.

## <a name="odbc_connstring"></a>Opción 2: proporcionar una cadena de conexión
Si desea proporcionar su información de conexión con una cadena de conexión, el resto de este tema le ayuda a obtener la cadena de conexión que necesita.

En este ejemplo se va a usar la siguiente cadena de conexión, que se conecta a Microsoft SQL Server.

    Driver={ODBC Driver 13 for SQL Server};server=localhost;database=WideWorldImporters;trusted_connection=Yes;

Escriba la cadena de conexión en el **ConnectionString** campo el **elegir un origen de datos** o **elegir un destino** página. Después de escribir la cadena de conexión, el asistente analiza la cadena y muestra las propiedades individuales y sus valores en la lista.

Esta es la pantalla que verá después de escribir la cadena de conexión.

![Conectarse a SQL con ODBC después de](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-after.jpg)

> [!NOTE]
> Las opciones de conexión para un controlador ODBC son los mismos si va a configurar el origen o el destino. Es decir, las opciones que ve son los mismos en ambos el **elegir un origen de datos** y **elegir un destino** páginas del asistente.

## <a name="get-the-connection-string-online"></a>Obtener la cadena de conexión en línea
Para buscar cadenas de conexión para el controlador ODBC en línea, consulte [la referencia de las cadenas de conexión](https://www.connectionstrings.com/). Este sitio de terceros contiene las cadenas de conexión de ejemplo y obtener más información acerca de los proveedores de datos y la información de conexión que se necesiten.

## <a name="get-the-connection-string-with-an-app"></a>Obtener la cadena de conexión con una aplicación
Para compilar y probar la cadena de conexión para el controlador ODBC en su propio equipo, puede usar el **Administrador de orígenes de datos ODBC** applet del Panel de Control. Crear un DSN de archivo para la conexión, a continuación, copiar la configuración de DSN de archivo para ensamblar la cadena de conexión. Esto requiere varios pasos, pero ayuda a asegurarse de que tiene una cadena de conexión válida.

1.  Buscar o desplazarse a la **orígenes de datos ODBC (64 bits)** applet del Panel de Control. Si sólo dispone de un controlador de 32 bits o tenga que utilizar un controlador de 32 bits, busque o vaya a **orígenes de datos ODBC (32 bits)** en su lugar.
2.  Inicie el applet del sistema. El **Administrador de orígenes de datos ODBC** abre la ventana.
3.  Ahora, vaya a la **DSN de archivo** ficha del applet. Haga clic en **Agregar**.

    En este ejemplo, cree un DSN de archivo en lugar de un DSN de usuario o un DSN de sistema, como el DSN de archivo guarda los pares de nombre y valor en el formato específico requerido para la cadena de conexión.

    ![Agregue un nuevo archivo DSN de ODBC](../../integration-services/import-export-data/media/add-a-new-odbc-file-dsn.png)

4.  En el **Create New Data Source** cuadro de diálogo, seleccione el controlador de la lista y, a continuación, haga clic en **siguiente**. En este ejemplo se va a crear un DSN que contiene los argumentos de cadena de conexión que se necesita para conectarse a Microsoft SQL Server.

    ![Crear nuevo origen de datos ODBC](../../integration-services/import-export-data/media/create-new-odbc-data-source.png)
    
5.  Seleccione una ubicación, escriba un nombre de archivo para el nuevo DSN de archivo y, a continuación, haga clic en **siguiente**. Recuerde que guarde el archivo para que pueda encontrarla y ábralo en un paso posterior.

    ![Guardar el DSN de archivo nuevo](../../integration-services/import-export-data/media/save-new-file-dsn.png)

6.  Revise el resumen de las selecciones y, a continuación, haga clic en **finalizar**.

7.  Tras hacer clic en **finalizar**, el controlador que seleccionó muestra uno o más pantallas propietarias para recopilar la información que necesita para conectarse. Normalmente esta información incluye el servidor, información de inicio de sesión y base de datos para orígenes de datos basados en servidor y archivo, formato y versión para orígenes de datos basados en archivos.

8. Después de configurar el origen de datos y haga clic en **finalizar**, normalmente ver un resumen de las selecciones y tiene la oportunidad de probarlas.

    ![DSN de archivo nuevo de prueba](../../integration-services/import-export-data/media/test-new-file-dsn.png)

9. Después de probar el origen de datos y cerrar los cuadros de diálogo, busque el DSN de archivo donde se guarda en el sistema de archivos. Si no cambia la extensión de archivo, la extensión predeterminada es. DSN.

10. Abra el archivo guardado con el Bloc de notas u otro editor de texto. Este es el contenido de nuestro ejemplo de SQL Server.

        [ODBC]  
        DRIVER=ODBC Driver 13 for SQL Server  
        TrustServerCertificate=No  
        DATABASE=WideWorldImporters    
        WSID=<local computer name>  
        APP=Microsoft® Windows® Operating System  
        Trusted_Connection=Yes  
        SERVER=localhost   
        
11. Copie y pegue los valores necesarios en una cadena de conexión en el que los pares de nombre y valor están separados por punto y coma.

    Después de ensamblar los valores necesarios en el DSN de archivo de ejemplo, tiene la siguiente cadena de conexión.
    
        DRIVER=ODBC Driver 13 for SQL Server;SERVER=localhost;DATABASE=WideWorldImporters;Trusted_Connection=Yes

    Normalmente no necesita todas las configuraciones de un DSN creado por el Administrador de orígenes de datos de ODBC para crear una cadena de conexión que funcione.  
    -   Siempre tendrá que especificar el controlador ODBC.
    -   Para un origen de datos basados en servidor, como SQL Server, normalmente se necesita servidor, base de datos y la información de inicio de sesión. Por lo que en el ejemplo de DSN, no necesita TrustServerCertificate, WSID o una aplicación.
    -   Para un origen de datos basados en archivos, se necesitan al menos nombre de archivo y ubicación.
    
12. Pegue esta cadena de conexión en el **ConnectionString** campo el **elegir un origen de datos** o **elegir un destino** página del asistente. El asistente analiza la cadena y está listo para continuar.

    ![Conectarse a SQL con ODBC después de](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-after.jpg)

## <a name="see-also"></a>Vea también
[Elija un origen de datos](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Elegir un destino](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)



