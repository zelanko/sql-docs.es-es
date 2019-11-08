---
title: Requisitos del sistema para SQL Server Native Client | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- system requirements [SQL Server Native Client]
- data access [SQL Server Native Client], system requirements
- SQL Server Native Client, system requirements
- SQLNCLI, system requirements
ms.assetid: 1c8e2f8a-a440-44da-8e3a-af632d34c52c
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e130b89b877f0f2b0cc1edb732008c8520c9347b
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/07/2019
ms.locfileid: "73758337"
---
# <a name="system-requirements-for-sql-server-native-client"></a>Requisitos del sistema para SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Para utilizar las características de acceso a datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como MARS, debe tener instalado el software siguiente:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client en su cliente.  
  
-   Una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en su servidor.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client requiere Windows Installer 3.0. Windows Installer 3.0 ya está instalado en los sistemas operativos [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. Para el resto de plataformas necesita instalarlo explícitamente. Para obtener más información, vea [Windows Installer 3,0 Redistributable](https://www.microsoft.com/download/details.aspx?id=16821).  
  
> [!NOTE]  
>  Asegúrese de que inicia sesión con privilegios de administrador antes de instalar este software.  
  
## <a name="operating-system-requirements"></a>Requisitos de sistema operativo  
 Para obtener una lista de sistemas operativos compatibles con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, consulte [directivas de soporte técnico para SQL Server Native Client](../../relational-databases/native-client/applications/support-policies-for-sql-server-native-client.md).  
  
## <a name="sql-server-requirements"></a>Requisitos de SQL Server  
 Para utilizar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client para tener acceso a los datos en las bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], debe tener instalada una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] admite las conexiones de todas las versiones de MDAC, Componentes de Windows Data Access y todas las versiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Cuando una versión del cliente anterior se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], los tipos de datos del servidor que el cliente no conoce se asignan a tipos que son compatibles con la versión del cliente. Para obtener más información, vea Compatibilidad de tipo de datos para versiones del cliente, más adelante en este tema.  
  
## <a name="cross-language-requirements"></a>Requisitos de idiomas  
 La versión en inglés de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client es compatible con todas las versiones traducidas de los sistemas operativos admitidos. Las versiones traducidas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Cliente son compatibles con sistemas operativos traducidos que estén en el mismo idioma que la versión traducida de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Las versiones traducidas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client también se admite en las versiones en inglés de los sistemas operativos compatibles siempre que se instale la configuración de idioma correspondiente.  
  
 Para actualizaciones:  
  
-   Las versiones en inglés de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client se pueden actualizar a cualquier versión traducida de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
-   Las versiones traducidas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client se pueden actualizar a cualquier versión traducida de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client en el mismo idioma.  
  
-   Las versiones traducidas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client se pueden actualizar a la versión en inglés de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
-   Las versiones traducidas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client no se pueden actualizar a las versiones traducidas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client en un idioma distinto.  
  
## <a name="data-type-compatibility-for-client-versions"></a>Compatibilidad de tipo de datos para las versiones del cliente  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client asignan los nuevos tipos de datos a los tipos de datos anteriores que son compatibles con clientes de nivel inferior, como se muestra en la tabla siguiente.  
  
 Las aplicaciones OLE DB y ADO pueden utilizar la palabra clave de la cadena de conexión **DataTypeCompatibility** con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client para trabajar con tipos de datos más antiguos. Cuando **DataTypeCompatibility=80**, los clientes de OLE DB se conectarán con la versión de flujo TDS de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], en lugar de la versión de TDS. Esto significa que el servidor realizará la conversión de nivel inferior y los tipos de datos posteriores para [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], en lugar de a través de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. También significa que las características disponibles en la conexión se limitarán al conjunto de funciones de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Los intentos de utilizar nuevos tipos de datos o funciones se detectan lo más pronto posible en las llamadas API y se devuelven los errores a la aplicación que realiza la llamada, en lugar de intentar pasar las solicitudes no válidas al servidor.  
  
 No hay ningún control **DataTypeCompatibility** para ODBC.  
  
 IDBInfo:: GetKeywords siempre devolverá una lista de palabras clave que corresponde a la versión del servidor en la conexión y no se ve afectada por **DataTypeCompatibility**.  
  
|Tipo de datos|SQL Server Native Client<br /><br /> Resultado de|SQL Server Native Client 11.0<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|Windows Data Access Components, MDAC y<br /><br /> aplicaciones OLE DB de SQL Server Native Client con DataTypeCompatibility=80|  
|---------------|--------------------------------------------------|-------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|  
|CLR UDT (\<= 8Kb)|udt|Udt|Varbinary|  
|varbinary(max)|varbinary|varbinary|Imagen|  
|varchar(max)|varchar|varchar|Texto|  
|nvarchar(max)|nvarchar|nvarchar|Ntext|  
|XML|XML|XML|Ntext|  
|UDT CLR (> 8 KB)|udt|varbinary|Imagen|  
|date|date|varchar|Varchar|  
|datetime2|datetime2|varchar|Varchar|  
|datetimeoffset|datetimeoffset|varchar|Varchar|  
|time|time|varchar|Varchar|  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Native Client programación](../../relational-databases/native-client/sql-server-native-client-programming.md)   
 [Instalar SQL Server Native Client](../../relational-databases/native-client/applications/installing-sql-server-native-client.md)  
  
  
