---
title: "Elegir un origen de datos (Asistente para importaci&#243;n y exportaci&#243;n de SQL Server) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.impexpwizard.chooseadatasource.f1"
ms.assetid: ebf28a62-dfc1-4b39-9db5-df1919e5fccb
caps.latest.revision: 124
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 113
---
# Elegir un origen de datos (Asistente para importaci&#243;n y exportaci&#243;n de SQL Server)
  Después de la página de bienvenida, el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muestra **Elegir un origen de datos**. En esta página, debe proporcionar información sobre el origen de datos y la manera de conectarse a él.
  
Para más información sobre los orígenes de datos que puede usar, vea [¿Qué orígenes de datos y destinos puedo usar?](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md#wizardSources)

## <a name="screen-shot-of-the-choose-a-data-source-page"></a>Captura de pantalla de la página Seleccionar un origen de datos 
En la captura de pantalla siguiente, se muestra la primera parte de la página **Seleccionar un origen de datos** del asistente.

![Elegir origen](../../integration-services/import-export-data/media/choose-source.png)

## <a name="choose-a-data-source"></a>Seleccionar un origen de datos
 **Origen de datos**  
Especifique el origen de datos seleccionando un proveedor de datos que pueda conectarse al origen. En la mayoría de los casos, el proveedor de datos que necesita es obvio por su nombre, ya que el nombre del proveedor contiene el nombre del origen; por ejemplo, SQL Server, Oracle, archivos planos, Excel y Access.

La lista de los proveedores de datos disponibles en la lista **Origen de datos** depende de los proveedores instalados en su equipo. También depende de si está ejecutando el asistente de 32 o 64 bits.

Es posible que haya más de un proveedor disponible para el origen de datos. Normalmente, puede seleccionar cualquier proveedor que funcione con su origen. Por ejemplo, para conectarse a Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, el Proveedor de datos .NET Framework para SQL Server o el Proveedor OLE DB de Microsoft para SQL Server. 

En algunos casos, tiene que empezar seleccionando el proveedor de datos genérico. Por ejemplo, si tiene un controlador ODBC para su origen de datos, seleccione el Proveedor de datos .NET Framework para ODBC.  
 
Para algunos orígenes de datos, puede que tenga que descargar el proveedor de datos de Microsoft o de un tercero. Para más información sobre los orígenes de datos que puede usar, vea [¿Qué orígenes de datos y destinos puedo usar?](Import%20and%20Export%20Data%20with%20the%20SQL%20Server%20Import%20and%20Export%20Wizard.md\#wizardSources)

## <a name="after-you-choose-a-data-source"></a>Después de seleccionar un origen de datos
Después de elegir un origen de datos, el resto de la propiedad de página **Elegir un origen de datos** tiene un número variable de opciones que dependen del proveedor de datos que elija.

En las siguientes secciones se enumeran opciones importantes para algunos orígenes de datos que se usan frecuentemente. No todos los orígenes que pueden estar disponibles en la lista desplegable **Origen de datos** se muestran aquí. Para obtener opciones y proveedores adicionales, vea la documentación específica del proveedor. 
  
> [!TIP]  Si su origen de datos necesita una cadena de conexión, puede encontrar ejemplos en este sitio de terceros: [Referencia de Connection Strings](https://www.connectionstrings.com/).  

## <a name="microsoft-sql-server"></a>Microsoft SQL Server 

### <a name="connect-to-sql-server-with-sql-server-native-client-or-the-microsoft-ole-db-provider-for-sql-server"></a>Conectarse a SQL Server con SQL Server Native Client o con el Proveedor OLE DB de Microsoft para SQL Server  

SQL Server Native Client y el proveedor OLE DB de Microsoft para SQL Server exponen el mismo conjunto de opciones. En la siguiente captura de pantalla se muestran las opciones de SQL Server Native Client como ejemplo.

![Conexión nativa de SQL Server](../../integration-services/import-export-data/media/sql-server-connection-native.png)

 **Nombre del servidor**  
 Escriba el nombre o la dirección IP del servidor que contiene los datos o elija un servidor de la lista.  
  
> [!NOTE] Si se encuentra en una red con varios servidores, será más sencillo escribir el nombre del servidor. Si hace clic en la lista desplegable, puede tardar mucho tiempo en consultar la red para obtener todos los servidores disponibles, y el nombre del servidor puede que no se encuentre en los resultados.

Para especificar un puerto TCP no estándar, escriba una coma después del nombre del servidor o la dirección IP y después escriba el número de puerto.
  
 **Utilizar autenticación de Windows**  
 Especifique si el asistente debe usar la autenticación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows para iniciar sesión en la base de datos. Para obtener una mayor seguridad, es recomendable utilizar la autenticación de Windows.  
  
 **Utilizar autenticación de SQL Server**  
 Especifique si el asistente debe usar la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para iniciar sesión en la base de datos. Si usa la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , debe proporcionar un nombre de usuario y una contraseña.  
  
 **Nombre de usuario**  
 Proporcione un nombre de usuario para la conexión de la base de datos cuando use la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Contraseña**  
 Proporcione la contraseña para la conexión de la base de datos cuando use la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Base de datos**  
 Seleccione una base de datos de la lista de bases de datos de la instancia especificada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Actualizar**  
 Actualice la lista de bases de datos disponibles al hacer clic en **Actualizar**.  
  
### <a name="connect-to-sql-server-with-the-net-framework-data-provider-for-sql-server"></a>Conectarse a SQL Server con el Proveedor de datos de .NET Framework para SQL Server 

Esta página presenta una lista agrupada de opciones para el proveedor de datos [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Las opciones importantes se enumeran aquí. Las opciones adicionales que aparecen al seleccionar este proveedor normalmente no son necesarias para establecer una conexión correctamente con la base de datos de origen de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 

Para más información, vea [Cadenas de conexión del Proveedor de datos de .NET Framework para SQL Server](https://www.connectionstrings.com/sqlconnection/).

![Red de conexión de SQL Server](../../integration-services/import-export-data/media/sql-server-connection-net.png)
  
 **Origen de datos**  
 Escriba el nombre o la dirección IP del servidor que contiene los datos o elija un servidor de la lista.  
  
> [!NOTE] Si se encuentra en una red con varios servidores, será más sencillo escribir el nombre del servidor. Si hace clic en la lista desplegable, puede tardar mucho tiempo en consultar la red para obtener todos los servidores disponibles, y el nombre del servidor puede que no se encuentre en los resultados.  
 
 Para especificar un puerto TCP no estándar, escriba una coma después del nombre del servidor o la dirección IP y después escriba el número de puerto.
 
 **Catálogo original**  
 Escriba el nombre de la base de datos de origen o elija una base de datos de la lista.  
  
 **Seguridad integrada**  
 Especifique **True** para establecer la conexión mediante la autenticación integrada de Windows (opción recomendada) o **False** para conectarse mediante la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si especifica **False**, debe especificar un Id. de usuario y una contraseña. El valor predeterminado es **False**.  
  
 **Id. de usuario**  
 Proporcione un nombre de usuario para la conexión de la base de datos cuando use la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Contraseña**  
 Proporcione la contraseña para la conexión de la base de datos cuando use la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

## <a name="oracle"></a>Oracle

Conéctese a Oracle mediante el proveedor de datos .NET Framework para Oracle o el proveedor OLE DB de Microsoft para Oracle. El proveedor de datos .NET Framework para Oracle es más sencillo de configurar y se muestra en la siguiente captura de pantalla.

Para más información, vea [Cadenas de conexión del Proveedor de datos de .NET Framework para Oracle](https://www.connectionstrings.com/net-framework-data-provider-for-oracle/) o [Cadenas de conexión del Proveedor OLE DB de Microsoft para Oracle](https://www.connectionstrings.com/microsoft-ole-db-provider-for-oracle-msdaora/).

![Conexión de Oracle](../../integration-services/import-export-data/media/oracle-connection.png)

## <a name="odbc-data-sources"></a>orígenes de datos de ODBC

Para cargar datos de cualquier origen que proporcione un controlador ODBC, seleccione el Proveedor de datos de .NET Framework para ODBC.

Para proporcionar una cadena de conexión para un origen de datos de ODBC, vea la documentación del controlador ODBC que quiera usar o busque ejemplos aquí: [Referencia de Connection Strings](https://www.connectionstrings.com/). 

En la siguiente captura de pantalla se muestra una conexión ODBC a SQL Server como ejemplo. La cadena de conexión que se ha usado en el ejemplo es:

    Driver={SQL Server};Server=(local);Database=TestData;Trusted_Connection=Yes;

Después de escribir la cadena de conexión en el campo **ConnectionString**, el asistente analiza la cadena y muestra las propiedades individuales y sus valores en la sección **Varios** de la lista.

![Conexión ODBC a SQL](../../integration-services/import-export-data/media/odbc-connection-sql.png)

## <a name="text-files-flat-files"></a>Archivos de texto (archivos planos)
 
 Existen varias páginas de opciones para los orígenes de datos de archivos planos.
 
 ### <a name="general-page"></a>Página General
 En la página **General**, busque y seleccione el archivo, y compruebe la configuración en la sección **Formato**.
 
 ![Conexión general de archivos planos](../../integration-services/import-export-data/media/flat-file-connection-general.png)  
   
Para obtener más información sobre la página **General**, consulte la siguiente página de referencia de Integration Services: [Editor del administrador de conexiones de archivos planos &#40;página General&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-general-page.md).  

### <a name="columns-page"></a>Página Columnas

 En la página **Columnas**, compruebe la lista de columnas y los delimitadores que el asistente ha identificado.
 
 ![Columnas de conexión de archivos planos](../../integration-services/import-export-data/media/flat-file-connection-columns.png)
  
Para obtener más información sobre la página **Columnas**, consulte la siguiente página de referencia de Integration Services: [Editor del administrador de conexiones de archivos planos &#40;página Columnas&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-columns-page.md).

### <a name="advanced-page"></a>Página Avanzadas

La página **Avanzadas** muestra información detallada sobre cada columna del origen de datos, incluidos su tamaño y tipo de datos.

En la siguiente captura de pantalla, tenga en cuenta que la columna **id** inicialmente tiene un tipo de datos de cadena.

![Conexión avanzada de archivos planos (inicial)](../../integration-services/import-export-data/media/flat-file-connection-advanced-before.png)

Haga clic en **Sugerir tipos** para mostrar el cuadro de diálogo **Sugerir tipos de columna**. 

![Sugerencia de conexiones de archivos planos](../../integration-services/import-export-data/media/flat-file-connection-suggest.png)

Después de que elija las opciones en el cuadro de diálogo **Sugerir tipos de columna** y haga clic en **Aceptar**, el asistente puede cambiar los tipos de datos de algunas de las columnas que se van a importar.

En la siguiente captura de pantalla se muestra que el asistente ha reconocido que la columna **id** del origen de datos es, de hecho, un número y no una cadena de texto, y ha cambiado el tipo de datos de la columna de una columna a un entero.

![Conexión avanzada de archivos planos (posterior)](../../integration-services/import-export-data/media/flat-file-connection-advanced-after.png)
  
Para obtener más información sobre la página **Avanzadas**, consulte la siguiente página de referencia de Integration Services: [Editor del administrador de conexiones de archivos planos &#40;página Avanzadas&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-advanced-page.md).

### <a name="preview-page"></a>Página Vista previa

En la página **Vista previa**, compruebe que la lista de columnas y los datos de ejemplos son lo que esperaba.

![Vista previa de conexiones de archivos planos](../../integration-services/import-export-data/media/flat-file-connection-preview.png)

Para obtener más información sobre la página **Vista previa**, consulte la siguiente página de referencia de Integration Services: [Editor del administrador de conexiones de archivos planos &#40;página Vista previa&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-preview-page.md).  
 
## <a name="microsoft-excel"></a>Microsoft Excel

En la siguiente captura de pantalla se muestra una conexión de ejemplo a un libro de Microsoft Excel.

![Conexión de Excel](../../integration-services/import-export-data/media/excel-connection.png) 
 
 **Ruta de acceso del archivo Excel**  
 Especifique la ruta de acceso y el nombre de archivo correspondientes a la hoja de cálculo desde la que se importarán los datos. Por ejemplo, **C:\\MisDatos.xlsx** para un archivo en el equipo local, o **\\\\Ventas\\BaseDeDatos\\Northwind.xlsx** para un archivo en un recurso compartido de red. O bien, haga clic en **Examinar**.  
  
 **Examinar**  
 Busque la hoja de cálculo desde el cuadro de diálogo **Abrir**.  

> [!NOTE] El asistente no puede abrir un archivo de Excel protegido mediante contraseña.

 **Versión de Excel**  
 Seleccione la versión de Excel que usa el libro de origen.

Es posible que tenga que descargar e instalar archivos adicionales para conectarse a la versión de Excel que seleccione. Consulte [Obtener las descargas que necesita para Excel y Access](Choose%20a%20Data%20Source%20\%28SQL%20Server%20Import%20and%20Export%20Wizard%29.md\#officeDownloads) en esta página para obtener más información.

Si tiene un problema al especificar una versión (por ejemplo, si no puede instalar el tiempo de ejecución de Access 2016 porque tiene Microsoft Office 365), pruebe a especificar una versión diferente, incluso una versión anterior (por ejemplo, 2013 en lugar de 2016).

**La primera fila tiene nombres de columna**  
Indique si la primera fila de los datos de origen contiene nombres de columna.
-   Si los datos de origen no contienen nombres de columna pero se habilita esta opción, el asistente trata la primera fila de los datos de origen como los nombres de columna.
-   Si los datos de origen contienen nombres de columna pero se deshabilita esta opción, el asistente trata la fila de nombres de columna como la primera fila de datos.

Si el origen de datos no tiene nombres de columna, el asistente usa F1, F2, etc. de forma interna como encabezados de columna temporales.

## <a name="microsoft-access"></a>Microsoft Access  

En la siguiente captura de pantalla se muestra una conexión de ejemplo a una base de datos de Microsoft Access.

![Conexión de Access](../../integration-services/import-export-data/media/access-connection.png)

 **Nombre de archivo**  
 Especifique la ruta de acceso y el nombre de archivo correspondientes al archivo de base de datos desde el que se importarán los datos. Por ejemplo, **C:\MyData.mdb, \\\Sales\Database\Northwind.mdb**. O bien, haga clic en **Examinar**.
 
 >   [!NOTE] El asistente solo puede conectarse a una base de datos de Access en el formato de archivo .MDB.  
  
 **Examinar**  
 Busque el archivo de base de datos desde el cuadro de diálogo **Abrir**.  
  
 **Nombre de usuario**  
Proporcione un nombre de usuario válido para la conexión de base de datos cuando un archivo de información de grupo de trabajo se asocie a la base de datos.  
  
 **Contraseña**  
Proporcione la contraseña de usuario para la conexión de base de datos cuando un archivo de información de grupo de trabajo se asocie a la base de datos.
 
Si la base de datos está protegida con una única contraseña para todos los usuarios, debe proporcionar este valor en el cuadro de diálogo **Propiedades de vínculo de datos**. Para abrir el cuadro de diálogo **Propiedades de vínculo de datos**, haga clic en **Avanzadas**.  
  
 **Avanzadas**  
Especifique las opciones avanzadas, como la contraseña de la base de datos o un archivo de información del grupo de trabajo no predeterminado, mediante el cuadro de diálogo **Propiedades de vínculo de datos**.  
  
## <a name="a-nameofficedownloadsaget-the-downloads-you-need-for-excel-and-access"></a><a name="officeDownloads"></a>Obtener las descargas que necesita para Excel y Access  
Es posible que tenga que descargar los componentes de conectividad para orígenes de datos de Microsoft Excel y Access si aún no están instalados.

Las versiones posteriores de los componentes pueden abrir archivos creados con versiones anteriores de los programas. En algunos casos, las versiones anteriores de los componentes también pueden abrir archivos creados con versiones posteriores de los programas.  
  
Si el equipo tiene una versión de 32 bits de Office, tendrá que instalar la versión de 32 bits de los componentes. También debe asegurarse de que ejecuta el asistente (o el paquete de Integration Services que crea) en modo de 32 bits.  
|Versión de Microsoft Office|Descargar|  
|------------------------------|--------------|  
|2007|[Controlador de 2007 Office System: componentes de conectividad de datos](https://www.microsoft.com/download/details.aspx?id=23734)|  
|2010|[Microsoft Access 2010 Runtime](https://www.microsoft.com/download/details.aspx?id=10910)|  
|2013|[Microsoft Access 2013 Runtime](http://www.microsoft.com/download/details.aspx?id=39358)|  
|2016|[Microsoft Access 2016 Runtime](https://www.microsoft.com/download/details.aspx?id=50040)|  
 
 
## <a name="azure-blob-storage"></a>Almacenamiento de blobs de Azure  
Para usar el origen de blobs de Azure, tendrá que instalar el Feature Pack de Azure para SSIS. Para obtener más información, vea [Azure Feature Pack para Integration Services &#40;SSIS&#41;](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).  

>   [!NOTE] Para garantizar que el Administrador de conexiones de almacenamiento de Azure y los componentes que lo usan (incluido el origen de blob) se puedan conectar tanto a las cuentas de almacenamiento general como a las cuentas de almacenamiento de blobs, descargue la versión más reciente de Azure Feature Pack [aquí](https://www.microsoft.com/download/details.aspx?id=49492). Para más información sobre estos dos tipos de cuentas de almacenamiento, vea [Introducción a Almacenamiento de Microsoft Azure](https://azure.microsoft.com/en-us/documentation/articles/storage-introduction/#general-purpose-storage-accounts).

![conexión de Almacenamiento de blobs de Azure](../../integration-services/import-export-data/media/azure-blob-storage-connection.png)

 **Usar una cuenta de Azure**  
 Especifique si usa una cuenta en línea.
  
 **Nombre de la cuenta de almacenamiento**  
 Especifique el nombre de la cuenta de almacenamiento de Azure.  
  
**Clave de cuenta**  
Proporcione la clave para la cuenta de almacenamiento de Azure.  
  
 **Usar HTTPS**  
 Especifique si desea utilizar HTTP o HTTPS para conectarse a la cuenta de almacenamiento.  
  
 **Usar cuenta de desarrollador local**  
 Especifique si desea utilizar el emulador de almacenamiento en el equipo local.  
  
 **Nombre del contenedor de blob**  
 Seleccione uno en la lista de contenedores de almacenamiento disponibles en la cuenta de almacenamiento especificada.  
  
 **Formato de archivo de blob**  
 Seleccione el formato de archivo de texto o Avro.  
  
 **Carácter delimitador de columna**  
 Si selecciona el formato de texto, especifique el carácter delimitador de columna.  
  
 **Usar la primera fila como nombres de columna**  
 Especifique si la primera fila de datos contiene nombres de columna.  
  
## <a name="whats-next"></a>¿Qué sigue?  
 Después de proporcionar información sobre el origen de datos y la manera de conectarse a él, la página siguiente es **Elegir un destino**. En esta página, debe proporcionar información sobre el destino de datos y la manera de conectarse a él. Para más información, vea [Elegir un destino](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md).  
