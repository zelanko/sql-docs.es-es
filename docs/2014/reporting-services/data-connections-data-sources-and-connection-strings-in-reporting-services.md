---
title: Conexiones de datos, orígenes de datos y cadenas de conexión en Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- connections [Reporting Services], data sources
- reports [Reporting Services], data
- expressions [Reporting Services], data sources
- data sources [Reporting Services], connections
- connection strings [Reporting Services]
- shared data sources [Reporting Services]
- Reporting Services, data sources
- logins [Reporting Services]
ms.assetid: 4d8f0ae1-102b-4b3d-9155-fa584c962c9e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 88f843db8280220b75025dc286fe692957bf2b77
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/28/2020
ms.locfileid: "78173964"
---
# <a name="data-connections-data-sources-and-connection-strings-in-reporting-services"></a>Data Connections, Data Sources, and Connection Strings in Reporting Services
  Para incluir datos en un informe de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , es preciso que antes cree *orígenes de datos* y *conjuntos de datos*. En este tema, se describe el tipo de orígenes de datos y cómo crear orígenes de datos, además se ofrece información importante relacionada con las credenciales de los orígenes de datos. Un origen de datos incluye el tipo de origen de datos, la información de conexión y el tipo de credenciales que se han de usar. Hay dos tipos de orígenes de datos: incrustados y compartidos. Un origen de datos incrustado se define en el informe y se usa solo en ese informe. Un origen de datos compartido se define independientemente de un informe y se puede usar en varios informes. Para obtener más información, vea [Conexiones de datos u orígenes de datos incrustados y compartidos &#40;Generador de informes y SSRS&#41;](../../2014/reporting-services/embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md) y [Conjuntos de datos incrustados y compartidos &#40;Generador de informes y SSRS&#41;](report-data/embedded-and-shared-datasets-report-builder-and-ssrs.md).

||
|-|
|**[!INCLUDE[applies](../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]Modo nativo &#124; [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] modo de SharePoint|

> [!NOTE]
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]



##  <a name="bkmk_data_sources"></a>Orígenes de datos incrustados y compartidos
 La diferencia entre los orígenes de datos incrustados y compartidos es la manera en que se crean, almacenan y administran.

-   En el Diseñador de informes, cree orígenes de datos incrustados o compartidos como parte de un proyecto de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] . Puede controlar si va a utilizarlos localmente para la obtención de una vista previa o implementarlos como parte del proyecto en un servidor de informes o un sitio de SharePoint. Puede utilizar las extensiones de datos personalizadas que se han instalado en el equipo y en el servidor de informes o un sitio de SharePoint donde se implementan los informes.

     Los administradores del sistema pueden instalar y configurar extensiones de procesamiento de datos y proveedores de datos de .NET Framework adicionales. Para obtener más información, vea [Extensiones de procesamiento de datos y proveedores de datos de .NET Framework &#40;SSRS&#41;](report-data/data-processing-extensions-and-net-framework-data-providers-ssrs.md).

     Los desarrolladores pueden usar la API de <xref:Microsoft.ReportingServices.DataProcessing> para crear extensiones de procesamiento de datos compatibles con tipos de orígenes de datos adicionales.

-   En el Generador de informes, desplácese a un servidor de informes o un sitio de SharePoint y seleccione orígenes de datos compartidos o cree orígenes de datos incrustados en el informe. No puede crear un origen de datos compartido en el Generador de informes. No puede utilizar extensiones de datos personalizadas en el Generador de informes

##  <a name="bkmk_DataConnections"></a>Extensiones de datos integradas
 Las extensiones de datos predeterminadas en [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] incluyen los siguientes tipos de conexiones de datos:

-   Microsoft SQL Server

-   Microsoft SQL Server Analysis Services

-   Lista de Microsoft SharePoint

-   [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)]

-   Almacenamiento de datos paralelo de Microsoft SQL Server

-   OLE DB

-   Oracle

-   SAP NetWeaver BI

-   Hyperion Essbase

-   Teradata

-   XML

-   ODBC

