---
title: Requisitos del sistema para el controlador OLE DB para SQL Server | Documentos de Microsoft
description: Requisitos para el controlador OLE DB para SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- system requirements [OLE DB Driver for SQL Server]
- data access [OLE DB Driver for SQL Server], system requirements
- OLE DB Driver for SQL Server, system requirements
- MSOLEDBSQL, system requirements
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5169c841784230d1ad4d99472dd636a490c750ce
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2018
---
# <a name="system-requirements-for-ole-db-driver-for-sql-server"></a>Requisitos del sistema para el controlador OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Para utilizar las características de acceso a datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como MARS, debe tener instalado el software siguiente:  

-   Controlador OLE DB para SQL Server en el cliente.  

-   Una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en su servidor.   

> [!NOTE]  
>  Asegúrese de que inicia sesión con privilegios de administrador antes de instalar este software.  

## <a name="operating-system-requirements"></a>Requisitos de sistema operativo  
 Para obtener una lista de sistemas operativos que admiten el controlador OLE DB para SQL Server, vea [admite directivas para el controlador OLE DB para SQL Server](../oledb/applications/support-policies-for-oledb-driver-for-sql-server.md).  

## <a name="sql-server-requirements"></a>Requisitos de SQL Server  
 Para usar el controlador OLE DB para SQL Server para obtener acceso a datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bases de datos, debe tener una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalado.  

 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] admite conexiones de todas las versiones de MDAC, Windows Data Access Components y todas las versiones de controlador de OLE DB para SQL Server. Cuando una versión del cliente anterior se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], los tipos de datos del servidor que el cliente no conoce se asignan a tipos que son compatibles con la versión del cliente. Para obtener más información, vea Compatibilidad de tipo de datos para versiones del cliente, más adelante en este tema.  

## <a name="cross-language-requirements"></a>Requisitos de idiomas  
 La versión en inglés de controlador OLE DB para SQL Server se admite en todas las versiones localizadas de sistemas operativos compatibles. Las versiones localizadas de controlador OLE DB para SQL Server se admiten en sistemas operativos localizados que estén en el mismo idioma como el localizado controlador OLE DB para la versión de SQL Server. Las versiones localizadas de controlador OLE DB para SQL Server también se admiten en las versiones en inglés de sistemas operativos compatibles siempre y cuando se instala la configuración de idioma correspondiente.  

 Para actualizaciones:  

-   Las versiones en inglés de controlador OLE DB para SQL Server pueden actualizarse a cualquier versión traducida de controlador de OLE DB para SQL Server.  

-   Las versiones localizadas de controlador OLE DB para SQL Server pueden actualizarse a versiones localizadas del controlador de OLE DB para SQL Server del mismo idioma.  

-   Versión localizada del controlador de OLE DB para SQL Server puede actualizarse a la versión en inglés de controlador de OLE DB para SQL Server.  

-   Las versiones localizadas de controlador OLE DB para SQL Server no puede actualizarse a localizado controlador OLE DB para las versiones de SQL Server de un idioma diferente.  

## <a name="data-type-compatibility-for-client-versions"></a>Compatibilidad de tipo de datos para las versiones del cliente  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y el controlador OLE DB para SQL Server mapa nuevos tipos de datos a tipos de datos más antiguos que son compatibles con clientes de nivel inferior, tal como se muestra en la tabla siguiente.  

 Aplicaciones OLE DB y ADO pueden utilizar el **DataTypeCompatibility** palabra clave de cadena de conexión con el controlador OLE DB para SQL Server para que funcione con los tipos de datos más antiguos. Cuando **DataTypeCompatibility = 80**, los clientes de OLE DB se conectarán mediante el [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] versión (TDS), en lugar de la versión TDS de flujo de datos tabulares. Esto significa que para [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y tipos de datos más adelante, conversión de nivel inferior se realizará por el servidor, en lugar de por el controlador OLE DB para SQL Server. También significa que las características disponibles en la conexión se limitarán al conjunto de funciones de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Los intentos de utilizar nuevos tipos de datos o funciones se detectan lo más pronto posible en las llamadas API y se devuelven los errores a la aplicación que realiza la llamada, en lugar de intentar pasar las solicitudes no válidas al servidor.   


 GetKeywords siempre devolverá una lista de palabras clave que corresponde a la versión del servidor en la conexión y no se ve afectada por **DataTypeCompatibility**.  

|Tipo de datos|Controlador OLE DB para SQL Server<br /><br />SQL Server 2005|SQL Server Native Client 11.0<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|Controlador OLE DB para SQL Server|Windows Data Access Components, MDAC y<br /><br /> Controlador de OLE DB para las aplicaciones de OLE DB de SQL Server con DataTypeCompatibility = 80|  
|---------------|--------------------------------------------------|-------------------------------------------------------------|-------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|  
|UDT de CLR (\<= 8 Kb)|udt|Udt|Udt|Varbinary|  
|varbinary(max)|varbinary|varbinary|varbinary|imagen|  
|ntext|varchar|varchar|varchar|Texto|  
|nvarchar(max)|nvarchar|nvarchar|nvarchar|Ntext|  
|xml|xml|xml|xml|Ntext|  
|CLR UDT (> 8Kb)|udt|varbinary|varbinary|imagen|  
|date|date|varchar|varchar|Varchar|  
|datetime2|datetime2|varchar|varchar|Varchar|  
|datetimeoffset|datetimeoffset|varchar|varchar|Varchar|  
|time|time|varchar|varchar|Varchar|  

## <a name="see-also"></a>Vea también  
 [Controlador OLE DB para la programación de SQL Server](../oledb/oledb-driver-for-sql-server-programming.md)   
 [Instalación del controlador OLE DB para SQL Server](../oledb/applications/installing-oledb-driver-for-sql-server.md)  
