---
title: Mediante la autenticación integrada | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- integrated authentication
ms.assetid: 9499ffdf-e0ee-4d3c-8bca-605371eb52d9
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c70de16565cd90c3ca594fffcbbcc82bae89b90e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32853180"
---
# <a name="using-integrated-authentication"></a>Uso de la autenticación integrada
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

El [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] en Linux y macOS admite las conexiones que usan Kerberos de autenticación integrada. Es compatible con el centro de distribución de claves (KDC) de Kerberos de MIT y funciona con las bibliotecas de v5 aplicación programa interfaz (GSSAPI) servicios de seguridad genérico y Kerberos.
  
## <a name="using-integrated-authentication-to-connect-to-includessnoversionincludesssnoversionmdmd-from-an-odbc-application"></a>Mediante la autenticación integrada para conectarse a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] desde una aplicación ODBC  

Puede habilitar la autenticación integrada de Kerberos mediante la especificación de **Trusted_Connection = yes** en la cadena de conexión de **SQLDriverConnect** o **SQLConnect**. Por ejemplo:  

```
Driver='ODBC Driver 13 for SQL Server';Server=your_server;Trusted_Connection=yes  
```
  
Cuando se conecta con un DSN, también puede agregar **Trusted_Connection = yes** a la entrada DSN en `odbc.ini`.
  
El `-E` opción de `sqlcmd` y `-T` opción de `bcp` también se puede utilizar para especificar la autenticación integrada; vea [conectar con **sqlcmd** ](../../../connect/odbc/linux-mac/connecting-with-sqlcmd.md) y [ Conectar con **bcp** ](../../../connect/odbc/linux-mac/connecting-with-bcp.md) para obtener más información.

Asegúrese de que la entidad de seguridad de cliente que se va a conectar a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] ya se ha autenticado con el KDC de Kerberos.
  
No se admiten**ServerSPN** ni **FailoverPartnerSPN** .  
  
## <a name="deploying-a-linux-or-macos-odbc-driver-application-designed-to-run-as-a-service"></a>Implementar un Linux o macOS ODBC Driver aplicación diseñada para ejecutarse como un servicio

Un administrador del sistema puede implementar una aplicación se ejecute como un servicio que usa la autenticación Kerberos para conectarse a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].  
  
Primero debe configurar Kerberos en el cliente y, a continuación, asegúrese de que la aplicación puede utilizar la credencial de Kerberos de la entidad de seguridad predeterminada.

Asegúrese de que usa `kinit` o PAM (módulo de autenticación acoplable) para obtener y almacenar en caché el TGT para la entidad de seguridad que usa la conexión, a través de uno de los métodos siguientes:  
  
-   Ejecutar `kinit`, pasando un nombre de entidad de seguridad y una contraseña.  
  
-   Ejecutar `kinit`, pasando un nombre de entidad de seguridad y la ubicación de un archivo keytab que contiene la clave de la entidad de seguridad creada con `ktutil`.  
  
-   Asegúrese de que se ha realizado el inicio de sesión en el sistema mediante el PAM (módulo de autenticación acoplable) de Kerberos.

Cuando una aplicación se ejecuta como un servicio, porque las credenciales de Kerberos caducan, renovar las credenciales para garantizar la disponibilidad continua del servicio. El controlador ODBC no renueva credenciales sí; Asegúrese de que hay un `cron` trabajo o el script que se ejecute periódicamente para renovar las credenciales antes de su caducidad. Para evitar que se solicite la contraseña para cada renovación, puede usar un archivo de tabla de claves.  
  
En este artículo sobre[el uso y la configuración de Kerberos](http://commons.oreilly.com/wiki/index.php/Linux_in_a_Windows_World/Centralized_Authentication_Tools/Kerberos_Configuration_and_Use) se ofrece información sobre las formas de aplicar la autenticación Kerberos a servicios en Linux.
  
## <a name="tracking-access-to-a-database"></a>Seguimiento del acceso a una base de datos

Un administrador de base de datos puede crear una traza de auditoría de acceso a una base de datos al utilizar cuentas del sistema para tener acceso a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] mediante la autenticación integrada.  
  
Iniciar una sesión en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] usa la cuenta del sistema y no hay ninguna funcionalidad en Linux para suplantar el contexto de seguridad. Por lo tanto, se requieren más acciones para determinar el usuario.
  
Para auditar las actividades de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] en nombre de los usuarios que no sea la cuenta del sistema, la aplicación debe utilizar [!INCLUDE[tsql](../../../includes/tsql_md.md)] **EXECUTE AS**.  
  