-   Modelo semántico de Microsoft BI para Power View: en un sitio de SharePoint que se haya configurado para una galería de PowerPoint y [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)], está disponible este tipo de origen de datos. Este tipo de origen de datos solo se usa para presentaciones de [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] . Para obtener más información, vea [compilar el Perfect BI Semantic Tabular Models para Power View](https://technet.microsoft.com/video/building-the-perfect-bi-semantic-tabular-models-for-power-view.aspx).

 Para obtener una lista completa de los orígenes de datos y las versiones que admite [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], vea [Orígenes de datos admitidos por Reporting Services &#40;SSRS&#41;](create-deploy-and-manage-mobile-and-paginated-reports.md).

##  <a name="bkmk_create_data_source"></a>Crear un origen de datos
 Para crear un origen de datos, debe disponer de la información siguiente:

-   **Tipo de origen de datos** El tipo de conexión, por ejemplo [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)],. Elija este valor en la lista desplegable de tipos de conexión.

-   **Información de conexión** La información de conexión incluye el nombre y la ubicación del origen de datos y las propiedades de conexión específicas de cada proveedor de datos. La *cadena de conexión* es la representación en texto de la información de conexión. Por ejemplo, si el origen de datos es una base de datos de SQL Server, puede especificar el nombre de la base de datos. Para los orígenes de datos incrustados, también puede escribir cadenas de conexión basadas en expresiones que se evalúan en tiempo de ejecución. Para obtener más información, vea [Cadenas de conexión basadas en expresiones](#bkmk_Expressions_in_connection_strings) más adelante en este tema.

-   **Credenciales** de Debe proporcionar las credenciales necesarias para tener acceso a los datos. El propietario del origen de datos debe haberle concedido los permisos apropiados para tener acceso al origen de datos y a los datos específicos del origen de datos. Por ejemplo, para conectar con la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../includes/sssampledbnormal-md.md)] instalada en un servidor de la red, debe tener permiso para conectar con el servidor así como permiso de solo lectura para tener acceso a la base de datos.

    > [!NOTE]
    >  Por diseño, las credenciales se administran independientemente de los orígenes de datos. Las credenciales que usa para obtener una vista previa del informe en un sistema local pueden ser distintas de las credenciales que necesita para ver el informe publicado. Después de guardar un origen de datos en el servidor de informes o en el sitio de SharePoint, es posible que necesite cambiar las credenciales para trabajar desde esa ubicación. Para obtener más información, vea [Credenciales para los orígenes de datos](#bkmk_credentials).

> [!NOTE]
>  Cuando cree un origen de datos incrustado para un informe en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], debe crear el origen de datos del Diseñador de informes en el Explorador de soluciones o en el panel Datos de informe, pero no en el Explorador de servidores. El Diseñador de informes de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no admite orígenes de datos de [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] creados en el Explorador de servidores.

 El panel Datos de informe muestra los orígenes de datos incrustados y las referencias a los orígenes de datos compartidos que se han agregado al informe. En el Generador de informes, una referencia de origen de datos compartido señala un origen de datos compartido en un servidor de informes o un sitio de SharePoint. En el Diseñador de informes, la referencia a un origen de datos compartido señala un origen de datos compartido del Explorador de soluciones en la carpeta Origen de datos compartido.

##  <a name="bkmk_credentials"></a>Credenciales para orígenes de datos
 Por diseño, las credenciales se pueden guardar y administrar independientemente de la información de conexión. Las credenciales se utilizan para crear un origen de datos, para ejecutar una consulta de conjunto de datos y para obtener la vista previa de un informe.

> [!NOTE]
>  Se recomienda no incluir información de inicio de sesión, como nombres y contraseñas de inicio de sesión, en las propiedades de conexión del origen de datos. Utilice orígenes de datos compartidos con credenciales almacenadas siempre que sea posible. En un entorno de creación, utilice la página Credenciales del cuadro de diálogo **Origen de datos** para especificar las credenciales al crear una conexión de datos o al ejecutar una consulta de conjunto de datos.

 Las credenciales que especifique para el acceso a datos desde el equipo se almacenan de forma segura en el archivo de configuración de proyecto local y son específicas del equipo. Si copia los archivos de proyecto en otro equipo, deberá volver a definir las credenciales para ese origen de datos.

 Cuando se implementa un informe en el servidor de informes o un sitio de SharePoint, los orígenes de datos incrustados y compartidos correspondientes se administran independientemente. Las credenciales del origen de datos necesarias para tener acceso a los datos del equipo pueden diferir de las credenciales necesarias para que el servidor de informes tenga acceso a los datos.

 ![Nota:](media/rs-fyinote.png "nota") Se recomienda comprobar que las conexiones de origen de datos continúan conectándose correctamente después de publicar un informe. Si necesita cambiar las credenciales, puede modificarlas directamente en el servidor de informes.

 Para cambiar los orígenes de datos que usa un informe, puede modificar las propiedades del informe en modo nativo Administrador de informes o desde bibliotecas de documentos en modo de SharePoint. Para obtener más información, vea lo siguiente:

