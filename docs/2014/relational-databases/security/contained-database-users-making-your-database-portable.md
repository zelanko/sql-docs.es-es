---
title: 'Usuarios de base de datos independiente: hacer que la base de datos sea portátil | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- contained database, users
- user [SQL Server], about contained database users
ms.assetid: e57519bb-e7f4-459b-ba2f-fd42865ca91d
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: e793680a5171493460ff1f66caf7a918103619cf
ms.sourcegitcommit: b75fc8cfb9a8657f883df43a1f9ba1b70f1ac9fb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/08/2018
ms.locfileid: "48851830"
---
# <a name="contained-database-users---making-your-database-portable"></a>Usuarios de base de datos independiente: hacer que la base de datos sea portátil
  Use los usuarios de base de datos independiente para autenticar conexiones [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y [!INCLUDE[ssSDS](../../includes/sssds-md.md)] en el nivel de base de datos. Una base de datos independiente es una base de datos que está aislada de otras bases de datos y de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/[!INCLUDE[ssSDS](../../includes/sssds-md.md)] (y de la base de datos maestra) que hospeda la base de datos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite usuarios de base de datos independientes para la autenticación de Windows y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Al usar [!INCLUDE[ssSDS](../../includes/sssds-md.md)], se combinan las reglas de usuarios de la base de datos independiente con las de firewall de nivel de base de datos. En este tema se revisan las diferencias y ventajas de utilizar el modelo de base de datos independiente en comparación con el modelo de inicio de sesión o usuario tradicionales y las reglas de firewall de Windows o de nivel de servidor. Es posible que la lógica de escenarios específicos, de manejabilidad o de software empresarial todavía pueda necesitar el uso de reglas de inicio de sesión o usuario tradicionales y de firewall de nivel de servidor.  
  
> [!NOTE]  
>  Como [!INCLUDE[msCoName](../../includes/msconame-md.md)] desarrolla el servicio [!INCLUDE[ssSDS](../../includes/sssds-md.md)] y avanza hacia contrato de nivel de servicio superiores garantizados, es posible que se le pida que cambie a las normas de modelo de usuario de base de datos independiente y las de firewall de ámbito de base de datos para lograr el contrato de nivel de servicio de mayor disponibilidad y mayores tasas de inicio de sesión máximas para una base de datos determinada. [!INCLUDE[msCoName](../../includes/msconame-md.md)] le recomienda que considere la posibilidad de realizar dichos cambios hoy mismo.  
  
## <a name="traditional-login-and-user-model"></a>Inicio de sesión tradicional y modelo de usuario  
 En el modelo tradicional de conexión, los usuarios de Windows o los miembros de los grupos de Windows se conectan a la [!INCLUDE[ssDE](../../includes/ssde-md.md)] al proporcionar las credenciales de usuario o grupo autenticadas por Windows. O bien, la conexión proporciona un nombre y contraseña, y se conecta mediante la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (que es la única opción cuando se conecta a [!INCLUDE[ssSDS](../../includes/sssds-md.md)]). En ambos casos, la base de datos maestra debe tener un inicio de sesión que coincida con las credenciales de conexión. Después de que la [!INCLUDE[ssDE](../../includes/ssde-md.md)] confirme las credenciales de autenticación de Windows o autentica las credenciales de autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , la conexión normalmente intenta conectarse a una base de datos de usuario. Para conectarse a una base de datos de usuario, el inicio de sesión se debe poder asignar (es decir, asociar) a un usuario de base de datos en la base de datos de usuario. También es posible que la cadena de conexión especifique la conexión a una base de datos que es opcional en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pero obligatoria en [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 El principio importante es que tanto el inicio de sesión (en la base de datos maestra) como el usuario (en la base de datos de usuario) deben existir y estar relacionados entre sí. Esto significa que la conexión a la base de datos de usuario tiene una dependencia en el inicio de sesión en la base de datos maestra y esto limita la capacidad de la base de datos de moverse a un servidor host de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] diferente. Además, si por cualquier motivo no hay una conexión a la base de datos maestra disponible (por ejemplo, una conmutación por error está en curso), aumentará el tiempo total de conexión o es posible que se agote el tiempo de espera de la conexión. En consecuencia, esto puede reducir la escalabilidad de la conexión.  
  
## <a name="contained-database-user-model"></a>Modelo de usuario de base de datos independiente  
 En el modelo de usuario de base de datos independiente, el inicio de sesión en la base de datos maestra no está presente. En su lugar, el proceso de autenticación se produce en la base de datos de usuario y el usuario de base de datos de la base de datos de usuario no tiene asociado ningún inicio de sesión en la base de datos maestra. El modelo de usuario de base de datos independiente admite tanto la autenticación de Windows (en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) como la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y [!INCLUDE[ssSDS](../../includes/sssds-md.md)]). Para conectarse como un usuario de base de datos independiente, la cadena de conexión siempre debe contener un parámetro para la base de datos de usuario de modo que la [!INCLUDE[ssDE](../../includes/ssde-md.md)] sepa qué base de datos es responsable de la administración del proceso de autenticación. La actividad del usuario de base de datos independiente se limita a la autenticación de base de datos, por lo que al conectarse como un usuario de base de datos independiente, la cuenta de usuario de base de datos debe crearse independientemente en cada base de datos que el usuario necesitará. Para cambiar las bases de datos, los usuarios de [!INCLUDE[ssSDS](../../includes/sssds-md.md)] deben crear una nueva conexión. Los usuarios de base de datos independiente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueden cambiar bases de datos si hay un usuario idéntico en otra base de datos.  
  
 Para [!INCLUDE[ssSDS](../../includes/sssds-md.md)], no se necesitan cambios en la cadena de conexión cuando se cambia desde el modelo tradicional al modelo de usuario de base de datos independiente. Para las conexiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el nombre de la base de datos debe agregarse a la cadena de conexión si no está ya presente.  
  
