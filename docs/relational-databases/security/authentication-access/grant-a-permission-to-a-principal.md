---
title: Conceder un permiso a una entidad de seguridad | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
helpviewer_keywords:
- Grant permission to a principal
ms.assetid: 4107389d-05b6-4aa3-9fa8-95b40cdf05dc
caps.latest.revision: 12
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 5a69323028abbd3c7684614593a1dba98dfb87c5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="grant-a-permission-to-a-principal"></a>Conceder un permiso a una entidad de seguridad
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  En este tema se describe cómo conceder permiso a una entidad de seguridad en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para conceder permiso a una entidad de seguridad, utilizando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
 Tenga en cuenta las siguientes prácticas recomendadas que pueden facilitar la administración de permisos.  
  
-   Conceda permiso a los roles, en lugar de a inicios de sesión o usuarios. Cuando un individuo es reemplazado por otro, quite del rol al individuo que se va y agregue al nuevo. Los permisos que puedan estar asociados al rol estarán disponibles automáticamente para el nuevo individuo. Si varias personas de una organización requieren los mismos permisos, al agregar cada uno de ellos al rol les concederá los mismos permisos.  
  
-   Configure elementos protegibles similares (tablas, vistas y procedimientos) para que sean propiedad de un esquema y, a continuación, conceda permisos al esquema. Por ejemplo, el esquema de nóminas puede poseer varias tablas, vistas y procedimientos almacenados. Al conceder acceso al esquema, todos los permisos necesarios para realizar la función de nómina se pueden conceder al mismo tiempo. Para obtener más información acerca de a qué elementos protegibles pueden concederse permisos, vea [Securables](../../../relational-databases/security/securables.md).  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 El otorgante de permisos (o la entidad de seguridad especificada con la opción AS) debe tener asignado el mismo permiso con GRANT OPTION o un permiso superior que implique el permiso que se va a conceder. Los miembros del rol fijo de servidor **sysadmin** pueden conceder cualquier permiso.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-grant-permission-to-a-principal"></a>Para conceder un permiso a una entidad de seguridad  
  
1.  En el Explorador de objetos, expanda la base de datos que contiene el objeto al que desea conceder permisos.  
  
    > [!NOTE]  
    >  Estos pasos abordan específicamente la concesión de permisos a un procedimiento almacenado, pero puede utilizar pasos similares para agregar permisos a tablas, vistas, funciones y ensamblados, así como a otros elementos protegibles. Para obtener más información, vea [GRANT &#40;Transact-SQL&#41;](../../../t-sql/statements/grant-transact-sql.md).  
  
2.  Expanda la carpeta **Programación** .  
  
3.  Expanda la carpeta **Procedimientos almacenados** .  
  
4.  Haga clic con el botón derecho en un procedimiento almacenado y seleccione **Propiedades**.  
  
5.  En el cuadro de diálogo *Propiedades del procedimiento almacenado –***nombre_procecimiento_almacenado*, en Seleccionar una página, seleccione **Permisos**. Utilice esta página para agregar usuarios o roles al procedimiento almacenado y especificar los permisos que los usuarios o los roles tienen.  
  
6.  Cuando termine, haga clic en **Aceptar**.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-grant-permission-to-a-principal"></a>Para conceder un permiso a una entidad de seguridad  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    -- Grants EXECUTE permission on stored procedure HumanResources.uspUpdateEmployeeHireInfo to an application role called Recruiting11.   
    USE AdventureWorks2012;  
    GO  
    GRANT EXECUTE ON OBJECT::HumanResources.uspUpdateEmployeeHireInfo  
        TO Recruiting11;  
    GO  
    ```  
  
 Para obtener más información, vea [GRANT &#40;Transact-SQL&#41;](../../../t-sql/statements/grant-transact-sql.md) y [GRANT &#40;permisos de objeto de Transact-SQL&#41;](../../../t-sql/statements/grant-object-permissions-transact-sql.md).  
  
## <a name="see-also"></a>Ver también  
 [Entidades de seguridad &#40;motor de base de datos&#41;](../../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
