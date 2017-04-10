---
title: "Elegir un destino (Asistente para importaci&#243;n y exportaci&#243;n de SQL Server) | Microsoft Docs"
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
  - "sql13.dts.impexpwizard.chooseadestination.f1"
ms.assetid: 1898be15-3e69-42d3-8ecb-3733c9f6c8e3
caps.latest.revision: 104
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 95
---
# Elegir un destino (Asistente para importaci&#243;n y exportaci&#243;n de SQL Server)
 Después de proporcionar información sobre el origen de datos y la manera de conectarse a él, el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muestra la página **Elegir un destino**. En esta página, debe proporcionar información sobre el destino de datos y la manera de conectarse a él.
  
Para obtener más información sobre los destinos de datos que puede usar, consulte [¿Qué orígenes de datos y destinos puedo usar?](Import%20and%20Export%20Data%20with%20the%20SQL%20Server%20Import%20and%20Export%20Wizard.md\#wizardSources). 

## <a name="screen-shot-of-the-destination-page"></a>Captura de pantalla de la página Destino
En la captura de pantalla siguiente, se muestra la primera parte de la página **Seleccionar un destino** del asistente.

![Elegir un destino](../../integration-services/import-export-data/media/choose-destination.png)

## <a name="choose-a-destination"></a>Seleccionar un destino
 **Destino**  
 Para especificar el destino, seleccione un proveedor de datos que pueda importar los datos al destino. En la mayoría de los casos, el proveedor de datos que necesita es obvio por su nombre, ya que el nombre del proveedor contiene el nombre del destino; por ejemplo, SQL Server, Oracle, archivos planos, Excel y Access.
 
La lista de los proveedores de datos disponibles en la lista **Destino** depende de los proveedores instalados en su equipo. También depende de si está ejecutando el asistente de 32 o 64 bits.

Es posible que haya más de un proveedor disponible para el destino. Normalmente, puede seleccionar cualquier proveedor que funcione con su destino. Por ejemplo, para conectarse a Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, el Proveedor de datos .NET Framework para SQL Server o el Proveedor OLE DB de Microsoft para SQL Server.
 
En algunos casos, tiene que empezar seleccionando el proveedor de datos genérico. Por ejemplo, si tiene un controlador ODBC para su destino, seleccione el proveedor de datos .NET Framework para ODBC.

Para algunos destinos, puede que tenga que descargar el proveedor de datos de Microsoft o de un tercero. Para obtener más información sobre los destinos de datos que puede usar, consulte [¿Qué orígenes de datos y destinos puedo usar?](Import%20and%20Export%20Data%20with%20the%20SQL%20Server%20Import%20and%20Export%20Wizard.md\#wizardSources).

## <a name="after-you-choose-a-destination"></a>Después de seleccionar un destino
Después de elegir un destino, el resto de la propiedad de página **Elegir un destino** tiene un número variable de opciones que dependen del proveedor de datos que elija.

En las siguientes secciones se enumeran opciones importantes para algunos destinos que se usan frecuentemente. Aquí no encontrará todos los destinos disponibles en la lista desplegable **Destino**. Para obtener opciones y proveedores adicionales, vea la documentación específica del proveedor.

> [!TIP] Si su destino necesita una cadena de conexión, encontrará ejemplos en este sitio de terceros: [The Connection Strings Reference](https://www.connectionstrings.com/) (Referencia de Connection Strings).  

## <a name="microsoft-sql-server"></a>Microsoft SQL Server 

Si quiere crear una base de datos de SQL Server como destino, seleccione SQL Server Native Client o el proveedor Microsoft OLE DB para SQL Server. Si selecciona el proveedor de datos .NET Framework para SQL Server, la opción para crear una base de datos no está disponible.  

### <a name="connect-to-sql-server-with-sql-server-native-client-or-the-microsoft-ole-db-provider-for-sql-server"></a>Conectarse a SQL Server con SQL Server Native Client o con el proveedor OLE DB de Microsoft para SQL Server  

SQL Server Native Client y el proveedor OLE DB de Microsoft para SQL Server exponen el mismo conjunto de opciones. En la siguiente captura de pantalla se muestran las opciones de SQL Server Native Client como ejemplo.

![Destino de SQL Native](../../integration-services/import-export-data/media/sql-native-destination.png)

 **Nombre del servidor**  
 Escriba el nombre o la dirección IP del servidor de destino o elija un servidor de la lista.  
  
> [!NOTE] Si se encuentra en una red con varios servidores, será más sencillo escribir el nombre del servidor. Si hace clic en la lista desplegable, puede tardar mucho tiempo en consultar la red para obtener todos los servidores disponibles, y el nombre del servidor puede que no se encuentre en los resultados.  
 
 Para especificar un puerto TCP no estándar, escriba una coma después del nombre del servidor o la dirección IP y después escriba el número de puerto.
 
 **Utilizar autenticación de Windows**  
 Especifique si el asistente debe usar la autenticación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows para iniciar sesión en la base de datos. Se recomienda la autenticación de Windows.  
  
 **Utilizar autenticación de SQL Server**  
 Especifique si el asistente debe usar la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para iniciar sesión en la base de datos. Si usa la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , debe proporcionar un nombre de usuario y una contraseña.  
  
 **Nombre de usuario**  
 Proporcione un nombre de usuario para la conexión de la base de datos cuando use la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Contraseña**  
 Proporcione la contraseña para la conexión de la base de datos cuando use la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Base de datos**  
 Seleccione una base de datos de la lista de bases de datos de la instancia especificada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Actualizar**  
 Para restaurar la lista de bases de datos disponibles, haga clic en **Actualizar**.  
  
### <a name="connect-to-sql-server-with-the-net-framework-data-provider-for-sql-server"></a>Conectarse a SQL Server con el proveedor de datos .NET Framework para SQL Server 

Esta página presenta una lista agrupada de opciones para el proveedor de datos [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Las opciones importantes se enumeran aquí. Las opciones adicionales que aparecen al seleccionar este proveedor no son necesarias para establecer conexión correctamente con la base de datos de destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 

Para obtener más información, vea [.NET Framework Data Provider for SQL Server connection strings](https://www.connectionstrings.com/sqlconnection/) (Cadenas de conexión del proveedor de datos .NET Framework para SQL Server).

![Red de destino de SQL Server](../../integration-services/import-export-data/media/sql-server-destination-net.png)
  
 **Destino**  
 Escriba el nombre o la dirección IP del servidor de destino o elija un servidor de la lista.  
  
> [!NOTE] Si se encuentra en una red con varios servidores, será más sencillo escribir el nombre del servidor. Si hace clic en la lista desplegable, puede tardar mucho tiempo en consultar la red para obtener todos los servidores disponibles, y el nombre del servidor puede que no se encuentre en los resultados.  
 
 Para especificar un puerto TCP no estándar, escriba una coma después del nombre del servidor o la dirección IP y después escriba el número de puerto.
 
 **Catálogo original**  
 Escriba el nombre de la base de datos de destino o elija una base de datos de la lista.  
  
 **Seguridad integrada**  
 Especifique **True** para establecer la conexión mediante la autenticación integrada de Windows (opción recomendada) o **False** para conectarse mediante la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si especifica **False**, debe especificar un Id. de usuario y una contraseña. El valor predeterminado es **False**.  
  
 **Id. de usuario**  
 Proporcione un nombre de usuario para la conexión de la base de datos cuando use la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Contraseña**  
 Proporcione la contraseña para la conexión de la base de datos cuando use la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

## <a name="oracle"></a>Oracle

Conéctese a Oracle mediante el proveedor de datos .NET Framework para Oracle o el proveedor OLE DB de Microsoft para Oracle. El proveedor de datos .NET Framework para Oracle es más sencillo de configurar y se muestra en la siguiente captura de pantalla.

Para obtener más información, vea [.NET Framework Data Provider for Oracle connection strings](https://www.connectionstrings.com/net-framework-data-provider-for-oracle/) (Cadenas de conexión del proveedor de datos .NET Framework para Oracle) o [Microsoft OLE DB Provider for Oracle connection strings](https://www.connectionstrings.com/microsoft-ole-db-provider-for-oracle-msdaora/) (Cadenas de conexión del proveedor OLE DB de Microsoft para Oracle).

![Destino de Oracle](../../integration-services/import-export-data/media/oracle-destination.png)

## <a name="odbc-destinations"></a>Destinos de ODBC

Para guardar datos en cualquier destino que proporcione un controlador ODBC, seleccione el proveedor de datos .NET Framework para ODBC.

Para proporcionar una cadena de conexión para un destino de ODBC, vea la documentación del controlador ODBC que quiera usar o busque ejemplos aquí: [The Connection Strings Reference](https://www.connectionstrings.com/) (Referencia de Connection Strings). 

En la siguiente captura de pantalla se muestra una conexión ODBC a SQL Server como ejemplo. La cadena de conexión que se ha usado en el ejemplo es:

    Driver={SQL Server};Server=(local);Database=TestData;Trusted_Connection=Yes;

Después de escribir la cadena de conexión en el campo **ConnectionString**, el asistente analiza la cadena y muestra las propiedades individuales y sus valores en la sección **Varios** de la lista.

![Destino de conexión ODBC a SQL](../../integration-services/import-export-data/media/odbc-connection-sql-destination.png)

 ## <a name="text-files-flat-files"></a>Archivos de texto (archivos planos)
 
![Destino de archivo plano](../../integration-services/import-export-data/media/flat-file-destination.png)  

**Nombre de archivo**  
 Especifique la ruta de acceso y el nombre de archivo correspondiente al archivo en el que almacenará los datos. O bien, haga clic en **Examinar** para buscar un archivo.  
  
 **Examinar**  
 Busque un archivo mediante el cuadro de diálogo **Abrir**.  
  
 **Configuración regional**  
 Especifique el Id. de configuración regional (LCID) que define el criterio de ordenación de los caracteres y el formato de fecha y hora.  
  
 **Unicode**  
 Indique si se va a utilizar Unicode. Si utiliza Unicode, no es necesario que especifique una página de códigos.  
  
 **Página de códigos**  
 Especifique la página de códigos correspondiente al idioma que desea utilizar.  
  
 **Formato**  
 Indique si se utiliza formato delimitado, de ancho fijo o derecho irregular.  
  
|Value|Description|  
|-----------|-----------------|  
|Delimitado|Las columnas se separan mediante un delimitador.|  
|Ancho fijo|Las columnas tienen un ancho fijo.|  
|Derecho irregular|Los archivos de derecho irregular son archivos en los que todas las columnas tienen un ancho fijo, a excepción de la última, que está delimitada por el delimitador de filas.|  
  
 **Calificador de texto**  
 Escriba el calificador de texto que desea utilizar. Puede, por ejemplo, especificar que el texto de cada columna se encierre entre comillas.  
  
 **Nombres de columna de la primera fila de datos**  
 Indique si desea mostrar los nombres de las columnas de la primera fila de datos.  
 
 ## <a name="microsoft-excel"></a>Microsoft Excel

>  **Vídeo**: un uso común del asistente es exportar datos a Excel. Aquí tiene un vídeo de cuatro minutos de YouTube en el que se explica cómo realizarlo con instrucciones simples y claras. [Using the SQL Server Import and Export Wizard to Export to Excel](https://go.microsoft.com/fwlink/?linkid=829049) (Usar el Asistente para importación y exportación de SQL Server para exportar a Excel). (En el vídeo, se usa [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 2012).

En la siguiente captura de pantalla se muestra una conexión de ejemplo a un libro de Microsoft Excel.

![Destino de Excel](../../integration-services/import-export-data/media/excel-destination.png) 
 
 **Ruta de acceso del archivo Excel**  
 Especifique la ruta de acceso y el nombre de archivo correspondientes a la hoja de cálculo a la que se exportarán los datos. Por ejemplo, **C:\\MisDatos.xlsx** para un archivo en el equipo local, o **\\\\Ventas\\BaseDeDatos\\Northwind.xlsx** para un archivo en un recurso compartido de red. O bien, haga clic en **Examinar**.   
  
 **Examinar**  
 Busque la hoja de cálculo desde el cuadro de diálogo **Abrir**.  

> [!NOTE] El asistente no puede abrir un archivo de Excel protegido mediante contraseña.

 **Versión de Excel**  
Seleccione la versión de Excel que usa el libro de destino.  

Es posible que tenga que descargar e instalar archivos adicionales para conectarse a la versión de Excel que seleccione. Consulte [Obtener las descargas que necesita para Excel y Access](Choose%20a%20Data%20Source%20\%28SQL%20Server%20Import%20and%20Export%20Wizard%29.md\#officeDownloads) en esta página para obtener más información.

Si tiene un problema al especificar una versión (por ejemplo, si no puede instalar el tiempo de ejecución de Access 2016 porque tiene Microsoft Office 365), pruebe a especificar una versión diferente, incluso una versión anterior (por ejemplo, 2013 en lugar de 2016).

**La primera fila tiene nombres de columna**  
Esta opción parece no tener ningún efecto en un destino de Excel. Si el destino no tiene nombres de columna, el controlador no genera nombres de columna, incluso con esta opción habilitada. De forma interna, el asistente usa F1, F2, etc. como encabezados de columna temporales.
 
## <a name="microsoft-access"></a>Microsoft Access  

En la siguiente captura de pantalla se muestra una conexión de ejemplo a una base de datos de Microsoft Access.

![Destino de Access](../../integration-services/import-export-data/media/access-destination.png)

 **Nombre de archivo**  
 Especifique la ruta de acceso y el nombre de archivo correspondientes al archivo de base de datos al que se exportarán los datos. Por ejemplo, **C:\MyData.mdb, \\\Sales\Database\Northwind.mdb**. O bien, haga clic en **Examinar**.
 
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
Para usar el destino de Blob de Azure, tendrá que instalar el Feature Pack de Azure para SSIS. Para obtener más información, vea [Azure Feature Pack para Integration Services &#40;SSIS&#41;](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).  

>   [!NOTE] Para garantizar que el Administrador de conexiones de almacenamiento de Azure y los componentes que lo usan (incluido el destino de blobs) se puedan conectar tanto a las cuentas de almacenamiento general como a las cuentas de almacenamiento de blobs, descargue la versión más reciente de Azure Feature Pack [aquí](https://www.microsoft.com/download/details.aspx?id=49492). Para obtener más información sobre estos dos tipos de cuentas de almacenamiento, vea [Introducción a Almacenamiento de Microsoft Azure](https://azure.microsoft.com/en-us/documentation/articles/storage-introduction/#general-purpose-storage-accounts).

![Destino de blobs de Azure](../../integration-services/import-export-data/media/azure-blob-destination.png)

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

## <a name="whats-next"></a>¿Qué debe hacer a continuación?  
 Después de proporcionar información sobre el destino de los datos y sobre cómo se conectará a estos, la página siguiente es **Especificar copia de tabla o consulta**. En esta página, especifique si quiere copiar una tabla completa o solo algunas filas. Para obtener más información, vea [Especificar copia de tabla o consulta](../../integration-services/import-export-data/specify-table-copy-or-query-sql-server-import-and-export-wizard.md).  
