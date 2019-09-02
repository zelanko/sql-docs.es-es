---
title: Historial de controladores para Microsoft SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 05/04/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c0fcc2172cca192c8c7580450ab50b4416f9ec2d
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2019
ms.locfileid: "70154182"
---
# <a name="driver-history-for-microsoft-sql-server"></a>Historial de controladores para Microsoft SQL Server

En esta página se describen las tecnologías de conexión de datos históricas de Microsoft para conectarse a SQL Server.

## <a name="odbc"></a>ODBC

Hay tres generaciones distintas de proveedores de controladores OLE DB de Microsoft para SQL Server. El primer controlador ODBC "SQL Server" todavía se incluye como parte de [los componentes de Windows Data Access](#microsoft-or-windows-data-access-components). No se recomienda usar este controlador para el nuevo desarrollo. A partir de SQL Server 2005, el [SQL Server Native Client](#sql-server-native-client) incluye una interfaz ODBC y es el controlador ODBC incluido con SQL Server 2005 a SQL Server 2012. No se recomienda usar este controlador para el nuevo desarrollo. Después de SQL Server 2012, el [Microsoft ODBC driver for SQL Server](#microsoft-odbc-driver-for-sql-server) es el controlador que se actualiza con las características de servidor más recientes que se van adelante.

### <a name="sql-server-native-client"></a>SQL Server Native Client

SQL Server Native Client es una biblioteca independiente que se utiliza para OLE DB y ODBC. SQL Server Native Client (a menudo abreviado SNAC) se incluyó en SQL Server 2005 a 2012. SQL Server Native Client se puede usar para las aplicaciones que necesitan aprovechar las nuevas características introducidas en SQL Server 2005 a SQL Server 2012. (Los componentes de Microsoft/Windows Data Access no se actualizan para estas nuevas características en SQL Server). En el caso de las nuevas características más allá de SQL Server 2012, no se actualizará SQL Server Native Client. Cambie al Microsoft ODBC Driver for SQL Server o al controlador de Microsoft OLE DB para SQL Server si desea sacar partido de las nuevas características de SQL Server que se van adelante.

Para obtener la documentación completa del SQL Server Native Client, consulte la [documentación de SQL Server Native Client](../relational-databases/native-client/sql-server-native-client-programming.md).

### <a name="microsoft-odbc-driver-for-sql-server"></a>Controlador ODBC de Microsoft para SQL Server

Después de SQL Server 2012, el controlador ODBC principal de SQL Server se ha desarrollado y publicado como Microsoft ODBC Driver for SQL Server. Para obtener más información, consulte la [documentación de Microsoft ODBC driver for SQL Server](./odbc/microsoft-odbc-driver-for-sql-server.md).

## <a name="ole-db"></a>OLE DB

Hay tres generaciones distintas de proveedores de OLE DB de Microsoft para SQL Server. El primer "proveedor OLE DB de Microsoft para SQL Server" (SQLOLEDB) todavía se suministra como parte de los [Componentes de Windows Data Access](#microsoft-or-windows-data-access-components). Este proveedor no se actualizará con las nuevas características y no se recomienda usar este controlador para el nuevo desarrollo. A partir de SQL Server 2005, el [SQL Server Native Client](#sql-server-native-client) incluye una interfaz del proveedor de OLE DB (SQLNCLI) y es el proveedor de OLE DB que se distribuye con SQL Server 2005 a SQL Server 2017. Se [anunció en desuso en 2011](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/), y no se recomienda usar este controlador para nuevos desarrollos. En 2017, la tecnología de acceso a datos de OLE DB no [quedó obsoleta y se anunció una nueva versión planeada](https://blogs.msdn.microsoft.com/sqlnativeclient/2017/10/06/announcing-the-new-release-of-ole-db-driver-for-sql-server/) para 2018. El nuevo proveedor de OLE DB se denomina "Microsoft OLE DB driver for SQL Server" (MSOLEDBSQL) y se mantiene y se admite actualmente.

## <a name="adonet"></a>ADO.NET

ADO.NET se presentó con el marco de Microsoft .NET y se sigue mejorando y manteniendo. Es un componente básico de la plataforma de Microsoft .NET. Para obtener más información, consulte [ADO.net de Microsoft para obtener SQL Server](ado-net/microsoft-ado-net-for-sql-server.md).

## <a name="jdbc"></a>JDBC

### <a name="microsoft-jdbc-driver-for-sql-server"></a>Controlador JDBC de Microsoft para SQL Server

Microsoft JDBC driver for SQL Server, que se presentó en 2000, se sigue mejorando y manteniendo. Tenía código abierto en 2016. Para obtener la información más reciente, incluido cómo descargar el controlador, consulte [información general del controlador JDBC](./jdbc/overview-of-the-jdbc-driver.md).

## <a name="php"></a>PHP

### <a name="microsoft-drivers-for-php-for-sql-server"></a>Controladores de Microsoft para PHP para SQL Server

Introducida en 2009 como proyecto de código abierto, los controladores de Microsoft para PHP para SQL Server continúan mejorando y manteniendo. Para obtener la información más reciente, incluido cómo descargar el controlador PHP, consulte [controladores de Microsoft para PHP para SQL Server](./php/microsoft-php-driver-for-sql-server.md).

## <a name="nodejs"></a>Node.js

### <a name="microsoft-driver-for-nodejs-for-sql-server"></a>Controlador de Microsoft para node. js para SQL Server

El controlador de Microsoft para node. js para SQL Server permite que las aplicaciones de node. js en Microsoft Windows y Microsoft Azure tengan acceso a Microsoft SQL Server y Microsoft Azure SQL Database. Los esfuerzos de desarrollo ya no se centran en este controlador. No se recomienda crear nuevas aplicaciones con el controlador de Microsoft para node. js para SQL Server.

Para obtener más información sobre el controlador de Microsoft para node. js para SQL Server, consulte [WindowsAzure/node-SQLServer](https://github.com/Azure/node-sqlserver).

### <a name="tedious"></a>Repetitiva

Microsoft actualmente contribuye y admite el módulo tedioso de código abierto en node. js para la conectividad a SQL Server mediante JavaScript. Para obtener más información, consulte [controlador de node. js para obtener SQL Server](./node-js/node-js-driver-for-sql-server.md).

## <a name="microsoft-or-windows-data-access-components"></a>Microsoft o Windows Data Access Components

Microsoft/Windows Data Access Components (MDAC/WDAC) se suministran con y son compatibles con Windows para la compatibilidad con versiones anteriores de aplicaciones y no forman parte de la pila de tecnología de SQL Server actual. No se agregarán nuevas características a los componentes en MDAC/WDAC y no se recomienda su uso en el desarrollo de nuevas aplicaciones.

Para los fines de este documento, puede dividir la pila de MDAC/WDAC en los componentes siguientes, en función de la tecnología y los productos:

* **ADO** (incluidos ADOMD y ADOX)
* **OLE DB** (incluidos OLE DB Core Services, SQL Server OLE DB proveedor, el proveedor de OLE DB de Oracle, el proveedor de OLE DB para controladores ODBC, el proveedor de formas de datos y el proveedor de datos remotos)
* **ODBC** (incluido el administrador de controladores ODBC, el controlador ODBC de SQL y el controlador ODBC para Oracle)

### <a name="mdacwdac-components"></a>Componentes de MDAC/WDAC

MDAC/WDAC incluye estos componentes:

* **ODBC:** La interfaz Microsoft Open Database Connectivity (ODBC) es una interfaz de lenguaje de programación C que permite a las aplicaciones tener acceso a los datos de diversos sistemas de administración de bases de datos (DBMS). Las aplicaciones que usan esta API solo tienen acceso a los orígenes de datos relacionales.
* **OLE DB:** OLE DB es un conjunto de interfaces COM para tener acceso a los datos de una variedad de almacenes de datos. Los proveedores de OLE DB existen para el acceso a datos en bases de datos, sistemas de archivos, almacenes de mensajes, servicios de directorio, flujos de trabajo y almacenes de documentos.
* **ADO:** Objetos de datos ActiveX (ADO) proporciona un modelo de programación de alto nivel. Aunque un poco menos eficaz que la codificación que OLE DB o ODBC directamente, ADO es sencillo de aprender y usar. Se puede usar desde lenguajes de script, como Microsoft Visual Basic Scripting Edition (VBScript) o Microsoft JScript.
* **ADOMD:** La multidimensional (ADOMD) de ADO se va a usar con proveedores de datos multidimensionales, como el proveedor OLAP de Microsoft, también conocido como proveedor de Analysis Services de Microsoft. No se han realizado mejoras importantes en las características desde MDAC 2,0.
* **ADOX:** Las extensiones de ADO para DDL y Security (ADOX) permiten la creación y modificación de definiciones de una base de datos, una tabla, un índice o un procedimiento almacenado. Puede usar ADOX con cualquier proveedor. El proveedor de OLE DB de Microsoft Jet proporciona compatibilidad total para ADOX, mientras que el proveedor de OLE DB de Microsoft SQL Server proporciona compatibilidad limitada.
* **Bibliotecas de red Microsoft SQL Server:** Las bibliotecas de red SQL Server permiten a SQLOLEDB y SQLODBC comunicarse con la base de datos de SQL Server. Las siguientes bibliotecas de red SQL Server han quedado en desuso en las versiones de MDAC/WDAC: Banyan Vines, AppleTalk, ServerNet, IPX/SPX, Giganet y RPC. TCP/IP y las canalizaciones con nombre seguirán siendo compatibles y estarán disponibles en el sistema operativo Windows de 64 bits.
* **MSDASQL:** El proveedor de Microsoft OLE DB para ODBC (MSDASQL) permite a las aplicaciones que se basan en OLE DB y ADO (que usa internamente OLEDB) tener acceso a los orígenes de datos a través de un controlador ODBC. MSDASQL es un proveedor OLEDB que se conecta a ODBC, en lugar de a una base de datos. Está diseñado como un puente desde OLE DB a un controlador ODBC cuando no existe ningún proveedor de OLE DB directo para un origen de datos. MSDASQL se suministra con el sistema operativo Windows, y Windows Server 2008 y Vista SP1 eran las primeras versiones de Windows para incluir una versión de 64 bits de la tecnología.

### <a name="deprecated-mdacwdac-components"></a>Componentes MDAC/WDAC en desuso

Estos componentes todavía se admiten en la versión actual de MDAC/WDAC, pero podrían quitarse en versiones futuras. Al desarrollar nuevas aplicaciones, Microsoft recomienda evitar el uso de estos componentes. Además, al actualizar o modificar las aplicaciones existentes, quite cualquier dependencia de estos componentes.

* **SQLOLEDB:** El proveedor de OLE DB de Microsoft para SQL Server (SQLOLEDB), que admite el acceso a Microsoft SQL Server, ha quedado en desuso. Es posible que no se admita su conectividad con versiones futuras de SQL Server. La capacidad de conectarse a versiones anteriores a SQL Server 7 se quitará del sistema operativo después de Windows 7. Las nuevas aplicaciones deben usar el controlador de Microsoft OLE DB para SQL Server (MSOLEDBSQL), que es compatible con las nuevas características de SQL Server. Las aplicaciones existentes deben migrar al controlador de Microsoft OLE DB para SQL Server también para mejorar el rendimiento, la confiabilidad y la compatibilidad. Para obtener más información, vea [actualizar una aplicación a OLE DB driver for SQL Server de MDAC](oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md).
* **SQLODBC:** El controlador ODBC de Microsoft SQL Server (SQLODBC), que admite el acceso a Microsoft SQL Server, ha quedado en desuso. Es posible que no se admita su conectividad con versiones futuras de SQL Server. La capacidad de conectarse a versiones anteriores a SQL Server 7 se quitará del sistema operativo después de Windows 7. Las nuevas aplicaciones deben usar el Microsoft ODBC Driver for SQL Server en Windows, que admite nuevas características de SQL Server. Las aplicaciones existentes deben migrar al Microsoft ODBC Driver for SQL Server también para mejorar el rendimiento, la confiabilidad y la compatibilidad. Para obtener información relevante, vea [actualizar una aplicación a SQL Server Native Client desde MDAC](../relational-databases/native-client/applications/updating-an-application-to-sql-server-native-client-from-mdac.md).
* **Microsoft Jet Motor de base de datos 4,0:** A partir de la versión 2,6, MDAC ya no contiene componentes de jet. En otras palabras, MDAC 2,6, 2,7 y 2,8 no contienen Microsoft Jet, el proveedor Microsoft Jet OLE DB, los controladores de base de datos de escritorio ODBC o los objetos de acceso a datos de jet (DAO). 

  No hay ninguna versión de 64 bits de jet Motor de base de datos, el controlador OLEDB de jet, los controladores Jet ODBC o Jet DAO disponibles. Para más información, vea el [artículo de Knowledge Base 957570](https://support.microsoft.com/kb/957570). En las versiones de 64 bits de Windows, jet de 32 bits se ejecuta en el subsistema WOW64 de Windows. Para obtener más información sobre WOW64, vea la [documentación de WOW64 de MSDN](/windows/desktop/WinProg64/wow64-implementation-details). Las aplicaciones nativas de 64 bits no se pueden comunicar con los controladores Jet de 32 bits que se ejecutan en WOW64.

  En lugar de Microsoft Jet, Microsoft recomienda usar [Microsoft SQL Server Express Edition](https://www.microsoft.com/sql-server/sql-server-editions-express) al desarrollar aplicaciones de acceso nuevas y que no sean de Microsoft que requieran un almacén de datos relacional. Estas aplicaciones Jet nuevas o convertidas pueden seguir usando jet con la intención de usar Microsoft Office 2003 y archivos anteriores (. mdb y. xls) para el almacenamiento de datos no principales. Sin embargo, para estas aplicaciones, debe planear la migración de jet al Motor de base de datos de Microsoft Access. Puede [Descargar Microsoft Access motor de base de datos](https://www.microsoft.com/download/details.aspx?id=54920), que le permite leer y escribir en archivos ya existentes en Office 2003 (. mdb y. xls) o en los formatos de archivo Office 2007 (*. accdb, *. xlsm, *. xlsx y *. xlsb).

  > [!IMPORTANT]
  > Lea el contrato de licencia para el usuario final de 2007 Office System para conocer las limitaciones de uso específicas.

  > [!NOTE]
  > SQL Server aplicaciones también pueden tener acceso al sistema de Office 2007 y versiones anteriores, desde SQL Server capacidades de conectividad de datos heterogéneas e Integration Services, a través del controlador de sistema de Office 2007. Además, las aplicaciones SQL Server de 64 bits pueden tener acceso a los archivos de sistema Jet y 2007 de Office de 32 bits mediante SQL Server Integration Services de 32 bits (SSIS) en Windows de 64 bits.

* **MSDADS:** Con el proveedor de OLE DB de Microsoft para el modelado de datos (MSDADS), puede crear relaciones jerárquicas entre las claves, los campos o los conjuntos de filas en una aplicación. No se han realizado mejoras importantes en las características desde MDAC 2,1. Este proveedor está en desuso. Microsoft recomienda que utilice XML, en lugar de MSDADS.
* **Oracle ODBC y oracle OLE DB:** El controlador ODBC de Microsoft para Oracle (Oracle ODBC) y Proveedor OLE DB de Microsoft para Oracle (Oracle OLE DB) proporcionan acceso a los servidores de bases de datos de Oracle. Se compilan con Oracle Call Interface (OCI) versión 7 y proporcionan compatibilidad completa con Oracle 7. Además, utiliza la emulación de Oracle 7 para proporcionar compatibilidad limitada con las bases de datos de Oracle 8. Oracle ya no admite aplicaciones que usan llamadas de la versión 7 de OCI. Estas tecnologías están en desuso. Si usa orígenes de datos de Oracle, debe migrar al controlador y al proveedor proporcionados por Oracle.
* **RDS:** Data Services remoto (RDS) es un mecanismo propietario de Microsoft para obtener acceso a objetos de conjunto de registros de ADO remotos a través de Internet o de una intranet. RDS está en desuso; no se han realizado mejoras de características importantes en RDS desde MDAC 2,1. Microsoft ha lanzado el .NET Framework, que tiene amplias funcionalidades de SOAP y reemplaza los componentes de RDS. Todos los componentes de servidor RDS se quitarán del sistema operativo después de Windows 7.
* **JRO:** Los objetos de replicación de jet (JRO) están en desuso. JRO se utiliza en ADO con bases de*datos Jet (. mdb) para crear y comprimir bases de datos Jet (. mdb) y realizar la administración de la replicación de jet. MDAC 2,7 será la última versión. JRO no estará disponible en el sistema operativo Windows de 64 bits. JRO no es compatible con el formato de archivo de Microsoft Access*2007 (. accdb).
* **compatibilidad con ODBC de 16 bits:** Si usa aplicaciones de 16 bits, debe migrar a una aplicación de 32 bits. la funcionalidad de 16 bits está en desuso y se quita de los sistemas operativos de 64 bits. Para obtener más información, vea el [artículo de Knowledge Base 896458](https://support.microsoft.com/kb/896458).
* **Proveedor simple OleDb (MSDAOSP):** OLEDB simple Provider ofrece un marco para compilar rápidamente OLE DB proveedores a través de datos simples. MSDAOSP está en desuso.
* **Biblioteca de cursores ODBC:** La biblioteca de cursores ODBC (ODBCCR32. dll) proporciona cursores de datos limitados del lado cliente. La biblioteca de cursores ODBC está en desuso; la aplicación puede usar implementaciones de cursor de servidor como reemplazo.
* **OLE DB la comunicación remota de la interfaz fuera de proceso:** La comunicación remota de la interfaz OLEDB (msdaps. dll) fue un intento de permitir que los proveedores de OLE DB se quedaran fuera de proceso. La comunicación remota de la interfaz de OLEDB fuera de proceso está en desuso.
* **Bibliotecas de red de SQL de AppleTalk y Banyan Vines:** Las bibliotecas de red de Banyan Vines, AppleTalk, ServerNet, IPX/SPX, Giganet y RPC SQL están en desuso. Si usa cualquiera de estas tecnologías, debe modificar las aplicaciones para que usen una de las otras bibliotecas de red, como TCP/IP y la canalización con nombre.

### <a name="mdacwdac-releases"></a>Versiones de MDAC/WDAC

Esta es una lista de los escenarios de compatibilidad de las versiones anteriores de MDAC/WDAC, empezando por la más temprana.

* **Mdac 1,5, mdac 2,0 y mdac 2,1:** Estas versiones de MDAC eran versiones independientes que se lanzaron a través de Microsoft Windows NT Option Pack, el SDK de la plataforma Microsoft Windows o el sitio web de MDAC. Estas versiones de MDAC ya no se admiten.
* **MDAC 2.5:** Esta versión de MDAC se incluyó en el sistema operativo Windows 2000. Los Service Packs de MDAC 2,5 se incluyeron con los Service Packs de Windows 2000 correspondientes.
* **MDAC 2.6:** MDAC 2.6 RTM, SP1 y SP2 se incluyeron con Microsoft SQL Server 2000 RTM, SP1 y SP2, respectivamente. Además, estos Service Packs de MDAC se publicaron en el sitio web de MDAC de acuerdo con la programación de versión de Service Pack Microsoft SQL Server 2000. Puede instalar esta versión de MDAC y sus Service Pack en las plataformas Windows 2000, Windows Millennium Edition, Windows NT, Windows 95 y Windows 98. Ya no se admite esta versión de MDAC.
* **MDAC 2.7:** Esta versión de MDAC se incluyó en los sistemas operativos Microsoft Windows XP RTM y SP1. Puede instalar esta versión de MDAC y sus Service Pack en plataformas Windows 2000, Windows Millennium, Windows NT y Windows 98. Puede instalar esta versión en la plataforma Windows XP solo a través del sistema operativo o sus paquetes de servicios. Ya no se admite esta versión de MDAC.
* **MDAC 2.8:** Esta versión de MDAC se incluye con Windows Server 2003 y Windows XP SP2 y versiones posteriores. También puede instalar esta versión de MDAC y sus Service Packs en Windows 2000.

  * La versión de 32 bits de MDAC 2,8 también se publicó en el sitio web de MDAC al mismo tiempo que se lanzó Windows Server 2003 al cliente.
  * La versión de 64 bits de MDAC 2,8 se lanzó con la versión de 64 bits de Windows Server 2003 y Windows XP.

* **Componentes de Windows Data Access (WDAC):** MDAC cambió su nombre a WDAC: "componentes de Windows Data Access" a partir de Windows Vista y Windows Server 2008. WDAC se incluye como parte del sistema operativo y no está disponible por separado para la redistribución. La capacidad de servicio de WDAC está sujeta al ciclo de vida del sistema operativo.

  las versiones de 32 bits y 64 bits de WDAC se publican con las versiones de 32 bits y 64 bits de los sistemas operativos Windows, respectivamente.

## <a name="obsolete-data-access-technologies"></a>Tecnologías de acceso a datos obsoletas

Las tecnologías obsoletas son tecnologías que no se han mejorado ni actualizado en varias versiones de producto y que se excluirán de versiones futuras del producto. No utilice estas tecnologías al escribir nuevas aplicaciones. Cuando modifique las aplicaciones existentes que se escriben con estas tecnologías, considere la posibilidad de migrar esas aplicaciones a ADO.NET u otra tecnología actual.

Los componentes siguientes se consideran obsoletos:

* **DB-Library:** DB-Library es un modelo de programación específicas de SQL Server que incluye las API de C. No se han realizado mejoras en las características de DB-Library desde SQL Server 6,5. Su versión final era SQL Server 2000 y no se trasladará al sistema operativo Windows de 64 bits.
* **SQL incrustado (E-SQL):** E-SQL es un modelo de programación específico de SQL Server que permite que las instrucciones Transact-SQL se incrusten en código de Visual C. No se han realizado mejoras en las características de E-SQL desde SQL Server 6,5. Su versión final era SQL Server 2000 y no se trasladará al sistema operativo Windows de 64 bits.
* **Objetos de acceso a datos (DAO):** DAO proporciona acceso a las bases de datos de JET (Access). Esta API se puede usar desde Microsoft Visual Basic, Microsoft Visual C++y lenguajes de scripting. Se incluyó con Microsoft Office 2000 y Office XP. DAO 3,6 es la versión final de esta tecnología. No estará disponible en el sistema operativo Windows de 64 bits.
* **Remote Data Objects (RDO):** RDO se diseñó específicamente para tener acceso a orígenes de datos relacionales ODBC remotos y facilitó el uso de ODBC sin código de aplicación complejo. Se incluyó con las versiones 4, 5 y 6 de Microsoft Visual Basic. La versión 2,0 de RDO era la versión final de esta tecnología.

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]