> [!IMPORTANT]  
>  Cuando se usa el modelo tradicional, los roles de nivel de servidor y los permisos de nivel de servidor pueden limitar el acceso a todas las bases de datos. Al usar el modelo de base de datos independiente, los propietarios de la base de datos y los usuarios de la base de datos con el permiso ALTER ANY USER pueden conceder acceso a la base de datos. Esto reduce el control de acceso de inicios de sesión de servidor con privilegios altos y amplía el control de acceso para incluir los usuarios de la base de datos con privilegios altos.  
  
## <a name="firewalls"></a>Firewalls  
  
### [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Las reglas de Firewall de Windows se aplican a todas las conexiones y tienen el mismo efecto en los inicios de sesión (conexiones de modelo tradicional) y los usuarios de la base de datos independiente. Para obtener más información sobre el Firewall de Windows, consulte [Configure a Windows Firewall for Database Engine Access](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md).  
  
### <a name="includesssdsincludessssds-mdmd-firewalls"></a>Firewalls de [!INCLUDE[ssSDS](../../includes/sssds-md.md)]  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] permite reglas de: firewall independientes para las conexiones de nivel de servidor (inicios de sesión) y las conexiones de nivel de base de datos (usuarios de base de datos independiente). Al conectarse a una base de datos de usuario, primero se comprueban las reglas de firewall de base de datos. Si no hay ninguna regla que permita acceder a la base de datos, se comprueban las reglas de firewall de nivel de servidor, lo que requiere acceso a la base de datos maestra del servidor lógico. Las reglas de firewall de nivel de base de datos combinadas con los usuarios de la base de datos independiente pueden eliminar la necesidad de acceder a la base de datos maestra del servidor durante la conexión, lo que puede mejorar la escalabilidad de la conexión.  
  
 Para obtener más información sobre las reglas de firewall de [!INCLUDE[ssSDS](../../includes/sssds-md.md)] , vea los temas siguientes:  
  
