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
manager: craigg
ms.openlocfilehash: 6462901ba1e3e73ca8c0a4ca448d8bc689bd8868
ms.sourcegitcommit: 958cffe9288cfe281280544b763c542ca4025684
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 02/23/2019
ms.locfileid: "56744435"
---
# <a name="system-requirements-for-ole-db-driver-for-sql-server"></a>Requisitos del sistema del controlador OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

  Para utilizar las características de acceso a datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como MARS, debe tener instalado el software siguiente:  

-   Controlador OLE DB para SQL Server en el cliente.  

-   Una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en su servidor.   

> [!NOTE]  
>  Asegúrese de que inicia sesión con privilegios de administrador antes de instalar este software.  

## <a name="operating-system-requirements"></a>Requisitos de sistema operativo  
 Para obtener una lista de sistemas operativos que admiten el controlador de OLE DB para SQL Server, vea [admiten las directivas de controlador de OLE DB para SQL Server](../oledb/applications/support-policies-for-oledb-driver-for-sql-server.md).  

 ## <a name="azure-active-directory-authentication-requirements"></a>Requisitos de autenticación de Azure Active Directory  
 Al usar métodos de autenticación de Azure Active Directory con el controlador OLE DB, asegúrese de que el [Active Directory Authentication Library para SQL Server](https://go.microsoft.com/fwlink/?LinkID=513072) se ha instalado. ADAL no es necesario para los otros métodos de autenticación o las operaciones de OLE DB.
Para más información, consulte [Uso de Azure Active Directory](features/using-azure-active-directory.md).

## <a name="sql-server-requirements"></a>requisitos de SQL Server  
 Para usar el controlador OLE DB para SQL Server para acceder a los datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bases de datos, debe tener una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalado.  

 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] admite las conexiones de todas las versiones de MDAC, Componentes de Windows Data Access y todas las versiones del controlador OLE DB para SQL Server. Cuando una versión del cliente anterior se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], los tipos de datos del servidor que el cliente no conoce se asignan a tipos que son compatibles con la versión del cliente. Para más información, consulte [Compatibilidad de tipo de datos para las versiones del cliente](#data-type-compatibility-for-client-versions).  

## <a name="cross-language-requirements"></a>Requisitos de idiomas  
 La versión en inglés del controlador OLE DB para SQL Server se admite en todas las versiones localizadas de los sistemas operativos compatibles. Las versiones localizadas del controlador OLE DB para SQL Server se admiten en sistemas operativos localizados que son el mismo idioma que el localizado controlador OLE DB para la versión de SQL Server. Las versiones localizadas del controlador OLE DB para SQL Server también se admiten en las versiones en inglés de los sistemas operativos compatibles (siempre que se instale la configuración de idioma correspondiente).  

 Para actualizaciones:  

-   Las versiones en inglés del controlador OLE DB para SQL Server pueden actualizarse a cualquier versión traducida de controlador de OLE DB para SQL Server.  

-   Las versiones localizadas del controlador OLE DB para SQL Server pueden actualizarse a versiones localizadas del controlador de OLE DB para SQL Server del mismo idioma.  

-   Versión localizada del controlador OLE DB para SQL Server puede actualizarse a la versión en inglés del controlador de OLE DB para SQL Server.  

-   Las versiones localizadas del controlador OLE DB para SQL Server no pueden actualizarse a localizado controlador OLE DB para las versiones de SQL Server de un idioma diferente.  

## <a name="data-type-compatibility-for-client-versions"></a>Compatibilidad de tipo de datos para las versiones del cliente  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y el controlador OLE DB para SQL Server asignan los nuevos tipos de datos a los tipos de datos anteriores que son compatibles con clientes de nivel inferior, como se muestra en la tabla siguiente.  

 Las aplicaciones OLE DB y ADO pueden usar el **DataTypeCompatibility** palabra clave de cadena de conexión con el controlador OLE DB para SQL Server para que funcione con tipos de datos más antiguos. Cuando **DataTypeCompatibility=80**, los clientes de OLE DB se conectarán con la versión de flujo TDS de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], en lugar de la versión de TDS. Esto significa que el servidor realizará la conversión de nivel inferior y los tipos de datos posteriores para [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], en lugar de hacerlo con el controlador OLE DB para SQL Server. También significa que las características disponibles en la conexión se limitarán al conjunto de funciones de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Los intentos de utilizar nuevos tipos de datos o funciones se detectan lo más pronto posible en las llamadas API y se devuelven los errores a la aplicación que realiza la llamada, en lugar de intentar pasar las solicitudes no válidas al servidor.   


 GetKeywords siempre devolverá una lista de palabras clave que corresponde a la versión del servidor en la conexión y no se ve afectada por **DataTypeCompatibility**.  

|Tipo de datos|SQL Server Native Client<br /><br />Resultado de|SQL Server Native Client 11.0<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|Controlador OLE DB para SQL Server|Windows Data Access Components, MDAC y<br /><br /> Controlador OLE DB para las aplicaciones OLE DB de SQL Server con DataTypeCompatibility = 80|  
|---------------|--------------------------------------------------|-------------------------------------------------------------|-------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|  
|CLR UDT (\<= 8 Kb)|udt|udt|udt|Varbinary|  
|varbinary(max)|varbinary|varbinary|varbinary|imagen|  
|ntext|varchar|varchar|varchar|Texto|  
|nvarchar(max)|NVARCHAR|NVARCHAR|NVARCHAR|Ntext|  
|xml|xml|xml|xml|Ntext|  
|UDT de CLR (> 8 Kb)|varbinary|udt|udt|imagen|  
|Date|varchar|Date|Date|Varchar|  
|datetime2|varchar|datetime2|datetime2|Varchar|  
|datetimeoffset|varchar|datetimeoffset|datetimeoffset|Varchar|  
|time|varchar|time|time|Varchar|  

## <a name="see-also"></a>Vea también  
 [Controlador OLE DB para SQL Server](../oledb/oledb-driver-for-sql-server.md)   
 [Instalación del controlador OLE DB para SQL Server](../oledb/applications/installing-oledb-driver-for-sql-server.md)  
