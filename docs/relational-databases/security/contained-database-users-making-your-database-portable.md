---
title: Acceso de usuario contenido a las bases de datos independientes
description: Obtenga información sobre cómo configurar el acceso de usuario contenido para bases de datos independientes y conozca las diferencias entre un modelo de usuario o inicio de sesión tradicional.
ms.custom: seo-lt-2019
ms.date: 01/28/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- contained database, users
- user [SQL Server], about contained database users
ms.assetid: e57519bb-e7f4-459b-ba2f-fd42865ca91d
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||=azure-sqldw-latest||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: decbd12174f6000a44a3cfd95b145c70de10740c
ms.sourcegitcommit: a5398f107599102af7c8cda815d8e5e9a367ce7e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/13/2020
ms.locfileid: "92004670"
---
# <a name="contained-database-users---making-your-database-portable"></a>Usuarios de base de datos independiente: hacer que la base de datos sea portátil

[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  Use los usuarios de base de datos independiente para autenticar conexiones [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y [!INCLUDE[ssSDS](../../includes/sssds-md.md)] en el nivel de base de datos. Una base de datos independiente es una base de datos que está aislada de otras bases de datos y de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ [!INCLUDE[ssSDS](../../includes/sssds-md.md)] (y de la base de datos maestra) que hospeda la base de datos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite usuarios de base de datos independientes para la autenticación de Windows y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Al usar [!INCLUDE[ssSDS](../../includes/sssds-md.md)], se combinan las reglas de usuarios de la base de datos independiente con las de firewall de nivel de base de datos. En este tema se revisan las diferencias y ventajas de utilizar el modelo de base de datos independiente en comparación con el modelo de inicio de sesión o usuario tradicionales y las reglas de firewall de Windows o de nivel de servidor. Es posible que la lógica de escenarios específicos, de manejabilidad o de software empresarial todavía pueda necesitar el uso de reglas de inicio de sesión o usuario tradicionales y de firewall de nivel de servidor.  
  
> [!NOTE]  
> Como [!INCLUDE[msCoName](../../includes/msconame-md.md)] desarrolla el servicio [!INCLUDE[ssSDS](../../includes/sssds-md.md)] y avanza hacia contrato de nivel de servicio superiores garantizados, es posible que se le pida que cambie a las normas de modelo de usuario de base de datos independiente y las de firewall de ámbito de base de datos para lograr el contrato de nivel de servicio de mayor disponibilidad y mayores tasas de inicio de sesión máximas para una base de datos determinada. [!INCLUDE[msCoName](../../includes/msconame-md.md)] le recomienda que considere la posibilidad de realizar dichos cambios hoy mismo.  
  
## <a name="traditional-login-and-user-model"></a>Inicio de sesión tradicional y modelo de usuario

 En el modelo tradicional de conexión, los usuarios de Windows o los miembros de los grupos de Windows se conectan a la [!INCLUDE[ssDE](../../includes/ssde-md.md)] al proporcionar las credenciales de usuario o grupo autenticadas por Windows. O bien, puede proporcionar un nombre y la contraseña y conectarse mediante autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . En ambos casos, la base de datos maestra debe tener un inicio de sesión que coincida con las credenciales de conexión. Después de que la [!INCLUDE[ssDE](../../includes/ssde-md.md)] confirme las credenciales de autenticación de Windows o autentica las credenciales de autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , la conexión normalmente intenta conectarse a una base de datos de usuario. Para conectarse a una base de datos de usuario, el inicio de sesión se debe poder asignar (es decir, asociar) a un usuario de base de datos en la base de datos de usuario. También es posible que la cadena de conexión especifique la conexión a una base de datos que es opcional en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pero obligatoria en [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 El principio importante es que tanto el inicio de sesión (en la base de datos maestra) como el usuario (en la base de datos de usuario) deben existir y estar relacionados entre sí. Esto significa que la conexión a la base de datos de usuario tiene una dependencia en el inicio de sesión en la base de datos maestra y esto limita la capacidad de la base de datos de moverse a un servidor host de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] diferente. Además, si por cualquier motivo no hay una conexión a la base de datos maestra disponible (por ejemplo, una conmutación por error está en curso), aumentará el tiempo total de conexión o es posible que se agote el tiempo de espera de la conexión. En consecuencia, esto puede reducir la escalabilidad de la conexión.  
  
## <a name="contained-database-user-model"></a>Modelo de usuario de base de datos independiente

 En el modelo de usuario de base de datos independiente, el inicio de sesión en la base de datos maestra no está presente. En su lugar, el proceso de autenticación se produce en la base de datos de usuario y el usuario de base de datos de la base de datos de usuario no tiene asociado ningún inicio de sesión en la base de datos maestra. El modelo de usuario de base de datos independiente admite tanto la autenticación de Windows como la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , y se puede usar tanto en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como en [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. Para conectarse como un usuario de base de datos independiente, la cadena de conexión siempre debe contener un parámetro para la base de datos de usuario de modo que la [!INCLUDE[ssDE](../../includes/ssde-md.md)] sepa qué base de datos es responsable de la administración del proceso de autenticación. La actividad del usuario de base de datos independiente se limita a la autenticación de base de datos, por lo que al conectarse como un usuario de base de datos independiente, la cuenta de usuario de base de datos debe crearse independientemente en cada base de datos que el usuario necesitará. Para cambiar las bases de datos, los usuarios de [!INCLUDE[ssSDS](../../includes/sssds-md.md)] deben crear una nueva conexión. Los usuarios de base de datos independiente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueden cambiar bases de datos si hay un usuario idéntico en otra base de datos.  
  
**Azure:** [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] y [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] admiten las identidades de Azure Active Directory como usuarios de base de datos independiente. [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] admite usuarios de base de datos independientes que usan autenticación de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , pero [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] no. Para más información, consulte [Usar la autenticación de Azure Active Directory para autenticación con SQL](/azure/azure-sql/database/authentication-aad-overview). Al utilizar la autenticación de Active Directory de Azure, las conexiones de SSMS se pueden realizar mediante autenticación universal de Active Directory.  Los administradores pueden configurar la autenticación universal para requerir Multi-Factor Authentication, que comprueba la identidad mediante una llamada de teléfono, un mensaje de texto, una tarjeta inteligente con pin o una notificación de aplicación móvil. Para obtener más información, vea [Compatibilidad de SSMS con Azure AD MFA con SQL Database y Azure Synapse Analytics](/azure/azure-sql/database/authentication-mfa-ssms-overview).  
  
 Para [!INCLUDE[ssSDS](../../includes/sssds-md.md)] y [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)], dado que el nombre de la base de datos siempre se requiere en la cadena de conexión, no se necesitan cambios en la cadena de conexión cuando se cambia desde el modelo tradicional al modelo de usuario de base de datos independiente. Para las conexiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , el nombre de la base de datos debe agregarse a la cadena de conexión si no está ya presente.  
  
> [!IMPORTANT]  
> Cuando se usa el modelo tradicional, los roles de nivel de servidor y los permisos de nivel de servidor pueden limitar el acceso a todas las bases de datos. Al usar el modelo de base de datos independiente, los propietarios de la base de datos y los usuarios de la base de datos con el permiso ALTER ANY USER pueden conceder acceso a la base de datos. Esto reduce el control de acceso de inicios de sesión de servidor con privilegios altos y amplía el control de acceso para incluir los usuarios de la base de datos con privilegios altos.  
  
## <a name="firewalls"></a>Firewalls  
  
### [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

 Las reglas de Firewall de Windows se aplican a todas las conexiones y tienen el mismo efecto en los inicios de sesión (conexiones de modelo tradicional) y los usuarios de la base de datos independiente. Para obtener más información sobre el Firewall de Windows, consulte [Configure a Windows Firewall for Database Engine Access](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md).  
  
### <a name="sssds-firewalls"></a>[!INCLUDE[ssSDS](../../includes/sssds-md.md)] Firewalls

 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] permite reglas de: firewall independientes para las conexiones de nivel de servidor (inicios de sesión) y las conexiones de nivel de base de datos (usuarios de base de datos independiente). Al conectarse a una base de datos de usuario, primero se comprueban las reglas de firewall de base de datos. Si no hay ninguna regla que permita acceder a la base de datos, se comprueban las reglas de firewall de nivel de servidor, lo que requiere acceso a la base de datos maestra del servidor maestro de SQL Database. Las reglas de firewall de nivel de base de datos combinadas con los usuarios de la base de datos independiente pueden eliminar la necesidad de acceder a la base de datos maestra del servidor durante la conexión, lo que puede mejorar la escalabilidad de la conexión.  
  
 Para obtener más información sobre las reglas de firewall de [!INCLUDE[ssSDS](../../includes/sssds-md.md)] , vea los temas siguientes:  
  
- [Firewall de Azure SQL Database](/previous-versions/azure/ee621782(v=azure.100))  
- [Cómo: Configurar los valores del firewall (Azure SQL Database)](/previous-versions/azure/jj553530(v=azure.100))  
- [sp_set_firewall_rule &#40;Base de datos SQL de Azure&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)  
- [sp_set_database_firewall_rule &#40;Base de datos SQL de Azure&#41;](../../relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database.md)  
  
## <a name="syntax-differences"></a>Diferencias de sintaxis  
  
|Modelo tradicional|Modelo de usuario de base de datos independiente|  
|-----------------------|-----------------------------------|  
|Cuando se conecta a la base de datos maestra:<br /><br /> `CREATE LOGIN login_name  WITH PASSWORD = 'strong_password';`<br /><br /> Después, cuando se conecta a una base de datos de usuario:<br /><br /> `CREATE USER 'user_name' FOR LOGIN 'login_name';`|Cuando se conecta a una base de datos de usuario:<br /><br /> `CREATE USER user_name  WITH PASSWORD = 'strong_password';`|  
  
|Modelo tradicional|Modelo de usuario de base de datos independiente|  
|-----------------------|-----------------------------------|  
|Para cambiar la contraseña, en el contexto de la base de datos maestra:<br /><br /> `ALTER LOGIN login_name  WITH PASSWORD = 'strong_password';`|Para cambiar la contraseña, en el contexto de la base de datos de usuario:<br /><br /> `ALTER USER user_name  WITH PASSWORD = 'strong_password';`|  

### <a name="managed-instance"></a>de SQL DB

Azure SQL Managed Instance se comporta como SQL Server local en el contexto de las bases de datos independientes. Asegúrese de cambiar el contexto de la base de datos de la base de datos maestra a la de usuario al crear el usuario contenido. Además, no debería haber ninguna conexión activa con la base de datos de usuario al establecer la opción de contención. 


Por ejemplo:

> [!WARNING]
> Antes de ejecutar el siguiente script, asegúrese de que no haya otras conexiones activas en la base de datos de Instancia administrada. El script puede afectar a otros procesos que se están ejecutando en la base de datos.

```sql
Use MASTER;
GO 

ALTER DATABASE Test
SET RESTRICTED_USER
WITH ROLLBACK IMMEDIATE;

ALTER DATABASE Test
SET containment=partial;

ALTER DATABASE Test
SET MULTI_USER;

USE Test;  
GO 

CREATE USER Carlo  
WITH PASSWORD='Enterpwdhere*'  

SELECT containment_desc FROM sys.databases
WHERE name='Test'
```

  
## <a name="remarks"></a>Observaciones  
  
- En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], los usuarios de la base de datos independiente deben estar habilitados para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para más información, consulte la [opción de configuración del servidor de autenticación de base de datos independiente](../../database-engine/configure-windows/contained-database-authentication-server-configuration-option.md).  
- Los usuarios de base de datos independiente y los inicios de sesión con nombres no superpuestos pueden coexistir en las aplicaciones.  
- Si hay un inicio de sesión en la base de datos maestra con el nombre **name1** y crea un usuario de base de datos independiente denominado **name1**, cuando se proporcione un nombre de base de datos en la cadena de conexión, el contexto del usuario de base de datos tendrá prioridad sobre el contexto de inicio de sesión al conectarse a la base de datos. Es decir, los usuarios de base de datos independiente tienen prioridad sobre los inicios de sesión con el mismo nombre.  
- En [!INCLUDE[ssSDS](../../includes/sssds-md.md)] , el nombre de un usuario de base de datos independiente no puede ser el mismo que el nombre de la cuenta de administrador del servidor.  
- La cuenta de administrador del servidor de [!INCLUDE[ssSDS](../../includes/sssds-md.md)] nunca puede ser un usuario de base de datos independiente. El administrador del servidor tiene los permisos necesarios para crear y administrar los usuarios de la base de datos independiente. El administrador del servidor puede conceder permisos a los usuarios de base de datos independiente en bases de datos de usuario.  
- Ya que los usuarios de base de datos independiente son entidades de seguridad de nivel de base de datos, deberá crear usuarios de base de datos independiente en cada base de datos en la que los utilizará. La identidad se limita a la base de datos y es independiente en todos los aspectos de un usuario con el mismo nombre y la misma contraseña de otra base de datos del mismo servidor.  
- Use las mismas contraseñas seguras que usaría normalmente para los inicios de sesión.  
  
## <a name="see-also"></a>Consulte también

 [Bases de datos independientes](../../relational-databases/databases/contained-databases.md)   
 [Prácticas recomendadas de seguridad con bases de datos independientes](../../relational-databases/databases/security-best-practices-with-contained-databases.md)   
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [Conexión a SQL Database mediante autenticación de Azure Active Directory](/azure/azure-sql/database/authentication-aad-overview)  
