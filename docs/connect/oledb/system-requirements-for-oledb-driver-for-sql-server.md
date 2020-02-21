---
title: Requisitos del sistema del controlador OLE DB para SQL Server | Microsoft Docs
description: Requisitos del controlador OLE DB para SQL Server
ms.custom: ''
ms.date: 02/12/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- system requirements [OLE DB Driver for SQL Server]
- data access [OLE DB Driver for SQL Server], system requirements
- OLE DB Driver for SQL Server, system requirements
- MSOLEDBSQL, system requirements
author: pmasl
ms.author: pelopes
ms.openlocfilehash: cec8b2aca53f64e7a3883dbccddce1a330c8a6e5
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67993776"
---
# <a name="system-requirements-for-ole-db-driver-for-sql-server"></a>Requisitos del sistema del controlador OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

  Para utilizar las características de acceso a datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como MARS, debe tener instalado el software siguiente:  

-   OLE DB Driver for SQL Server en el cliente.  

-   Una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en su servidor.   

> [!NOTE]  
>  Asegúrese de que inicia sesión con privilegios de administrador antes de instalar este software.  

## <a name="operating-system-requirements"></a>Requisitos de sistema operativo  
 Para obtener una lista de sistemas operativos que admiten OLE DB driver for SQL Server, consulte [Directivas de compatibilidad de OLE DB Driver for SQL Server](../oledb/applications/support-policies-for-oledb-driver-for-sql-server.md).  

 ## <a name="azure-active-directory-authentication-requirements"></a>Requisitos de autenticación de Azure Active Directory  
 Al usar métodos de autenticación de Azure Active Directory con el controlador OLE DB, asegúrese de que se ha instalado la [Biblioteca de autenticación de Active Directory para SQL Server](https://go.microsoft.com/fwlink/?LinkID=513072). ADAL no es necesario con los demás métodos de autenticación u operaciones de OLE DB.
Para más información, consulte: [Uso de Azure Active Directory](features/using-azure-active-directory.md).

## <a name="sql-server-requirements"></a>requisitos de SQL Server  
 Para usar OLE DB Driver for SQL Server para acceder a los datos de las bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], debe tener instalada una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] admite las conexiones de todas las versiones de MDAC, Componentes de Windows Data Access y todas las versiones del controlador OLE DB para SQL Server. Cuando una versión del cliente anterior se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], los tipos de datos del servidor que el cliente no conoce se asignan a tipos que son compatibles con la versión del cliente. Para más información, consulte [Compatibilidad de tipo de datos para las versiones del cliente](#data-type-compatibility-for-client-versions).  

## <a name="cross-language-requirements"></a>Requisitos de idiomas  
 La versión en inglés de OLE DB Driver for SQL Server se admite con todas las versiones localizadas de los sistemas operativos admitidos. Las versiones localizadas de OLE DB Driver for SQL Server se admiten en sistemas operativos localizados que estén en el mismo idioma que la versión de OLE DB Driver for SQL Server localizada. Las versiones localizadas del controlador OLE DB para SQL Server también se admiten en las versiones en inglés de los sistemas operativos compatibles (siempre que se instale la configuración de idioma correspondiente).  

 Para actualizaciones:  

-   Las versiones en inglés de OLE DB Driver for SQL Server se pueden actualizar a cualquier versión localizada de OLE DB Driver for SQL Server.  

-   Las versiones localizadas de OLE DB Driver for SQL Server se pueden actualizar a versiones localizadas de OLE DB Driver for SQL Server del mismo idioma.  

-   La versión localizada de OLE DB Driver for SQL Server se puede actualizar a la versión en inglés de OLE DB Driver for SQL Server.  

-   Las versiones localizadas de OLE DB Driver for SQL Server no se pueden actualizar a versiones localizadas de OLE DB Driver for SQL Server de un idioma localizado diferente.  

## <a name="data-type-compatibility-for-client-versions"></a>Compatibilidad de tipo de datos para las versiones del cliente  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y el controlador OLE DB para SQL Server asignan los nuevos tipos de datos a los tipos de datos anteriores que son compatibles con clientes de nivel inferior, como se muestra en la tabla siguiente.  

 Las aplicaciones OLE DB y ADO pueden usar la palabra clave de cadena de conexión **DataTypeCompatibility** con OLE DB Driver for SQL Server para funcionar con tipos de datos más antiguos. Cuando **DataTypeCompatibility=80**, los clientes de OLE DB se conectarán con la versión de flujo TDS de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], en lugar de la versión de TDS. Esto significa que el servidor realizará la conversión de nivel inferior y los tipos de datos posteriores para [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], en lugar de hacerlo con el controlador OLE DB para SQL Server. También significa que las características disponibles en la conexión se limitarán al conjunto de funciones de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Los intentos de utilizar nuevos tipos de datos o funciones se detectan lo más pronto posible en las llamadas API y se devuelven los errores a la aplicación que realiza la llamada, en lugar de intentar pasar las solicitudes no válidas al servidor.   


 IDBInfo::GetKeywords siempre devolverá una lista de palabras clave que corresponde a la versión de servidor de la conexión y no se verá afectado por **DataTypeCompatibility**.  

|Tipo de datos|SQL Server Native Client<br /><br />SQL Server 2005|SQL Server Native Client 11.0<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|Controlador OLE DB para SQL Server|Windows Data Access Components, MDAC y<br /><br /> aplicaciones OLE DB de OLE DB Driver for SQL Server con DataTypeCompatibility=80|  
|---------------|--------------------------------------------------|-------------------------------------------------------------|-------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|  
|CLR UDT (\<= 8 Kb)|udt|udt|udt|Varbinary|  
|varbinary(max)|varbinary|varbinary|varbinary|Imagen|  
|ntext|varchar|varchar|varchar|Texto|  
|nvarchar(max)|NVARCHAR|NVARCHAR|NVARCHAR|Ntext|  
|Xml|Xml|Xml|Xml|Ntext|  
|CLR UDT (> 8 Kb)|varbinary|udt|udt|Imagen|  
|date|varchar|date|date|Varchar|  
|datetime2|varchar|datetime2|datetime2|Varchar|  
|datetimeoffset|varchar|datetimeoffset|datetimeoffset|Varchar|  
|time|varchar|time|time|Varchar|  

## <a name="see-also"></a>Consulte también  
 [Controlador OLE DB para SQL Server](../oledb/oledb-driver-for-sql-server.md)   
 [Instalación del controlador OLE DB para SQL Server](../oledb/applications/installing-oledb-driver-for-sql-server.md)  
