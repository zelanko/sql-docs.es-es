---
title: Crear un usuario de base de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- SQL12.SWB.DATABASEUSER.GENERAL.F1
- sql12.swb.user.securables.f1
helpviewer_keywords:
- database users, creating
- creating users with Management Studio
- mapping users
- users [SQL Server], creating
- database user additions [SQL Server]
- database users, mapping
- CREATE USER [Management Studio]
- users [SQL Server], adding
- mapping database users
ms.assetid: 782798d3-9552-4514-9f58-e87be4b264e4
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 8d99b7e43a2218c79538fc2e7245733dec44e39f
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52542488"
---
# <a name="create-a-database-user"></a>Crear un usuario de base de datos
  En este tema se describe cómo crear un usuario de base de datos asignado a un inicio de sesión en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. El usuario de la base de datos es la identidad del inicio de sesión cuando está conectado a una base de datos. El usuario de la base de datos puede utilizar el mismo nombre que el inicio de sesión, pero no es necesario. En este tema se supone que ya existe un inicio de sesión en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obtener información sobre cómo crear un inicio de sesión, vea [crear un inicio de sesión](create-a-login.md).  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Información previa](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para crear un usuario de base de datos, utilizando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Información previa  
 Un usuario es una entidad de seguridad de la base de datos. Los inicios de sesión deben estar asignados a un usuario de base de datos para poder conectarse a una base de datos. Un inicio de sesión se puede asignar a bases de datos diferentes como usuarios diferentes pero solo se puede asignar como un usuario en cada base de datos. En una base de datos parcialmente independiente, puede crearse un usuario que no tenga un inicio de sesión. Para obtener más información sobre los usuarios de la base de datos independiente, vea [CREATE USER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-user-transact-sql). Si el usuario invitado de una base de datos está habilitado, un inicio de sesión que no esté asignado a un usuario de la base de datos puede entrar en la base de datos como el usuario invitado.  
  
> [!IMPORTANT]  
>  El usuario invitado suele estar deshabilitado. No habilite al usuario invitado a menos que sea necesario.  
  
 Como entidad de seguridad, se pueden conceder permisos a los usuarios. El ámbito de un usuario es la base de datos. Para establecer conexión con una base de datos concreta de la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], un inicio de sesión debe estar asignado a un usuario de la base de datos. Los permisos dentro de la base de datos se conceden y deniegan al usuario de la base de datos, no al inicio de sesión.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Debe tener el permiso `ALTER ANY USER` para la base de datos.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
##### <a name="to-create-a-database-user"></a>Para crear un usuario de base de datos  
  
1.  En el Explorador de objetos, expanda la carpeta **Bases de datos** .  
  
2.  Expanda la base de datos en la que se va a crear el usuario de la misma.  
  
3.  Haga clic con el botón derecho en la carpeta **Seguridad**, seleccione **Nuevo** y después **Usuario...**.  
  
4.  En el cuadro de diálogo **Usuario de base de datos - Nuevo**, en la página **General**, seleccione uno de los tipos de usuario siguientes de la lista **Tipo de usuario**: **Usuario SQL con inicio de sesión**, **usuario SQL sin inicio de sesión**, **usuario asignado a un certificado**, **usuario asignado a una clave asimétrica**, o **usuario de Windows** .  
  
5.  En el cuadro **Nombre de usuario** , escriba un nombre para el nuevo usuario. Si ha elegido **Usuario de Windows** en la lista **Tipo de usuario**, también puede hacer clic en los puntos suspensivos **(...)** para abrir el cuadro de diálogo **Seleccione Usuario o Grupo**.  
  
6.  En el cuadro **Nombre de inicio de sesión** , escriba el inicio de sesión para el usuario. Como alternativa, haga clic en los puntos suspensivos **(...)** para abrir el cuadro de diálogo **Seleccionar inicio de sesión**. Si selecciona**Usuario SQL con inicio de sesión** o **Usuario de Windows** en la lista **Tipo de usuario** , estará disponible **Nombre de inicio de sesión** .  
  
