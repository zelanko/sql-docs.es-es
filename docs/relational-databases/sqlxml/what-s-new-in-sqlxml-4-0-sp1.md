---
title: ¿Qué&#39;s de SQLXML 4.0 SP1 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- registry keys [SQLXML]
- SQLNCLI, SQLXML
- what's new [SQLXML]
- SQLXML, what's new
- migrating SQLXML applications
- redistributing SQLXML
- SQL Server Native Client, SQLXML
- side-by-side installations [SQLXML]
ms.assetid: 48f7720b-1705-402d-93ce-097ff1737877
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: deb6b0044caabeaca23f5bb7c01f976ca6b874e3
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56016846"
---
# <a name="what39s-new-in-sqlxml-40-sp1"></a>¿Qué&#39;s de SQLXML 4.0 SP1
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQLXML 4.0 SP1 incluye varias actualizaciones y mejoras. En este tema se resumen las actualizaciones y se proporcionan vínculos a información más detallada, si está disponible. SQLXML 4.0 SP1 proporciona mejoras adicionales para admitir los nuevos tipos de datos introducidos de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]. En esta sección se incluyen los siguientes temas:  
  
-   Instalar SQLXML 4.0 SP1  
  
-   Problemas de la instalación simultánea  
  
-   SQLXML 4.0 y MSXML  
  
-   Redistribuir SQLXML 4.0  
  
-   Compatibilidad con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cliente nativo  
  
-   Compatibilidad con los tipos de datos introducidos en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]  
  
-   Cambios de carga masiva XML en SQLXML 4.0  
  
-   Cambios de claves del Registro en SQLXML 4.0  
  
-   Problemas de migración  
  
