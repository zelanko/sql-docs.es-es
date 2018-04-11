---
title: Prácticas recomendadas de seguridad con bases de datos independientes | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: databases
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- contained database, threats
ms.assetid: 026ca5fc-95da-46b6-b882-fa20f765b51d
caps.latest.revision: 14
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c18410a29b500b3fd4fadfac987b1e94503ec7bb
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/10/2018
---
# <a name="security-best-practices-with-contained-databases"></a>Prácticas recomendadas de seguridad con bases de datos independientes
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Las bases de datos independientes tienen algunas amenazas únicas que los administradores de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] deben comprender y mitigar. La mayoría de ellas están relacionadas con el proceso de autenticación de **USER WITH PASSWORD** , que traslada el límite de autenticación del nivel de [!INCLUDE[ssDE](../../includes/ssde-md.md)] al de base de datos.  
  
## <a name="threats-related-to-users"></a>Amenazas relacionadas con usuarios  
 Los usuarios de una base de datos independiente que dispongan del permiso **ALTER ANY USER** , como los miembros de los roles fijos de base de datos **db_owner** y **db_securityadmin** , pueden conceder acceso a la base de datos sin el conocimiento ni el permiso del administrador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . La concesión de acceso a usuarios en una base de datos independiente incrementa el área expuesta al ataque potencial en toda la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Los administradores deben comprender esta delegación de control de acceso y ser sumamente cuidadosos cuando conceden el permiso **ALTER ANY USER** a los usuarios de base de datos independiente. Todos los propietarios de bases de datos tienen el permiso **ALTER ANY USER** . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deben auditar periódicamente a los usuarios de una base de datos independiente.  
  
### <a name="accessing-other-databases-using-the-guest-account"></a>Acceder a otras bases de datos mediante la cuenta Invitado  
 Los propietarios y los usuarios de bases de datos con el permiso **ALTER ANY USER** pueden crear usuarios de bases de datos independientes. Después de conectarse a una base de datos independiente en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], un usuario de base de datos independiente puede obtener acceso a otras bases de datos en [!INCLUDE[ssDE](../../includes/ssde-md.md)], si en estas bases de datos se ha habilitado la cuenta **Invitado** .  
  
### <a name="creating-a-duplicate-user-in-another-database"></a>Crear un usuario duplicado en otra base de datos  
 Algunas aplicaciones pueden solicitar que un usuario tenga acceso a más de una base de datos. Se puede hacer creando usuarios de bases de datos independientes idénticos en cada base de datos. Use la opción SID al crear el segundo usuario con contraseña. En el ejemplo siguiente se crean dos usuarios idénticos en dos bases de datos.  
  
```  
USE DB1;  
GO  
CREATE USER Carlo WITH PASSWORD = '<strong password>';   
-- Return the SID of the user  
SELECT SID FROM sys.database_principals WHERE name = 'Carlo';  
  
-- Change to the second database  
USE DB2;  
GO  
CREATE USER Carlo WITH PASSWORD = '<same password>', SID = <SID from DB1>;  
GO  
```  
  
 Para ejecutar una consulta entre bases de datos, debe establecer la opción **TRUSTWORTHY** en la base de datos que realiza la llamada. Por ejemplo, si el usuario (Carlo) definido anteriormente está en DB1, para ejecutar `SELECT * FROM db2.dbo.Table1;` el valor de **TRUSTWORTHY** debe estar activado para la base de datos DB1. Ejecute el código siguiente para activar la configuración **TRUSTWORTHY** .  
  
```  
ALTER DATABASE DB1 SET TRUSTWORTHY ON;  
```  
  
### <a name="creating-a-user-that-duplicates-a-login"></a>Crear un usuario que duplica un inicio de sesión  
 Si se crea un usuario de base de datos independiente con contraseña, con el mismo nombre que un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y si el inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se conecta especificando la base de datos independiente como el catálogo inicial, el inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no podrá conectarse. La conexión se evaluará como el usuario de base de datos independiente con entidad de seguridad con contraseña en la base de datos independiente en vez de como usuario basado en el inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Esto podría ocasionar una denegación de servicio intencional o accidental para el inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Como práctica recomendada, los miembros del rol fijo de servidor **sysadmin** siempre deben considerar realizar la conexión sin usar la opción de catálogo inicial. De esta forma, se conecta el inicio de sesión a la base de datos maestra y se evita que un propietario de base de datos use incorrectamente el intento de inicio de sesión. Después, el administrador puede cambiar a la base de datos independiente con la instrucción **USE***\<basededatos>*. Además, puede establecer la base de datos predeterminada del inicio de sesión en la base de datos independiente, que completa el inicio de sesión en la base de datos **maestra**y, a continuación, transfiere el inicio de sesión a la base de datos independiente.  
  
