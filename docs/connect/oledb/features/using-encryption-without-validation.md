---
title: Utilizar el cifrado sin validación | Documentos de Microsoft
description: Utilizar el cifrado sin validación
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], encryption
- cryptography [OLE DB Driver for SQL Server]
- MSOLEDBSQL, encryption
- encryption [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, encryption
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 96e33a0dfdb301c9088d37d6b33460b8c453c1b2
ms.sourcegitcommit: 354ed9c8fac7014adb0d752518a91d8c86cdce81
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/14/2018
ms.locfileid: "35612340"
---
# <a name="using-encryption-without-validation"></a>Utilizar el cifrado sin validación
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cifra siempre los paquetes de red asociados al inicio de sesión. Si no se ha proporcionado ningún certificado en el servidor cuando este se inicia, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] genera un certificado autofirmado que se utiliza para cifrar los paquetes de inicio de sesión.  

Los certificados autofirmados no garantizan la seguridad. El protocolo de enlace cifrado se basa en NT LAN Manager (NTLM). Se recomienda encarecidamente que aprovisionar un certificado comprobable en SQL Server para una conexión segura. Capa de seguridad de transporte (TLS) puede estar seguro únicamente con la validación de certificados.

Las aplicaciones pueden solicitar también el cifrado de todo el tráfico de red mediante palabras clave de cadenas de conexión o propiedades de conexión. Las palabras clave son "Encrypt" para OLE DB cuando se usa una cadena de proveedor con **IDBInitialize:: Initialize**, o "Use Encryption for Data" para ADO y OLE DB cuando se usa una cadena de inicialización con **IDataInitialize**. Esto también se puede configurar por [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager mediante la **Forzar cifrado de protocolo** opción y la configuración en el cliente para que solicite conexiones cifradas. De forma predeterminada, el cifrado de todo el tráfico de red de una conexión requiere que se proporcione un certificado en el servidor. Estableciendo el cliente para confiar en el certificado en el servidor, pueden ser vulnerables a ataques de man-in-the-middle. Si implementa un certificado comprobable en el servidor, asegúrese de que cambia la configuración del cliente sobre el certificado de confianza en FALSE.

Para obtener información sobre las palabras clave de cadena de conexión, vea [Using Connection String Keywords con controlador OLE DB para SQL Server](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md ).  
  
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
||||||

> [!CAUTION]
> La tabla anterior solo proporciona a una guía en el comportamiento del sistema en diferentes configuraciones. Para una conexión segura, asegúrese de que el cliente y el servidor requieren cifrado. Asegúrese también de que el servidor tiene un certificado comprobable y que la **TrustServerCertificate** configuración en el cliente se establece en FALSE.

## <a name="ole-db-driver-for-sql-server"></a>Controlador OLE DB para SQL Server 
 El controlador OLE DB para SQL Server admite el cifrado sin validación mediante la adición de la propiedad de inicialización de SSPROP_INIT_TRUST_SERVER_CERTIFICATE datos origen, que se implementa en el conjunto de propiedades DBPROPSET_SQLSERVERDBINIT. Además, una conexión nueva palabra clave de cadena, "TrustServerCertificate", tal y como se ha agregado. Acepta valores sí o no; no es el valor predeterminado. Cuando se utilizan componentes de servicio, acepta valores true o false; false es el valor predeterminado.  
  
 Para obtener más información acerca de las mejoras realizadas en el conjunto de propiedades DBPROPSET_SQLSERVERDBINIT, vea [propiedades de inicialización y autorización](../../oledb/ole-db-data-source-objects/initialization-and-authorization-properties.md).  

  
## <a name="see-also"></a>Vea también  
 [Controlador OLE DB para las características de SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md)  
  
  
