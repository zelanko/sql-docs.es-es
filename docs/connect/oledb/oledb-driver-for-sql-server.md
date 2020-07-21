---
title: Controlador Microsoft OLE DB para SQL Server
description: Microsoft OLE DB Driver for SQL Server proporciona conectividad a SQL Server y Azure SQL Database a través de API de OLE DB estándar.
ms.custom: ''
ms.date: 05/06/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- MSOLEDBSQL, about OLE DB Driver for SQL Server
- OLE DB Driver for SQL Server, about OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server], about OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server
- MSOLEDBSQL
- native data access [OLE DB Driver for SQL Server]
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 7f66fc300dce4e3b9fac9a2476c4703fd5be5c88
ms.sourcegitcommit: fb1430aedbb91b55b92f07934e9b9bdfbbd2b0c5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2020
ms.locfileid: "82886368"
---
# <a name="microsoft-ole-db-driver-for-sql-server"></a>Controlador Microsoft OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

El controlador OLE DB para SQL Server es una interfaz de programación de aplicaciones (API) de acceso a datos independiente que se introdujo en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y que se utiliza para OLE DB. El controlador OLE DB para SQL Server entrega el controlador OLE DB de SQL en una biblioteca de vínculos dinámicos (DLL). También ofrece muchas más funciones nuevas de las que se proporcionaban en Data Access Components para Windows (DAC para Windows, anteriormente Microsoft Data Access Components o MDAC). Puede usar el controlador OLE DB para SQL Server para crear aplicaciones o mejorar las existentes incorporando las características introducidas en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], como la compatibilidad con conjuntos de resultados activos múltiples (MARS), los tipos de datos definidos por el usuario (UDT), las notificaciones de consulta, el aislamiento de instantánea y el tipo de datos XML.  
  
> [!NOTE]  
> Para obtener una lista de las diferencias entre el controlador OLE DB para SQL Server y Windows DAC, además de información sobre los problemas a tener en cuenta antes de actualizar una aplicación de Windows DAC al controlador OLE DB para SQL Server, vea [Actualización de una aplicación al controlador OLE DB para SQL Server desde MDAC](../oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md).  

> [!IMPORTANT]
> El anterior [proveedor de Microsoft OLE DB para SQL Server](../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) (SQLOLEDB) y de [OLE DB para SQL Server Native Client](../../relational-databases/native-client/sql-server-native-client.md) (SQLNCLI) permanece en desuso y no se recomienda utilizarlo para nuevos trabajos de desarrollo.
  
 El controlador OLE DB para SQL Server puede usarse junto con los servicios principales de OLE DB que se proporcionan con Windows DAC, pero no se trata de un requisito; la opción de usar o no los servicios principales depende de los requisitos de la aplicación en cuestión (por ejemplo, si se requiere la agrupación de conexiones).  
  
 Las aplicaciones de objetos de datos ActiveX (ADO) pueden usar el controlador OLE DB para SQL Server, pero es recomendable usar ADO junto con la palabra clave de cadena de conexión **DataTypeCompatibility**, o su propiedad **DataSource** correspondiente. Al usar el controlador OLE DB para SQL Server, las aplicaciones de ADO pueden aprovecharse de esas nuevas características introducidas en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] que están disponibles mediante el controlador OLE DB para SQL Server mediante las palabras clave de cadena de conexión o las propiedades de OLE DB o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Para más información sobre el uso de estas características con ADO, vea [Uso de ADO con el controlador OLE DB para SQL Server](../oledb/applications/using-ado-with-oledb-driver-for-sql-server.md).  
  
 El controlador OLE DB para SQL Server se diseñó para proporcionar un método simplificado de acceso a datos nativos de SQL Server mediante OLE DB. Permite innovar y desarrollar nuevas características de acceso a datos sin modificar los componentes actuales de Windows DAC, que ya forman parte de la plataforma Microsoft Windows.  
  
 Aunque OLE DB Driver for SQL Server usa los componentes de Windows DAC, no depende explícitamente de ninguna versión en concreto de Windows DAC. Puede usar el controlador OLE DB para SQL Server con la versión de Windows DAC que esté instalada en cualquier sistema operativo compatible con el controlador OLE DB para SQL Server.  

 ## <a name="different-generations-of-ole-db-drivers"></a>Diferentes generaciones de controladores OLE DB

