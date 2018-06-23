---
title: Utilizar el cifrado sin validación | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data access [SQL Server Native Client], encryption
- cryptography [SQL Server Native Client]
- SQLNCLI, encryption
- encryption [SQL Server Native Client]
- SQL Server Native Client, encryption
ms.assetid: f4c63206-80bb-4d31-84ae-ccfcd563effa
caps.latest.revision: 17
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: eda7a4e7ac9d6558301affc7d2b027c55bc1f7e7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36200528"
---
# <a name="using-encryption-without-validation"></a>Utilizar el cifrado sin validación
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cifra siempre los paquetes de red asociados al inicio de sesión. Si no se ha proporcionado ningún certificado en el servidor cuando este se inicia, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] genera un certificado autofirmado que se utiliza para cifrar los paquetes de inicio de sesión.  
  
 Las aplicaciones pueden solicitar también el cifrado de todo el tráfico de red mediante palabras clave de cadenas de conexión o propiedades de conexión. Las palabras clave son "Encrypt" para ODBC y OLE DB cuando se usa una cadena de proveedor con **IDBInitialize:: Initialize**, o "Use Encryption for Data" para ADO y OLE DB cuando se usa una cadena de inicialización con **IDataInitialize** . Esto también se puede configurar por [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager mediante la **Forzar cifrado de protocolo** opción. De forma predeterminada, el cifrado de todo el tráfico de red de una conexión requiere que se proporcione un certificado en el servidor.  
  
 Para obtener información sobre las palabras clave de cadena de conexión, vea [Using Connection String Keywords with SQL Server Native Client](../applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 Para habilitar el cifrado que se usará cuando no se ha proporcionado un certificado en el servidor, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager puede utilizarse para establecer el **Forzar cifrado de protocolo** y **confiar en certificado de servidor**  opciones. En ese caso, el cifrado utilizará un certificado de servidor autofirmado sin validación si no se ha proporcionado ningún certificado comprobable en el servidor.  
  
 Las aplicaciones también pueden utilizar la palabra clave "TrustServerCertificate" o su atributo de conexión asociado para garantizar que se realiza el cifrado. La configuración de las aplicaciones nunca reduce el nivel de seguridad establecido por el Administrador de configuración cliente de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], pero sí puede reforzarlo. Por ejemplo, si **Forzar cifrado de protocolo** no se ha establecido para el cliente, una aplicación puede solicitar cifrado en Sí. Para garantizar el cifrado incluso cuando no se ha proporcionado un certificado de servidor, una aplicación puede solicitar el cifrado y "TrustServerCertificate". Sin embargo, si "TrustServerCertificate" no está habilitado en la configuración del cliente, se requiere igualmente un certificado de servidor. En la tabla siguiente se describen todos los casos:  
  
|Cliente configurado con Forzar cifrado de protocolo|Cliente configurado con Confiar en certificado de servidor|Cadena/atributo de conexión Encrypt/Use Encryption for Data|Cadena/atributo de conexión Trust Server Certificate|Resultado|  
|----------------------------------------------|---------------------------------------------|------------------------------------------------------------------------------|----------------------------------------------------------------------|------------|  
|no|N/D|No (valor predeterminado)|Pasa por alto|No se produce el cifrado.|  
|no|N/D|Sí|No (valor predeterminado)|El cifrado solamente se produce si hay un certificado de servidor comprobable; de lo contrario, se produce un error en el intento de conexión.|  
|no|N/D|Sí|Sí|El cifrado se produce siempre, pero puede que se utilice un certificado de servidor autofirmado.|  
|Sí|no|Pasa por alto|Pasa por alto|El cifrado solamente se produce si hay un certificado de servidor comprobable; de lo contrario, se produce un error en el intento de conexión.|  
|Sí|Sí|No (valor predeterminado)|Pasa por alto|El cifrado se produce siempre, pero puede que se utilice un certificado de servidor autofirmado.|  
|Sí|Sí|Sí|No (valor predeterminado)|El cifrado solamente se produce si hay un certificado de servidor comprobable; de lo contrario, se produce un error en el intento de conexión.|  
|Sí|Sí|Sí|Sí|Siempre se produce cifrado, pero puede usar un certificado de servidor autofirmado.|  
  
## <a name="sql-server-native-client-ole-db-provider"></a>Proveedor OLE DB de SQL Server Native Client  
 El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client admite el cifrado sin validación mediante la adición de la propiedad de inicialización de SSPROP_INIT_TRUST_SERVER_CERTIFICATE datos origen, que se implementa en el conjunto de propiedades DBPROPSET_SQLSERVERDBINIT conjunto. Además, una conexión nueva palabra clave de cadena, "TrustServerCertificate", tal y como se ha agregado. Acepta valores sí o no; no es el valor predeterminado. Cuando se utilizan componentes de servicio, acepta valores true o false; false es el valor predeterminado.  
  
 Para obtener más información acerca de las mejoras realizadas en el conjunto de propiedades DBPROPSET_SQLSERVERDBINIT, vea [propiedades de inicialización y autorización](../../native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md).  
  
## <a name="sql-server-native-client-odbc-driver"></a>Controlador ODBC de SQL Server Native Client  
 El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC Native Client admite el cifrado sin validación mediante la incorporación del [SQLSetConnectAttr](../../native-client-odbc-api/sqlsetconnectattr.md) y [SQLGetConnectAttr](../../native-client-odbc-api/sqlgetconnectattr.md) funciones. SQL_COPT_SS_TRUST_SERVER_CERTIFICATE se ha agregado para aceptar SQL_TRUST_SERVER_CERTIFICATE_YES o SQL_TRUST_SERVER_CERTIFICATE_NO, siendo SQL_TRUST_SERVER_CERTIFICATE_NO el valor predeterminado. Además, se ha agregado una nueva palabra clave de cadena de conexión, "TrustServerCertificate". Acepta valores sí o no; "no" es el valor predeterminado.  
  
## <a name="see-also"></a>Vea también  
 [Características de SQL Server Native Client](sql-server-native-client-features.md)  
  
  