-   Como práctica recomendada, no cree usuarios de bases de datos independientes con contraseñas que tengan el mismo nombre que los inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Si existe el inicio de sesión duplicado, conéctese a la base de datos **maestra** sin especificar ningún catálogo inicial y, a continuación, ejecute el comando **USE** para cambiar a la base de datos independiente.  
  
-   Cuando estén presentes bases de datos independientes, los usuarios de base de datos que no sean bases de datos independientes deben conectarse al [!INCLUDE[ssDE](../../includes/ssde-md.md)] sin usar ningún catálogo inicial ni especificar el nombre de una base de datos dependiente como el catálogo inicial. De esta forma, se evita la conexión a la base de datos independiente bajo un control menos directo por parte de los administradores de [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
### <a name="increasing-access-by-changing-the-containment-status-of-a-database"></a>Incrementar el acceso cambiando el estado de contención de una base de datos  
 Los inicios de sesión con el permiso **ALTER ANY DATABASE** , como los miembros del rol fijo de servidor **dbcreator** , y los usuarios de una base de datos dependiente con el permiso **CONTROL DATABASE** , como los miembros del rol fijo de base de datos **db_owner** , pueden cambiar la configuración de contención de una base de datos. Si la configuración de contención de una base de datos se cambia de **NONE** a **PARTIAL** o **FULL**, se puede conceder acceso de usuario mediante la creación de usuarios de bases de datos independientes con contraseñas. De esta forma, se podría proporcionar acceso sin el conocimiento ni el consentimiento de los administradores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para evitar que las bases de datos sean independientes, establezca el valor de la opción **autenticación de la base de datos independiente** de [!INCLUDE[ssDE](../../includes/ssde-md.md)] en 0. Para evitar que se conecten los usuarios de bases de datos independientes con contraseñas en las bases de datos independientes seleccionadas, use desencadenadores de inicio de sesión para cancelar los intentos de inicios de sesión de los usuarios de bases de datos independientes con contraseñas.  
  
### <a name="attaching-a-contained-database"></a>Adjuntar una base de datos independiente  
 Si se adjunta una base de datos independiente, un administrador podría dar acceso a usuarios no deseados a la instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Un administrador al que le preocupe este riesgo puede poner en línea la base de datos en el modo **RESTRICTED_USER** , que evita la autenticación de usuarios de bases de datos independientes con contraseñas. Solo las entidades de seguridad autorizadas mediante inicios de sesión podrán acceder a [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 Los usuarios se crean con los requisitos de contraseña en vigor en el momento de su creación y las contraseñas no se vuelven a comprobar cuando se adjunte una base de datos. Si se adjunta una base de datos independiente que permitía contraseñas no seguras en un sistema con una directiva de contraseñas más estricta, un administrador podría permitir contraseñas que no cumplan la directiva de contraseñas actual en el [!INCLUDE[ssDE](../../includes/ssde-md.md)]que se adjunta. Los administradores pueden evitar la conservación de contraseñas no seguras exigiendo que todas las contraseñas se restablezcan para la base de datos adjunta.  
  
### <a name="password-policies"></a>Directivas de contraseñas  
 Se puede requerir que las contraseñas de una base de datos sean contraseñas seguras, pero no se pueden proteger mediante directivas de contraseñas sólidas. Use la autenticación de Windows siempre que sea posible para aprovechar las directivas de contraseñas más amplias disponibles de Windows.  
  
### <a name="kerberos-authentication"></a>Autenticación Kerberos  
 Los usuarios de bases de datos independientes con contraseñas usan la autenticación Kerberos. Siempre que sea posible, use la autenticación de Windows para aprovechar características de Windows como Kerberos.  
  
### <a name="offline-dictionary-attack"></a>Ataque por diccionario sin conexión  
 Los valores hash de contraseña de los usuarios de bases de datos independientes se almacenan en la base de datos independiente. Cualquiera que tenga acceso a los archivos de la base de datos podría realizar un ataque por diccionario contra los usuarios de bases de datos independientes con contraseña de un sistema no auditado. Para mitigar esta amenaza, restrinja el acceso a los archivos de base de datos o solo permita conexiones a bases de datos independientes mediante la autenticación de Windows.  
  
## <a name="escaping-a-contained-database"></a>Establecer secuencias de escape en una base de datos independiente  
 Si una base de datos es independiente parcialmente, los administradores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deben auditar periódicamente las capacidades de los usuarios y de los módulos de bases de datos independientes.  
  
## <a name="denial-of-service-through-autoclose"></a>Denegación de servicio mediante AUTO_CLOSE  
 No configure bases de datos independientes para que se cierren automáticamente. Si se cierra la base de datos, su apertura para autenticar un usuario consume recursos adicionales y podría contribuir a un ataque de denegación de servicio.  
  
## <a name="see-also"></a>Vea también  
 [Bases de datos independientes](../../relational-databases/databases/contained-databases.md)   
 [Migrar a una base de datos parcialmente independiente](../../relational-databases/databases/migrate-to-a-partially-contained-database.md)  
  
  
