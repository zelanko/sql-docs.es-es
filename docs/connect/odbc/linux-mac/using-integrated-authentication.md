---
title: Mediante la autenticación integrada | Microsoft Docs
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
ms.openlocfilehash: c37c170360e966e730b120601efd6867f2bb2659
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/16/2018
ms.locfileid: "42787112"
---
# <a name="using-integrated-authentication"></a>Uso de la autenticación integrada
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

[!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en Linux y macOS admite conexiones que usan la autenticación integrada de Kerberos. Es compatible con el centro de distribución de claves (KDC) de Kerberos del MIT y funciona con API de servicios de seguridad genéricos (GSSAPI) y bibliotecas de Kerberos v5.
  
## <a name="using-integrated-authentication-to-connect-to-includessnoversionincludesssnoversion-mdmd-from-an-odbc-application"></a>Uso de la autenticación integrada para conectarse a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] desde una aplicación ODBC  

Puede habilitar la autenticación integrada de Kerberos si especifica **Trusted_Connection = yes** en la cadena de conexión de **SQLDriverConnect** o **SQLConnect**. Por ejemplo:  

```
Driver='ODBC Driver 13 for SQL Server';Server=your_server;Trusted_Connection=yes  
```
  
Cuando se conecta con un DSN, también puede agregar **Trusted_Connection = yes** a la entrada DSN en `odbc.ini`.
  
El `-E` opción de `sqlcmd` y `-T` opción de `bcp` también puede utilizarse para especificar la autenticación integrada; vea [conectarse con **sqlcmd** ](../../../connect/odbc/linux-mac/connecting-with-sqlcmd.md) y [ Conectando con **bcp** ](../../../connect/odbc/linux-mac/connecting-with-bcp.md) para obtener más información.

Asegúrese de que el servidor principal de Linux que se va a conectar a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ya esté autenticado con el KDC de Kerberos.
  
No se admiten**ServerSPN** ni **FailoverPartnerSPN** .  
  
## <a name="deploying-a-linux-or-macos-odbc-driver-application-designed-to-run-as-a-service"></a>Implementación de un Linux o macOS ODBC Driver aplicación diseñada para ejecutarse como un servicio

Un administrador del sistema puede implementar una aplicación para que se ejecute como un servicio que usa la autenticación Kerberos para conectarse a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
Primero, debe configurar Kerberos en el cliente y, luego, asegurarse de que la aplicación puede usar la credencial Kerberos de la entidad de seguridad predeterminada.

Asegúrese de que usa `kinit` o PAM (módulo de autenticación acoplable) para obtener y almacenar en caché el TGT de la entidad de seguridad que usa la conexión, con uno de los siguientes métodos:  
  
-   Ejecute `kinit` y transmita el nombre y la contraseña de una entidad de seguridad.  
  
-   Ejecute `kinit` y transmita el nombre de una entidad de seguridad y una ubicación de un archivo keytab que contiene la clave de la entidad de seguridad, creada por `ktutil`.  
  
-   Asegúrese de que se ha realizado el inicio de sesión en el sistema mediante el PAM (módulo de autenticación acoplable) de Kerberos.

Cuando una aplicación se ejecuta como un servicio, puesto que las credenciales de Kerberos expiran por diseño, renueve las credenciales para garantizar la disponibilidad continua del servicio. El controlador ODBC no renovarse credenciales; Asegúrese de que hay un `cron` trabajo o un script que se ejecute periódicamente para renovar las credenciales antes de su caducidad. Para evitar la necesidad de la contraseña para cada renovación, puede usar un archivo keytab.  
  
En este artículo sobre[el uso y la configuración de Kerberos](http://commons.oreilly.com/wiki/index.php/Linux_in_a_Windows_World/Centralized_Authentication_Tools/Kerberos_Configuration_and_Use) se ofrece información sobre las formas de aplicar la autenticación Kerberos a servicios en Linux.
  
## <a name="tracking-access-to-a-database"></a>Seguimiento del acceso a una base de datos

Los administradores de bases de datos pueden crear una pista de auditoría del acceso a una base de datos cuando se usan cuentas del sistema para acceder a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mediante la autenticación integrada.  
  
Para iniciar sesión en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se usa la cuenta del sistema, y no existe ninguna función en Linux para suplantar el contexto de seguridad. Por lo tanto, se requieren más acciones para determinar el usuario.
  
Para auditar las actividades realizadas en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en nombre de usuarios distintos a la cuenta del sistema, la aplicación debe usar **EXECUTE AS** de [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
Para mejorar su rendimiento, las aplicaciones pueden utilizar la agrupación de conexiones con la autenticación integrada y la auditoría. Pero combinar la agrupación de conexiones, la autenticación integrada y la auditoría trae consigo un riesgo de seguridad, ya que el administrador de controladores unixODBC permite que distintos usuarios reutilicen las conexiones agrupadas. Para obtener más información, consulte este artículo sobre la [agrupación de conexiones ODBC](http://www.unixodbc.org/doc/conn_pool.html).  

Antes de permitir su reutilización, las aplicaciones deben restablecer las conexiones agrupadas al ejecutar `sp_reset_connection`.  

## <a name="using-active-directory-to-manage-user-identities"></a>Uso de Active Directory para administrar identidades de usuario

Los administradores del sistema de aplicaciones no necesitan administrar conjuntos separados de credenciales de inicio de sesión para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se puede configurar Active Directory como un centro de distribución de claves (KDC) para la autenticación integrada. Consulte [Microsoft Kerberos](/windows/desktop/SecAuthN/microsoft-kerberos) para obtener más información.

## <a name="using-linked-server-and-distributed-queries"></a>Uso de un servidor vinculado y consultas distribuidas

Los desarrolladores pueden implementar una aplicación que utilice un servidor vinculado o consultas distribuidas sin que haya un administrador de base de datos que mantenga conjuntos separados de credenciales de SQL. En estos casos, los desarrolladores deben configurar una aplicación para que use la autenticación integrada:  
  
-   El usuario inicia sesión en un equipo cliente y se autentica en el servidor de aplicaciones.  
  
-   El servidor de aplicaciones se autentica como una base de datos distinta y se conecta a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se autentica como un usuario de base de datos en otra base de datos ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]).  
  
Tras configurar la autenticación integrada, las credenciales se transmiten al servidor vinculado.  
  
## <a name="integrated-authentication-and-sqlcmd"></a>Autenticación integrada y sqlcmd
Para acceder a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mediante la autenticación integrada, use la opción `-E` de `sqlcmd`. Asegúrese de que la cuenta que se ejecuta `sqlcmd` está asociado a la entidad de seguridad de cliente de Kerberos de forma predeterminada.

## <a name="integrated-authentication-and-bcp"></a>Autenticación integrada y bcp
Para acceder a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mediante la autenticación integrada, use la opción `-T` de `bcp`. Asegúrese de que la cuenta que se ejecuta `bcp` está asociado a la entidad de seguridad de cliente de Kerberos de forma predeterminada. 
  
Es un error usar `-T` con el `-U` o `-P` opción.
  
## <a name="supported-syntax-for-an-spn-registered-by-includessnoversionincludesssnoversion-mdmd"></a>Sintaxis admitida para un SPN registrado por [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]

La sintaxis que usan los SPN en los atributos de cadena de conexión o atributos de conexión es la siguiente:  

|Sintaxis|Descripción|  
|----------|---------------|  
|MSSQLSvc/*fqdn*:*port*|SPN predeterminado generado por el proveedor cuando se usa TCP. *puerto* en un número de puerto TCP. *fqdn* es un nombre de dominio completo.|  
  
## <a name="authenticating-a-linux-or-macos-computer-with-active-directory"></a>Autenticación de un equipo Linux o macOS con Active Directory

Para configurar Kerberos, escribir datos en el `krb5.conf` archivo. `krb5.conf` se encuentra en `/etc/` pero puede hacer referencia a otro archivo con la sintaxis, por ejemplo, `export KRB5_CONFIG=/home/dbapp/etc/krb5.conf`. A continuación se muestra un archivo `krb5.conf` de ejemplo:  
  
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
  
Si el equipo Linux o macOS está configurado para utilizar el protocolo de configuración dinámica de Host (DHCP) con un servidor DHCP de Windows que proporciona a los servidores DNS para usar, puede usar **dns_lookup_kdc = true**. Ahora, puede usar Kerberos para iniciar sesión en su dominio con el comando `kinit alias@YYYY.CORP.CONTOSO.COM`. Los parámetros se pasan a `kinit` distinguen mayúsculas de minúsculas y la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] equipo configurado para estar en el dominio debe tener ese usuario `alias@YYYY.CORP.CONTOSO.COM` agregado para el inicio de sesión. Ahora puede usar conexiones de confianza (**Trusted_Connection=YES** en una cadena de conexión, **bcp -T** o **sqlcmd -E**).  
  
La hora en el equipo Linux o macOS y la hora en el centro de distribución de claves de Kerberos (KDC) deben ser parecidas. Asegúrese de que la hora del sistema esté configurada correctamente, por ejemplo, mediante el protocolo de tiempo de redes (NTP).  

Si se produce un error en la autenticación Kerberos, el controlador ODBC en Linux o macOS no usa la autenticación NTLM.  

Para obtener más información sobre la autenticación de equipos Linux o macOS con Active Directory, consulte [autenticar los clientes de Linux con Active Directory](http://technet.microsoft.com/magazine/2008.12.linux.aspx#id0060048) y [procedimientos recomendados para integrar OS X con Active Directory](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf). Para obtener más información sobre la configuración de Kerberos, consulte el [MIT Kerberos documentación](https://web.mit.edu/kerberos/krb5-1.12/doc/index.html).

## <a name="see-also"></a>Ver también  
[Instrucciones de programación](../../../connect/odbc/linux-mac/programming-guidelines.md)

[Notas de la versión](../../../connect/odbc/linux-mac/release-notes.md)

[Uso de Azure Active Directory](../../../connect/odbc/using-azure-active-directory.md)
