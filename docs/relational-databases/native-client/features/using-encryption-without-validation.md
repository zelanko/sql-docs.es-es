---
title: Utilizar el cifrado sin validación | Microsoft Docs
ms.custom: ''
ms.date: 12/21/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data access [SQL Server Native Client], encryption
- cryptography [SQL Server Native Client]
- SQLNCLI, encryption
- encryption [SQL Server Native Client]
- SQL Server Native Client, encryption
ms.assetid: f4c63206-80bb-4d31-84ae-ccfcd563effa
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: a8e991c2287ba946e8e53b040655b603c4bd5553
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39533055"
---
# <a name="using-encryption-without-validation"></a>Utilizar el cifrado sin validación
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cifra siempre los paquetes de red asociados al inicio de sesión. Si no se ha proporcionado ningún certificado en el servidor cuando este se inicia, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] genera un certificado autofirmado que se utiliza para cifrar los paquetes de inicio de sesión.  

Los certificados autofirmados no garantiza la seguridad. El protocolo de enlace cifrado se basa en NT LAN Manager (NTLM). Se recomienda que aprovisione un certificado que se pueda comprobar en SQL Server para la conectividad segura. Capa de seguridad de transporte (TLS) puede estar seguro sólo con validación del certificado.

Las aplicaciones pueden solicitar también el cifrado de todo el tráfico de red mediante palabras clave de cadenas de conexión o propiedades de conexión. Las palabras clave son "Encrypt" para ODBC y OLE DB cuando se usa una cadena de proveedor con **IDBInitialize:: Initialize**, o "Use Encryption for Data" para ADO y OLE DB cuando se usa una cadena de inicialización con **IDataInitialize** . También puede configurarse por [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager mediante la **Forzar cifrado de protocolo** opción y el cliente para que solicite conexiones cifradas mediante la configuración. De forma predeterminada, el cifrado de todo el tráfico de red de una conexión requiere que se proporcione un certificado en el servidor. Al configurar el cliente para confiar en el certificado en el servidor, puede volverse vulnerable a ataques man-in-the-middle. Si implementa un certificado que se pueda comprobar en el servidor, asegúrese de que cambia la configuración del cliente sobre el certificado de confianza en FALSE.

Para obtener información sobre las palabras clave de cadena de conexión, vea [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 Para permitir usar el cifrado cuando no se ha proporcionado un certificado en el servidor, se puede usar el Administrador de configuración de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para establecer las opciones **Forzar cifrado de protocolo** y **Confiar en certificado de servidor**. En ese caso, el cifrado utilizará un certificado de servidor autofirmado sin validación si no se ha proporcionado ningún certificado comprobable en el servidor.  
  
 Las aplicaciones también pueden utilizar la palabra clave "TrustServerCertificate" o su atributo de conexión asociado para garantizar que se realiza el cifrado. La configuración de las aplicaciones nunca reduce el nivel de seguridad establecido por el Administrador de configuración cliente de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], pero sí puede reforzarlo. Por ejemplo, si **Forzar cifrado de protocolo** no está establecido para el cliente, una aplicación puede solicitar su propio cifrado. Para garantizar el cifrado incluso cuando no se ha proporcionado un certificado de servidor, una aplicación puede solicitar el cifrado y "TrustServerCertificate". Sin embargo, si "TrustServerCertificate" no está habilitado en la configuración del cliente, se requiere igualmente un certificado de servidor. En la tabla siguiente se describen todos los casos:  
  
|Cliente configurado con Forzar cifrado de protocolo|Cliente configurado con Confiar en certificado de servidor|Cadena/atributo de conexión Encrypt/Use Encryption for Data|Cadena/atributo de conexión Trust Server Certificate|Resultado|  
|----------------------------------------------|---------------------------------------------|------------------------------------------------------------------------------|----------------------------------------------------------------------|------------|  
|no|N/D|No (valor predeterminado)|Omitido|No se produce el cifrado.|  
|no|N/D|Sí|No (valor predeterminado)|El cifrado solamente se produce si hay un certificado de servidor comprobable; de lo contrario, se produce un error en el intento de conexión.|  
|no|N/D|Sí|Sí|El cifrado se produce siempre, pero puede que se utilice un certificado de servidor autofirmado.|  
|Sí|no|Omitido|Omitido|El cifrado solamente se produce si hay un certificado de servidor comprobable; de lo contrario, se produce un error en el intento de conexión.|  
|Sí|Sí|No (valor predeterminado)|Omitido|El cifrado se produce siempre, pero puede que se utilice un certificado de servidor autofirmado.|  
|Sí|Sí|Sí|No (valor predeterminado)|El cifrado solamente se produce si hay un certificado de servidor comprobable; de lo contrario, se produce un error en el intento de conexión.|  
|Sí|Sí|Sí|Sí|El cifrado se produce siempre, pero es posible que se use un certificado de servidor autofirmado.|  
||||||

> [!CAUTION]
> La tabla anterior sólo proporciona a una guía en el comportamiento del sistema en configuraciones diferentes. Para la conectividad segura, asegúrese de que el cliente y servidor requieren cifrado. También asegúrese de que el servidor tiene un certificado que se pueda comprobar y que la **TrustServerCertificate** configuración en el cliente está establecido en FALSE.

## <a name="sql-server-native-client-ole-db-provider"></a>Proveedor OLE DB de SQL Server Native Client  
 El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client admite el cifrado sin validación mediante la adición de la propiedad de inicialización de SSPROP_INIT_TRUST_SERVER_CERTIFICATE data source, que se implementa en el conjunto de propiedades DBPROPSET_SQLSERVERDBINIT conjunto. Además, se ha agregado una nueva palabra clave de cadena de conexión, "TrustServerCertificate". Acepta valores sí o no; no es el valor predeterminado. Cuando se utilizan componentes de servicio, acepta valores true o false; false es el valor predeterminado.  
  
 Para obtener más información acerca de las mejoras realizadas en el conjunto de propiedades DBPROPSET_SQLSERVERDBINIT, vea [propiedades de inicialización y autorización](../../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md).  
  
## <a name="sql-server-native-client-odbc-driver"></a>Controlador ODBC de SQL Server Native Client  
 El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client admite el cifrado sin validación mediante la incorporación del [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) y [SQLGetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md) funciones. SQL_COPT_SS_TRUST_SERVER_CERTIFICATE se ha agregado para aceptar SQL_TRUST_SERVER_CERTIFICATE_YES o SQL_TRUST_SERVER_CERTIFICATE_NO, siendo SQL_TRUST_SERVER_CERTIFICATE_NO el valor predeterminado. Además, se ha agregado una nueva palabra clave de cadena de conexión, "TrustServerCertificate". Acepta valores sí o no; "no" es el valor predeterminado.  
  
## <a name="see-also"></a>Vea también  
 [Características de SQL Server Native Client](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
