---
title: Nombres de entidad de seguridad de servicio (SPN) en conexiones de cliente (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: e212010e-a5b6-4ad1-a3c0-575327d3ffd3
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 62073e1618d4ab43acbbfbaad1fb6e2ff16c7658
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62631703"
---
# <a name="service-principal-names-spns-in-client-connections-ole-db"></a>Nombres de entidad de seguridad del servicio (SPN) en conexiones cliente (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  En este tema se describen propiedades y funciones miembro de OLE DB compatibles con los nombres principales de servicio (SPN) en aplicaciones cliente. Para más información sobre los SPN en las aplicaciones cliente, vea [Compatibilidad con Nombre de la entidad de seguridad del servicio &#40;SPN&#41; en conexiones de cliente](../../../relational-databases/native-client/features/service-principal-name-spn-support-in-client-connections.md). Para obtener un ejemplo, vea [autenticación integrada de Kerberos &#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-how-to/integrated-kerberos-authentication-ole-db.md).  
  
## <a name="provider-initialization-string-keywords"></a>Palabras clave de cadena de inicialización de proveedor  
 Las siguientes palabras clave de cadena de inicialización de proveedor admiten SPN en aplicaciones OLE DB. En la tabla siguiente, los valores de la columna de palabra clave se usan para la cadena del proveedor de IDBInitialize::Initialize. Los valores de la columna de descripción se usan en cadenas de inicialización al conectar con ADO o IDataInitialize::GetDataSource.  
  
|Palabra clave|Descripción|Valor|  
|-------------|-----------------|-----------|  
|ServerSPN|Dirección SPN del servidor|SPN del servidor. El valor predeterminado es una cadena vacía, que hace que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client use el valor predeterminado, SPN generado por proveedor.|  
|FailoverPartnerSPN|SPN de asociado de conmutación por error|SPN del asociado de conmutación por error. El valor predeterminado es una cadena vacía, que hace que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client use el valor predeterminado, SPN generado por proveedor.|  
  
## <a name="data-source-initialization-properties"></a>Propiedades de inicialización de origen de datos  
 Las siguientes propiedades en el **DBPROPSET_SQLSERVERDBINIT** conjunto de propiedades permiten a las aplicaciones especificar SPN.  
  
|Name|Tipo|Uso|  
|----------|----------|-----------|  
|SSPROP_INIT_SERVERSPN|VT_BSTR, lectura/escritura|Especifica el SPN del servidor. El valor predeterminado es una cadena vacía, que hace que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client use el valor predeterminado, SPN generado por proveedor.|  
|SSPROP_INIT_FAILOVERPARTNERSPN|VT_BSTR, lectura/escritura|Especifica el SPN para el asociado de conmutación por error. El valor predeterminado es una cadena vacía, que hace que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client use el valor predeterminado, SPN generado por proveedor.|  
  
## <a name="data-source-properties"></a>Propiedades de origen de datos  
 Las siguientes propiedades en el **DBPROPSET_SQLSERVERDATASOURCEINFO** conjunto de propiedades permiten que las aplicaciones detectar el método de autenticación.  
  
|Nombre|Tipo|Uso|  
|----------|----------|-----------|  
|SSPROP_INTEGRATEDAUTHENTICATIONMETHOD|VT_BSTR, solo lectura|Devuelve el método de autenticación que utiliza la conexión. El valor devuelto a la aplicación es el valor que Windows devuelve a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Estos son los valores posibles: <br />"NTLM", que se devuelve cuando una conexión se abre mediante la autenticación NTLM.<br />"Kerberos", que se devuelve cuando una conexión se abre mediante la autenticación Kerberos.<br /><br /> Si se ha abierto una conexión y no se puede determinar el método de autenticación, se devuelve VT_EMPTY.<br /><br /> Esta propiedad solo se puede leer cuando se ha inicializado un origen de datos. Si intenta leer la propiedad antes de que se haya inicializado un origen de datos, IDBProperties::GetProperies devolverá DB_S_ERRORSOCCURRED o DB_E_ERRORSOCCURRED, según corresponda, y DBPROPSTATUS_NOTSUPPORTED se establecerá en DBPROPSET_PROPERTIESINERROR para esta propiedad. Este comportamiento está de acuerdo con la especificación básica de OLE DB.|  
|SSPROP_MUTUALLYAUTHENICATED|VT_BOOL, solo lectura|Devuelve VARIANT_TRUE si los servidores de la conexión se autenticaron mutuamente; de lo contrario, devuelve VARIANT_FALSE.<br /><br /> Esta propiedad solo se puede leer cuando se ha inicializado un origen de datos. Si hay un intento de leer la propiedad antes de que se haya inicializado un origen de datos, IDBProperties::GetProperies devolverá DB_S_ERRORSOCCURRED o DB_E_ERRORSOCCURRED, según corresponda, y DBPROPSTATUS_NOTSUPPORTED se establecerá en DBPROPSET_PROPERTIESINERROR para esta propiedad. Este comportamiento está de acuerdo con la especificación básica de OLE DB<br /><br /> Si este atributo se consulta para una conexión que no usó la autenticación de Windows, se devuelve VARIANT_FALSE.|  
  
## <a name="ole-db-api-support-for-spns"></a>Compatibilidad de API OLE DB con SPN  
 La tabla siguiente describe las funciones del miembro OLE DB que admiten SPN en conexiones de cliente:  
  
|Función de miembro|Descripción|  
|---------------------|-----------------|  
|IDataInitialize::GetDataSource|*pwszInitializationString* puede contener las nuevas palabras clave **ServerSPN** y **FailoverPartnerSPN**.|  
|IDataInitialize::GetInitializationString|Si SSPROP_INIT_SERVERSPN y SSPROP_INIT_FAILOVERPARTNERSPN tienen valores no predeterminados, se incluirán en la cadena de inicialización mediante *ppwszInitString* como valores de palabra clave para **ServerSPN** y **FailoverPartnerSPN**. De lo contrario, estas palabras clave no estarán incluidas en la cadena de inicialización.|  
|IDBInitialize::Initialize|Si están habilitados los mensajes configurando DBPROP_INIT_PROMPT en las propiedades de inicialización de origen de datos, se mostrará el cuadro de diálogo Inicio de sesión de OLE DB. Esto permite escribir SPN tanto para el servidor principal como para su asociado de conmutación por error.<br /><br /> La cadena de proveedor de DPPROP_INIT_PROVIDERSTRING, si se establece, reconoce las nuevas palabras clave **ServerSPN** y **FailoverPartnerSPN** y usa sus valores, si están presentes, para inicializar SSPROP_INIT_SERVER_SPN y SSPROP_INIT_FAILOVER_PARTNER_SPN.<br /><br /> IDBProperties:: SetProperties se puede llamar para establecer las propiedades SSPROP_INIT_SERVER_SPN y SSPROP_INIT_FAILOVER_PARTNER_SPN antes de llamar a IDBInitialize:: Initialize. Ésta es una alternativa a utilizar una cadena de proveedor.<br /><br /> Si una propiedad se establece en más de un lugar, un valor establecido mediante programación tiene precedencia sobre un conjunto de valores en la cadena de proveedor. Un conjunto de valores en una cadena de inicialización tiene precedencia sobre un conjunto de valores en un cuadro de diálogo de inicio de sesión.<br /><br /> Si la misma palabra clave aparece más de una vez en la cadena del proveedor, el valor de primera aparición tiene prioridad.|  
|IDBProperties::GetProperties|Se puede llamar a IDBProperties::GetProperties para obtener los valores de las nuevas propiedades de inicialización de origen de datos SSPROP_INIT_SERVERSPN y SSPROP_INIT_FAILOVERPARTNERSPN y de las nuevas propiedades de origen de datos SSPROP_AUTHENTICATIONMETHOD y SSPROP_MUTUALLYAUTHENTICATED.|  
|IDBProperties::GetPropertyInfo|IdbProperties::GetPropertyInfo incluirá las nuevas propiedades de inicialización de origen de datos SSPROP_INIT_SERVERSPN y SSPROP_INIT_FAILOVERPARTNERSPN, o bien las nuevas propiedades de origen de datos SSPROP_AUTHENTICATION_METHOD y SSPROP_MUTUALLYAUTHENTICATED.|  
|IDBProperties::SetProperties|Se puede llamar a IDBProperties::SetProperties para establecer los valores de las nuevas propiedades de inicialización de origen de datos SSPROP_INITSERVERSPN y SSPROP_INIT_FAILOVERPARTNERSPN.<br /><br /> Estas propiedades se pueden establecer en cualquier momento, pero si el origen de datos ya está abierto, se devolverá el error siguiente: DB_E_ERRORSOCCURRED, "operación de varios pasos de OLE DB generó errores. Compruebe los valores de estado de OLE DB si es posible. No se realizó ningún trabajo."|  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Native Client &#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