Para mejorar su rendimiento, las aplicaciones pueden utilizar la agrupación de conexiones con la autenticación integrada y la auditoría. Sin embargo, al combinar la agrupación de conexiones, la autenticación integrada y auditoría, crea un riesgo de seguridad porque permite que el Administrador de controladores unixODBC distintos usuarios reutilicen las conexiones agrupadas. Para obtener más información, consulte este artículo sobre la [agrupación de conexiones ODBC](http://www.unixodbc.org/doc/conn_pool.html).  

Antes de volver a utilizarlas, las aplicaciones deben restablecer las conexiones agrupadas ejecutando `sp_reset_connection`.  

## <a name="using-active-directory-to-manage-user-identities"></a>Uso de Active Directory para administrar identidades de usuario

Un administrador del sistema de aplicación no tiene que administrar conjuntos separados de credenciales de inicio de sesión para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]. Se puede configurar Active Directory como un centro de distribución de claves (KDC) para la autenticación integrada. Vea [Microsoft Kerberos](https://msdn.microsoft.com/en-us/library/windows/desktop/aa378747(v=vs.85).aspx) para obtener más información.

## <a name="using-linked-server-and-distributed-queries"></a>Uso de un servidor vinculado y consultas distribuidas

Los desarrolladores pueden implementar una aplicación que utilice un servidor vinculado o consultas distribuidas sin que haya un administrador de base de datos que mantenga conjuntos separados de credenciales de SQL. En esta situación, un desarrollador debe configurar una aplicación para usar la autenticación integrada:  
  
-   El usuario inicia sesión en un equipo cliente y se autentica en el servidor de aplicaciones.  
  
-   El servidor de aplicaciones se autentica como otra base de datos y se conecta a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] se autentica como un usuario de base de datos a otra base de datos ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].  
  
Tras configurar la autenticación integrada, las credenciales se transmiten al servidor vinculado.  
  
## <a name="integrated-authentication-and-sqlcmd"></a>Autenticación integrada y sqlcmd
Para tener acceso a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] utilizando la autenticación integrada, utilice la `-E` opción de `sqlcmd`. Asegúrese de que la cuenta que se ejecuta `sqlcmd` está asociado a la entidad de seguridad del cliente de Kerberos de forma predeterminada.

## <a name="integrated-authentication-and-bcp"></a>Autenticación integrada y bcp
Para tener acceso a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] utilizando la autenticación integrada, utilice la `-T` opción de `bcp`. Asegúrese de que la cuenta que se ejecuta `bcp` está asociado a la entidad de seguridad del cliente de Kerberos de forma predeterminada. 
  
Es un error utilizar `-T` con el `-U` o `-P` opción.
  
## <a name="supported-syntax-for-an-spn-registered-by-includessnoversionincludesssnoversionmdmd"></a>Sintaxis compatible con un SPN registrado por [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]

La sintaxis que usan los SPN en la cadena de conexión o atributos de conexión es como sigue:  

|Sintaxis|Description|  
|----------|---------------|  
|MSSQLSvc/*fqdn*:*port*|SPN predeterminado generado por el proveedor cuando se usa TCP. *puerto* en un número de puerto TCP. *fqdn* es un nombre de dominio completo.|  
  
## <a name="authenticating-a-linux-or-macos-computer-with-active-directory"></a>Autenticar un Linux o macOS equipo con Active Directory

Para configurar Kerberos, escriba datos en el `krb5.conf` archivo. `krb5.conf` se encuentra en `/etc/` pero puede hacer referencia a otro archivo utilizando la sintaxis p. ej. `export KRB5_CONFIG=/home/dbapp/etc/krb5.conf`. El siguiente es un ejemplo `krb5.conf` archivo:  
  
```  
[libdefaults]  
default_realm = YYYY.CORP.CONTOSO.COM  
dns_lookup_realm = false  
dns_lookup_kdc = true  
ticket_lifetime = 24h  
forwardable = yes  
  
[domain_realm]  
.yyyy.corp.contoso.com = YYYY.CORP.CONTOSO.COM  
.zzzz.corp.contoso.com = ZZZZ.CORP.CONTOSO.COM  
```  
  
Si el equipo Linux o Mac OS está configurado para usar el protocolo de configuración dinámica de Host (DHCP) con un servidor de DHCP de Windows que proporciona los servidores DNS que usa, puede usar **dns_lookup_kdc = true**. Ahora, puede utilizar Kerberos para iniciar sesión en su dominio emitiendo el comando `kinit alias@YYYY.CORP.CONTOSO.COM`. Parámetros pasados a `kinit` distinguen mayúsculas de minúsculas y la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] equipo configurado para estar en el dominio debe tener ese usuario `alias@YYYY.CORP.CONTOSO.COM` agregado para el inicio de sesión. Ahora, puede utilizar conexiones de confianza (**Trusted_Connection = YES** en una cadena de conexión, **bcp -T**, o **sqlcmd -E**).  
  
Deben cerrar el momento en el equipo Linux o Mac OS y el momento en el centro de distribución de claves (KDC) de Kerberos. Asegúrese de que la hora del sistema se establece correctamente, por ejemplo, mediante el protocolo de tiempo de red (NTP).  

Si se produce un error en la autenticación Kerberos, el controlador ODBC en Linux o Mac OS no utiliza la autenticación NTLM.  

Para obtener más información sobre la autenticación de equipos Linux o Mac OS con Active Directory, vea [autenticar clientes de Linux con Active Directory](http://technet.microsoft.com/magazine/2008.12.linux.aspx#id0060048) y [prácticas recomendadas para la integración de OS X con Active Directory](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf). Para obtener más información sobre la configuración de Kerberos, consulte el [documentación de Kerberos del MIT](https://web.mit.edu/kerberos/krb5-1.12/doc/index.html).

## <a name="see-also"></a>Vea también  
[Instrucciones de programación](../../../connect/odbc/linux-mac/programming-guidelines.md)

[Notas de la versión](../../../connect/odbc/linux-mac/release-notes.md)

[Con Azure Active Directory](../../../connect/odbc/using-azure-active-directory.md)
