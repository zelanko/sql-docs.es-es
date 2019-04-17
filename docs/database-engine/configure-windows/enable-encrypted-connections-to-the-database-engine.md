---
title: Habilitar conexiones cifradas en el motor de base de datos | Microsoft Docs
ms.custom: ''
ms.date: 04/09/2019
ms.prod: sql
ms.prod_service: security
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- connections [SQL Server], encrypted
- SSL [SQL Server]
- Secure Sockets Layer (SSL)
- encryption [SQL Server], connections
- cryptography [SQL Server], connections
- certificates [SQL Server], installing
- requesting encrypted connections
- installing certificates
- security [SQL Server], encryption
ms.assetid: e1e55519-97ec-4404-81ef-881da3b42006
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 28a2c9bd527fb4996730630a6121d205fbaebf04
ms.sourcegitcommit: 5f38c1806d7577f69d2c49e66f06055cc1b315f1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/09/2019
ms.locfileid: "59429351"
---
# <a name="enable-encrypted-connections-to-the-database-engine"></a>Habilitar conexiones cifradas en el motor de base de datos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  En este tema se describe cómo habilitar conexiones cifradas para una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] mediante la especificación de un certificado para el [!INCLUDE[ssDE](../../includes/ssde-md.md)] utilizando el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . El equipo servidor debe tener un certificado y el equipo cliente debe estar configurado para confiar en la entidad de certificación raíz del certificado. La puesta en servicio es el proceso de instalar un certificado mediante su importación en Windows.  
  
 El certificado debe estar emitido para la **Autenticación de servidor**. El nombre del certificado debe ser el nombre de dominio completo (FQDN) del equipo.  
  
 Los certificados se almacenan localmente para los usuarios del equipo. Para instalar un certificado para usarlo con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], debe ejecutar el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con una cuenta que tenga privilegios de administrador local.

 El cliente debe ser capaz de comprobar la propiedad del certificado utilizado por el servidor. Si el cliente tiene el certificado de clave pública de la entidad de certificación que firmó el certificado del servidor, no es necesario realizar una mayor configuración. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows incluye los certificados de clave pública de muchas entidades de certificación. Si el certificado del servidor lo firmó una entidad de certificación pública o privada para la que el cliente no tiene certificado de clave pública, debe instalar el certificado de clave pública de esta entidad de certificación.  
  
> [!NOTE]  
> Si desea utilizar el cifrado con un clúster de conmutación por error, debe instalar el certificado del servidor con el nombre DNS completo del servidor virtual en todos los nodos del clúster de conmutación por error. Por ejemplo, si tiene un clúster con dos nodos cuyos nombres son test1.*\<su empresa>*.com y test2.*\<su empresa>*.com y un servidor virtual llamado virtsql, deberá instalar un certificado para virtsql.*\<su empresa>*.com en ambos nodos. El valor de la opción **ForceEncryption** se puede establecer en **Sí**.