-   [Almacenar credenciales en un Reporting Services](report-data/store-credentials-in-a-reporting-services-data-source.md) origen [de datos almacenar credenciales en un origen de datos de Reporting Services](report-data/store-credentials-in-a-reporting-services-data-source.md)

-   [Especificación de información de credenciales y conexión para los orígenes de datos de informes](report-data/specify-credential-and-connection-information-for-report-data-sources.md)

-   [Especificar conexiones para extensiones de procesamiento de datos personalizadas](report-data/specify-connections-for-custom-data-processing-extensions.md)

-   [Especificar credenciales en el Generador de informes](../../2014/reporting-services/specify-credentials-in-report-builder.md)

-   [Agregar y comprobar una conexión de datos o un origen de datos &#40;Generador de informes y SSRS&#41;](report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)

##  <a name="bkmk_connection_examples"></a>Ejemplos de cadenas de conexión comunes
 Las cadenas de conexión son la representación en texto de las propiedades de conexión para un proveedor de datos. En la tabla siguiente se muestran ejemplos de cadenas de conexión para diversos tipos de conexión.

|**Origen de datos**|**Ejemplo**|**Descripción**|
|---------------------|-----------------|---------------------|
|Base de datos de SQL Server en el servidor local|`data source="(local)";initial catalog=AdventureWorks`|Establezca el tipo de origen de datos en `Microsoft SQL Server`. Para obtener más información, vea [Tipo de conexión de SQL Server &#40;SSRS&#41;](report-data/sql-server-connection-type-ssrs.md).|
|Base de datos de SQL Server en el servidor local|`data source="(local)";initial catalog=AdventureWorks`|Establezca el tipo de origen de datos en `Microsoft SQL Server`.|
|Instancia de SQL Server<br /><br /> database|`Data Source=localhost\MSSQL10_50.InstanceName; Initial Catalog=AdventureWorks`|Establezca el tipo de origen de datos en `Microsoft SQL Server`.|
|Base de datos de SQL Server Express|`Data Source=localhost\MSSQL10_50.SQLEXPRESS; Initial Catalog=AdventureWorks`|Establezca el tipo de origen de datos en `Microsoft SQL Server`.|
|[!INCLUDE[ssSDS](../includes/sssds-md.md)]en la nube|`Data Source=<host>;Initial Catalog=AdventureWorks; Encrypt=True`|Establezca el tipo de origen de datos en `Azure SQL Database`. Para obtener más información, vea [Tipo de conexión SQL Azure &#40;SSRS&#41;](report-data/sql-azure-connection-type-ssrs.md).|
|Almacenamiento de datos paralelo de SQL Server|`HOST=<IP address>;database= AdventureWorks; port=<port>`|Establezca el tipo de origen de datos en `Microsoft SQL Server Parallel Data Warehouse`. Para obtener más información, vea [Tipo de conexión Almacenamiento de datos paralelo de SQL Server &#40;SSRS&#41;](report-data/sql-server-parallel-data-warehouse-connection-type-ssrs.md).|
|Base de datos de Analysis Services en el servidor local|`data source=localhost;initial catalog=Adventure Works DW`|Establezca el tipo de origen de datos en `Microsoft SQL Server Analysis Services`. Para más información, vea [Tipo de conexión de Analysis Services para MDX &#40;SSRS&#41;](report-data/analysis-services-connection-type-for-mdx-ssrs.md) o [Tipo de conexión de Analysis Services para DMX &#40;SSRS&#41;](report-data/analysis-services-connection-type-for-dmx-ssrs.md).|
|Base de datos de modelo tabular de Analysis Services con una perspectiva Sales|`Data source=<servername>;initial catalog= Adventure Works DW;cube='Sales'`|Establezca el tipo de origen de datos en `Microsoft SQL Server Analysis Services`. Especifique el nombre de la perspectiva en la configuración cube=. Para obtener más información, vea [Perspectivas &#40;SSAS tabular&#41;](https://docs.microsoft.com/analysis-services/tabular-models/perspectives-ssas-tabular).|
|Origen de datos de modelo de informe en un servidor de informes configurado en modo nativo|`Server=http://myreportservername/reportserver; datasource=/models/Adventure Works`|Especifique la dirección URL del servidor de informes o de la biblioteca de documentos, y la ruta de acceso al modelo publicado en el espacio de nombres de la carpeta del servidor de informes o de la carpeta de la biblioteca de documentos.
|Origen de datos de modelo de informe en un servidor de informes configurado en el modo integrado de SharePoint|`Server=http://server; datasource=http://server/site/documents/models/Adventure Works.smdl`|Especifique la dirección URL del servidor de informes o de la biblioteca de documentos, y la ruta de acceso al modelo publicado en el espacio de nombres de la carpeta del servidor de informes o de la carpeta de la biblioteca de documentos.|
|
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Servidor de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 2000|`provider=MSOLAP.2;data source=<remote server name>;initial catalog=FoodMart 2000`|Configure el tipo de origen de datos en `OLE DB Provider for OLAP Services 8.0`.<br /><br /> Puede conseguir una conexión más rápida con orígenes de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2000 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] si establece la propiedad `ConnectTo` en `8.0`. Para establecer esta propiedad, use la pestaña **Propiedades avanzadas** del cuadro de diálogo **Propiedades de conexión** .|
|Servidor Oracle|`data source=myserver`|Configure el tipo de origen de datos en `Oracle`. También es necesario instalar las herramientas de cliente de Oracle tanto en el equipo del Diseñador de informes como en el servidor de informes. Para obtener más información, vea [Tipo de conexión de Oracle &#40;SSRS&#41;](report-data/oracle-connection-type-ssrs.md).|
|Origen de datos SAP Netweaver BI|`DataSource=http://mySAPNetWeaverBIServer:8000/sap/bw/xml/soap/xmla`|Configure el tipo de origen de datos en `SAP NetWeaver BI`. Para obtener más información, vea [Tipo de conexión de SAP NetWeaver BI &#40;SSRS&#41;](report-data/sap-netweaver-bi-connection-type-ssrs.md).|
|Origen de datos de Hyperion Essbase|`Data Source=http://localhost:13080/aps/XMLA; Initial Catalog=Sample`|Configure el tipo de origen de datos en `Hyperion Essbase`. Para obtener más información, vea [Tipo de conexión de Hyperion Essbase &#40;SSRS&#41;](report-data/hyperion-essbase-connection-type-ssrs.md).|
|Origen de datos de Teradata|`data source=`\<NNN>. \<Nnn>. \<Nnn>. \<Nnn>`;`|Configure el tipo de origen de datos en `Teradata`. La cadena de conexión es una dirección IP (protocolo de Internet) formada por cuatro campos, donde cada campo puede tener de uno a tres dígitos. Para más información, vea [Tipo de conexión de Teradata &#40;SSRS&#41;](report-data/teradata-connection-type-ssrs.md).|
|Origen de datos XML, servicio web|`data source=http://adventure-works.com/results.aspx`|Configure el tipo de origen de datos en `XML`. La cadena de conexión es una dirección URL de un servicio web que admite el Lenguaje de definición de servicios web (WSDL). Para más información, vea [Tipo de conexión XML &#40;SSRS&#41;](report-data/xml-connection-type-ssrs.md).|
|Origen de datos XML, documento XML|`http://localhost/XML/Customers.xml`|Configure el tipo de origen de datos en `XML`. La cadena de conexión es una dirección URL que lleva al documento XML.|
|Origen de datos XML, documento XML incrustado|*Vacía*|Configure el tipo de origen de datos en `XML`. Los datos XML se incrustan en la definición de informe.|

Si no puede conectar con un servidor de informes mediante `localhost`, compruebe que se ha habilitado el protocolo de red TCP/IP. Para obtener más información, consulte [Configure Client Protocols](../database-engine/configure-windows/configure-client-protocols.md).

##  <a name="bkmk_special_password_characters"></a>Caracteres especiales en una contraseña
 Si configura el origen de datos ODBC o SQL para que le solicite una contraseña o la incluya en la cadena de conexión y un usuario especifica una contraseña con caracteres especiales, como por ejemplo signos de puntuación, algunos controladores de origen de datos subyacentes no podrán validar los caracteres especiales. Cuando procese el informe, es posible que aparezca un mensaje para indicarle que la contraseña no es válida. Si cambiar la contraseña resulta poco práctico, hable con el administrador de la base de datos para almacenar las credenciales adecuadas en el servidor como parte de un nombre del origen de datos OBDC (DSN) del sistema. Para obtener información, vea "OdbcConnection.ConnectionString" en la documentación de [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] SDK.

##  <a name="bkmk_Expressions_in_connection_strings"></a>Cadenas de conexión basadas en expresiones
 Las cadenas de conexión basadas en expresiones se evalúan en tiempo de ejecución. Por ejemplo, puede especificar el origen de datos como un parámetro, incluir la referencia de parámetro en la cadena de conexión y permitir al usuario elegir un origen de datos para el informe. Por ejemplo, imagine que una empresa multinacional tiene servidores de datos en varios países. Con una cadena de conexión basada en una expresión, un usuario que ejecute un informe de ventas puede seleccionar un origen de datos para un país determinado antes de ejecutar el informe.

 El ejemplo siguiente ilustra el uso de una expresión de origen de datos en una cadena de conexión de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . En el ejemplo se da por hecho que se ha creado un parámetro de informe denominado `ServerName`:

```
="data source=" & Parameters!ServerName.Value & ";initial catalog=AdventureWorks"
```

 Las expresiones de origen de datos se procesan en tiempo de ejecución o cuando se genera una vista previa del informe. La expresión debe estar escrita en [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]. Use las directrices siguientes cuando defina una expresión de origen de datos:

-   Diseñe el informe usando una cadena de conexión estática. Una cadena de conexión estática es una cadena de conexión que no se ha establecido mediante una expresión (por ejemplo, cuando sigue lo pasos para crear un origen de datos específico para el informe o compartido, está definiendo una cadena de conexión estática). Usar una cadena de conexión estática permite conectarse al origen de datos en el Diseñador de informes, de forma que puede obtener los resultados de la consulta que necesita para crear el informe.

-   Cuando defina una conexión de origen de datos, no use un origen de datos compartido. No es posible usar una expresión de origen de datos en un origen de datos compartido. Deberá definir un origen de datos incrustado para el informe.

-   Especifique las credenciales independientemente de la cadena de conexión. Puede utilizar credenciales almacenadas, credenciales solicitadas o seguridad integrada.

-   Agregue un parámetro de informe para especificar un origen de datos. Para los valores de parámetro, puede proporcionar una lista estática de valores disponibles (en este caso, los valores disponibles deben ser orígenes de datos que pueda usar con el informe) o definir una consulta que recupere una lista de orígenes de datos en tiempo de ejecución.

-   Asegúrese de que la lista de orígenes de datos comparta el mismo esquema de la base de datos. El diseño de un informe empieza con la información de esquema. Si el esquema utilizado para definir el informe y el esquema real utilizado por el informe en tiempo de ejecución no coinciden, es posible que el informe no se ejecute.

-   Antes de publicar el informe, reemplace la cadena de conexión estática con una expresión. Espere hasta que haya finalizado de diseñar el informe para reemplazar la cadena de conexión estática con una expresión. Una vez que use una expresión, no podrá ejecutar la consulta en el Diseñador de informes. Además, la lista de campos del panel Datos de informe y la lista Parámetros no se actualizarán de forma automática.

## <a name="see-also"></a>Consulte también
 [Conexiones de datos u orígenes de datos incrustados y Compartidos &#40;generador de informes y SSRS&#41;](../../2014/reporting-services/embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md) [administrar orígenes](report-data/manage-report-data-sources.md) de datos de informe [(cuadro de diálogo), credenciales](../../2014/reporting-services/data-source-properties-dialog-box-credentials.md) propiedades del [origen de datos compartido cuadro de diálogo, credenciales](../../2014/reporting-services/shared-data-source-properties-dialog-box-credentials.md) [crear, modificar y eliminar orígenes de datos compartidos &#40;SSRS&#41;](report-data/create-modify-and-delete-shared-data-sources-ssrs.md) [establecer propiedades de implementación &#40;](tools/set-deployment-properties-reporting-services.md) Reporting Services [especificar información de credenciales y conexión para los orígenes de datos de informe](report-data/specify-credential-and-connection-information-for-report-data-sources.md) [Agregar y Generador de informes y SSRS&#41;](report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)
