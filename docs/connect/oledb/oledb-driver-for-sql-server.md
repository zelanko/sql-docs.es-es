---
title: Controlador OLE DB para SQL Server | Documentos de Microsoft
description: Controlador OLE DB para SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: OLE DB Driver
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
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
ms.author: Pedro.Lopes
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 40458d9c9c3b547a40be170e390344d8bb5f181a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="ole-db-driver-for-sql-server"></a>Controlador OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

  Controlador de OLE DB para SQL Server es una datos independiente acceso aplicación interfaz de programación (API) utilizada para OLE DB, que se introdujo en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Controlador de OLE DB para SQL Server ofrece al controlador OLE DB de SQL en una biblioteca de vínculos dinámicos (DLL). También ofrece muchas más funciones nuevas de las que se proporcionaban en Data Access Components para Windows (DAC para Windows, anteriormente Microsoft Data Access Components o MDAC). Controlador de OLE DB para SQL Server puede utilizarse para crear nuevas aplicaciones o mejorar las aplicaciones existentes que necesitan aprovechar las características introducidas en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], por ejemplo, varios conjuntos de resultados activos (MARS), tipos de datos definidos por el usuario (UDT), consulta admiten notificaciones, el aislamiento de instantánea y el tipo de datos XML.  
  
> [!NOTE]  
>  Para obtener una lista de las diferencias entre el controlador OLE DB para SQL Server y Windows DAC, además de información sobre los problemas a tener en cuenta antes de actualizar una aplicación de Windows DAC al controlador de OLE DB para SQL Server, vea [actualizar una aplicación a controlador de OLE DB de SQL Servidor de MDAC](../oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md).  
  
 El controlador OLE DB para SQL Server puede utilizarse junto con OLE DB Core servicios suministrados con DAC para Windows, pero esto no es un requisito; la opción de usar los servicios principales o no depende de los requisitos de la aplicación individual (por ejemplo, si se requiere la agrupación de conexiones).  
  
 Las aplicaciones de objeto de datos ActiveX (ADO) pueden usar el controlador OLE DB para SQL Server, pero se recomienda usar ADO junto con el **DataTypeCompatibility** palabra clave de cadena de conexión (o el correspondiente  **Origen de datos** propiedad). Cuando se usa el controlador OLE DB para SQL Server, las aplicaciones ADO pueden aprovecharse de las nuevas características introducidas en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] que están disponibles mediante el controlador OLE DB para SQL Server a través de palabras clave de cadena de conexión o propiedades de OLE DB o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Para obtener más información sobre el uso de estas características con ADO, vea [utilizar ADO con el controlador OLE DB para SQL Server](../oledb/applications/using-ado-with-oledb-driver-for-sql-server.md).  
  
 Controlador de OLE DB para SQL Server se diseñó para proporcionar un método simplificado de obtener acceso a datos nativos a SQL Server mediante OLE DB. Proporciona una manera innovar y desarrollar nuevas características de acceso de datos sin tener que cambiar los componentes de Windows DAC actuales, que forman parte de la plataforma Microsoft Windows.  
  
 Mientras el controlador OLE DB para SQL Server utiliza componentes de DAC para Windows, no es explícitamente depende de una versión concreta de DAC para Windows. Puede usar el controlador OLE DB para SQL Server con la versión de DAC para Windows que se instala con cualquier sistema operativo compatible con el controlador OLE DB para SQL Server.  

 ## <a name="different-generations-of-ole-db-drivers"></a>Diferentes generaciones de controladores de OLE DB

Hay tres generaciones distintas de proveedores de Microsoft OLE DB para SQL Server.

