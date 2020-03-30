---
title: Creación de una especificación de auditoría de servidor y de auditoría de base de datos
description: Obtenga información sobre cómo crear una auditoría de SQL Server y una especificación de auditoría de base de datos mediante SQL Server Management Studio o Transact-SQL (T-SQL)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: security
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.swb.sqlaudit.dbaudit.general.f1
helpviewer_keywords:
- audits [SQL Server], creating database specification
- database audit [SQL Server]
ms.assetid: 26ee85de-6e97-4318-b526-900924d96e62
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: d9ab1fa97653513d18c43b916ca5bfbc2105e8e7
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "75557880"
---
# <a name="create-a-server-audit-and-database-audit-specification"></a>Crear una especificación de auditoría de servidor y de auditoría de base de datos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En este tema se describe cómo crear una especificación de auditoría de servidor y de auditoría de base de datos en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 La*auditoría* de una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o de una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] implica el seguimiento y registro de los eventos que se producen en el sistema. El objeto *SQL Server Audit* recopila una única instancia de acciones y grupos de acciones de nivel de servidor o de base de datos para su supervisión. La auditoría se realiza en el nivel de instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Es posible tener varias auditorías por cada instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . El objeto *Especificación de auditoría de base de datos* pertenece a una auditoría. Puede crear una única especificación de auditoría de base de datos para cada base de datos de SQL Server y cada auditoría. Para obtener más información, vea [SQL Server Audit &#40;motor de base de datos&#41;](../../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para crear una especificación de auditoría de servidor y de auditoría de base de datos, utilizando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitaciones y restricciones  
 Las especificaciones de auditoría de base de datos son objetos no protegibles que residen en una base de datos determinada. Cuando se crea una especificación de auditoría de servidor de base de datos, está en un estado deshabilitado.  
  
 Cuando cree o modifique una especificación de auditoría de base de datos en una base de datos de usuario, no incluya acciones de auditoría en objetos del ámbito de servidor, como las vistas del sistema. Si los objetos del ámbito de servidor están incluidos, se creará la auditoría. Sin embargo, los objetos del ámbito de servidor no están incluidos y no se devolverá ningún error. Para auditar objetos del ámbito de servidor, utilice una especificación de auditoría de base de datos en la base de datos maestra.  
  
 Las especificaciones de auditoría de base de datos residen en la base de datos en la que se crearon, con la excepción de la base de datos del sistema **tempdb** .  
  
###  <a name="security"></a><a name="Security"></a> Seguridad  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permisos  
  
-   Los usuarios con el permiso ALTER ANY DATABASE AUDITpueden crear las especificaciones de auditoría de base de datos y enlazarlas a cualquier auditoría.  
  
-   Después de crearse una especificación de auditoría de base de datos, podrá ser vista por las entidades de seguridad que cuenten con los permisos CONTROL SERVER o ALTER ANY DATABASE AUDIT, o por la cuenta sysadmin.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-create-a-server-audit"></a>Para crear una auditoría de servidor  
  
1.  En el Explorador de objetos, expanda la carpeta **Seguridad** .  
  
2.  Haga clic con el botón derecho en la carpeta **Auditorías** y, después, seleccione **Nueva auditoría...** . Para obtener más información, consulte [Crear una auditoría de servidor y una especificación de auditoría de servidor](../../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md).  
  
3.  Cuando termine de seleccionar opciones, haga clic en **Aceptar**.  

#### <a name="to-create-a-database-level-audit-specification"></a>Para crear una especificación de auditoría de nivel de base de datos  
  
1.  En el Explorador de objetos, expanda la base de datos donde desea crear una especificación de auditoría.  
  
2.  Expanda la carpeta **Seguridad** .  
  
3.  Haga clic con el botón derecho en la carpeta **Especificaciones de auditoría de base de datos** y seleccione **Nueva especificación de auditoría de base de datos...** .  
  
     Las siguientes opciones están disponibles en el cuadro de diálogo **Crear especificación de auditoría de base de datos** .  
  
     **Nombre**  
     El nombre de la especificación de auditoría de base de datos. Se genera automáticamente al crear una nueva especificación de auditoría de servidor, pero se puede modificar.  
  
     **Auditoría**  
     Nombre de un objeto de auditoría de servidor existente. Escriba el nombre de la auditoría o selecciónelo en la lista.  
  
     **Tipo de acción de auditoría**  
     Especifica los grupos de acciones de auditoría y las acciones de auditoría en el nivel de base de datos que se desean capturar. Para obtener la lista de grupos de acciones de auditoría y de acciones de auditoría de nivel de base de datos, así como una descripción de los eventos que contienen, vea [Grupos de acciones y acciones de SQL Server Audit](../../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md).  
  
     **Esquema de objeto**  
     Muestra el esquema para el **Nombre de objeto**especificado.  
  
     **Nombre de objeto**  
     Nombre del objeto que se va a auditar. Este valor solo está disponible para las acciones de auditoría, no se aplica a los grupos de auditoría.  
  
     **Puntos suspensivos (...)**  
     Abre el cuadro de diálogo **Seleccionar objetos** para buscar y seleccionar un objeto disponible, basándose en el **Tipo de acción de auditoría**especificado.  
  
     **Nombre de la entidad**  
     La cuenta por la que se va filtrar la auditoría para el objeto que se va a auditar.  
  
     **Puntos suspensivos (...)**  
     Abre el cuadro de diálogo **Seleccionar objetos** para buscar y seleccionar un objeto disponible, basándose en el **Nombre de objeto**especificado.  
  
4.  Cuando termine de seleccionar opciones, haga clic en **Aceptar**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-create-a-server-audit"></a>Para crear una auditoría de servidor  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    USE master ;  
    GO  
    -- Create the server audit.   
    CREATE SERVER AUDIT Payrole_Security_Audit  
        TO FILE ( FILEPATH =   
    'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA' ) ;   
    GO  
    -- Enable the server audit.   
    ALTER SERVER AUDIT Payrole_Security_Audit   
    WITH (STATE = ON) ;  
    ```  
  
#### <a name="to-create-a-database-level-audit-specification"></a>Para crear una especificación de auditoría de nivel de base de datos  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. En el ejemplo se crea una especificación de auditoría de base de datos denominada `Audit_Pay_Tables` que audita las instrucciones SELECT e INSERT por el usuario `dbo` , para la tabla `HumanResources.EmployeePayHistory` basándose en la auditoría de servidor definida anteriormente.  
  
    ```  
    USE AdventureWorks2012 ;   
    GO  
    -- Create the database audit specification.   
    CREATE DATABASE AUDIT SPECIFICATION Audit_Pay_Tables  
    FOR SERVER AUDIT Payrole_Security_Audit  
    ADD (SELECT , INSERT  
         ON HumanResources.EmployeePayHistory BY dbo )   
    WITH (STATE = ON) ;   
    GO  
  
    ```  
  
 Para obtener más información, vea [CREATE SERVER AUDIT &#40;Transact-SQL&#41;](../../../t-sql/statements/create-server-audit-transact-sql.md) y [CREATE DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../../t-sql/statements/create-database-audit-specification-transact-sql.md).  
  
  
