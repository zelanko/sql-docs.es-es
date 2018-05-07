---
title: Combinación de un rol | Microsoft Docs
ms.custom: ''
ms.date: 07/14/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: security
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- SQL13.SWB.DATABASEUSER.MEMBERSHIP.F1
helpviewer_keywords:
- adding a member to a role
- join a role
ms.assetid: 05c8d10d-5823-46c6-8b1a-81722da6a42b
caps.latest.revision: 13
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 1a422023129646f855b29ec5a6eb1587a54c0ed3
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="join-a-role"></a>combinar un rol
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  En este tema se describe cómo asignar roles a inicios de sesión y a usuarios de base de datos en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Use los roles de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para administrar eficazmente los permisos. Asigne permisos a roles y, a continuación, agregue o quite usuarios e inicios de sesión a los roles. Mediante el uso de roles, los permisos no se tienen que mantener individualmente para cada usuario.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] admite cuatro tipos de roles.  
  
-   Roles fijos de servidor  
  
-   Roles de servidor definidos por el usuario  
  
-   Roles fijos de base de datos  
  
-   Roles de base de datos definidos por el usuario  
  
 Los roles fijos están disponibles automáticamente en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Estos roles disponen de los permisos necesarios para realizar las tareas habituales. Para obtener más información sobre los roles fijos, vea los siguientes vínculos: El usuario crea los roles definidos por el usuario y se pueden personalizar con los permisos que se seleccionen. Para obtener más información sobre los roles definidos por el usuario, vea los siguientes vínculos:  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para asignar roles a inicios de sesión y a usuarios de base de datos, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   El cambio de nombre de un rol de base de datos no modifica el número de identificación, el propietario, ni los permisos del rol.  
  
-   Los roles de base de datos se pueden ver en las vistas de catálogos sys.database_role_members y sys.database_principals.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Requiere el permiso **ALTER ANY ROLE** en la base de datos, el permiso **ALTER** en el rol o la pertenencia a **db_securityadmin**.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-add-a-member-to-a-fixed-server-role"></a>Para agregar un miembro a un rol fijo de servidor  
  
1.  En el Explorador de objetos, expanda el servidor en el que desea modificar un rol fijo de servidor.  
  
2.  Expanda la carpeta **Seguridad** .  
  
3.  Expanda la carpeta **Roles de servidor** .  
  
4.  Haga clic con el botón derecho en el rol que quiere editar y seleccione **Propiedades**.  
  
5.  En el cuadro de diálogo *Propiedades del rol de servidor –***nombre_del_rol_de_servidor*, en la página **Miembros**, haga clic en **Agregar**.  
  
6.  En el cuadro de diálogo **Seleccionar inicio de sesión o rol de servidor** , en **Escribir los nombres de objeto para seleccionar (ejemplos)**, especifique el inicio de sesión o el rol de servidor que quiere agregar a este rol de servidor. O bien, haga clic en **Examinar…** y seleccione cualquier objeto disponible en el cuadro de diálogo **Buscar objetos** o todos ellos. Haga clic en **Aceptar** para volver al cuadro de diálogo **Propiedades del rol de servidor –***nombre_del_rol_de_servidor*.  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-add-a-member-to-a-user-defined-database-role"></a>Para agregar un miembro a un rol de base de datos definido por el usuario  
  
1.  En el Explorador de objetos, expanda el servidor en el que desea editar un rol de base de datos definido por el usuario.  
  
2.  Expanda la carpeta **Bases de datos** .  
  
3.  Expanda la base de datos en la que desea editar un rol de base de datos definido por el usuario.  
  
4.  Expanda la carpeta **Seguridad** .  
  
5.  Expanda la carpeta **Roles** .  
  
6.  Expanda la carpeta **Roles de servidor** .  
  
7.  Haga clic con el botón derecho en el rol que quiere editar y seleccione **Propiedades**.  
  
8.  En el cuadro de diálogo *Propiedades del rol de base de datos –***nombre_del_rol_de_la_base_de_datos*, en la página **General**, haga clic en **Agregar**.  
  
9. En el cuadro de diálogo **Seleccionar usuario o rol de base de datos** , en **Escribir los nombres de objeto para seleccionar (ejemplos)**, especifique el inicio de sesión o el rol de la base de datos que quiere agregar a este rol de base de datos. O bien, haga clic en **Examinar…** y seleccione cualquier objeto disponible en el cuadro de diálogo **Buscar objetos** o todos ellos. Haga clic en **Aceptar** para volver al cuadro de diálogo **Propiedades del rol de base de datos –***nombre_del_rol_de_la_base_de_datos*.  
  
10. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-add-a-member-to-a-fixed-server-role"></a>Para agregar un miembro a un rol fijo de servidor  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    ALTER SERVER ROLE diskadmin ADD MEMBER [Domain\Juan] ;  
    GO  
    ```  
  
 Para obtener más información, vea [ALTER ROLE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-role-transact-sql.md).  
  
#### <a name="to-add-a-member-to-a-user-defined-database-role"></a>Para agregar un miembro a un rol de base de datos definido por el usuario  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    ALTER ROLE Marketing ADD MEMBER [Domain\Juan] ;  
    GO  
    ```  
  
 Para obtener más información, vea [sp_addrolemember &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md).  
  
## <a name="see-also"></a>Ver también  
 [Roles de nivel de servidor](../../../relational-databases/security/authentication-access/server-level-roles.md)   
 [Roles de nivel de base de datos](../../../relational-databases/security/authentication-access/database-level-roles.md)   
 [Roles de aplicación](../../../relational-databases/security/authentication-access/application-roles.md)  
  
  