> [!NOTE]
> Al crear conexiones cifradas para un indexador de Azure Search en SQL Server en una máquina virtual de Azure, consulte [Configuración de una conexión desde un indexador de Azure Search a SQL Server en una máquina virtual de Azure](https://azure.microsoft.com/documentation/articles/search-howto-connecting-azure-sql-iaas-to-azure-search-using-indexers/). 

## <a name="certificate-requirements"></a>Requisitos de certificado

Para que SQL Server cargue un certificado SSL, el certificado debe cumplir las condiciones siguientes:

- El certificado debe estar en un almacén de certificados del equipo local o en el almacén de certificados del usuario actual.
- La cuenta de servicio de SQL Server debe tener el permiso necesario para acceder al certificado SSL.
- La hora actual del sistema debe ser posterior al valor de la propiedad **Válido desde** del certificado y anterior a la propiedad Válido hasta del certificado.
- El certificado debe estar destinado a la autenticación del servidor. Para esto es necesario que la propiedad **Uso mejorado de clave** del certificado para especificar **Autenticación del servidor (1.3.6.1.5.5.7.3.1)**.
- El certificado se debe crear mediante la opción **KeySpec** de **AT_KEYEXCHANGE**. Por lo general, la propiedad de uso de clave del certificado (**KEY_USAGE**) incluye también el cifrado de clave (**CERT_KEY_ENCIPHERMENT_KEY_USAGE**).
- La propiedad **Asunto** del certificado debe indicar que el nombre común (CN) es el mismo que el nombre del host o nombre de dominio completo (FQDN) del servidor. Si SQL Server se ejecuta en un clúster de conmutación por error, el nombre común debe coincidir con el del host o FQDN del servidor virtual y los certificados deben estar en todos los nodos del clúster de conmutación por error.
- SQL Server 2008 R2 y SQL Server 2008 R2 Native Client admiten los certificados comodín. Es posible que otros clientes no admitan los certificados comodín. Para más información, consulte la documentación del cliente y [KB258858](http://support.microsoft.com/kb/258858).

## <a name="to-provision-install-a-certificate-on-the-server"></a>Para proporcionar (instalar) un certificado en el servidor  

> [!NOTE]
> Vea [Administración de certificados (Administrador de configuración de SQL Server)](manage-certificates.md) para agregar un certificado en un único servidor.
  
1. En el menú **Inicio** , haga clic en **Ejecutar**; en el cuadro **Abrir** , escriba **MMC** y haga clic en **Aceptar**.  
  
2. En el menú **Archivo** de la consola MMC, haga clic en **Agregar o quitar complemento**.  
  
3. En el cuadro de diálogo **Agregar o quitar complemento** , haga clic en **Agregar**.  
  
4. En el cuadro de diálogo **Agregar un complemento independiente** , haga clic en **Certificados**y, después, en **Agregar**.  
  
5. En el cuadro de diálogo **Complemento de certificados** , haga clic en **Cuenta de equipo**y, después, en **Finalizar**.  
  
6. En el cuadro de diálogo **Agregar un complemento independiente** , haga clic en **Cerrar.**  
  
7. En el cuadro de diálogo **Agregar o quitar complemento** , haga clic en **Aceptar**.  
  
8. En el complemento **Certificados** , expanda **Certificados**, expanda **Personal**. Tras ello, haga clic con el botón derecho en **Certificados**, seleccione **Todas las tareas**y, finalmente, haga clic en **Importar**.  

9. Haga clic con el botón derecho en el certificado importado, seleccione **Todas las tareas**y, luego, haga clic en **Administrar claves privadas**. En el cuadro de diálogo **Seguridad** , agregue el permiso de lectura para la cuenta de usuario que la cuenta de servicio de SQL Server usa.  
  
10. Finalice el **Asistente para importación de certificados**para agregar un certificado al equipo y cierre la consola MMC. Para obtener más información acerca de cómo agregar un certificado a un equipo, vea la documentación de Windows.  
  
## <a name="to-provision-install-a-certificate-across-multiple-servers"></a>Para aprovisionar (instalar) un certificado en varios servidores

> [!NOTE]
> Vea [Administración de certificados (Administrador de configuración de SQL Server)](manage-certificates.md) para agregar un certificado en varios servidores.

## <a name="to-export-the-server-certificate"></a>Para exportar el certificado del servidor  
  
1. En el complemento **Certificados** , busque el certificado en la carpeta **Certificados** / **Personal** , haga clic con el botón secundario en **Certificado**, seleccione **Todas las tareas**y, a continuación, en **Exportar**.  
  
2. Complete el **Asistente para exportación de certificados**y guarde el archivo del certificado en una ubicación adecuada.  
  
## <a name="to-configure-the-server-to-force-encrypted-connections"></a>Para configurar el servidor para forzar conexiones cifradas  
  
1. En **Administrador de configuración de SQL Server**, expanda **Configuración de red de SQL Server**, haga clic con el botón derecho en **Protocolos de** _\<instancia de servidor>_ y, después, seleccione **Propiedades**.  
  
2. En el cuadro de diálogo **Protocolos de** _\<nombre de instancia>_ **Propiedades**, en la pestaña **Certificado**, seleccione el certificado que quiera en el menú desplegable del cuadro **Certificado** y, después, haga clic en **Aceptar**.  
  
3. En la pestaña **Marcas** , en el cuadro **ForceEncryption** , seleccione **Sí**y, a continuación, haga clic en **Aceptar** para cerrar el cuadro de diálogo.  
  
4. Reinicie el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  

> [!NOTE]
> Para garantizar que la conectividad entre el cliente y el servidor es segura, configure el cliente para que solicite conexiones cifradas. Se explican más detalles [más adelante en este artículo](#to-configure-the-client-to-request-encrypted-connections).

### <a name="wildcard-certificates"></a>Certificados comodín

A partir de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client admiten los certificados comodín. Es posible que otros clientes no admitan los certificados comodín. Para más información, vea la documentación del cliente. El certificado comodín no se puede seleccionar con el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para usar un certificado comodín, debe editar la clave del Registro `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQLServer\SuperSocketNetLib` y escribir la huella digital del certificado, sin espacios en blanco, en el valor **Certificado**.  

> [!WARNING]  
> [!INCLUDE[ssnoteregistry_md](../../includes/ssnoteregistry-md.md)]  

## <a name="to-configure-the-client-to-request-encrypted-connections"></a>Para configurar el cliente de modo que solicite conexiones cifradas  

1. Copie el certificado original o el archivo del certificado exportado en el equipo cliente.  
  
2. En el equipo cliente, use el complemento **Certificados** para instalar el certificado raíz o el archivo del certificado exportado.  
  
3. En el panel de la consola, haga clic con el botón derecho en **Configuración de SQL Server Native Client**y, después, haga clic en **Propiedades**.  
  
4. En la página **Marcas** , en el cuadro **Forzar cifrado de protocolo** , haga clic en **Sí**.  
  
## <a name="to-encrypt-a-connection-from-sql-server-management-studio"></a>Para cifrar una conexión desde SQL Server Management Studio  
  
1. En la barra de herramientas del Explorador de objetos, haga clic en **Conectar**y, a continuación, en **Motor de base de datos**.  
  
2. En el cuadro de diálogo **Conectar al servidor** , rellene la información de conexión y, a continuación, haga clic en **Opciones**.  
  
3. En la pestaña **Propiedades de conexión** , haga clic en **Cifrar conexión**.  
  
## <a name="see-also"></a>Consulte también

[Soporte de TLS 1.2 para Microsoft SQL Server](https://support.microsoft.com/kb/3135244)