Hay tres generaciones distintas de proveedores de OLE DB de Microsoft para SQL Server.

### <a name="1-microsoft-ole-db-provider-for-sql-server-sqloledb"></a>1. Proveedor Microsoft OLE DB para SQL Server (SQLOLEDB)
El [proveedor OLE DB de Microsoft para SQL Server](../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) (SQLOLEDB) todavía se suministra como parte de los [Componentes de Windows Data Access](/previous-versions/windows/desktop/ms692897(v=vs.85)). Ya no se mantiene y no se recomienda usar este controlador para nuevos desarrollos.

### <a name="2-sql-server-native-client-snac"></a>2. SQL Server Native Client (SNAC)
A partir de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [SQL Server Native Client (SNAC)](../../relational-databases/native-client/sql-server-native-client.md) incluye una interfaz del proveedor OLE DB (SQLNCLI), y es el proveedor OLE DB que se incluye con [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] mediante [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].

Se [anunció en desuso en 2011](/archive/blogs/sqlnativeclient/microsoft-is-aligning-with-odbc-for-native-relational-data-access), y no se recomienda usar este controlador para nuevos desarrollos. Para más información sobre el ciclo de vida de SNAC y las descargas disponibles, vea [SNAC lifecycle explained](/archive/blogs/sqlreleaseservices/snac-lifecycle-explained) (Explicación del ciclo de vida de SNAC).

### <a name="3-microsoft-ole-db-driver-for-sql-server-msoledbsql"></a>3. Controlador Microsoft OLE DB para SQL Server (MSOLEDBSQL)
OLE DB [dejó de estar en desuso](/archive/blogs/sqlnativeclient/announcing-the-new-release-of-ole-db-driver-for-sql-server) y se lanzó en 2018.

El nuevo proveedor OLE DB se conoce como el controlador OLE DB de Microsoft para SQL Server (MSOLEDBSQL). El nuevo proveedor se actualizará con las características más recientes del servidor en el futuro.

> [!NOTE]
> Para usar el nuevo controlador OLE DB de Microsoft para SQL Server en las aplicaciones existentes, debe planear la conversión de las cadenas de conexión de SQLOLEDB o SQLNCLI a MSOLEDBSQL.
  
## <a name="in-this-section"></a>En esta sección  
[Casos de uso del controlador OLE DB para SQL Server](../oledb/when-to-use-oledb-driver-for-sql-server.md)  
 Describe la forma en que el controlador OLE DB para SQL Server se ajusta a las tecnologías de acceso a datos de Microsoft, sus semejanzas y diferencias con Windows DAC y ADO.NET, y, además, proporciona indicaciones para decidir qué tecnología de acceso a datos se va a usar.  
  
 [Características del controlador OLE DB para SQL Server](../oledb/features/oledb-driver-for-sql-server-features.md )  
 Describe las características compatibles con el controlador OLE DB para SQL Server.  
  
 [Compilación de aplicaciones con el controlador OLE DB para SQL Server](../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
 Proporciona información general sobre el desarrollo del controlador OLE DB para SQL Server, incluidas las diferencias que existen con Windows DAC, los componentes que usa y la forma en que se puede usar con ADO.  
  
 Esta sección también trata sobre el controlador OLE DB para la instalación e implementación de SQL Server, incluida la forma de redistribuir el controlador OLE DB para la biblioteca de SQL Server.  
  
 [Requisitos del sistema del controlador OLE DB para SQL Server](../oledb/system-requirements-for-oledb-driver-for-sql-server.md)  
 Describe los recursos del sistema necesarios para usar el controlador OLE DB para SQL Server.  
  
 [Programación del controlador OLE DB para SQL Server](../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
 Proporciona información sobre cómo usar el controlador OLE DB para SQL Server.  
  
 [Búsqueda de más información sobre el controlador OLE DB para SQL Server](../oledb/finding-more-oledb-driver-for-sql-server-information.md)  
 Proporciona recursos adicionales del controlador OLE DB para SQL Server, incluidos los vínculos a recursos externos y orientación adicional.  
  
  
## <a name="see-also"></a>Consulte también  
 [Actualización de una aplicación desde SQL Server 2005 Native Client](../oledb/applications/updating-an-application-from-sql-server-2005-native-client.md)    
 [Temas de procedimientos de OLE DB](../oledb/ole-db-how-to/ole-db-how-to-topics.md)  
  
  