### <a name="1-microsoft-ole-db-provider-for-sql-server-sqloledb"></a>1. Proveedor Microsoft OLE DB para SQL Server (SQLOLEDB)
El [proveedor Microsoft OLE DB para SQL Server](../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) (SQLOLEDB) todavía se incluye como parte del [Windows Data Access Components](https://msdn.microsoft.com/en-us/library/ms692897.aspx). No se mantiene ya y no se recomienda utilizar este controlador para el nuevo desarrollo.

### <a name="2-sql-server-native-client-snac"></a>2. SQL Server Native Client (SNAC)
A partir de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [SQL Server Native Client (SNAC)](../../relational-databases/native-client/sql-server-native-client.md) incluye una interfaz de proveedor de OLE DB (SQLNCLI) y es el proveedor OLE DB que se incluye con [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] a través de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].

Era [anunció su eliminación en 2011](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/) y no se recomienda utilizar este controlador para el nuevo desarrollo. Para obtener más información sobre el ciclo de vida SNAC y descargas disponibles, consulte [ciclo de vida SNAC explicada](https://blogs.msdn.microsoft.com/sqlreleaseservices/snac-lifecycle-explained/).

### <a name="3-microsoft-ole-db-driver-for-sql-server-msoledbsql"></a>3. Controlador de Microsoft OLE DB para SQL Server (MSOLEDBSQL)
OLE DB [undeprecated](https://blogs.msdn.microsoft.com/sqlnativeclient/2017/10/06/announcing-the-new-release-of-ole-db-driver-for-sql-server/) y publicadas en 2018.

El nuevo proveedor de OLE DB se llama el controlador OLE DB de Microsoft para SQL Server (MSOLEDBSQL). El nuevo proveedor se actualizará con las últimas características de servidor en el futuro.

> [!NOTE]
> Para usar el controlador de OLE DB para Microsoft nueva para SQL Server en las aplicaciones existentes, debe planear convertir las cadenas de conexión de SQLOLEDB o SQLNCLI, a MSOLEDBSQL.
  
## <a name="in-this-section"></a>En esta sección  
[Casos de uso del controlador OLE DB para SQL Server](../oledb/when-to-use-oledb-driver-for-sql-server.md)  
 Describe cómo controlador OLE DB para SQL Server se ajusta con datos de Microsoft tecnologías de acceso, ¿cómo se compara con DAC para Windows y ADO.NET y proporciona punteros para decidir qué tecnología de acceso a datos.  
  
 [Controlador OLE DB para las características de SQL Server](../oledb/features/oledb-driver-for-sql-server-features.md )  
 Describe las características admitidas por el controlador OLE DB para SQL Server.  
  
 [Compilación de aplicaciones con el controlador OLE DB para SQL Server](../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
 Proporciona información general del controlador de OLE DB para el desarrollo de SQL Server, incluido cómo difiere de la DAC para Windows, los componentes que utiliza, y cómo puede usar ADO con él.  
  
 Esta sección también trata el controlador OLE DB para la instalación de SQL Server y la implementación, incluida la forma de redistribuir el controlador OLE DB para la biblioteca de SQL Server.  
  
 [Requisitos del sistema del controlador OLE DB para SQL Server](../oledb/system-requirements-for-oledb-driver-for-sql-server.md)  
 Describe los recursos del sistema necesarios para usar el controlador OLE DB para SQL Server.  
  
 [Programación del controlador OLE DB para SQL Server](../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
 Proporciona información sobre cómo usar el controlador OLE DB para SQL Server.  
  
 [Búsqueda de más información sobre el controlador OLE DB para SQL Server](../oledb/finding-more-oledb-driver-for-sql-server-information.md)  
 Proporciona recursos adicionales sobre el controlador OLE DB para SQL Server, incluidos los vínculos a recursos externos y obtención de más ayuda.  
  
  
## <a name="see-also"></a>Vea también  
 [Actualizar una aplicación de SQL Server 2005 Native Client](../oledb/applications/updating-an-application-from-sql-server-2005-native-client.md)    
 [Temas "Cómo..." de OLE DB](../oledb/ole-db-how-to/ole-db-how-to-topics.md)  
  
  
