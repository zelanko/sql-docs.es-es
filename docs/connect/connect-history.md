---
title: Historial de controladores para Microsoft SQL Server | Microsoft Docs
description: En esta página se describen las tecnologías de conexión de datos históricos de Microsoft para conectarse a SQL Server.
ms.custom: ''
ms.date: 05/04/2018
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3724e9c616a17e490946888d2acc8c886a57545a
ms.sourcegitcommit: 1a96abbf434dfdd467d0a9b722071a1ca1aafe52
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2020
ms.locfileid: "81529072"
---
# <a name="driver-history-for-microsoft-sql-server"></a>Historial de controladores para Microsoft SQL Server

En esta página se describen las tecnologías de conexión de datos históricos de Microsoft para conectarse a SQL Server.

## <a name="odbc"></a>ODBC

Hay tres generaciones distintas de proveedores de controladores OLE DB de Microsoft para SQL Server. El primer controlador ODBC "SQL Server" todavía se suministra como parte de [Microsoft Data Access Components](#microsoft-or-windows-data-access-components). No se recomienda usar este controlador para nuevos desarrollos. A partir de SQL Server 2005, [SQL Server Native Client](#sql-server-native-client) incluye una interfaz ODBC, que es el controlador ODBC que se incluye con SQL Server 2005 hasta SQL Server 2012. No se recomienda usar este controlador para nuevos desarrollos. Tras SQL Server 2012, el [Microsoft ODBC Driver for SQL Server](#microsoft-odbc-driver-for-sql-server) es el controlador que se actualiza con las características de servidor más recientes en el futuro.

### <a name="sql-server-native-client"></a>SQL Server Native Client

SQL Server Native Client es una biblioteca independiente que se utiliza con OLE DB y ODBC. SQL Server Native Client (a menudo abreviado SNAC) se incluye con SQL Server 2005 hasta 2012. SQL Server Native Client se puede usar para las aplicaciones que han de aprovechar las nuevas características introducidas en SQL Server 2005 hasta SQL Server 2012. (Microsoft/Windows Data Access Components se actualizan con estas nuevas características de SQL Server). En el caso de las nuevas características posteriores a SQL Server 2012, no se actualizará SQL Server Native Client. Cambie a Microsoft ODBC Driver for SQL Server o a OLE DB Driver for SQL Server si quiere sacar partido de las nuevas características de SQL Server en el futuro.

Para obtener la documentación completa del SQL Server Native Client, consulte la [documentación de SQL Server Native Client](../relational-databases/native-client/sql-server-native-client-programming.md).

### <a name="microsoft-odbc-driver-for-sql-server"></a>Controlador ODBC de Microsoft para SQL Server

Tras SQL Server 2012, el controlador ODBC principal de SQL Server se ha desarrollado y publicado como Microsoft ODBC Driver for SQL Server. Para más información, consulte la [documentación de Microsoft ODBC Driver for SQL Server](./odbc/microsoft-odbc-driver-for-sql-server.md).

## <a name="ole-db"></a>OLE DB

Hay tres generaciones distintas de proveedores de OLE DB de Microsoft para SQL Server. El primer "proveedor OLE DB de Microsoft para SQL Server" (SQLOLEDB) todavía se suministra como parte de los [Componentes de Windows Data Access](#microsoft-or-windows-data-access-components). Este proveedor no se actualizará con las nuevas características y no se recomienda usar este controlador para nuevos desarrollos. A partir de SQL Server 2005, [SQL Server Native Client (SNAC)](#sql-server-native-client) incluye una interfaz del proveedor OLE DB (SQLNCLI), que es el proveedor OLE DB que se incluye con SQL Server 2005 hasta SQL Server 2017. Se [anunció en desuso en 2011](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/), y no se recomienda usar este controlador para nuevos desarrollos. En 2017, la tecnología de acceso a datos OLE DB dejó de estar [en desuso y se anunció una nueva versión planeada](https://blogs.msdn.microsoft.com/sqlnativeclient/2017/10/06/announcing-the-new-release-of-ole-db-driver-for-sql-server/) para 2018. El nuevo proveedor OLE DB se conoce como "Microsoft OLE DB Driver for SQL Server" (MSOLEDBSQL) y actualmente se mantiene y recibe soporte.

## <a name="adonet"></a>ADO.NET

ADO.NET se presentó con Microsoft .NET Framework y se sigue mejorando y manteniendo. Se trata de un componente básico de Microsoft .NET Framework. Para más información, consulte [Microsoft ADO.NET para SQL Server](ado-net/microsoft-ado-net-sql-server.md).

## <a name="jdbc"></a>JDBC

### <a name="microsoft-jdbc-driver-for-sql-server"></a>Microsoft JDBC Driver para SQL Server

Presentado en el año 2000, Microsoft JDBC Driver para SQL Server se sigue mejorando y manteniendo. Era de código abierto en 2016. Para obtener la información más reciente, incluido cómo descargar el controlador, consulte [Introducción al controlador JDBC](./jdbc/overview-of-the-jdbc-driver.md).

## <a name="php"></a>PHP

### <a name="microsoft-drivers-for-php-for-sql-server"></a>Controladores de Microsoft para PHP para SQL Server

Presentados en 2009 como proyecto de código abierto, los controladores de Microsoft para PHP para SQL Server se siguen mejorando y manteniendo. Para obtener la información más reciente, incluido cómo descargar el controlador PHP, consulte [Controladores de Microsoft para PHP para SQL Server](./php/microsoft-php-driver-for-sql-server.md).

## <a name="nodejs"></a>Node.js

### <a name="microsoft-driver-for-nodejs-for-sql-server"></a>Controlador de Microsoft para Node.js para SQL Server

El controlador de Microsoft para Node.js para SQL Server permite que las aplicaciones de Node.js en Microsoft Windows y Microsoft Azure tengan acceso a Microsoft SQL Server y Microsoft Azure SQL Database. Las iniciativas de desarrollo ya no se centran en este controlador. No se recomienda crear aplicaciones con el controlador de Microsoft para Node.js para SQL Server.

Para obtener más información sobre el controlador de Microsoft para Node.js para SQL Server, consulte [WindowsAzure/node-sqlserver](https://github.com/Azure/node-sqlserver).

### <a name="tedious"></a>Tedious

Microsoft actualmente contribuye y admite el módulo Tedious de código abierto de Node.js para la conectividad a SQL Server mediante JavaScript. Para más información, consulte [Node.js Driver para SQL Server](./node-js/node-js-driver-for-sql-server.md).

## <a name="microsoft-or-windows-data-access-components"></a>Microsoft o Windows Data Access Components

Microsoft/Windows Data Access Components (MDAC/WDAC) se suministran y son compatibles con Windows para la compatibilidad con versiones anteriores de aplicaciones y no forman parte de la pila de tecnología de SQL Server actual. No se agregarán nuevas características a los componentes de MDAC/WDAC y no se recomienda su uso en el desarrollo de nuevas aplicaciones.

A los efectos de este documento, puede dividir la pila de MDAC/WDAC en los componentes siguientes, en función de la tecnología y los productos:

* **ADO** (ADOMD y ADOX incluidos)
* **OLE DB** (incluidos OLE DB Core Services, el proveedor OLE DB para SQL Server, el proveedor OLE DB para Oracle, el proveedor OLE DB para controladores ODBC, el proveedor de formas de datos y el proveedor de datos remotos)
* **ODBC** (incluidos el administrador de controladores ODBC, el controlador ODBC de SQL y el controlador ODBC para Oracle)

### <a name="mdacwdac-components"></a>Componentes MDAC/WDAC

MDAC/WDAC incluyen estos componentes:

* **ODBC:** La interfaz de conectividad abierta de bases de datos (ODBC) de Microsoft es una interfaz de lenguaje de programación C que permite a las aplicaciones acceder a los datos de diversos sistemas de administración de bases de datos (DBMS). Las aplicaciones que usan esta API solo tienen acceso a los orígenes de datos relacionales.
* **OLE DB:** OLE DB es un conjunto de interfaces COM para acceder a los datos de diversos almacenes de datos. Los proveedores OLE DB existen para acceder a datos de bases de datos, sistemas de archivos, almacenes de mensajes, servicios de directorio, flujos de trabajo y almacenes de documentos.
* **ADO:** Objetos de datos ActiveX (ADO) ofrece un modelo de programación general. Aunque un poco menos eficaz que la codificación que OLE DB u ODBC directamente, ADO es sencillo de aprender y usar. Como tal, no puede usarse en lenguajes de script, como JScript o Visual Basic Scripting Edition (VBScript).
* **ADOMD:** La multidimensional de ADO (ADOMD) se va a usar con proveedores de datos multidimensionales, como el proveedor OLAP de Microsoft, también conocido como proveedor de Microsoft Analysis Services. No se han realizado mejoras importantes en las características desde MDAC 2.0.
* **ADOX:** Las extensiones de ADO para lenguaje de definición de datos y seguridad (ADOX) permiten la creación y modificación de definiciones de una base de datos, una tabla, un índice o un procedimiento almacenado. Se puede usar ADOX con cualquier proveedor. El proveedor OLE DB de Microsoft Jet proporciona compatibilidad total con ADOX, mientras que el proveedor OLE DB de Microsoft SQL Server ofrece compatibilidad limitada.
* **Bibliotecas de red de Microsoft SQL Server:** Las bibliotecas de red de SQL Server permiten a SQLOLEDB y SQLODBC comunicarse con la base de datos de SQL Server. Las siguientes bibliotecas de red SQL Server han quedado en desuso en las versiones de MDAC/WDAC: Banyan Vines, AppleTalk, ServerNet, IPX/SPX, Giganet y RPC. TCP/IP y las canalizaciones con nombre seguirán siendo compatibles y estarán disponibles en el sistema operativo Windows de 64 bits.
* **MSDASQL:** El proveedor OLE DB de Microsoft para ODBC (MSDASQL) permite a las aplicaciones que se basan en OLE DB y ADO (que OLEDB usa internamente) acceder a los orígenes de datos a través de un controlador ODBC. MSDASQL es un proveedor OLEDB que se conecta a ODBC, en lugar de a una base de datos. Consiste en un puente desde OLE DB a un controlador ODBC cuando no existe ningún proveedor OLE DB directo para un origen de datos. MSDASQL se suministra con el sistema operativo Windows, y Windows Server 2008 y Vista SP1 fueron las primeras versiones de Windows en incluir una versión de 64 bits de la tecnología.

### <a name="deprecated-mdacwdac-components"></a>Componentes MDAC/WDAC en desuso

Estos componentes todavía se admiten en la versión actual de MDAC/WDAC, pero podrían quitarse en versiones futuras. Al desarrollar nuevas aplicaciones, Microsoft recomienda evitar el uso de estos componentes. Además, al actualizar o modificar las aplicaciones existentes, quite cualquier dependencia de estos componentes.

* **SQLOLEDB:** El proveedor OLE DB de Microsoft para SQL Server (SQLOLEDB), que admite el acceso a Microsoft SQL Server, ha quedado en desuso. Es posible que no se admita su conectividad con versiones futuras de SQL Server. La capacidad de conectarse a versiones anteriores a SQL Server 7 se quitará del sistema operativo después de Windows 7. Las nuevas aplicaciones deben usar Microsoft OLE DB Driver for SQL Server (MSOLEDBSQL), que admite las nuevas características de SQL Server. Las aplicaciones existentes también deben migrar a Microsoft OLE DB Driver for SQL Server para mejorar el rendimiento, la confiabilidad y la compatibilidad. Para más información, consulte [Actualización de una aplicación a OLE DB Driver for SQL Server desde MDAC](oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md).
* **SQLODBC:** El controlador ODBC de Microsoft SQL Server (SQLODBC), que admite el acceso a Microsoft SQL Server, ha quedado en desuso. Es posible que no se admita su conectividad con versiones futuras de SQL Server. La capacidad de conectarse a versiones anteriores a SQL Server 7 se quitará del sistema operativo después de Windows 7. Las nuevas aplicaciones deben usar Microsoft ODBC Driver for SQL Server en Windows, que admite nuevas características de SQL Server. Las aplicaciones existentes también deben migrar a Microsoft ODBC Driver for SQL Server para mejorar el rendimiento, la confiabilidad y la compatibilidad. Para obtener información relacionada, consulte [Actualización de una aplicación a SQL Server Native Client desde MDAC](../relational-databases/native-client/applications/updating-an-application-to-sql-server-native-client-from-mdac.md).
* **Motor de base de datos Microsoft Jet 4.0:** A partir de la versión 2.6, MDAC ya no contiene componentes Jet. En otras palabras, MDAC 2.6, 2.7 y 2.8 no contienen Microsoft Jet, el proveedor OLE DB de Microsoft Jet, los controladores de base de datos de escritorio ODBC o los objetos de acceso a datos de Jet (DAO). 

  No hay ninguna versión de 64 bits del motor de base de datos Jet, el controlador OLEDB para Jet, los controladores ODBC para Jet o los objetos de acceso a datos (DAO) de Jet disponibles. Para más información, vea el [artículo de Knowledge Base 957570](https://support.microsoft.com/kb/957570). En las versiones de 64 bits de Windows, las instancias de Jet de 32 bits se ejecutan en el subsistema WOW64 de Windows. Para más información sobre WOW64, consulte la [documentación de WOW64 de MSDN](/windows/desktop/WinProg64/wow64-implementation-details). Las aplicaciones nativas de 64 bits no pueden comunicarse con los controladores Jet de 32 bits que se ejecutan en WOW64.

  En lugar de Microsoft Jet, Microsoft recomienda usar [Microsoft SQL Server Express Edition](https://www.microsoft.com/sql-server/sql-server-editions-express) al desarrollar nuevas aplicaciones que no sean de Microsoft Access y que requieran un almacén de datos relacionales. Estas aplicaciones Jet nuevas o convertidas pueden seguir usando Jet con la intención de usar archivos de Microsoft Office 2003 y versiones anteriores (.mdb y .xls) para el almacenamiento de datos no principal. Sin embargo, para estas aplicaciones, debe planear la migración del motor de base de datos Jet al de Microsoft Access. Puede [descargar el motor de base de datos de Microsoft Access](https://www.microsoft.com/download/details.aspx?id=54920), que le permite leer y escribir en archivos ya existentes en Office 2003 (.mdb y .xls) o en los formatos de archivo de Office 2007 (*.accdb, *.xlsm, *.xlsx y *.xlsb).

  > [!IMPORTANT]
  > Lea el contrato de licencia para el usuario final de 2007 Office System para conocer las limitaciones de uso específicas.

  > [!NOTE]
  > Las aplicaciones de SQL Server también pueden acceder a 2007 Office System y versiones anteriores, a los archivos de conectividad de datos heterogéneos de SQL Server, así como a las capacidades de Integration Services, a través del controlador 2007 Office System. Además, las aplicaciones de SQL Server de 64 bits pueden acceder a los archivos de Jet y 2007 Office System de 32 bits mediante SQL Server Integration Services (SSIS) de 32 bits en Windows de 64 bits.

* **MSDADS:** Con el proveedor OLE DB de Microsoft para formas de datos (MSDADS), puede crear relaciones jerárquicas entre las claves, los campos o los conjuntos de filas de una aplicación. No se han realizado mejoras importantes en las características desde MDAC 2.1. Este proveedor ha quedado en desuso. Microsoft recomienda que se utilice XML, en lugar de MSDADS.
* **Oracle ODBC y Oracle OLE DB:** El controlador ODBC de Microsoft para Oracle (Oracle ODBC) y el proveedor OLE DB de Microsoft para Oracle (Oracle OLE DB) proporcionan acceso a los servidores de bases de datos de Oracle. Se compilan con Oracle Call Interface (OCI) versión 7 y proporcionan compatibilidad completa con Oracle 7. Además, utilizan la emulación de Oracle 7 para proporcionar compatibilidad limitada con las bases de datos de Oracle 8. Oracle ya no admite aplicaciones que usan llamadas a la versión 7 de OCI. Estas tecnologías han quedado en desuso. Si usa orígenes de datos de Oracle, debe migrar al proveedor y controlador proporcionados por Oracle.
* **RDS:** Remote Data Services (RDS) es un mecanismo propietario de Microsoft para acceder a objetos de conjuntos de registros ADO remotos a través de Internet o de una intranet. RDS ha quedado en desuso; no se han realizado mejoras importantes en las características en RDS desde MDAC 2.1. Microsoft ha lanzado .NET Framework, que tiene amplias funcionalidades de SOAP y reemplaza los componentes de RDS. Todos los componentes de servidor RDS se quitarán del sistema operativo después de Windows 7.
* **JRO:** Los objetos de replicación de Jet (JRO) están en desuso. JRO se utiliza en ADO con bases de datos Jet ( *.mdb) para crear y comprimir bases de datos Jet (.mdb) y realizar la administración de replicación de Jet. MDAC 2.7 será la última versión. JRO no estará disponible en el sistema operativo Windows de 64 bits. JRO no es compatible con el formato de archivo de Microsoft Access 2007 (* .accdb).
* **Compatibilidad con ODBC de 16 bits:** Si usa aplicaciones de 16 bits, debe migrar a una aplicación de 32 bits. La funcionalidad de 16 bits ha quedado en desuso y se quita de los sistemas operativos de 64 bits. Para obtener más información, vea el [artículo de Knowledge Base 896458](https://support.microsoft.com/kb/896458).
* **Proveedor simple OLEDB (MSDAOSP):** este proveedor ofrece un marco para compilar rápidamente proveedores OLE DB a través de datos simples. MSDAOSP ha quedado en desuso.
* **Biblioteca de cursores ODBC:** La biblioteca de cursores ODBC (ODBCCR32.dll) proporciona cursores de datos limitados del lado cliente. esta biblioteca ha quedado en desuso; la aplicación puede usar implementaciones de cursor del lado servidor como reemplazo.
* **Comunicación remota de la interfaz OLE DB fuera de proceso:** la comunicación remota de la interfaz OLEDB (msdaps.dll) fue un intento de permitir que los proveedores OLE DB se ejecutaran fuera de proceso. La comunicación remota de la interfaz OLEDB fuera de proceso ha quedado en desuso.
* **Bibliotecas de red de SQL de AppleTalk y Banyan Vines:** Las bibliotecas de red de Banyan Vines, AppleTalk, ServerNet, IPX/SPX, Giganet y RPC SQL han quedado en desuso. Si usa cualquiera de estas tecnologías, debe modificar las aplicaciones para que usen alguna otra biblioteca de red, como TCP/IP y la canalización con nombre.

### <a name="mdacwdac-releases"></a>Versiones de MDAC/WDAC

Esta es una lista de los escenarios de compatibilidad de las versiones anteriores de MDAC/WDAC, empezando por la primera.

* **MDAC 1.5, MDAC 2.0 y MDAC 2.1:** Estas versiones de MDAC eran versiones independientes que se lanzaron a través de Microsoft Windows NT Option Pack, el SDK de la plataforma Microsoft Windows o el sitio web de MDAC. Ya no se admiten estas versiones de MDAC.
* **MDAC 2.5:** esta versión de MDAC se incluyó en el sistema operativo Windows 2000. Los Service Pack de MDAC 2.5 se incluyeron con los Service Pack de Windows 2000 correspondientes.
* **MDAC 2.6:** MDAC 2.6 RTM, SP1 y SP2 se incluyeron con Microsoft SQL Server 2000 RTM, SP1 y SP2, respectivamente. Además, estos Service Pack de MDAC se publicaron en el sitio web de MDAC de acuerdo con la programación de lanzamiento de los Service Pack de Microsoft SQL Server 2000. Puede instalar esta versión de MDAC y sus Service Pack en las plataformas Windows 2000, Windows Millennium Edition, Windows NT, Windows 95 y Windows 98. Ya no se admite esta versión de MDAC.
* **MDAC 2.7:** esta versión de MDAC se incluyó en los sistemas operativos Microsoft Windows XP RTM y SP1. Puede instalar esta versión de MDAC y sus Service Pack en plataformas Windows 2000, Windows Millennium, Windows NT y Windows 98. Solo puede instalar esta versión en la plataforma Windows XP a través del sistema operativo o sus Service Pack. Ya no se admite esta versión de MDAC.
* **MDAC 2.8:** esta versión de MDAC se incluye con Windows Server 2003 y Windows XP SP2 y versiones posteriores. También puede instalar esta versión de MDAC y sus Service Pack en Windows 2000.

  * La versión de 32 bits de MDAC 2.8 también se publicó en el sitio web de MDAC al mismo tiempo que se publicó Windows Server 2003 para el cliente.
  * La versión de 64 bits de MDAC 2.8 se lanzó con la versión de 64 bits de Windows Server 2003 y Windows XP.

* **Windows Data Access Components (WDAC):** a partir de Windows Vista y Windows Server 2008, MDAC cambió su nombre a WDAC: "Windows Data Access Components". WDAC se incluye como parte del sistema operativo y no está disponible por separado para la redistribución. La capacidad de servicio de WDAC está sujeta al ciclo de vida del sistema operativo.

  Las versiones de 32 bits y 64 bits de WDAC se publican con las versiones de 32 bits y 64 bits de los sistemas operativos Windows, respectivamente.

## <a name="obsolete-data-access-technologies"></a>Tecnologías de acceso a datos obsoletas

Las tecnologías obsoletas son aquellas que no se han mejorado ni actualizado en varias versiones de producto y que se excluirán de versiones futuras del producto. No utilice estas tecnologías al escribir nuevas aplicaciones. Cuando modifique las aplicaciones existentes que se escriben con estas tecnologías, considere la posibilidad de migrar esas aplicaciones a ADO.NET u otra tecnología actual.

Los siguientes componentes se consideran obsoletos:

* **DB-Library:** DB-Library es un modelo de programación específico de SQL Server que incluye las API de C. No se han realizado mejoras en las características de DB-Library desde SQL Server 6.5. Se publicó por última vez con SQL Server 2000 y no se portará al sistema operativo Windows de 64 bits.
* **SQL incrustado(E-SQL):** E-SQL es un modelo de programación específico de SQL Server que permite insertar instrucciones Transact-SQL en código de Visual C. No se han realizado mejoras en las características de E-SQL desde SQL Server 6.5. Se publicó por última vez con SQL Server 2000 y no se portará al sistema operativo Windows de 64 bits.
* **Objetos de acceso a datos (DAO):** DAO proporciona acceso a las bases de datos JET (Access). Esta API se puede usar desde Microsoft Visual Basic, Microsoft Visual C++ y lenguajes de scripting. Se incluyó con Microsoft Office 2000 y Office XP. DAO 3.6 es la versión final de esta tecnología. No estará disponible en el sistema operativo Windows de 64 bits.
* **Remote Data Objects (RDO):** RDO se diseñó específicamente para acceder a orígenes de datos relacionales ODBC remotos y facilitó el uso de ODBC sin código de aplicación complejo. Se incluyó con las versiones 4, 5 y 6 de Microsoft Visual Basic. La versión 2.0 de RDO fue la versión final de esta tecnología.

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]
