---
title: Historial de controlador de Microsoft SQL Server | Documentos de Microsoft
ms.custom: ''
ms.date: 5/4/2018
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: David-Engel
ms.author: v-daveng
manager: kenvh
ms.openlocfilehash: 2f2f4bafe48018da5c6f634b272a540021fd4ca2
ms.sourcegitcommit: 6fd8a193728abc0a00075f3e4766a7e2e2859139
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/17/2018
ms.locfileid: "34236043"
---
# <a name="driver-history-for-microsoft-sql-server"></a>Historial de controlador de Microsoft SQL Server

Esta página describe las tecnologías de conexión de datos históricos de Microsoft para conectarse a SQL Server.

## <a name="odbc"></a>ODBC

Hay tres generaciones distintas de los controladores ODBC de Microsoft para SQL Server. El primer controlador ODBC "SQL Server" aún se incluye como parte del [Windows Data Access Components](#microsoft-or-windows-data-access-components). No se recomienda utilizar este controlador para el nuevo desarrollo. A partir de SQL Server 2005, la [SQL Server Native Client](#sql-server-native-client) incluye una interfaz ODBC y es el controlador ODBC que se incluye con SQL Server 2005 mediante SQL Server 2012. No se recomienda utilizar este controlador para el nuevo desarrollo. Después de SQL Server 2012, el [Microsoft ODBC Driver para SQL Server](#microsoft-odbc-driver-for-sql-server) es el controlador que se actualiza con las últimas características de servidor en el futuro.

### <a name="sql-server-native-client"></a>SQL Server Native Client

SQL Server Native Client es una biblioteca independiente que se usa para OLE DB y ODBC. SQL Server Native Client (a menudo abreviado como SNAC) se incluyó en SQL Server 2005 a través de 2012. SQL Server Native Client puede utilizarse para las aplicaciones que necesitan aprovechar las nuevas características presentadas en SQL Server 2005 mediante SQL Server 2012. (Microsoft/Windows Data Access Components no se actualizan para estas nuevas características de SQL Server). Para las nuevas características más allá de SQL Server 2012, SQL Server Native Client no se actualizará. Cambiar a Microsoft ODBC Driver para SQL Server o el controlador OLE DB de Microsoft para SQL Server si desea aprovechar las ventajas de las nuevas características de SQL Server en el futuro.

Para obtener documentación completa de SQL Server Native Client, vea el [documentación de SQL Server Native Client](../relational-databases/native-client/sql-server-native-client-programming.md).

### <a name="microsoft-odbc-driver-for-sql-server"></a>Controlador ODBC de Microsoft para SQL Server

Después de SQL Server 2012, principal ODBC driver for SQL Server se ha desarrollado y lanzado como el controlador ODBC de Microsoft para SQL Server. Para obtener más información, consulte el [Microsoft ODBC Driver para la documentación de SQL Server](./odbc/microsoft-odbc-driver-for-sql-server.md).

## <a name="ole-db"></a>OLE DB

Hay tres generaciones distintas de proveedores de Microsoft OLE DB para SQL Server. El primer "Microsoft OLE DB proveedor para SQL Server" (SQLOLEDB) todavía se incluye como parte del [Windows Data Access Components](#microsoft-or-windows-data-access-components). Este proveedor no se actualizará con las nuevas características y no se recomienda utilizar este controlador para el nuevo desarrollo. A partir de SQL Server 2005, la [SQL Server Native Client](#sql-server-native-client) incluye una interfaz de proveedor de OLE DB (SQLNCLI) y es el proveedor OLE DB que se incluye con SQL Server 2005 mediante SQL Server 2017. Era [anunció su eliminación en 2011](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/) y no se recomienda utilizar este controlador para el nuevo desarrollo. En 2017, la tecnología de acceso a datos de OLE DB era posteriormente [undeprecated y una nueva versión planeada se anunció](https://blogs.msdn.microsoft.com/sqlnativeclient/2017/10/06/announcing-the-new-release-of-ole-db-driver-for-sql-server/) para 2018. El nuevo proveedor de OLE DB se llama "Microsoft OLE DB Driver para SQL Server" (MSOLEDBSQL) y actualmente se mantiene y compatibles.

## <a name="adonet"></a>ADO.NET

ADO.NET se introdujo con Microsoft .NET Framework y continúa se ha mejorado y se mantiene. Es un componente básico de Microsoft .NET Framework. Para obtener más información, consulte [Microsoft ADO.NET para SQL Server](ado-net/microsoft-ado-net-for-sql-server.md).

## <a name="jdbc"></a>JDBC

### <a name="microsoft-jdbc-driver-for-sql-server"></a>Controlador JDBC de Microsoft para SQL Server

Se introdujo en 2000, el controlador JDBC de Microsoft para SQL Server sigue se ha mejorado y mantiene. Es código abierto de 2016. Para ver la información más reciente, incluido cómo descargar el controlador, consulte [información general del controlador JDBC](./jdbc/overview-of-the-jdbc-driver.md).

## <a name="php"></a>PHP

### <a name="microsoft-drivers-for-php-for-sql-server"></a>Controladores de Microsoft para PHP para SQL Server

Se introdujo en 2009 como un proyecto de código abierto, Drivers de Microsoft para PHP para SQL Server se siguen mejorado y mantiene. Para ver la información más reciente, incluido cómo descargar el controlador PHP, consulte [Microsoft Drivers for PHP para SQL Server](./php/microsoft-php-driver-for-sql-server.md).

## <a name="nodejs"></a>Node.js

### <a name="microsoft-driver-for-nodejs-for-sql-server"></a>Controlador de Microsoft para Node.js para SQL Server

Microsoft Driver for Node.js para SQL Server permite que las aplicaciones Node.js en Microsoft Windows y Microsoft Windows Azure tener acceso a Microsoft SQL Server y base de datos de SQL Azure de Microsoft Windows. Los esfuerzos de desarrollo ya no se se basan en este controlador. No se recomienda para crear nuevas aplicaciones con Microsoft Driver para Node.js para SQL Server.

Para obtener más información acerca de Microsoft Driver para Node.js para SQL Server, vea [WindowsAzure / nodo sqlserver](https://github.com/Azure/node-sqlserver).

### <a name="tedious"></a>Una tarea tediosa

Actualmente, Microsoft contribuye a y admite el módulo de una tarea tediosa de código abierto en Node.js para la conectividad a SQL Server mediante JavaScript. Para obtener más información, consulte [controlador Node.js para SQL Server](./node-js/node-js-driver-for-sql-server.md).

## <a name="microsoft-or-windows-data-access-components"></a>Microsoft o Windows Data Access Components

Microsoft/Windows Data Access Components (MDAC/WDAC) se distribuyen con compatibles con Windows para la aplicación con las versiones anteriores compatibilidad y no forman parte de la pila de tecnología de SQL Server actual. Ninguna característica nueva se agregará a los componentes de MDAC/WDAC y no se recomienda para usarlas en el desarrollo de nuevas aplicaciones.

Para los fines de este documento, puede dividir la pila MDAC/WDAC en los componentes siguientes, según la tecnología y productos:

* **ADO** (incluidos ADOMD y ADOX)
* **OLE DB** (incluidos los servicios de principales de OLE DB, el proveedor OLE DB de SQL Server, proveedor OLE DB de Oracle, proveedor OLE DB para controladores ODBC, proveedor de formas de datos y proveedor de datos remoto)
* **ODBC** (incluido el Administrador de controladores ODBC, el controlador ODBC de SQL y el controlador ODBC para Oracle)

### <a name="mdacwdac-components"></a>Componentes MDAC/WDAC

MDAC/WDAC incluye los siguientes componentes:

* **ODBC:** la interfaz de Microsoft Open Database Connectivity (ODBC) es una interfaz de lenguaje de programación de C que permite a las aplicaciones tener acceso a datos desde una variedad de sistemas de administración de bases de datos (DBMS). Las aplicaciones que utilizan esta API se limitan a tener acceso a solo los orígenes de datos relacionales.
* **OLE DB:** OLE DB es un conjunto de interfaces COM para tener acceso a datos en una variedad de almacenes de datos. Existen proveedores OLE DB para tener acceso a datos en las bases de datos, sistemas de archivos, los almacenes de mensajes, servicios de directorio, flujo de trabajo y almacenes de documentos.
* **ADO:** ActiveX Data Objects (ADO) proporciona un modelo de programación de alto nivel. Aunque un poco más rendimiento que codificar directamente a OLE DB u ODBC, ADO es fácil de aprender y de usar. Se puede utilizar desde lenguajes de secuencias de comandos, como Microsoft Visual Basic Scripting Edition (VBScript) o Microsoft JScript.
* **ADOMD:** es multidimensional ADO (ADOMD) para su uso con proveedores de datos multidimensionales, como proveedor de OLAP de Microsoft, también conocido como proveedor de servicios de Microsoft Analysis. Se realizaron sin mejoras en sus características más importantes a él desde la versión 2.0 de MDAC.
* **ADOX:** las extensiones de ADO para DDL y seguridad (ADOX) permiten la creación y modificación de las definiciones de base de datos, tabla, índice o procedimiento almacenado. Puede usar ADOX con cualquier proveedor. El proveedor OLE DB de Microsoft Jet proporciona compatibilidad completa con ADOX, mientras que el proveedor OLE DB de Microsoft SQL Server proporciona compatibilidad limitada.
* **Bibliotecas de red de Microsoft SQL Server:** las bibliotecas de red de SQL Server permiten SQLOLEDB ni SQLODBC para comunicarse con la base de datos de SQL Server. Las siguientes bibliotecas de red de SQL Server han quedado en desuso en versiones MDAC/WDAC: Banyan Vines, AppleTalk, ServerNet, IPX/SPX, Giganet y RPC. TCP/IP y canalizaciones con nombre seguirán siendo compatible y están disponibles en el sistema operativo de Windows de 64 bits.
* **MSDASQL:** el proveedor Microsoft OLE DB para ODBC (MSDASQL) permite a las aplicaciones que se basan en OLE DB y ADO (que utiliza internamente OLEDB) para tener acceso a origen de datos a través de un controlador ODBC. MSDASQL es un proveedor OLEDB que se conecta a ODBC, en lugar de una base de datos. Está diseñado como un puente de OLE DB para un controlador ODBC cuando no hay ningún proveedor de OLE DB directa para un origen de datos. MSDASQL se suministra con el sistema operativo Windows y Windows Server 2008 y para Vista SP1 son que la primera Windows libera para incluir una versión de 64 bits de la tecnología.

### <a name="deprecated-mdacwdac-components"></a>Componentes MDAC/WDAC desusados

Estos componentes se siguen admitiendo en la versión actual de MDAC/WDAC, pero es posible que se quiten en versiones futuras. Al desarrollar nuevas aplicaciones, Microsoft recomienda evitar el uso de estos componentes. Además, al actualizar o modificar las aplicaciones existentes, quite la dependencia de estos componentes.

* **SQLOLEDB:** el proveedor OLE DB de Microsoft para SQL Server (SQLOLEDB), que admite el acceso a Microsoft SQL Server, está en desuso. Podrían no admitirse su conectividad a versiones futuras de SQL Server. La capacidad para conectarse a versiones anteriores a SQL Server 7 se quitará el sistema operativo después de Windows 7. Las aplicaciones nuevas deben utilizar el controlador OLE DB de Microsoft para SQL Server (MSOLEDBSQL), que admite las nuevas características de SQL Server. Las aplicaciones existentes deben migrar al controlador OLE DB de Microsoft para SQL Server así un mejor rendimiento, confiabilidad y compatibilidad. Para obtener más información, consulte [actualizar una aplicación a controlador de OLE DB para SQL Server de MDAC](oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md).
* **SQLODBC:** el Microsoft SQL Server ODBC Driver (SQLODBC), que admite el acceso a Microsoft SQL Server, está en desuso. Podrían no admitirse su conectividad a versiones futuras de SQL Server. La capacidad para conectarse a versiones anteriores a SQL Server 7 se quitará el sistema operativo después de Windows 7. Aplicaciones nuevas deben usar Microsoft ODBC Driver for SQL Server en Windows, que admite las nuevas características de SQL Server. Las aplicaciones existentes deben migrar a Microsoft ODBC Driver para SQL Server así un mejor rendimiento, confiabilidad y compatibilidad. Para obtener información relevante, vea [actualizar una aplicación a SQL Server Native Client de MDAC](../relational-databases/native-client/applications/updating-an-application-to-sql-server-native-client-from-mdac.md).
* **Motor de base de datos de Microsoft Jet 4.0:** a partir de la versión 2.6, MDAC ya no contiene componentes de Jet. En otras palabras, MDAC 2.6, 2.7 y 2.8 no contienen Microsoft Jet, el proveedor OLE DB de Microsoft Jet, los controladores de base de datos de escritorio ODBC o Jet Data Access Objects (DAO). Los componentes de motor de base de datos de Microsoft Jet 4.0 entró en un estado de degradación funcional, Ingeniería sostenida y no han recibido las mejoras de características del nivel desde que se está convirtiendo en una parte de Microsoft Windows en Windows 2000.

  No hay disponible ninguna versión de 64 bits del motor de base de datos de Jet, el controlador OLE DB para Jet, los controladores ODBC de Jet o Jet DAO. Para obtener más información, consulte [artículo de Knowledge Base 957570](http://support.microsoft.com/kb/957570). En las versiones de 64 bits de Windows, Jet de 32 bits se ejecuta en el subsistema de WOW64 de Windows. Para obtener más información en WOW64, vea el [documentación de MSDN WOW64](https://msdn.microsoft.com/library/windows/desktop/aa384274(v=vs.85).aspx). Las aplicaciones nativas de 64 bits no pueden comunicarse con los controladores de Jet de 32 bits que ejecuta en WOW64.

  En lugar de Microsoft Jet, Microsoft recomienda el uso de [Microsoft SQL Server Express Edition](https://www.microsoft.com/sql-server/sql-server-editions-express) al desarrollar nuevas aplicaciones no sean de Microsoft Access que requiera un almacén de datos relacional. Estas aplicaciones de Jet nuevas o convertidas pueden seguir usando Jet con la intención de usar Microsoft Office 2003 y los archivos de versiones anteriores (.mdb y .xls) para el almacenamiento de datos no principal. Sin embargo, para estas aplicaciones, debe planear migrar de Jet para 2007 Office System Driver. También puede [descargar 2007 Office System Driver](https://www.microsoft.com/downloads/details.aspx?displaylang=en&FamilyID=7554f536-8c28-4598-9b72-ef94e038c891), lo que permite leer y escribir en los archivos existentes en Office 2003 (.mdb y .xls) o los formatos de archivo de Office 2007 (*.accdb, *.xlsm, *.xlsx y *.xlsb).

  > [!IMPORTANT]
  > Lea el contrato de licencia de usuario final de 2007 Office System para conocer las limitaciones de uso específicos.

  > [!NOTE]
  > Aplicaciones de SQL Server también se puede tener acceso a 2007 Office System y versiones anteriores, los archivos de la conectividad de datos heterogéneos de SQL Server y Integrations Services capacidades, a través de 2007 Office System Driver. Además, pueden tener acceso las aplicaciones de SQL Server de 64 bits a Jet de 32 bits y los archivos de Office System 2007 mediante el uso de SQL Server Integration Services (SSIS) de 32 bits en Windows de 64 bits.

* **MSDADS:** con el proveedor Microsoft OLE DB para datos de forma (MSDADS), puede crear relaciones jerárquicas entre las claves, campos o conjuntos de filas en una aplicación. Mejoras en sus características más importantes no se han realizado desde MDAC 2.1. Este proveedor está en desuso. Microsoft recomienda que utilice XML, en lugar de MSDADS.
* **Oracle, ODBC y OLE DB de Oracle:** el controlador de ODBC de Oracle de Microsoft (ODBC de Oracle) y el proveedor Microsoft OLE DB para Oracle (Oracle OLE DB) proporcionan acceso a los servidores de base de datos de Oracle. Que se compilan mediante Oracle Call Interface (OCI) versión 7 y proporcionan compatibilidad completa para Oracle 7. Asimismo, usa la emulación de Oracle 7 para proporcionar una compatibilidad limitada para las bases de datos de Oracle 8. Oracle ya no admite las aplicaciones que utilizan las llamadas OCI versión 7. Estas tecnologías están en desuso. Si utiliza orígenes de datos de Oracle, debe migrar al proveedor y controlador suministrado por Oracle.
* **RDS:** Remote Data Services (RDS) es un mecanismo de Microsoft propietario para tener acceso a objetos de conjunto de registros ADO remotos a través de Internet o una Intranet. RDS está en desuso; no se ha realizado mejoras en sus características más importantes a RDS desde MDAC 2.1. Microsoft ha lanzado el .NET Framework, que tiene amplias capacidades de SOAP y reemplaza los componentes RDS. Todos los componentes de servidor RDS se quitará el sistema operativo después de Windows 7.
* **JRO:** Jet Replication Objects (JRO) está en desuso. JRO se utiliza dentro de ADO con Jet (*.mdb) bases de datos para crear y comprimir bases de datos Jet (.mdb) y realizar la administración de replicación de Jet. MDAC 2.7 será su última versión. JRO no estará disponible en el sistema operativo de Windows de 64 bits. JRO no se admite en el formato de archivo de Microsoft Access 2007 (*.accdb).
* **compatibilidad con ODBC de 16 bits:** si usas aplicaciones de 16 bits, debe migrar a una aplicación de 32 bits. funcionalidad de 16 bits está en desuso y se está quitando de sistemas operativos de 64 bits. Para obtener más información, consulte [el artículo de Knowledge base 896458](http://support.microsoft.com/kb/896458).
* **Proveedor OLEDB Simple (MSDAOSP):** un proveedor sencillo de OLEDB ofrece un marco para crear rápidamente los proveedores OLE DB a través de datos simple. MSDAOSP está en desuso.
* **Biblioteca de cursores ODBC:** biblioteca de cursores ODBC (ODBCCR32.dll) proporciona los cursores de datos de cliente limitado. Biblioteca de cursores ODBC está desusado; la aplicación puede usar implementaciones de cursores de servidor como un valor de reemplazo.
* **Comunicación remota de interfaz de fuera de proceso de OLE DB:** comunicación remota de la interfaz de OLE DB (msdaps.dll) fue un intento para permitir que los proveedores de OLE DB ejecutar fuera del proceso. Comunicación remota OLEDB interfaz fuera de proceso está en desuso.
* **Bibliotecas de red de SQL de Banyan Vines y AppleTalk:** el Banyan Vines, AppleTalk, ServerNet, IPX/SPX, Giganet y RPC SQL bibliotecas de red están en desuso. Si usa cualquiera de estas tecnologías, debe modificar las aplicaciones para usar una de las otras bibliotecas de red, como TCP/IP y canalizaciones con nombre.

### <a name="mdacwdac-releases"></a>Versiones MDAC/WDAC

Esta es una lista de los escenarios de compatibilidad de las versiones anteriores de MDAC/WDAC, empezando por la más temprana.

* **MDAC 1.5, MDAC 2.0 y 2.1 de MDAC:** estas versiones de MDAC eran versiones independientes que se hayan publicado a través de Microsoft Windows NT Option Pack, el SDK de plataforma de Microsoft Windows o el sitio Web de MDAC. Ya no se admiten estas versiones de MDAC.
* **MDAC 2.5:** esta versión de MDAC se incluyó con el sistema operativo Windows 2000. Service packs de MDAC 2.5 se incluye con Windows 2000 service Pack correspondientes.
* **MDAC 2.6:** MDAC 2.6 RTM, SP1 y SP2 se incluían con Microsoft SQL Server 2000 RTM, SP1 y SP2, respectivamente. Además, estos MDAC service Pack se han publicado en el sitio Web de MDAC según la programación de la versión de service pack de Microsoft SQL Server 2000. Puede instalar esta versión de MDAC y sus service packs en plataformas de Windows 2000, Windows Millennium Edition, Windows NT, Windows 95 y Windows 98. Ya no se admite esta versión de MDAC.
* **MDAC 2.7:** esta versión de MDAC se incluyen con los sistemas operativos Microsoft Windows XP RTM y SP1. Puede instalar esta versión de MDAC y sus service packs en plataformas de Windows 2000, Windows Millennium, Windows NT y Windows 98. Puede instalar esta versión en la plataforma Windows XP sólo a través del sistema operativo o sus paquetes de servicios. Ya no se admite esta versión de MDAC.
* **MDAC 2.8:** esta versión de MDAC se incluye con Windows Server 2003 y Windows XP SP2 y versiones posteriores. También puede instalar esta versión de MDAC y sus service packs en Windows 2000.

  * La versión de 32 bits de MDAC 2.8 se publicó en el sitio Web de MDAC también al mismo tiempo que se liberó por Windows Server 2003 para el cliente.
  * La versión de 64 bits de MDAC 2.8 se publicó con la versión de 64 bits de Windows Server 2003 y Windows XP.

* **Windows Data Access Components (WDAC):** MDAC cambia su nombre a WDAC - "Windows Data Access Components" a partir de Windows Vista y Windows Server 2008. WDAC se incluye como parte del sistema operativo y no está disponible por separado para su redistribución. Capacidad de servicio para WDAC está sujeto el ciclo de vida del sistema operativo.

  se publican versiones de 32 bits y 64 bits de WDAC con las versiones de 32 bits y 64 bits de los sistemas operativos de Windows, respectivamente.

## <a name="obsolete-data-access-technologies"></a>Tecnologías de acceso a datos obsoletos

Tecnologías obsoletas son tecnologías que no se han mejorado o actualiza en varias versiones del producto y que no se tendrán en versiones futuras del producto. No utilice estas tecnologías al escribir nuevas aplicaciones. Cuando se modifican las aplicaciones existentes que se han escrito mediante estas tecnologías, considere la posibilidad de migrar estas aplicaciones a ADO.NET u otra tecnología actual.

Los componentes siguientes se consideran obsoletos:

* **DB-Library:** DB-Library es un modelo de programación específicos de SQL Server que incluye las API de C. No ha habido ningún mejoras de características a la biblioteca de base de datos desde SQL Server 6.5. La versión final era con SQL Server 2000, y no se transferirá al sistema operativo de Windows de 64 bits.
* **SQL incrustado (E-SQL):** E-SQL es un modelo de programación específicos de SQL Server que permite que las instrucciones de Transact-SQL incrustar en código de Visual C. No hay mejoras de características se realizaron en E-SQL desde SQL Server 6.5. La versión final era con SQL Server 2000, y no se transferirá al sistema operativo de Windows de 64 bits.
* **Objetos de acceso a datos (DAO):** DAO proporciona acceso a las bases de datos JET (Access). Esta API puede utilizarse desde Microsoft Visual Basic, Microsoft Visual C++ y lenguajes de scripting. Se incluye con Microsoft Office 2000 y Office XP. DAO 3.6 es la versión final de esta tecnología. No estará disponible en el sistema operativo de Windows de 64 bits.
* **Objetos de datos remotos (RDO):** RDO se ha diseñado específicamente para tener acceso a orígenes de datos relacionales de ODBC remotos y más fácil usar ODBC sin código de aplicación compleja. Se incluyen con las versiones 4, 5 y 6 de Microsoft Visual Basic. RDO versión 2.0 era la versión final de esta tecnología.