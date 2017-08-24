---
title: Cifrado de las conexiones a SQL Server en Linux | Documentos de Microsoft
description: Este tema describe cifrar conexiones a SQL Server en Linux.
author: tmullaney
ms.date: 06/14/2017
ms.author: thmullan;rickbyh
manager: jhubbard
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 
helpviewer_keywords:
- Linux, encrypted connections
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: dfbfeee8292f3af4020185248d3d6a3fad3c71ea
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="encrypting-connections-to-sql-server-on-linux"></a>Cifrado de las conexiones a SQL Server en Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../../docs/includes/tsql-appliesto-sslinux-only.md)]

[!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)]en Linux puede usar seguridad de capa de transporte (TLS) para cifrar los datos transmitidos a través de una red entre una aplicación cliente y una instancia de [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)]. [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)]es compatible con los mismos protocolos TLS en Windows y Linux: TLS 1.0, 1.1 y 1.2. Sin embargo, son específicos del sistema operativo en el que los pasos para configurar TLS [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] está ejecutando.  
 
## <a name="typical-scenario"></a>Escenario típico 
TLS se utiliza para cifrar las conexiones desde una aplicación cliente para [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)]. Cuando se configura correctamente, TLS proporciona privacidad y la integridad de datos para las comunicaciones entre el cliente y el servidor.  
Los siguientes pasos describen un escenario típico:  

1. Administrador de base de datos genera una clave privada y un certificado (CSR) de solicitud de firma. Nombre común del CSR debe coincidir con el nombre del servidor que los clientes que se especifican en su cadena de conexión de SQL Server. Este nombre común suele ser el nombre de dominio completo de la [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] host. Para usar el mismo certificado para varios servidores, puede usar un carácter comodín en el nombre común (por ejemplo, `"*.contoso.com"` en lugar de `"node1.contoso.com"`).   
2. El CSR se envía a una entidad de certificación (CA) para la firma. La CA debe ser de confianza para todos los equipos cliente que se conectan a [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)]. La entidad de certificación devuelve un certificado de firma para el Administrador de base de datos.   
3. Configura el Administrador de base de datos [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] para utilizar la clave privada y el certificado de firma para conexiones TLS.   
4. Los clientes especificar `"Encrypt=True"` y `"TrustServerCertificate=False"` en sus cadenas de conexión. (Los nombres de parámetro concreto pueden ser diferentes en función de qué controlador se está usando). Clientes ahora intento cifrar las conexiones a SQL Server y compruebe la validez del certificado de SQL Server para evitar ataques de man-in-the-middle.  
 
## <a name="configuring-tls-on-linux"></a>Configuración de TLS en Linux  

Use `mssql-conf` para configurar TLS para una instancia de [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] ejecutan en Linux. Se admiten las siguientes opciones:  

