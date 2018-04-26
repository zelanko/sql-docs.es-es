---
title: Cifrado de las conexiones a SQL Server en Linux | Documentos de Microsoft
description: Este artículo describe cifrar conexiones a SQL Server en Linux.
author: tmullaney
ms.date: 01/30/2018
ms.author: meetb
manager: craigg
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: ''
helpviewer_keywords:
- Linux, encrypted connections
ms.workload: Inactive
ms.openlocfilehash: b60ded8bde38413ccc2818efd2ca3852d88f235c
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="encrypting-connections-to-sql-server-on-linux"></a>Cifrado de las conexiones a SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en Linux puede usar seguridad de capa de transporte (TLS) para cifrar los datos transmitidos a través de una red entre una aplicación cliente y una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] es compatible con los mismos protocolos TLS en Windows y Linux: TLS 1.0, 1.1 y 1.2. Sin embargo, son específicos del sistema operativo en el que los pasos para configurar TLS [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] está ejecutando.  

## <a name="requirements-for-certificates"></a>Requisitos de los certificados 
Antes de comenzar, debe asegurarse de que los certificados cumplen estos requisitos:
- Debe ser la hora actual del sistema después de la fecha válido desde propiedad del certificado y antes de la fecha válido para la propiedad del certificado.
- El certificado debe estar destinado a la autenticación del servidor. Esto requiere la propiedad de uso mejorado de clave del certificado para especificar la autenticación de servidor (1.3.6.1.5.5.7.3.1).
- El certificado debe crearse mediante la opción KeySpec de AT_KEYEXCHANGE. Normalmente, la propiedad de uso de la clave del certificado (KEY_USAGE) también incluye cifrado de clave (CERT_KEY_ENCIPHERMENT_KEY_USAGE).
- La propiedad de asunto del certificado debe indicar que el nombre común (CN) es el mismo que el nombre de host o nombre de dominio completo (FQDN) del equipo del servidor. Nota: se admiten certificados comodín. 

## <a name="overview"></a>Información general
TLS se utiliza para cifrar las conexiones desde una aplicación cliente para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Cuando se configura correctamente, TLS proporciona privacidad y la integridad de datos para las comunicaciones entre el cliente y el servidor.  Conexiones TLS pueden ser iniciado por el cliente o servidor iniciada. 


## <a name="client-initiated-encryption"></a>Cifrado iniciada por el cliente 
- **Generar certificado** (/ CN debe coincidir con el nombre de dominio completo del host de SQL Server)

> [!NOTE]
> En este ejemplo se utiliza un certificado autofirmado, esto no debe usarse para escenarios de producción. Debe utilizar los certificados de entidad emisora de certificados. 

        openssl req -x509 -nodes -newkey rsa:2048 -subj '/CN=mssql.contoso.com' -keyout mssql.key -out mssql.pem -days 365 
        sudo chown mssql:mssql mssql.pem mssql.key 
        sudo chmod 600 mssql.pem mssql.key   
        sudo mv mssql.pem /etc/ssl/certs/ 
        sudo mv mssql.key /etc/ssl/private/ 

- **Configurar SQL Server**

        systemctl stop mssql-server 
        cat /var/opt/mssql/mssql.conf 
        sudo /opt/mssql/bin/mssql-conf set network.tlscert /etc/ssl/certs/mssqlfqdn.pem 
        sudo /opt/mssql/bin/mssql-conf set network.tlskey /etc/ssl/private/mssqlfqdn.key 
        sudo /opt/mssql/bin/mssql-conf set network.tlsprotocols 1.2 
        sudo /opt/mssql/bin/mssql-conf set network.forceencryption 0 

