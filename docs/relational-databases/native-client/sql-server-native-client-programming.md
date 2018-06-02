---
title: Programación de SQL Server Native Client | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQLNCLI, about SQL Server Native Client
- SQL Server Native Client, about SQL Server Native Client
- data access [SQL Server Native Client], about SQL Server Native Client
- data access [SQL Server Native Client]
- SQL Server Native Client
- SQLNCLI
- native data access [SQL Server Native Client]
ms.assetid: 14ba2cb1-a424-4e4d-b224-0bf1015ab801
caps.latest.revision: 66
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: e7574f58ead9dc10afaf2cf6a9dc65c48a8c24f4
ms.sourcegitcommit: 2d93cd115f52bf3eff3069f28ea866232b4f9f9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/01/2018
ms.locfileid: "34706883"
---
# <a name="sql-server-native-client-programming"></a>Programación de SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client es una interfaz de programación de aplicaciones (API) de acceso a datos independiente que se introdujo en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y que se utiliza tanto para OLE DB como para ODBC. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client combina el proveedor OLE DB de SQL y el controlador ODBC de SQL en una biblioteca de vínculos dinámicos (DLL) nativa. También ofrece muchas más funciones nuevas de las que se proporcionaban en Data Access Components para Windows (DAC para Windows, anteriormente Microsoft Data Access Components o MDAC). Puede utilizar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client para crear nuevas aplicaciones o mejorar las existentes incorporando las características introducidas en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], como la compatibilidad con conjuntos de resultados activos múltiples (MARS), los tipos de datos definidos por el usuario (UDT), las notificaciones de consulta, el aislamiento de instantánea y el tipo de datos XML.  
  
> [!NOTE]  
>  Para obtener una lista de las diferencias entre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client y DAC para Windows, además de información sobre los problemas a tener en cuenta antes de actualizar una aplicación de Windows DAC a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, vea [actualizar una aplicación a SQL Server Cliente nativo de MDAC](../../relational-databases/native-client/applications/updating-an-application-to-sql-server-native-client-from-mdac.md).  
  
 El controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client siempre se utiliza junto con el administrador de controladores ODBC que se proporciona con DAC para Windows. El proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client puede utilizarse junto con los servicios principales de OLE DB que se proporcionan con DAC para Windows, pero no se trata de un requisito; la opción de usar o no los servicios principales depende de los requisitos de la aplicación individual (por ejemplo, si se requiere la agrupación de conexiones).  
  
 Objeto de datos ActiveX (ADO) aplicaciones pueden utilizar el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor Native Client OLE DB, pero se recomienda usar ADO junto con el **DataTypeCompatibility** palabra clave de cadena de conexión (o su correspondiente  **Origen de datos** propiedad). Al utilizar el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, las aplicaciones ADO pueden aprovecharse de esas nuevas características introducidas en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] que se encuentran disponibles a través de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client mediante las palabras clave de cadena de conexión o mediante las propiedades de OLE DB o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Para obtener más información sobre el uso de estas características con ADO, vea [usar ADO con SQL Server Native Client](../../relational-databases/native-client/applications/using-ado-with-sql-server-native-client.md).  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client se diseñó para proporcionar un método simplificado de acceso a datos nativos de SQL Server mediante OLE DB u ODBC. Es un método simplificado en el sentido de que combina las tecnologías de OLE DB y ODBC en una sola biblioteca, y permite innovar y desarrollar nuevas características de acceso a datos sin modificar los componentes actuales de DAC para Windows, que ya forman parte de la plataforma Microsoft Windows.  
  
 Aunque [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client usa los componentes de DAC para Windows, no depende explícitamente de ninguna versión en concreto de DAC para Windows. Puede usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client con la versión de DAC para Windows que esté instalada en cualquier sistema operativo compatible con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
## <a name="in-this-section"></a>En esta sección  
 [SQL Server Native Client](../../relational-databases/native-client/sql-server-native-client.md)  
 Enumera las características nuevas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client más significativas.  
  
 [Cuándo debe utilizarse SQL Server Native Client](../../relational-databases/native-client/when-to-use-sql-server-native-client.md)  
 Describe la forma en que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client se ajusta a las tecnologías de acceso a datos de Microsoft, sus semejanzas y diferencias con DAC para Windows y ADO.NET y, además, proporciona punteros para decidir qué tecnología de acceso a datos se va a usar.  
  
 [Características de SQL Server Native Client](../../relational-databases/native-client/features/sql-server-native-client-features.md)  
 Describe las características compatibles con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
 [Generar aplicaciones con SQL Server Native Client](../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
 Proporciona información general sobre el desarrollo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, como las diferencias que existen con Windows DAC, los componentes que utiliza y la forma en que puede utilizarse con ADO.  
  
 En esta sección también se explica la instalación e implementación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, incluida la forma de redistribuir la biblioteca de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
 [Requisitos del sistema para SQL Server Native Client](../../relational-databases/native-client/system-requirements-for-sql-server-native-client.md)  
 Describe el sistema de recursos necesario para usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
 [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
 Proporciona información sobre la forma de usar el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
 Proporciona información sobre la forma de usar el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
 [Más información sobre SQL Server Native Client](../../relational-databases/native-client/finding-more-sql-server-native-client-information.md)  
 Proporciona recursos adicionales sobre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, incluidos vínculos a recursos externos y obtención de más ayuda.  
  
 [Errores SQL Server Native Client](http://msdn.microsoft.com/library/ebd0e9a8-5fe5-4b15-9a44-2f131a13c186)  
 Contiene temas sobre errores en tiempo de ejecución asociados a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
## <a name="see-also"></a>Vea también  
 [Actualizar una aplicación de SQL Server 2005 Native Client](../../relational-databases/native-client/applications/updating-an-application-from-sql-server-2005-native-client.md)   
 [Temas de procedimientos de ODBC](../../relational-databases/native-client-odbc-how-to/odbc-how-to-topics.md)   
 [Temas de procedimientos de OLE DB](../../relational-databases/native-client-ole-db-how-to/ole-db-how-to-topics.md)  
  
  