-   [Firewall de la base de datos SQL de Azure](http://msdn.microsoft.com/library/azure/ee621782.aspx)  
  
-   [Configurar los valores de firewall (Base de datos SQL de Azure)](http://msdn.microsoft.com/library/azure/jj553530.aspx)  
  
-   [sp_set_firewall_rule &#40;Base de datos SQL de Azure&#41;](/sql/relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database)  
  
-   [sp_set_database_firewall_rule &#40;Base de datos SQL de Azure&#41;](/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database)  
  
## <a name="syntax-differences"></a>Diferencias de sintaxis  
  
|Modelo tradicional|Modelo de usuario de base de datos independiente|  
|-----------------------|-----------------------------------|  
|Cuando se conecta a la base de datos maestra:<br /><br /> `CREATE LOGIN login_name  WITH PASSWORD = 'strong_password';`<br /><br /> Después, cuando se conecta a una base de datos de usuario:<br /><br /> `CREATE USER 'user_name' FOR LOGIN 'login_name';`|Cuando se conecta a una base de datos de usuario:<br /><br /> `CREATE USER user_name  WITH PASSWORD = 'strong_password';`|  
  
|Modelo tradicional|Modelo de usuario de base de datos independiente|  
|-----------------------|-----------------------------------|  
|Para cambiar la contraseña, en el contexto de la base de datos maestra:<br /><br /> `ALTER LOGIN login_name  WITH PASSWORD = 'strong_password';`|Para cambiar la contraseña, en el contexto de la base de datos de usuario:<br /><br /> `ALTER USER user_name  WITH PASSWORD = 'strong_password';`|  
  
## <a name="remarks"></a>Comentarios  
  
-   En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], los usuarios de la base de datos independiente deben estar habilitados para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, vea [contained database authentication Server Configuration Option](../../database-engine/configure-windows/contained-database-authentication-server-configuration-option.md).  
  
-   Los usuarios de base de datos independiente y los inicios de sesión con nombres no superpuestos pueden coexistir en las aplicaciones.  
  
-   Si hay un inicio de sesión en la base de datos maestra con el nombre **name1** y crea un usuario de base de datos independiente denominado **name1**, cuando se proporcione un nombre de base de datos en la cadena de conexión, el contexto del usuario de base de datos tendrá prioridad sobre el contexto de inicio de sesión al conectarse a la base de datos. Es decir, los usuarios de base de datos independiente tienen prioridad sobre los inicios de sesión con el mismo nombre.  
  
-   En [!INCLUDE[ssSDS](../../includes/sssds-md.md)] , el nombre de un usuario de base de datos independiente no puede ser el mismo que el nombre de la cuenta de administrador del servidor.  
  
-   La cuenta de administrador del servidor de [!INCLUDE[ssSDS](../../includes/sssds-md.md)] nunca puede ser un usuario de base de datos independiente. El administrador del servidor tiene los permisos necesarios para crear y administrar los usuarios de la base de datos independiente. El administrador del servidor puede conceder permisos a los usuarios de base de datos independiente en bases de datos de usuario.  
  
-   Ya que los usuarios de base de datos independiente son entidades de seguridad de nivel de base de datos, deberá crear usuarios de base de datos independiente en cada base de datos en la que los utilizará. La identidad se limita a la base de datos y es independiente en todos los aspectos de un usuario con el mismo nombre y la misma contraseña de otra base de datos del mismo servidor.  
  
-   Use las mismas contraseñas seguras que usaría normalmente para los inicios de sesión.  
  
## <a name="see-also"></a>Vea también  
 [Bases de datos independientes](../databases/contained-databases.md)   
 [Prácticas recomendadas de seguridad con bases de datos independientes](../databases/security-best-practices-with-contained-databases.md)   
 [CREATE USER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-user-transact-sql)  
  
  
