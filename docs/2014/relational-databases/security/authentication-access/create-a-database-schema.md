---
title: Creación de un esquema de la base de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql12.swb.schemas.general.f1
helpviewer_keywords:
- creating schemas with Management Studio
- CREATE SCHEMA [Management Studio]
- database schemas
- schemas [SQL Server], creating
ms.assetid: ed2a5522-f4d2-4111-95a4-d3e1e5081739
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 3c3747149b23c6217f321eff9d19621189b89b66
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63011987"
---
# <a name="create-a-database-schema"></a>Crear un esquema de la base de datos
  En este tema se describe cómo crear un esquema en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
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
  
-   Cuando se crea un objeto de base de datos, si especifica una entidad de seguridad de dominio válida (usuario o grupo) como la propietaria del objeto, la entidad de seguridad de dominio se agregará a la base de datos como esquema. Esa entidad de seguridad de dominio será la propietaria del nuevo esquema.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
  
-   Requiere el permiso CREATE SCHEMA en la base de datos.  
  
-   Para especificar otro usuario como el propietario del esquema que se está creando, el autor de la llamada debe tener el permiso IMPERSONATE sobre ese usuario. Si se especifica un rol de base de datos como propietario, el autor de la llamada debe pertenecer al rol o debe tener el permiso ALTER para el rol.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
##### <a name="to-create-a-schema"></a>Para crear un esquema  
  
1.  En el Explorador de objetos, expanda la carpeta **Bases de datos** .  
  
2.  Expanda la base de datos en la que se va a crear el esquema de la misma.  
  
3.  Haga clic con el botón derecho en la carpeta **Seguridad** , seleccione **Nuevo**y seleccione **Esquema**.  
  
4.  En el cuadro de diálogo **Esquema - Nuevo** , en la página **General** , escriba un nombre para el nuevo esquema en el cuadro **Nombre de esquema** .  
  
5.  En el cuadro **Propietario del esquema** , escriba el nombre del usuario o rol de base de datos que va a poseer el esquema. Como alternativa, haga clic en **Buscar** para abrir el cuadro de diálogo **Buscar roles y usuarios** .  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="additional-options"></a>Opciones adicionales  
 En el cuadro de diálogo **Esquema - Nuevo** también se ofrecen opciones en dos páginas adicionales: **Permisos** y **Propiedades extendidas**.  
  
-   La página **Permisos** muestra todos los elementos protegibles posibles y los permisos en esos elementos protegibles que se pueden conceder al inicio de sesión.  
  
-   La página **Propiedades extendidas** permite agregar propiedades personalizadas a los usuarios de base de datos.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-create-a-schema"></a>Para crear un esquema  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Creates the schema Sprockets owned by Annik that contains table NineProngs.   
    -- The statement grants SELECT to Mandar and denies SELECT to Prasanna.  
  
    CREATE SCHEMA Sprockets AUTHORIZATION Annik  
        CREATE TABLE NineProngs (source int, cost int, partnumber int)  
        GRANT SELECT ON SCHEMA::Sprockets TO Mandar  
        DENY SELECT ON SCHEMA::Sprockets TO Prasanna;  
    GO  
    ```  
  
 Para obtener más información, vea [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-schema-transact-sql).  
  
  