7.  En el cuadro **Esquema predeterminado** , especifique el esquema al que pertenecerán los objetos creados por este usuario. Como alternativa, haga clic en los puntos suspensivos **(...)** para abrir el cuadro de diálogo **Seleccionar esquema**. Si selecciona**Usuario SQL con inicio de sesión** , **Usuario SQL sin inicio de sesión**, **Usuario de Windows**en la lista **Tipo de usuario** , estará disponible **Esquema predeterminado** .  
  
8.  En el cuadro de **Nombre de certificado** , escriba el certificado que se utilizará para el usuario de base de datos. Como alternativa, haga clic en los puntos suspensivos **(...)** para abrir el cuadro de diálogo **Seleccionar certificado**. Si selecciona**Usuario asignado a un certificado** en la lista **Tipo de usuario** , estará disponible **Nombre de certificado** .  
  
9. En el cuadro **Nombre de clave asimétrica**  , escriba la clave que se va a usar para el usuario de base de datos. Como alternativa, haga clic en los puntos suspensivos **(...)** para abrir el cuadro de diálogo **Seleccionar clave asimétrica**. Si selecciona**Usuario asignado a una clave asimétrica** en la lista **Tipo de usuario** , estará disponible **Nombre de clave asimétrica** .  
  
10. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="additional-options"></a>Opciones adicionales  
 El **usuario de base de datos - nuevo** cuadro de diálogo también proporciona opciones en cuatro páginas adicionales: **Esquemas de propiedad**, **pertenencia**, **elementos protegibles**, y **propiedades extendidas**.  
  
-   La página **Esquemas de propiedad** enumera todos los esquemas posibles que pueden ser propiedad del nuevo usuario de base de datos. Para agregar o quitar esquemas en un usuario de base de datos, en **Esquemas propiedad de este usuario**, active o desactive las casillas situadas junto a los esquemas.  
  
-   La página **Pertenencia** enumera todos los roles de pertenencia de base de datos posibles que pueden ser propiedad del nuevo usuario de base de datos. Para agregar o quitar roles en un usuario de base de datos, en **Pertenencia al rol de la base de datos**, active o desactive las casillas situadas junto a los roles.  
  
-   La página **Elementos protegibles** muestra todos los elementos protegibles posibles y los permisos en esos elementos protegibles que se pueden conceder al inicio de sesión.  
  
-   La página **Propiedades extendidas** permite agregar propiedades personalizadas a los usuarios de base de datos. En esta página están disponibles las opciones siguientes.  
  
     **Base de datos**  
     Muestra el nombre de la base de datos seleccionada. Este campo es de solo lectura.  
  
     **Intercalación**  
     Muestra la intercalación utilizada para la base de datos seleccionada. Este campo es de solo lectura.  
  
     **Propiedades**  
     Muestra o especifica las propiedades extendidas del objeto. Cada propiedad extendida está formada por un par nombre/valor de metadatos asociados al objeto.  
  
     **Puntos suspensivos (...)**  
     Haga clic en los puntos suspensivos **(...)** situados detrás de **Valor** para abrir el cuadro de diálogo **Valor para propiedad extendida**. Escriba o muestre el valor de la propiedad extendida en esta ubicación mayor. Para obtener más información, vea [Valor para propiedad extendida (cuadro de diálogo)](../../databases/value-for-extended-property-dialog-box.md).  
  
     **Eliminar**  
     Elimina la propiedad extendida que se ha seleccionado.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-create-a-database-user"></a>Para crear un usuario de base de datos  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    -- Creates the login AbolrousHazem with password '340$Uuxwp7Mcxo7Khy'.  
    CREATE LOGIN AbolrousHazem   
        WITH PASSWORD = '340$Uuxwp7Mcxo7Khy';  
    GO  
  
    -- Creates a database user for the login created above.  
    CREATE USER AbolrousHazem FOR LOGIN AbolrousHazem;  
    GO  
    ```  
  
 Para obtener más información, vea [CREATE USER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-user-transact-sql).  
  
## <a name="see-also"></a>Vea también  
 [Entidades de seguridad &#40;motor de base de datos&#41;](principals-database-engine.md)  
  
  
