---
title: "Creación de un esquema de la base de datos | Microsoft Docs"
ms.custom: 
ms.date: 07/05/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: security
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.schemas.general.f1
helpviewer_keywords:
- creating schemas with Management Studio
- CREATE SCHEMA [Management Studio]
- database schemas
- schemas [SQL Server], creating
ms.assetid: ed2a5522-f4d2-4111-95a4-d3e1e5081739
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 67fa7df893601b65f5c27d55c4007386672d9e17
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="create-a-database-schema"></a>Crear un esquema de la base de datos
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] En este tema se describe cómo crear un esquema en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para crear un esquema, utilizando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   El esquema nuevo es propiedad de una de las siguientes entidades de seguridad de nivel de base de datos: usuario de base de datos, rol de base de datos o rol de aplicación. Los objetos creados dentro de un esquema son propiedad del esquema y tienen un **principal_id** NULL en **sys.objects**. La propiedad de los objetos incluidos en el esquema puede transferirse a cualquier entidad de seguridad de nivel de base de datos, pero el propietario del esquema siempre mantiene el permiso CONTROL en los objetos del esquema.  
  
-   Al crear un objeto de base de datos, si especifica una entidad de seguridad de dominio válida (usuario o grupo) como la propietaria del objeto, la entidad de seguridad de dominio se agrega a la base de datos como esquema. Esa entidad de seguridad de dominio es la propietaria del nuevo esquema.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
  
-   Requiere el permiso CREATE SCHEMA en la base de datos.  
  
-   Para especificar otro usuario como el propietario del esquema que se está creando, el autor de la llamada debe tener el permiso IMPERSONATE sobre ese usuario. Si se especifica un rol de base de datos como propietario, el autor de la llamada debe cumplir uno de los siguientes criterios: pertenencia al rol o permiso ALTER en el rol.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
##### <a name="to-create-a-schema"></a>Para crear un esquema  
  
1.  En el Explorador de objetos, expanda la carpeta **Bases de datos** .  
  
2.  Expanda la base de datos en la que se va a crear el esquema de la misma.  
  
3.  Haga clic con el botón derecho en la carpeta **Seguridad** , seleccione **Nuevo**y seleccione **Esquema**.  
  
4.  En el cuadro de diálogo **Esquema - Nuevo** , en la página **General** , escriba un nombre para el nuevo esquema en el cuadro **Nombre de esquema** .  
  
5.  En el cuadro **Propietario del esquema** , escriba el nombre del usuario o rol de base de datos que va a poseer el esquema. Como alternativa, haga clic en **Buscar** para abrir el cuadro de diálogo **Buscar roles y usuarios** .  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="additional-options"></a>Opciones adicionales  
 El cuadro de diálogo **Esquema - Nuevo** también proporciona opciones de dos páginas adicionales: **Permisos** y **Propiedades extendidas**.  
  
-   La página **Permisos** muestra todos los elementos protegibles posibles y los permisos en esos elementos protegibles que se pueden conceder al inicio de sesión.  
  
-   La página **Propiedades extendidas** permite agregar propiedades personalizadas a los usuarios de base de datos.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-create-a-schema"></a>Para crear un esquema  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  En el siguiente ejemplo se crea un esquema denominado `Chains` y luego se crea una tabla denominada `Sizes`.  
    ```sql  
    CREATE SCHEMA Chains;
    GO
    CREATE TABLE Chains.Sizes (ChainID int, width dec(10,2));
    ```

4.  Se pueden realizar opciones adicionales en una sola instrucción. En el ejemplo siguiente se crea el esquema `Sprockets`, que es propiedad de Annik y contiene la tabla `NineProngs`. La instrucción concede el permiso `SELECT` a Mandar y deniega el permiso `SELECT` a Prasanna.  

    ```sql  
    CREATE SCHEMA Sprockets AUTHORIZATION Annik  
        CREATE TABLE NineProngs (source int, cost int, partnumber int)  
        GRANT SELECT ON SCHEMA::Sprockets TO Mandar  
        DENY SELECT ON SCHEMA::Sprockets TO Prasanna;  
    GO  
    ```  
5. Ejecute la siguiente instrucción para ver los esquemas de esta base de datos:

   ```sql
   SELECT * FROM sys.schemas;
   ```

 Para obtener más información, vea [CREATE INDEX &#40;Transact-SQL&#41;](../../../t-sql/statements/create-schema-transact-sql.md).  
  
  