- **Registrar el certificado en el equipo cliente (Windows, Linux o Mac OS)**

    -   Si utilizas un certificado firmado de CA, tendrá que copiar el certificado de entidad de certificación (CA) en lugar del certificado de usuario en el equipo cliente. 
    -   Si está utilizando el certificado autofirmado, copie el archivo PEM en las siguientes carpetas correspondientes a la distribución y ejecutar los comandos para habilitarlos 
        - **Ubuntu**: certificado de copia para ```/usr/share/ca-certificates/``` rename extensión .crt use certificados de ca dpkg reconfigure para habilitarlo como certificado de entidad emisora de certificados del sistema. 
        - **RHEL**: certificado de copia a ```/etc/pki/ca-trust/source/anchors/``` usar ```update-ca-trust``` para habilitarlo como certificado de entidad emisora de certificados del sistema.
        - **SUSE**: certificado de copia a ```/usr/share/pki/trust/anchors/``` usar ```update-ca-certificates``` para habilitarlo como certificado de entidad emisora de certificados del sistema.
        - **Windows**: importar el archivo PEM como un certificado de usuario actual -> entidades de certificación raíz -> certificados de confianza
        - **macOS**: 
           - Copie el certificado para ```/usr/local/etc/openssl/certs```
           - Ejecute el siguiente comando para obtener el valor de hash: ```/usr/local/Cellar/openssql/1.0.2l/openssql x509 -hash -in mssql.pem -noout```
           - Cambiar el nombre de la unidad cert en valor. Por ejemplo: ```mv mssql.pem dc2dd900.0```. Asegúrese de que dc2dd900.0 está en ```/usr/local/etc/openssl/certs```
    
-   **Ejemplos de cadena de conexión** 

    - **[!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)]**   
  ![Cuadro de diálogo de conexión de SSMS](media/sql-server-linux-encrypted-connections/ssms-encrypt-connection.png "cuadro de diálogo de conexión de SSMS")  
  
    - **SQLCMD** 

            sqlcmd  -S <sqlhostname> -N -U sa -P '<YourPassword>' 
    - **ADO.NET** 

            "Encrypt=True; TrustServerCertificate=False;" 
    - **ODBC** 

            "Encrypt=Yes; TrustServerCertificate=no;" 
    - **JDBC** 
    
            "encrypt=true; trustServerCertificate=false;" 

## <a name="server-initiated-encryption"></a>Server inició cifrado 

- **Generar certificado** (/ CN debe coincidir con el nombre de dominio completo del host de SQL Server)
        
        openssl req -x509 -nodes -newkey rsa:2048 -subj '/CN=mssql.contoso.com' -keyout mssql.key -out mssql.pem -days 365 
        sudo chown mssql:mssql mssql.pem mssql.key 
        sudo chmod 600 mssql.pem mssql.key   
        sudo mv mssql.pem /etc/ssl/certs/ 
        sudo mv mssql.key /etc/ssl/private/ 

- **Configurar SQL Server**

        systemctl stop mssql-server 
        cat /var/opt/mssql/mssql.conf 
        sudo /opt/mssql/bin/mssql-conf set network.tlscert /etc/ssl/certs/mssqlfqdn.pem 
        sudo /opt/mssql/bin/mssql-conf set network.tlskey /etc/ssl/private/mssqlfqdn.key 
        sudo /opt/mssql/bin/mssql-conf set network.tlsprotocols 1.2 
        sudo /opt/mssql/bin/mssql-conf set network.forceencryption 1 
        
-   **Ejemplos de cadena de conexión** 

    - **SQLCMD**

            sqlcmd  -S <sqlhostname> -U sa -P '<YourPassword>' 
    - **ADO.NET** 

            "Encrypt=False; TrustServerCertificate=False;" 
    - **ODBC** 

            "Encrypt=no; TrustServerCertificate=no;"  
    - **JDBC** 
    
            "encrypt=false; trustServerCertificate=false;" 
            
> [!NOTE]
> Establecer **TrustServerCertificate** en True si el cliente no puede conectarse a la entidad emisora de certificados para validar la autenticidad de la unidad cert

## <a name="common-connection-errors"></a>Errores de conexión comunes  

|Mensaje de error |Fix |
|--- |--- |
|La cadena de certificado fue emitida por una entidad que no es de confianza.  |Este error se produce cuando los clientes no pueden comprobar la firma en el certificado presentado por SQL Server durante el protocolo de enlace TLS. Asegúrese de que el cliente confíe en el [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] directamente el certificado o la entidad de certificación que firmó el certificado de SQL Server. |
|El nombre principal de destino es incorrecto.  |Asegúrese de que el campo de nombre común en el certificado del servidor de SQL coincide con el nombre del servidor especificado en la cadena de conexión del cliente. |  
|El host remoto forzó el cierre una conexión existente. |Este error puede producirse cuando el cliente no es compatible con la versión del protocolo TLS requerida SQL Server. Por ejemplo, si [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] está configurado para requerir TLS 1.2, asegúrese de que los clientes también admiten el protocolo TLS 1.2. |
| | |   