|Opción |Description |
|--- |--- |
|`network.forceencryption` |Si es 1, a continuación, [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] obliga a todas las conexiones que se cifren. De forma predeterminada, esta opción es 0. |  
|`network.tlscert` |Archivo de la ruta de acceso absoluta para el certificado que [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] utiliza para TLS. Ejemplo: `/etc/ssl/certs/mssql.pem` el archivo de certificado debe ser accesible para la cuenta de mssql. Microsoft recomienda restringir el acceso al archivo mediante `chown mssql:mssql <file>; chmod 400 <file>`. |  
|`network.tlskey` |Archivo de la ruta de acceso absoluta a la clave privada que [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] utiliza para TLS. Ejemplo: `/etc/ssl/private/mssql.key` el archivo de certificado debe ser accesible para la cuenta de mssql. Microsoft recomienda restringir el acceso al archivo mediante `chown mssql:mssql <file>; chmod 400 <file>`. | 
|`network.tlsprotocols` |Una lista separada por comas de las TLS protocolos se admiten en SQL Server. [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)]siempre intenta negociar el protocolo permitido más fuerte. Si un cliente no es compatible con cualquier protocolo permitido, [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] rechazará el intento de conexión.  Para la compatibilidad, se permiten todos los protocolos admitidos de forma predeterminada (1.2, 1.1, 1.0).  Si los clientes admiten TLS 1.2, Microsoft recomienda que permite solo TLS 1.2. |  
|`network.tlsciphers` |Especifica los cifrados permitidos por [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] para TLS. Esta cadena debe tener el formato por [formato de lista de cifrado de OpenSSL](https://www.openssl.org/docs/man1.0.2/apps/ciphers.html). En general, no es necesario cambiar esta opción. <br /> De forma predeterminada, se permiten los cifrados siguientes: <br /> `ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128-SHA:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA` |   
| | |
 
## <a name="example"></a>Ejemplo 
Este ejemplo utiliza un certificado autofirmado. En escenarios de producción normal, el certificado podría estar firmado por una entidad de certificación que sea de confianza para todos los clientes.  
 
### <a name="step-1-generate-private-key-and-certificate"></a>Paso 1: Generar el certificado y clave privada 
Abra un comando terminal en el equipo Linux donde [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] está ejecutando. Ejecute los siguientes comandos:  

- Generar un certificado autofirmado. Asegúrese de que la/CN coincide con el nombre de dominio completo del host de SQL Server. También puede usar caracteres comodín, por ejemplo `'/CN=*.contoso.com'`.    
   ```  
   openssl req -x509 -nodes -newkey rsa:2048 -subj '/CN=mssql.contoso.com' -keyout mssql.key -out mssql.pem -days 365 
   ```  

- Restringir el acceso a`mssql`  
   ```  
   sudo chown mssql:mssql mssql.pem mssql.key 
   sudo chmod 400 mssql.pem mssql.key 
   ```  
 
- Mover a los directorios del sistema de SSL (opcionales)  
   ```  
   sudo mv mssql.pem /etc/ssl/certs/ 
   sudo mv mssql.key /etc/ssl/private/ 
   ```  
 
### <a name="step-2-configure--includessnoversiondocsincludesssnoversion-mdmd"></a>Paso 2: configurar[!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)]  
Usar `mssql-conf` configurar [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] para utilizar el certificado y la clave de TLS. Para mayor seguridad, también puede establecer TLS 1.2 como el único protocolo permitido y forzar a todos los clientes a usar conexiones cifradas.  

```  
sudo /opt/mssql/bin/mssql-conf set network.tlscert /etc/ssl/certs/mssql.pem 
sudo /opt/mssql/bin/mssql-conf set network.tlskey /etc/ssl/private/mssql.key 
sudo /opt/mssql/bin/mssql-conf set network.tlsprotocols 1.2 
sudo /opt/mssql/bin/mssql-conf set network.forceencryption 1 
```
 
### <a name="step-3-restart-includessnoversiondocsincludesssnoversion-mdmd"></a>Paso 3: reiniciar[!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] 
[!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)]debe reiniciarse para que estos cambios surtan efecto.  
`sudo systemctl restart mssql-server`  
 
### <a name="step-4-copy-self-signed-certificate-to-client-machines"></a>Paso 4: Copiar el certificado autofirmado a equipos cliente 
Dado que este ejemplo utiliza un certificado autofirmado por el [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] host, el certificado (no la clave privada) se debe copiar e instalar como un certificado raíz de confianza en todos los equipos cliente que se conectan a [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)]. Si el certificado está firmado por una CA que ya es de confianza para todos los clientes, este paso no es necesario. 
 
### <a name="step-5-connect-from-clients-using-tls"></a>Paso 5: Conectarse desde los clientes que usan TLS 
Conectarse a [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] desde un cliente con el cifrado habilitado y `TrustServerCertificate` establecido en `False` en la cadena de conexión. Estos son algunos ejemplos de cómo especificar estos parámetros mediante controladores y herramientas diferentes. 

sqlcmd  
`sqlcmd -N -C -S mssql.contoso.com -U sa -P '<YourPassword>'`  

[!INCLUDE[ssmanstudiofull-md](../../docs/includes/ssmanstudiofull-md.md)]   
  ![Cuadro de diálogo de conexión de SSMS](media/sql-server-linux-encrypted-connections/ssms-encrypt-connection.png "cuadro de diálogo de conexión de SSMS")  
  
ADO.NET  
`"Encrypt=true; TrustServerCertificate=true;"`  

ODBC   
`"Encrypt=yes; TrustServerCertificate=no;"`  

JDBC  
`"encrypt=true; trustServerCertificate=false;" `

 
## <a name="common-connection-errors"></a>Errores de conexión comunes  

|Mensaje de error |Fix |
|--- |--- |
|La cadena de certificado fue emitida por una entidad que no es de confianza.  |Este error se produce cuando los clientes no pueden comprobar la firma en el certificado presentado por SQL Server durante el protocolo de enlace TLS. Asegúrese de que el cliente confíe en el [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] directamente el certificado o la entidad de certificación que firmó el certificado de SQL Server. |
|El nombre principal de destino es incorrecto.  |Asegúrese de que el campo de nombre común en el certificado del servidor de SQL coincide con el nombre del servidor especificado en la cadena de conexión del cliente. |  
|El host remoto forzó el cierre una conexión existente. |Este error puede producirse cuando el cliente no es compatible con la versión del protocolo TLS requerida SQL Server. Por ejemplo, si [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] está configurado para requerir TLS 1.2, asegúrese de que los clientes también admiten el protocolo TLS 1.2. |
| | |   


