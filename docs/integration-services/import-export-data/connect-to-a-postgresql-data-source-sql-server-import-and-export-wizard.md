---
title: Conectarse a un origen de datos de PostgreSQL (SQL Server importar y exportar) | Documentos de Microsoft
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b7a75a72-b267-444f-9eb8-d23eb333fc35
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 4c82ae7eedc3e18e7591cf7ab30a507920695247
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard"></a>Conectarse a un origen de datos de PostgreSQL (importación de SQL Server y Asistente para exportación)
Este tema muestra cómo conectarse a un **PostgreSQL** del origen de datos de la **elegir un origen de datos** o **elegir un destino** página de la importación de SQL Server y el Asistente para exportación. 

> [!IMPORTANT]
> Los requisitos detallados y los requisitos previos para conectarse a una base de datos PostgreSQL quedan fuera del ámbito de este artículo de Microsoft. En este artículo se da por supuesto que ya tiene instalado el software de cliente de PostgreSQL y que puede ya conectarse correctamente a la base de datos de PostgreSQL de destino. Para obtener más información, consulte la documentación de PostgreSQL o el Administrador de base de datos PostgreSQL.

## <a name="get-the-postgresql-odbc-driver"></a>Obtener el controlador ODBC de PostgreSQL

### <a name="install-the-odbc-driver-with-stack-builder"></a>Instalar al controlador ODBC con el generador de pila
Ejecutar el generador de pila para agregar el controlador de ODBC de PostgreSQL (psqlODBC) a la instalación de PostgreSQL.

![Instalar PostgreSQL ODBC con el generador de pila](../../integration-services/import-export-data/media/install-postgresql-odbc-with-stack-builder.png)

### <a name="or-download-the-latest-odbc-driver"></a>O bien, descargue el controlador más reciente de ODBC
O bien, descargue el instalador de Windows para la versión más reciente del controlador ODBC de PostgreSQL (psqlODBC) directamente desde este sitio FTP: [https://www.postgresql.org/ftp/odbc/versions/msi/](https://www.postgresql.org/ftp/odbc/versions/msi/). Extraiga los archivos desde el archivo .zip y ejecute el archivo. msi.

## <a name="connect-to-postgresql-with-the-postgresql-odbc-driver-psqlodbc"></a>Conectar con PostgreSQL con el controlador de ODBC de PostgreSQL (psqlODBC)
Controladores ODBC no aparezcan en la lista desplegable de orígenes de datos. Para conectar con un controlador ODBC, empiece seleccionando la **proveedor de datos de .NET Framework para ODBC** como el origen de datos en el **elegir un origen de datos** o **elegir un destino** página. Este proveedor actúa como un contenedor para el controlador ODBC.

Esta es la pantalla genérica que se ve inmediatamente después de seleccionar el proveedor de datos de .NET Framework para ODBC.

![Conectarse a PostgreSQL con ODBC antes de](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-postgresql-odbc-driver"></a>Opciones para especificar (controlador PostgreSQL ODBC)

> [!NOTE]
> Las opciones de conexión para este proveedor de datos y el controlador ODBC son los mismos si PostgreSQL es el origen o el destino. Es decir, las opciones que ve son los mismos en ambos el **elegir un origen de datos** y **elegir un destino** páginas del asistente.

Para conectarse a PostgreSQL con el controlador ODBC de PostgreSQL, ensamblar una cadena de conexión que incluye las siguientes opciones y sus valores. El formato de una cadena de conexión completa sigue inmediatamente a la lista de opciones.

> [!TIP]
> Obtener ayuda para ensamblar una cadena de conexión que está bien. O bien, en lugar de proporcionar una cadena de conexión, proporcionar un DSN (nombre de origen de datos) existente o crear uno nuevo. Para obtener más información acerca de estas opciones, consulte [conectar a un origen de datos ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).

**Controlador**  
El nombre del controlador ODBC: ya sea **PostgreSQL ODBC Driver(UNICODE)** o **PostgreSQL ODBC Driver(ANSI)**.

**Server**  
El nombre del servidor de PostgreSQL. 

**Puerto**  
El puerto que se usará para conectarse al servidor de PostgreSQL.

**Base de datos**  
El nombre de la base de datos PostgreSQL.

**UID** y **Pwd**   
El **Uid** (Id. de usuario) y **Pwd** (contraseña) para conectarse.

### <a name="connection-string-format"></a>Formato de cadena de conexión
Este es el formato de cadena de conexión típica. 

    ```
    Driver={PostgreSQL ODBC Driver(UNICODE)};Server=<server>;Port=<port>;Database=<database>;UID=<user id>;PWD=<password>
    ```

### <a name="enter-the-connection-string"></a>Escriba la cadena de conexión
Escriba la cadena de conexión en el **ConnectionString** campo o escriba el nombre DSN en el **Dsn** campo, en la **elegir un origen de datos** o **elegir un destino** página. Después de escribir la cadena de conexión, el asistente analiza la cadena y muestra las propiedades individuales y sus valores en la lista.

En el ejemplo siguiente se utiliza esta cadena de conexión.

    ```
    Driver={PostgreSQL ODBC Driver(UNICODE)};Server=127.0.0.1;Port=5432;Database=postgres;UID=postgres;PWD=********
    ```

Esta es la pantalla que verá después de escribir la cadena de conexión.

![Conectarse a PostgreSQL con ODBC](../../integration-services/import-export-data/media/connect-to-postgresql-with-odbc.png)

## <a name="other-data-providers-and-more-info"></a>Otros proveedores de datos y obtener más información
Para obtener información sobre cómo conectarse a PostgreSQL con un proveedor de datos que no aparece aquí, consulte [las cadenas de conexión de PostgreSQL](https://www.connectionstrings.com/postgresql/). Este sitio de terceros también contiene más información sobre los proveedores de datos y los parámetros de conexión descritos en esta página.

## <a name="see-also"></a>Vea también
[Elija un origen de datos](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Elegir un destino](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


