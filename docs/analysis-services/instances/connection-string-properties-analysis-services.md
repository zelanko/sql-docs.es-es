---
title: "Propiedades de cadena de conexión (Analysis Services) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 29a00a41-5b0d-44b2-8a86-1b16fe507768
caps.latest.revision: "18"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 10c3749dafe92066faed35c4af06444e2fcd55ff
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="connection-string-properties-analysis-services"></a>Propiedades de cadena de conexión (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Este tema documentan las propiedades de cadena de conexión puede establecer en una de las herramientas de diseñador o de administración o vea en las cadenas de conexión generadas por las aplicaciones de cliente que se conectan a y consultar los datos de Analysis Services. Por tanto, solo se tratan un subconjunto de las propiedades disponibles. La lista completa incluye numerosas propiedades de servidor y base de datos, lo que permite personalizar una conexión para una aplicación específica, independientemente de cómo esté configurada la instancia o la base de datos en el servidor.  
  
 Los desarrolladores que crean cadenas de conexión personalizadas en código de aplicación deben revisar la documentación de la API para el cliente de ADOMD.NET con el fin de ver una lista más detallada: <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>  
  
 Las bibliotecas de cliente de Analysis Services, ADOMD.NET, AMO y el proveedor OLE DB para Analysis Services usan las propiedades descritas en este tema. La mayoría de las propiedades de cadena de conexión se puede usar con las tres bibliotecas de cliente. Las excepciones se indican en la descripción.  
  
 En este tema se incluyen las secciones siguientes:  
  
 [Parámetros de conexión de uso común](#bkmk_common)  
  
 [Autenticación y seguridad](#bkmk_auth)  
  
 [Parámetros de uso especial](#bkmk_special)  
  
 [Reservado para uso futuro](#bkmk_reserved)  
  
 [Ejemplos de cadena de conexión](#bkmk_examples)  
  
 [Formatos de cadena de conexión usados en Analysis Services](#bkmk_supportedstrings)  
  
 [Cifrar cadenas de conexión](#bkmk_encrypt)  
  
> [!NOTE]  
>  Si al establecer propiedades se establece involuntariamente la misma propiedad dos veces, se usa la última de la cadena de conexión.  
  
 Para obtener más información sobre cómo especificar una conexión de Analysis Services en aplicaciones de Microsoft existentes, vea [Conectarse desde aplicaciones cliente &#40;Analysis Services&#41;](../../analysis-services/instances/connect-from-client-applications-analysis-services.md).  
  
##  <a name="bkmk_common"></a> Parámetros de conexión de uso común  
 En la tabla siguiente se describen las propiedades más usadas para generar una cadena de conexión.  
  
|Propiedad|Description|Ejemplo|  
|--------------|-----------------|-------------|  
|**Data Source** o **DataSource**|Especifica la instancia del servidor. Esta propiedad es necesaria para todas las conexiones. Los valores válidos incluyen el nombre de red o la dirección IP del servidor, local o localhost para las conexiones locales, una dirección URL si el servidor está configurado para acceso HTTP o HTTPS, o el nombre de un archivo de cubo (.cub) local.|`Data source=AW-SRV01` para la instancia predeterminada y el puerto (TCP 2383).<br /><br /> `Data source=AW-SRV01$Finance:8081` para una instancia con nombre ($Finance) y un puerto fijo.<br /><br /> `Data source=AW-SRV01.corp.Adventure-Works.com` para un nombre de dominio completo, suponiendo la instancia y el puerto predeterminados.<br /><br /> `Data source=172.16.254.1` para una dirección IP del servidor, omitiendo la búsqueda del servidor DNS, que es útil para solucionar problemas de conexión.|  
|**Initial Catalog** o **Catalog**|Especifica el nombre de la base de datos de Analysis Services a la que se va a conectar. La base de datos se debe implementar en Analysis Services y debe tener permiso para conectarse a ella. Esta propiedad es opcional para las conexiones de AMO, pero es obligatoria para ADOMD.NET.|`Initial catalog=AdventureWorks2016`|  
|**Proveedor**|Los valores válidos incluyen MSOLAP. \<versión >, donde \<versión > es 4, 5, 6 o 7.<br /><br /> -   MSOLAP.4 se publicó en SQL Server 2008 y de nuevo en SQL Server 2008 R2 (el nombre de archivo es msolap100.dll para SQL Server 2008 y 2008 R2)<br />-   MSOLAP.5 se publicó en SQL Server 2012 (el nombre de archivo es msolap110.dll)<br />-   MSOLAP.6 released in SQL Server 2014 (el nombre de archivo es msolap1200.dll)<br />-   MSOLAP.7 se publicó en SQL Server 2016 (el nombre de archivo es msolap130.dll)<br /><br /> Esta propiedad es opcional. De forma predeterminada, las bibliotecas de cliente leen la versión actual del proveedor OLE DB del Registro. Solo necesita establecer esta propiedad si necesita una versión específica del proveedor de datos, por ejemplo para conectarse a una instancia de SQL Server 2012.<br /><br /> MSOLAP.4 se publicó tanto en SQL Server 2008 como en SQL Server 2008 R2. La versión 2008 R2 admite libros de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] y en ocasiones debe instalarse manualmente en los servidores de SharePoint. Para distinguir entre estas versiones, debe comprobar el número de compilación en las propiedades de archivo del proveedor: vaya a Archivos de programa\Microsoft Analysis Services\AS OLEDB\10. Haga clic con el botón secundario en msolap110.dll y seleccione **Propiedades**. Haga clic en **Detalles**. Vea la información de la versión del archivo. La versión debe incluir 10.50. \<númeroDeCompilación > para SQL Server 2008 R2. Para más información, consulte [Instalar el proveedor OLE DB de Analysis Services en servidores de SharePoint](http://msdn.microsoft.com/en-us/2c62daf9-1f2d-4508-a497-af62360ee859) y [Proveedores de datos usados para las conexiones de Analysis Services](../../analysis-services/instances/data-providers-used-for-analysis-services-connections.md).|`Provider=MSOLAP.7` se usa para las conexiones que necesitan la versión SQL Server 2016 del proveedor OLE DB para Analysis Services.|  
|**Cubo**|Nombre del cubo o nombre de la perspectiva. Una base de datos puede contener varios cubos y perspectivas. Cuando hay varios destinos posibles, incluya el nombre del cubo o de la perspectiva en la cadena de conexión.|`Cube=SalesPerspective` muestra que puede usar la propiedad de cadena de conexión Cube para especificar el nombre de un cubo o el nombre de una perspectiva.|  
  
##  <a name="bkmk_auth"></a> Autenticación y seguridad  
 Esta sección incluye las propiedades de cadena de conexión relacionadas con la autenticación y el cifrado. Analysis Services solo usa la autenticación de Windows, pero puede establecer propiedades en la cadena de conexión para pasar un nombre de usuario y una contraseña específicos.  
  
 Las propiedades se muestran en orden alfabético.  
  
|Propiedad|Description|  
|--------------|-----------------|  
|**EffectiveUserName**|Se emplea cuando se debe suplantar una identidad de usuario final en el servidor. Especifique la cuenta en el formato dominio\usuario. Para usar esta propiedad, el autor de la llamada debe tener permisos administrativos en Analysis Services. Para obtener más información acerca de esta propiedad en un libro de Excel desde SharePoint, vea [Usar EffectiveUserName de Analysis Services en SharePoint Server 2013](http://go.microsoft.com/fwlink/?LinkId=311905). Para obtener una ilustración de cómo se usa esta propiedad con Reporting Services, vea [Usar EffectiveUserName para suplantar en SSAS](http://go.microsoft.com/fwlink/?LinkId=301385).<br /><br /> **EffectiveUserName** se usa en [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para la instalación de SharePoint con el fin de capturar información de uso. La identidad del usuario se proporciona al servidor para poder grabar en los archivos de registro los eventos o los errores que incluyen la identidad del usuario. En el caso de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)], no se emplea con fines de autorización.|  
|**Encrypt Password**|Especifica si se va a usar una contraseña local para cifrar cubos locales. Los valores válidos son True o False. El valor predeterminado es False.|  
|**Encryption Password**|Contraseña que se usa para descifrar un cubo local cifrado. El valor predeterminado es una contraseña vacía. El usuario debe establecer explícitamente este valor.|  
|**Impersonation Level**|Indica el nivel de suplantación que se permite usar al servidor al suplantar al cliente. Los valores válidos incluyen:<br /><br /> -   Anonymous. El cliente es anónimo para el servidor. El proceso de servidor no puede obtener información sobre el cliente y no se puede suplantar al cliente.<br />-   Identify. El proceso de servidor puede obtener la identidad del cliente. El servidor puede suplantar la identidad del cliente con fines de autorización, pero no puede obtener acceso a los objetos del sistema como el cliente.<br />-   Impersonate. Es el valor predeterminado. La identidad del cliente se puede suplantar, pero solo cuando se establece la conexión, no en cada llamada.<br />-   Delegate. El proceso de servidor puede suplantar el contexto de seguridad del cliente mientras actúa en nombre de este. El proceso de servidor también puede realizar llamadas salientes a otros servidores mientras actúa en nombre del cliente.|  
|**Seguridad integrada**|La identidad de Windows del autor de la llamada se usa para conectarse a Analysis Services. Los valores válidos son en blanco, SSPI y BASIC.<br /><br /> **Integrated Security**=**SSPI** es el valor predeterminado para las conexiones TCP, que permiten una autenticación NTLM, Kerberos o anónima. El valor predeterminado es dejarla en blanco para las conexiones HTTP.<br /><br /> Cuando se usa **SSPI**, **ProtectionLevel** debe establecerse en uno de los valores siguientes: **Connect**, **PktIntegrity**, **PktPrivacy**.|  
|**Persist Encrypted**|Establezca esta propiedad cuando la aplicación cliente necesite que el objeto de origen de datos conserve información confidencial de autenticación, como una contraseña, en formato cifrado. De forma predeterminada, la información de autenticación no se guarda.|  
|**Persist Security Info**|Los valores válidos son True y False. Cuando se establece en True, se puede obtener de la conexión la información de seguridad, como la identidad del usuario o la contraseña especificada anteriormente en la cadena de conexión, una vez realizada la conexión. El valor predeterminado es False.|  
|**Nivel de protección**|Determina el nivel de seguridad usado en la conexión. Los valores válidos son:<br /><br /> -   **None**. Conexiones no autenticadas o anónimas. No realiza ninguna autenticación sobre los datos enviados al servidor.<br />-   **Connect**. Conexiones autenticadas. Solo se realiza la autenticación cuando el cliente establece una relación con un servidor.<br />-   **Integridad de PKT**. Conexiones cifradas. Comprueba que se reciben todos los datos del cliente y que no se han cambiado durante el tránsito.<br />-   **Privacidad de PKT**. Cifrado firmado, solo se admite para XMLA. Comprueba que se reciben todos los datos del cliente, que no han cambiado en el tránsito y protege la privacidad de los datos cifrándolos.<br /><br /> Para obtener más información, vea [Establishing Secure Connections in ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-client/connections-in-adomd-net-establishing-secure-connections.md).|  
|**Roles**|Especifique una lista delimitada por comas de los roles predefinidos para conectarse a un servidor o una base de datos mediante los permisos propios de ese rol. Si se omite esta propiedad, se usan todos los roles y los permisos vigentes son la combinación de todos los roles. Si se establece la propiedad en un valor vacío (por ejemplo, Roles=’ ‘), la conexión de cliente no tendrá pertenencia a roles.<br /><br /> Un administrador que usa esta propiedad se conecta con los permisos concedidos por el rol. Pueden producirse errores en algunos comandos si el rol no proporciona suficientes permisos.|  
|**SSPI**|Especifica explícitamente qué paquete de seguridad se va a usar para la autenticación de cliente cuando **Integrated Security** se ha establecido en **SSPI**. SSPI admite varios paquetes, pero puede usar esta propiedad para especificar un paquete determinado. Los valores válidos son Negociar, Kerberos, NTLM y Usuario anónimo. Si no se establece esta propiedad, todos los paquetes estarán disponibles para la conexión.|  
|**Use Encryption for Data**|Cifra las transmisiones de datos. Los valores válidos son True y False.|  
|**User ID**=…; **Password**=|**User ID** y **Password** se usan juntos. Analysis Services suplanta la identidad de usuario especificada mediante estas credenciales. En una conexión de Analysis Services, solo se ponen las credenciales en la línea de comandos cuando el servidor está configurado para acceso HTTP y ha especificado la autenticación básica en lugar de la seguridad integrada en el directorio virtual de IIS. Cuando se conecta directamente al servidor, los parámetros de la cadena de conexión **UserID** y **Password** se ignoran y la conexión se realiza con el contexto del usuario que ha iniciado sesión. <br /><br />El nombre de usuario y la contraseña deben ser las credenciales de una identidad de Windows, ya sea una cuenta de usuario local o de dominio. Observe que **User ID** tiene un espacio incrustado. Otros alias para esta propiedad pueden ser **UserName** (sin espacio en blanco) y **UID**. El alias para **Password** es **PWD**.|  
  
##  <a name="bkmk_special"></a> Parámetros de uso especial  
 En esta sección se describen los restantes parámetros de cadena de conexión. Se emplean para asegurar comportamientos de conexión específicos que necesita una aplicación.  
  
 Las propiedades se muestran en orden alfabético.  
  
|Propiedad|Description|  
|--------------|-----------------|  
|**Application Name**|Establece el nombre de la aplicación asociada a la conexión. Este valor puede ser útil para supervisar eventos de seguimiento, especialmente si varias aplicaciones tienen acceso a las mismas bases de datos. Por ejemplo, agregar Application Name=’test’ a una cadena de conexión hace que 'test' aparezca en un seguimiento de SQL Server Profiler, como se muestra en la captura de pantalla siguiente:<br /><br /> ![SSAS_AppNameExcample](../../analysis-services/instances/media/ssas-appnameexcample.gif "SSAS_AppNameExcample")<br /><br /> Los alias para esta propiedad incluyen **sspropinitAppName**, **AppName**. Para obtener más información, vea [Usar el parámetro de nombre de aplicación al conectarse a SQL Server](http://go.microsoft.com/fwlink/?LinkId=301699).|  
|**AutoSyncPeriod**|Establece la frecuencia (en milisegundos) de sincronización de caché de cliente y servidor. ADOMD.NET proporciona almacenamiento en caché de cliente para los objetos usados con frecuencia que tienen una sobrecarga mínima de memoria. Esto ayuda a reducir el número de ciclos de ida y vuelta al servidor. El valor predeterminado es de 10000 milisegundos (o diez segundos). Cuando se establece en NULL o en 0, se desactiva la sincronización automática.|  
|**Character Encoding**|Define cómo se codifican los caracteres en la solicitud. Los valores válidos son Default (predeterminado) o UTF-8 (son equivalentes) y UTF-16| 
|**CommitTimeout**|Una propiedad XMLA. Determina cuánto tiempo, en milisegundos, espera la fase de confirmación de un comando que se está ejecutando en ese momento antes de revertirse. Cuando es mayor que 0, reemplaza el valor de la propiedad CommitTimeout correspondiente en la configuración del servidor. |   
|**CompareCaseSensitiveStringFlags**|Ajusta las comparaciones de cadenas con distinción entre mayúsculas y minúsculas para una configuración regional especificada. Para obtener más información sobre la configuración de esta, vea [CompareCaseSensitiveStringFlags (Propiedad)](http://msdn.microsoft.com/library/aa237459\(v=sql.80\).aspx).|  
|**Compression Level**|Si **TransportCompression** es XPRESS, puede establecer el nivel de compresión para controlar cuánta compresión se usa. Los valores válidos son de 0 a 9, siendo 0 el que tiene menos compresión y 9 el que tiene más compresión. Una compresión mayor reduce el rendimiento. El valor predeterminado es 0.|  
|**Connect Timeout**|Determina el tiempo máximo (en segundos) durante el que el cliente intenta establecer una conexión antes de agotarse el tiempo de espera. Si una conexión no se completa dentro de este período, el cliente deja de intentar la conexión y genera un error.|  
|**MDX Compatibility**|El propósito de esta propiedad es asegurar un conjunto coherente de comportamientos MDX para las aplicaciones que emiten consultas MDX. Excel, que usa consultas MDX para rellenar y calcular una tabla dinámica conectada a Analysis Services, establece esta propiedad en 1 para asegurarse de que los miembros marcadores de posición en jerarquías desiguales son visibles en una tabla dinámica. Los valores válidos incluyen 0, 1, 2.<br /><br /> 0 y 1 exponen los miembros marcadores de posición; 2 no los expone. Si está vacío, se supone el valor0.|  
|**MDX Missing Member Mode=Error**|Indica si los miembros que faltan se omiten en las instrucciones MDX. Los valores válidos son Default, Error e Ignore. Default (el valor predeterminado) usa un valor definido por el servidor. Error genera un error cuando no existe un miembro. Ignore especifica que se deben pasar por alto los valores ausentes.|  
|**Optimize Response**|Máscara de bits que indica cuáles de las siguientes optimizaciones de respuesta de consulta están habilitadas.<br /><br /> -   0x01 Usar el NormalTupleSet (este es el valor predeterminado)<br />-   0x02 Usar cuando las segmentaciones de datos están vacías|  
|**Packet Size**|Tamaño del paquete de red (en bytes) entre 512 y 32.767. El tamaño de paquete de red predeterminado es 4096.|  
|**Protocol Format**|Establece el formato del XML que se envía al servidor. Los valores válidos son Default, XML o Binary. El protocolo es XMLA. Puede especificar que el XML se envíe en formato comprimido (este es el valor predeterminado), como XML sin formato o en un formato binario. El formato binario codifica los elementos y atributos XML, haciéndolos menores. La compresión es un formato propietario que reduce aún más el tamaño de las solicitudes y las respuestas. Los formatos de compresión y binario se usan para acelerar las solicitudes y las respuestas de transferencia de datos.<br /><br /> Debe usar una biblioteca de cliente en la conexión si emplea un formato binario o comprimido. El proveedor OLE DB puede dar formato a las solicitudes y las respuestas como un formato binario o comprimido. AMO y ADOMD.NET dan formato a las solicitudes como texto, pero aceptan respuestas en formato binario o comprimido.<br /><br /> Esta propiedad de cadena de conexión es equivalente a las configuraciones del servidor **EnableBinaryXML** y **EnableCompression** .|  
|**Real Time Olap**|Establezca esta propiedad para omitir el almacenamiento en caché, haciendo que todas las particiones escuchen activamente las notificaciones de consulta. De forma predeterminada, esta propiedad no está establecida.|  
|**Safety Options**|Establece el nivel de seguridad para las funciones y las acciones definidas por el usuario. Los valores válidos son 0, 1, 2. En una conexión de Excel, esta propiedad es Safety Options=2. Los detalles acerca de esta opción se encuentran en <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>.|  
|**SQLQueryMode**|Especifica si las consultas SQL incluyen cálculos. Los valores válidos son Data, Calculated, IncludeEmpty. Data significa que no se permite ningún cálculo. Calculated permite cálculos. IncludeEmpty permite que se devuelvan cálculos y filas vacías en el resultado de la consulta.|  
|**Timeout**|Especifica cuánto tiempo (en segundos) la biblioteca de cliente espera que se complete un comando antes de generar un error.|  
|**Transport Compression**|Define cómo se comprimen las comunicaciones de cliente y servidor, cuando la compresión se especifica mediante la propiedad **Protocol Format** . Los valores válidos son Default, None, Compressed y **gzip**. Default indica que no hay compresión para TCP, o **gzip** para HTTP. None indica que no se usa ninguna compresión. Compressed usa compresión XPRESS (SQL Server 2008 y versiones posteriores). **gzip** solo es válido para las conexiones HTTP, donde la solicitud HTTP incluye Accept-Encoding=gzip.|  
|**UseExistingFile**|Se usa al conectarse a un cubo local. Esta propiedad especifica si se sobrescribe el cubo local. Los valores válidos son True o False. Si se establece en True, el archivo de cubo debe existir. El archivo existente será el destino de la conexión. Si se establece en False, se sobrescribe el archivo de cubo.|  
|**VisualMode**|Establezca esta propiedad para controlar cómo se agregan los miembros cuando se aplica la seguridad de dimensión.<br /><br /> En el caso de datos de cubo que todos pueden ver, tiene sentido agregar todos los miembros porque todos los valores que contribuyen al total son visibles. Sin embargo, si se filtran o se limitan las dimensiones según la identidad del usuario, mostrar un total basado en todos los miembros (combinando los valores restringidos y los permitidos en un único total) puede resultar confuso o mostrar más información de la que se debe revelar.<br /><br /> Para especificar cómo se agregan los miembros cuando se aplica la seguridad de dimensión, puede establecer esta propiedad en True para usar solo los valores permitidos en la agregación o en False para excluir del total los valores restringidos.<br /><br /> Cuando se establece en la cadena de conexión, este valor se aplica en el nivel de cubo o de perspectiva. Dentro de un modelo, puede controlar los totales visuales en un nivel más específico.<br /><br /> Los valores válidos son 0, 1, y 2.<br /><br /> -   0 es el valor predeterminado. Actualmente, el comportamiento predeterminado es equivalente a 2, donde las agregaciones incluyen los valores que se ocultan al usuario.<br />-   1 excluye los valores ocultos del total. Esta es la configuración predeterminada para Excel.<br />-   2 incluye los valores ocultos en el total. Este es el valor predeterminado en el servidor.<br /><br /> Los alias para esta propiedad incluyen **Visual Total** o **Default MDX Visual Mode**.|  
  
##  <a name="bkmk_reserved"></a> Reservado para uso futuro  
 Las propiedades siguientes se permiten en una cadena de conexión, pero no están operativas en las versiones actuales de Analysis Services.  
  
-   Usuario autenticado  
  
-   Autenticación de caché  
  
-   Modo de caché (el uso de esta propiedad se investigó en versiones anteriores. Aunque puede encontrar entradas de blog que recomienden su uso, debe evitar establecer esta propiedad a menos que se lo indique el personal de soporte técnico de Microsoft).  
  
-   Directiva de caché  
  
-   Relación de caché  
  
-   Relación de caché2  
  
-   Límite de depuración dinámica  
  
-   Modo de depuración  
  
-   Mode  
  
-   SQLCompatibility  
  
-   Usar caché de fórmulas  
  
##  <a name="bkmk_examples"></a> Ejemplos de cadena de conexión  
 En esta sección se muestra la cadena de conexión que es más probable que deba usar al configurar una conexión de Analysis Services en las aplicaciones que se usan habitualmente.  
  
 **Cadena de conexión genérica**  
  
 Puede usar una cadena de conexión como esta si va a configurar una conexión desde Reporting Services.  
  
 `Data source=<servername>; initial catalog=<databasename>`  
  
 **Cadena de conexión en Excel**  
  
 La cadena de conexión predeterminada de ADOMD.NET en Excel especifica el proveedor de datos, el servidor, el nombre de la base de datos y la seguridad integrada de Windows. El nivel de compatibilidad con MDX siempre se establece en 1. Aunque puede cambiar el valor para la sesión actual, Excel restablecerá la compatibilidad con MDX en 1 la próxima vez que se abra el archivo.  
  
 `Provider=MSOLAP.5;Integrated Security=SSPI;Persist Security Info=True;Initial Catalog=Adventure Works DW 2008R2;Data Source=AW-SRV01;MDX Compatibility=1;Safety Options=2;MDX Missing Member Mode=Error`  
  
 Para más información, vea [Conexiones de datos, orígenes de datos y cadenas de conexión &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md) y [Autenticación de datos para Excel Services en SharePoint Server 2013](http://go.microsoft.com/fwlink/?LinkId=296350).  
  
##  <a name="bkmk_supportedstrings"></a> Formatos de cadena de conexión usados en Analysis Services  
 En esta sección se enumeran todos los formatos de cadena de conexión admitidos por Analysis Services. Excepto para las conexiones a bases de datos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , puede especificar estas cadenas de conexiones en aplicaciones que se conectan a Analysis Services.  
  
 **Conexiones nativas (o directas) con el servidor**  
  
 `Data Source=server[:port][\instance]` donde “port” y “\instance” son opcionales. Por ejemplo, si se especifica “Data Source=server1”, se abre una conexión a la instancia predeterminada (y el puerto predeterminado 2383) en un servidor denominado “server1”.  
  
 “Data Source=server1: port1” abrirá una conexión a una instancia de Analysis Services que se ejecute en el puerto “port1” en “server1”.  
  
 “Data Source=server1\instance1” abrirá una conexión con el Explorador de SQL (en su puerto predeterminado 2382), resolverá el puerto para la instancia denominada “instance1” y, después, abrirá la conexión con ese puerto de Analysis Services.  
  
 “Data Source=server1:port1\instance1” abrirá una conexión con el Explorador de SQL en “port1”, resolverá el puerto para la instancia denominada “instance1” y, después, abrirá la conexión con ese puerto de Analysis Services.  
  
 **Conexiones de cubo locales (archivos .cub)**  
  
 `Data Source=<path>`, por ejemplo “Data Source=c:\temp\a.cub”  
  
 **Conexiones HTTP a msmdpump.dll**  
  
 `Data Source=<URL>`, donde URL es la dirección HTTP o HTTPS a la carpeta virtual de IIS que contiene msmdpump.dll. Para obtener más información, vea [Configure HTTP Access to Analysis Services on Internet Information Services &#40;IIS&#41; 8.0](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md).  
  
 **Conexiones HTTP a libros de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] (archivos .xlsx, .xlsb o .xlsm)**  
  
 `Data Source=<URL>`, donde la dirección URL es la ruta de acceso de SharePoint a un libro de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] publicado en una biblioteca de SharePoint. Por ejemplo, `Data Source=http://localhost/Shared Documents/Sales.xlsx`.  
  
 **Conexiones HTTP a los archivos de conexión de modelos semánticos de BI**  
  
 `Data Source=<URL>` donde URL es la ruta de acceso de SharePoint al archivo .bism. Por ejemplo, `Data Source=http://localhost/Shared Documents/Sales.bism`.  
  
 **Conexiones de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] insertadas**  
  
 `Data Source=$Embedded$` donde $embedded$ es un moniker que hace referencia a un modelo de datos insertados de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en el libro. Esta cadena de conexión se crea y administra internamente. No la modifique. Las cadenas de conexión incrustadas las resuelve el complemento [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para Excel en estaciones de trabajo cliente, o las instancias de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint en una granja de SharePoint.  
  
 **Contexto del servidor local en los procedimientos almacenados de Analysis Services**  
  
 `Data Source=*`, donde * se resuelve en la instancia local.  
  
##  <a name="bkmk_encrypt"></a> Cifrar cadenas de conexión  
 Analysis Services utiliza sus propias claves de cifrado para cifrar cadenas de conexión. No se genera un certificado autofirmado.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] cifra y almacena las cadenas de conexión que emplea para conectarse a cada uno de sus orígenes de datos. Si la conexión a un origen de datos requiere un nombre de usuario y contraseña, puede hacer que [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] almacene el nombre y la contraseña con la cadena de conexión o puede hacer que se le solicite el nombre y la contraseña cada vez que se requiera una conexión al origen de datos. Si [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] solicita la información de usuario, significa que esta información no tiene por qué almacenarse y cifrarse. No obstante, si almacena esta información en la cadena de conexión, será necesario cifrar y proteger esta información.  
  
 Para cifrar y proteger la información de la cadena de conexión, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utiliza la API de protección de datos.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utiliza una clave de cifrado independiente para cifrar la información de la cadena de conexión para cada base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] crea esta clave cuando se crea la base de datos y cifra la información de la cadena de conexión según la cuenta de inicio de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Cuando se inicia [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , la clave cifrada para cada base de datos se lee, se descifra y se almacena. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utiliza a continuación la clave descifrada adecuada para descifrar la información de la cadena de conexión del origen de datos cuando [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] necesita conectarse a un origen de datos.  
  
## <a name="see-also"></a>Vea también  
 [Configurar el acceso HTTP a Analysis Services en Internet Information Services &#40;IIS&#41; 8.0](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md)   
 [Configurar Analysis Services para la delegación restringida de Kerberos](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md)   
 [Proveedores de datos usados para conexiones de Analysis Services](../../analysis-services/instances/data-providers-used-for-analysis-services-connections.md)   
 [Conectar a Analysis Services](../../analysis-services/instances/connect-to-analysis-services.md)  
  
  