## <a name="installing-sqlxml-40-sp1"></a>Instalar SQLXML 4.0 SP1  
 Antes de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], SQLXML 4.0 se comercializó junto con SQL Server y formó parte de la instalación predeterminada de todas las versiones de SQL Server, salvo SQL Server Express. A partir de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], la versión más reciente de SQLXML (SQLXML 4.0 SP1) ya no está incluida en SQL Server. Para instalar SQLXML 4.0 SP1, descárguelo desde [ubicación de instalación para SQLXML 4.0 SP1](https://www.microsoft.com/download/details.aspx?id=30403).  
  
 Los archivos de SQLXML 4.0 SP1 se instalan en la ubicación siguiente:  
  
 `%PROGRAMFILES%\SQLXML 4.0\`  
  
> [!NOTE]  
>  Como parte del proceso de instalación de SQLXML 4.0, se realiza una configuración adecuada del Registro.  
  
 Para permitir que las aplicaciones SQLXML de 32 bits se ejecutan bajo Windows on Windows (WOW64) en los sistemas operativos Windows de 64 bits, ejecute el paquete SQLXML 4.0 SP1 de 64 bits, llamado sqlxml4.msi, que puede encontrar en el Centro de descarga.  
  
#### <a name="uninstalling-sqlxml-40-sp1"></a>Desinstalar SQLXML 4.0 SP1  
 Existen claves del Registro compartidas entre SQLXML 3.0 SP3, SQLXML 4.0 y SQLXML 4.0 SP1. Si las versiones más recientes de SQLXML se desinstalan en el mismo equipo que contiene SQLXML 3.0 SP3, podría necesitar reinstalar SQLXML 3.0 SP3.  
  
## <a name="side-by-side-installation-issues"></a>Problemas de la instalación simultánea  
 El proceso de instalación de SQLXML 4.0 no quita los archivos instalados con versiones anteriores de SQLXML. Por lo tanto, es posible que el equipo tenga archivos DLL para instalaciones de SQLXML de distinta versión. Puede ejecutar las instalaciones simultáneamente. SQLXML 4.0 incluye PROGID independientes y dependientes de la versión. Todas las aplicaciones de producción deben usar PROGID dependientes de la versión.  
  
## <a name="sqlxml-40-sp1-and-msxml"></a>SQLXML 4.0 SP1 y MSXML  
 SQLXML 4.0 no instala MSXML. SQLXML 4.0 utiliza MSXML 6.0, que se instala como parte de la instalación de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o una instalación posterior.  
  
## <a name="redistributing-sqlxml-40-sp1"></a>Redistribuir SQLXML 4.0 SP1  
 Puede distribuir SQLXML 4.0 SP1 mediante el paquete de instalación redistribuible. Una manera de instalar varios paquetes en lo que al usuario le parece ser una instalación única es usar tecnología de encadenador y arranque. Para obtener más información, vea la sección Crear un paquete de arranque personalizado para Visual Studio 2005 y Agregar requisitos previos personalizados.  
  
 Si su aplicación está diseñada para una plataforma distinta de aquella en la que se desarrolló, puede descargar versiones de sqlncli.msi para x64, Itanium y x86 en el Centro de descarga de Microsoft.  
  
 También existen programas de instalación de redistribución independientes para MSXML 6.0 (msxml6.msi). Puede encontrarlos en el CD de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la ubicación siguiente:  
  
 `%CD%\Setup\`  
  
 Estos archivos de instalación pueden utilizarse para instalar MSXML 6.0 directamente desde el CD. También pueden utilizarse para redistribuir libremente MSXML 6.0 junto con SQLXML 4.0 SP1 con sus propias aplicaciones personalizadas.  
  
 También necesitará redistribuir [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client si lo utiliza como proveedor de datos con la aplicación. Para obtener más información, vea [Instalar SQL Server Native Client](../../relational-databases/native-client/applications/installing-sql-server-native-client.md).  
  
## <a name="support-for-sql-server-native-client"></a>Compatibilidad con SQL Server Native Client  
 SQLXML 4.0 admite ambos SQLOLEDB y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedores de cliente nativo. Se recomienda que use la misma versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor Native Client y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] porque [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client se desarrolló para admitir los nuevos tipos de datos que se incluyen en el servidor, como el **Date, Time**, **DateTime2**, y **dateTimeOffset** tipos de datos de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y compatible con [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Native Client.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client es una tecnología de acceso a datos introducida en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Combina el proveedor SQLOLEDB y el controlador SQLODBC en una biblioteca de vínculos dinámicos (DLL) nativa, a la vez que ofrece una nueva funcionalidad independiente y distinta de Microsoft Data Access Components (MDAC).  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client puede utilizarse para crear nuevas aplicaciones o mejorar las aplicaciones existentes que necesitan aprovechar las características introducidas en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que no son compatibles con SQLOLEDB ni SQLODBC en MDAC y [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. Por ejemplo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client es necesaria para características SQLXML del lado cliente, como FOR XML, para usar el **xml** tipo de datos. Para obtener más información, consulte [formato XML del lado cliente &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml/formatting/client-side-xml-formatting-sqlxml-4-0.md), [utilizar ADO para ejecutar consultas de SQLXML 4.0](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md), y [SQL Server Native Client Programming](../../relational-databases/native-client/sql-server-native-client-programming.md).  
  
> [!NOTE]  
>  SQLXML 4.0 no es totalmente compatible con versiones anteriores a SQLXML 3.0. Debido a algunas correcciones de errores y otros cambios funcionales, en especial la eliminación de la compatibilidad SQLXML ISAPI, no pueden utilizarse directorios virtuales de IIS con SQLXML 4.0. Aunque la mayoría de las aplicaciones se ejecutarán con modificaciones menores, debe probarlas antes de pasarlas a producción con SQLXML 4.0.  
  
## <a name="support-for-data-types-introduced-in-sql-server-2005-and-sql-server-2008"></a>Compatibilidad con los tipos de datos en SQL Server 2005 y SQL Server 2008  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] introdujo el **xml** tipo de datos y SQLXML 4.0 admite la **xml** tipo de datos. Para obtener más información, consulte [compatibilidad con tipos de datos en SQLXML 4.0 xml](../../relational-databases/sqlxml/xml-data-type-support-in-sqlxml-4-0.md).  
  
 Para obtener ejemplos de cómo usar el **xml** tipo en SQLXML al asignar vistas XML de datos, cargar XML de forma masiva o ejecutar diagramas de actualización XML, consulte los ejemplos proporcionados en los temas siguientes.  
  
-   [Asignación predeterminada de atributos y elementos XSD a tablas y columnas](../../relational-databases/sqlxml-annotated-xsd-schemas-using/default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)  
  
-   [Insertar datos con diagramas de actualización XML](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md)  
  
-   [Ejemplos de documentos XML de la carga masiva](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/xml-bulk-load-examples-sqlxml-4-0.md)  
  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] introdujo el **fecha y hora**, **DateTime2**, y **DateTimeOffset** tipos de datos. SQLXML 4.0 SP1 habilitará estos cuatro nuevos tipos de datos como tipos escalares integrados cuando se usan con el proveedor OLE DB (SQLNCLI.11) de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Native Client, que se distribuye con [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
## <a name="xml-bulk-load-changes-for-sqlxml-40-sp1"></a>Cambios de carga masiva XML en SQLXML 4.0 SP1  
  
-   SQLXML 4.0, el campo de desbordamiento SchemaGen se crea mediante la **xml** tipo de datos. Para obtener más información, consulte [modelo de objeto de carga masiva de XML de SQL Server](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/sql-server-xml-bulk-load-object-model-sqlxml-4-0.md).  
  
-   Si previamente ha creado aplicaciones de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic y desea usar SQLXML 4.0, debe volver a compilar la aplicación con referencia a Xblkld4.dll.  
  
-   En aplicaciones de Visual Basic Scripting Edition, deberá registrar el archivo DLL que desee utilizar. En el ejemplo siguiente, si especifica PROGID independientes de la versión, la aplicación dependerá del último archivo DLL registrado:  
  
    ```  
    set objBulkLoad = CreateObject("SQLXMLBulkLoad.SQLXMLBulkLoad")   
    ```  
  
    > [!NOTE]  
    >  El PROGID dependiente de la versión es SQLXMLBulkLoad.SQLXMLBulkLoad.4.0.  
  
## <a name="registry-key-changes-for-sqlxml-40"></a>Cambios de claves del Registro en SQLXML 4.0  
 En SQLXML 4.0, las claves del Registro han cambiado a los siguientes valores con respecto a versiones anteriores:  
  
 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML4\TemplateCacheSize  
  
 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML4\SchemaCacheSize  
  
 Debe cambiar los valores si desea que estas claves estén vigentes para SQLXML 4.0.  
  
 Además, SQLXML 4.0 introduce las siguientes claves del Registro:  
  
-   `HKEY_LOCAL_MACHINE\Software\Microsoft\MSSQLServer\Client\SQLXML4\ReportErrorsWithSQLInfo`  
  
     De forma predeterminada, SQLXML 4.0 devuelve la información de errores nativos que proporcionan OLE DB y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en lugar de un error SQLXML de alto nivel (como sucedía en versiones anteriores de SQLXML). Si no desea usar este comportamiento, el valor de esta clave del Registro de tipo DWORD debe establecerse en 0 (el valor predeterminado es 1).  
  
-   HKEY_LOCAL_MACHINE\Software\Microsoft\MSSQLServer\Client\SQLXML4\FORXML_GenerateGUIDBraces  
  
     De forma predeterminada, SQLXML devuelve los valores GUID de SQL Server sin incluirlos entre llaves. Si desea que el valor GUID que se devuelva con las llaves (por ejemplo, {*algún GUID*}), el valor de esta clave del registro debe establecerse en 1 (valor predeterminado es 0).  
  
-   HKEY_LOCAL_MACHINE\Software\Microsoft\MSSQLServer\Client\SQLXML4\SQL2000CompatMode  
  
     De forma predeterminada, cuando el analizador XML carga los datos, los espacios en blanco se normalizan conforme a las reglas de XML 1.0. Esto provoca la pérdida de algunos caracteres de espacio en blanco en los datos. De este modo, es posible que la representación textual de los datos no sea la misma después del análisis, aunque semánticamente los datos sean los mismos.  
  
     Esta clave se incluye para que pueda elegir si desea mantener los caracteres de espacio en blanco en los datos. Si agrega esta clave del Registro y establece su valor en 0, los caracteres de espacio en blanco (LF, CR y tabulación) del código XML se devuelven codificados en el caso de los valores de atributo. En el caso de los valores de elemento, solamente CR se devuelve codificado.  
  
     Por ejemplo:  
  
    ```  
    CREATE TABLE T( Col1 int, Col2 nvarchar(100));  
    GO  
    -- Insert data with tab, line feed and carriage return).  
    INSERT INTO T VALUES (1, 'This is a tab    . This is a line feed and CR   
     more text');  
    GO  
    -- Test this query (without the registry key).  
    SELECT * FROM T   
    FOR XML AUTO;  
    -- This is the result (no encoding of special characters).  
    <?xml version="1.0" encoding="utf-8" ?>  
    <r>  
      <T Col1="1"   
         Col2="This is a tab    . This is a line feed and CR   
     more text"/>  
    </r>  
    -- Now add registry key with value 0 and execute the query again.  
    -- Note the encoding for carriage return, line-feed and tab in the attribute value.  
    <?xml version="1.0" encoding="utf-8" ?>  
    <r>  
      <T Col1="1"   
         Col2="This is a tab    . This is a line feed and CR   
     more text"/>  
    </r>  
  
    -- Update the query and specify ELEMENTS directive  
    SELECT * FROM T  
    FOR XML AUTO, ELEMENTS  
    -- Only the carriage return is returned encoded.  
    <?xml version="1.0" encoding="utf-8" ?>  
    <r>  
       <T>  
          <Col1>1</Col1>  
          <Col2>This is a tab    . This is a line feed and CR   
     more text</Col2>  
       </T>  
    </r>  
    ```  
  
## <a name="migration-issues"></a>Problemas de migración  
 A continuación se indican una serie de problemas que pueden afectar a la migración de aplicaciones SQLXML heredadas a SQLXML 4.0.  
  
### <a name="ado-and-sqlxml-40-queries"></a>Consultas SQLXML 4.0 y ADO  
 En versiones anteriores de SQLXML, se proporcionaba compatibilidad para la ejecución de consultas basadas en URL mediante el uso de directorios virtuales de IIS y el filtro SQLXML ISAPI. En aplicaciones que utilizan SQLXML 4.0, esta compatibilidad ya no está disponible.  
  
 Ahora, las consultas, plantillas y diagramas de actualización SQLXML pueden ejecutarse mediante las extensiones SQLXML a Objetos de datos ActiveX (ADO), que se introdujeron por primera vez en Microsoft Data Access Components (MDAC) 2.6 y versiones posteriores.  
  
 Para obtener más información, consulte [utilizar ADO para ejecutar consultas de SQLXML 4.0](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
### <a name="supportability-for-sqlxml-30-isapi-and-data-types-introduced-in-sql-server-2005"></a>Compatibilidad con SQLXML 3.0 ISAPI y tipos de datos introducidos en SQL Server 2005  
 Porque la compatibilidad con ISAPI se ha quitado de SQLXML 4.0, si la solución requiere la escritura de datos mejorado las características introducidas en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] , como el [tipo de datos xml](../../t-sql/xml/xml-transact-sql.md) o [tipos de datos definido por el usuario (UDT)](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)y acceso basado en Web, necesitará utilizar otra solución, como [clases administradas de SQLXML](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/sqlxml-4-0-net-framework-support-managed-classes.md) u otro tipo de controlador HTTP, como Native XML Web Services para SQL Server 2005.  
  
 Como alternativa, si no necesita estas extensiones de tipo, puede continuar utilizando SQLXML 3.0 para conectarse a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] las instalaciones. La compatibilidad de SQLXML 3.0 ISAPI se trabajar con estas versiones posteriores, pero no admite ni reconoce las **xml** tipo de datos o UDT tipo de soporte técnico que se introdujo en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
### <a name="xml-bulk-load-security-changes-for-temporary-files"></a>Cambios de seguridad de la carga masiva XML para archivos temporales  
 En SQLXML 4.0 y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], los permisos de archivo de carga masiva XML se conceden al usuario que ejecuta la operación de carga masiva. Los permisos de lectura y escritura se heredan del sistema de archivos. En versiones anteriores de SQLXML y SQL Server, la carga masiva XML en SQLXML creaba archivos temporales que no estaban protegidos y que podía leer cualquier usuario.  
  
### <a name="migration-issues-for-client-side-for-xml"></a>Problemas de migración en consultas FOR XML del lado cliente  
 Debido a cambios en el motor de ejecución, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueden devolver valores diferentes en los metadatos de una tabla base que se devolvería si se ha ejecutado la consulta FOR XML en [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]. En los casos en los que esto ocurre, el formato del lado cliente de los resultados de la consulta FOR XML será diferente según la versión en la que se ejecute la consulta.  
  
 Si una consulta FOR XML es ejecutado en el cliente utilizando SQLXML 3.0 en un **xml** columna de tipo de datos, los datos en los resultados se devolverá como una cadena con entidades. En SQLXML 4.0, si se especifica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client (SQLNCLI11) como proveedor, los datos se devolverán como XML.  
  
  
