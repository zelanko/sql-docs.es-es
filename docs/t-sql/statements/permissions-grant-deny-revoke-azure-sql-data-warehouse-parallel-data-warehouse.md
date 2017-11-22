---
title: Almacenamientos de datos paralelo y de datos de SQL Azure Perms REVOKE denegar GRANT | Documentos de Microsoft
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: 5a3b7424-408e-4cb0-8957-667ebf4596fc
caps.latest.revision: "9"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: a21ee8a4a525e2b8c522de140a3f482915cdb361
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="permissions-grant-deny-revoke-azure-sql-data-warehouse-parallel-data-warehouse"></a>Permisos: GRANT, DENY y REVOKE (almacenamiento de datos SQL Azure, almacenamiento de datos en paralelo)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Use [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] **GRANT** y **DENY** instrucciones para conceder o denegar un permiso (como **actualización**) en un elemento protegible (por ejemplo, una base de datos, tabla, vista etcetera.) para una entidad de seguridad (un inicio de sesión, un usuario de base de datos o un rol de base de datos). Use **REVOCAR** para quitar la concesión o denegación de un permiso.  
  
 Permisos de nivel de servidor se aplican a los inicios de sesión. Permisos de nivel de base de datos se aplican a los usuarios de base de datos y roles de base de datos.  
  
 Para ver qué permisos han sido concedidos y denegados, consulte las vistas de sys.server_permissions y sys.database_permissions. Los permisos que no explícitamente se conceden o deniegan a una entidad de seguridad se pueden heredarlos con pertenencia a un rol que tenga permisos. Los permisos de los roles fijos de base de datos no se puede cambiar y no aparecen en las vistas sys.server_permissions y sys.database_permissions.  
  
-   **GRANT** concede explícitamente uno o varios permisos.  
  
-   **DENY** deniega explícitamente la entidad de seguridad de tener uno o varios permisos.  
  
-   **REVOCAR** quita existente **GRANT** o **DENY** permisos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "icono de vínculo de tema") [convenciones de sintaxis de Transact-SQL &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Azure SQL Data Warehouse and Parallel Data Warehouse  
GRANT   
    <permission> [ ,...n ]  
    [ ON [ <class_type> :: ] securable ]   
    TO principal [ ,...n ]  
    [ WITH GRANT OPTION ]  
[;]  
  
DENY   
    <permission> [ ,...n ]  
    [ ON [ <class_type> :: ] securable ]   
    TO principal [ ,...n ]  
    [ CASCADE ]  
[;]  
  
REVOKE   
    <permission> [ ,...n ]  
    [ ON [ <class_type> :: ] securable ]   
    [ FROM | TO ] principal [ ,...n ]  
    [ CASCADE ]  
[;]  
  
<permission> ::=  
{ see the tables below }  
  
<class_type> ::=  
{  
      LOGIN  
    | DATABASE  
    | OBJECT  
    | ROLE  
    | SCHEMA  
    | USER  
}  
```  
  
## <a name="arguments"></a>Argumentos  
 \<permiso > [ **,**... *n* ]  
 Uno o varios permisos para conceder, denegar o revocar.  
  
 ON [ \<class_type >::] *protegible* el **ON** cláusula describe el parámetro que se puede proteger en el que se va a conceder, denegar o revocar permisos.  
  
 \<class_type > el tipo de clase del elemento protegible. Esto puede ser **inicio de sesión**, **base de datos**, **objeto**, **esquema**, **rol**, o **usuario** . También se pueden conceder permisos a la **SERVER***class_type*, pero **SERVER** no se especifica para esos permisos. **Base de datos** no se especifica si el permiso incluye la palabra **base de datos** (por ejemplo **ALTER ANY DATABASE**). Si no *class_type* se especifica y el tipo de permiso no está restringido en el servidor o la clase de base de datos, se supone que la clase **objeto**.  
  
 *elemento protegible*  
 El nombre del inicio de sesión, base de datos, tabla, vista, esquema, procedimiento, rol o usuario en el que se va a conceder, denegar o revocar permisos. Se puede especificar el nombre del objeto con las reglas de nomenclatura de tres partes que se describen en [convenciones de sintaxis de Transact-SQL &#40; Transact-SQL &#41; ](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
 PARA *principal* [ **,**... *n* ]  
 Una o más entidades que se va a conceder, denegar o revocar permisos. Entidad de seguridad es el nombre de un inicio de sesión, el usuario de base de datos o el rol de base de datos.  
  
 DE *principal* [ **,**... *n* ]  
 Una o más entidades revocar los permisos de.  Entidad de seguridad es el nombre de un inicio de sesión, el usuario de base de datos o el rol de base de datos. **DE** sólo puede utilizarse con un **REVOCAR** instrucción. **PARA** puede utilizarse con **GRANT**, **DENY**, o **REVOCAR**.  
  
 WITH GRANT OPTION  
 Indica que el receptor también podrá conceder el permiso especificado a otras entidades de seguridad.  
  
 CASCADE  
 Indica que el permiso se deniega o revoca para la entidad de seguridad especificada y todas las otras entidades de seguridad a la que la entidad de seguridad concede el permiso. Se requiere si la entidad de seguridad tiene el permiso con **GRANT OPTION**.  
  
 GRANT OPTION FOR  
 Indica que se revocará la capacidad de conceder el permiso especificado. Esto es necesario cuando se utiliza el **CASCADE** argumento.  
  
> [!IMPORTANT]  
>  Si la entidad de seguridad tiene el permiso especificado sin el **GRANT** opción, se revocará el permiso.  
  
## <a name="permissions"></a>Permissions  
 Para conceder un permiso, el Otorgante de permisos debe tener el mismo permiso con la **WITH GRANT OPTION**, o debe tener un permiso superior que implique el permiso que se va a conceder.  Los propietarios de objetos pueden conceder permisos para los objetos que poseen. Entidades de seguridad con **CONTROL** permiso para un elemento protegible puede conceder permisos para ese elemento.  Los miembros de la **db_owner** y **db_securityadmin** roles fijos de base de datos pueden conceder cualquier permiso en la base de datos.  
  
## <a name="general-remarks"></a>Notas generales  
 Denegar o revocar permisos para una entidad de seguridad no afectará a las solicitudes que han pasado la autorización y se está ejecutando actualmente. Para restringir el acceso inmediatamente, debe cancelar las solicitudes activas o eliminar las sesiones actuales.  
  
> [!NOTE]  
>  Funciones más fijas de servidor no están disponibles en esta versión. Usar las funciones de base de datos definido por el usuario en su lugar. Los inicios de sesión no se puede agregar a la **sysadmin** rol fijo de servidor. Conceder el **CONTROL SERVER** permiso se aproxima a la pertenencia a la **sysadmin** rol fijo de servidor.  
  
 Algunas instrucciones requieren varios permisos. Por ejemplo crear una tabla requiere el **CREATE TABLE** permisos en la base de datos y la **ALTER SCHEMA** permiso para la tabla que contendrá la tabla.  
  
 PDW a veces ejecuta los procedimientos almacenados para distribuir las acciones del usuario a los nodos de proceso. Por lo tanto, no se puede denegar el permiso execute para una base de datos completa. (Por ejemplo `DENY EXECUTE ON DATABASE::<name> TO <user>;` se producirá un error.) Como una solución alternativa, denegar el permiso execute para esquemas de usuario u objetos específicos (procedimientos).  
  
### <a name="implicit-and-explicit-permissions"></a>Permisos implícitos y explícitos  
 Un *permiso explícito* es un **GRANT** o **DENY** permiso otorgado a una entidad de seguridad mediante un **GRANT** o **DENY**instrucción.  
  
 Un *permiso implícito* es un **GRANT** o **DENY** permiso que una entidad de seguridad (inicio de sesión, usuario o rol de base de datos) se hereda de otro rol de base de datos.  
  
 También se puede heredar un permiso implícito de una cobertura o el permiso primario. Por ejemplo, **actualización** puedan heredarse los permisos en una tabla manteniendo **actualización** permiso en el esquema que contiene la tabla, o **CONTROL** permiso en la tabla.  
  
### <a name="ownership-chaining"></a>Encadenamiento de propiedad  
 Cuando varios objetos de base de datos tienen acceso entre sí secuencialmente, la secuencia se conoce como un *cadena*. Aunque estas cadenas no existen de manera independiente, cuando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] recorre los eslabones de una cadena, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] evalúa los permisos de los objetos que la componen de manera distinta a si se estuviese obteniendo acceso a los objetos por separado. El encadenamiento de propiedad tiene importantes implicaciones para administrar la seguridad. Para obtener más información sobre cadenas de propiedad, vea [cadenas de propiedad](http://msdn.microsoft.com/en-us/library/ms188676\(v=sql11\).aspx) y [Tutorial: cadenas de propiedad y cambio de contexto](http://msdn.microsoft.com/en-us/library/bb153640\(v=sql11\).aspx).  
  
## <a name="permission-list"></a>Lista de permisos  
  
### <a name="server-level-permissions"></a>Permisos de nivel de servidor  
 Permisos de nivel de servidor concedido, se pueden denegar y revocar desde los inicios de sesión.  
  
 **Permisos que se aplican a los servidores**  
  
-   CONTROL SERVER  
  
-   ADMINISTER BULK OPERATIONS  
  
-   ALTER ANY CONNECTION  
  
-   ALTER ANY DATABASE  
  
-   CREATE ANY DATABASE  
  
-   ALTER ANY EXTERNAL DATA SOURCE  
  
-   ALTER ANY EXTERNAL FILE FORMAT  
  
-   ALTER ANY LOGIN  
  
-   ALTER SERVER STATE  
  
-   CONNECT SQL  
  
-   VIEW ANY DEFINITION  
  
-   VIEW ANY DATABASE  
  
-   VIEW SERVER STATE  
  
 **Permisos que se aplican a los inicios de sesión**  
  
-   CONTROLAR EL INICIO DE SESIÓN  
  
-   ALTER EN EL INICIO DE SESIÓN  
  
-   SUPLANTAR EN INICIO DE SESIÓN  
  
-   VIEW DEFINITION  
  
### <a name="database-level-permissions"></a>Permisos de nivel de base de datos  
 Permisos de nivel de base de datos pueden tener, denegado y revocados de usuarios de base de datos y roles de base de datos definido por el usuario.  
  
 **Permisos que se aplican a todas las clases de base de datos**  
  
-   CONTROL  
  
-   ALTER  
  
-   VIEW DEFINITION  
  
 **Permisos que se aplican a todas las clases de base de datos excepto a los usuarios**  
  
-   TAKE OWNERSHIP  
  
 **Permisos que se aplican únicamente a las bases de datos**  
  
-   ALTER ANY DATABASE  
  
-   ALTER EN LA BASE DE DATOS  
  
-   ALTER ANY DATASPACE  
  
-   ALTER ANY ROLE  
  
-   ALTER ANY SCHEMA  
  
-   ALTER ANY USER  
  
-   BACKUP DATABASE  
  
-   CONECTARSE A LA BASE DE DATOS  
  
-   CREATE PROCEDURE  
  
-   CREATE ROLE  
  
-   CREATE SCHEMA  
  
-   CREATE TABLE  
  
-   CREATE VIEW  
  
-   SHOWPLAN  
  
 **Permisos que se aplican únicamente a los usuarios**  
  
-   IMPERSONATE  
  
 **Permisos que se aplican a las bases de datos, esquemas y objetos**  
  
-   ALTER  
  
-   DELETE  
  
-   EXECUTE  
  
-   INSERT  
  
-   SELECT  
  
-   UPDATE  
  
-   REFRENCES  
  
 Para una definición de cada tipo de permiso, vea [permisos (motor de base de datos)](http://msdn.microsoft.com/library/ms191291.aspx).  
  
### <a name="chart-of-permissions"></a>Gráfico de permisos  
 Todos los permisos se representan gráficamente en este póster. Se trata de la manera más fácil de Ver jerarquía anidada de permisos. Por ejemplo la **ALTER LOGIN de ON** permiso se puede conceder por sí mismo, pero también se incluye si se concede un inicio de sesión el **CONTROL** permiso ese inicio de sesión, o si un inicio de sesión se le concede la **ALTER ANY Inicio de sesión** permiso.  
  
 ![Póster de permisos de seguridad APS](../../t-sql/statements/media/aps-security-perms-poster.png "póster de permisos de seguridad APS")  
  
 Para descargar una versión de tamaño completo de este póster, consulte [permisos de SQL Server PDW](http://go.microsoft.com/fwlink/?LinkId=244249)en la sección de archivos del sitio de Yammer de APS (o una solicitud por correo electrónico desde  **apsdoc@microsoft.com** .  
  
## <a name="default-permissions"></a>Permisos predeterminados  
 En la lista siguiente se describe los permisos predeterminados:  
  
-   Cuando se crea un inicio de sesión mediante el uso de la **CREATE LOGIN** instrucción nuevo inicio de sesión recibe el **CONNECT SQL** permiso.  
  
-   Todos los inicios de sesión son miembros de la **público** rol de servidor y no se puede quitar **público**.  
  
-   Cuando se crea un usuario de base de datos mediante el uso de la **CREATE USER** permiso, el usuario de base de datos recibe la **conectar** permiso en la base de datos.  
  
-   Todas las entidades, incluido el **público** rol, no tener ningún permiso explícito o implícito de forma predeterminada.  
  
-   Cuando un inicio de sesión o usuario se convierte en el propietario de un objeto o base de datos, el inicio de sesión o el usuario siempre tendrá todos los permisos en la base de datos o el objeto. Los permisos de la propiedad no se puede cambiar y no están visibles como permisos explícitos. El **GRANT**, **DENY**, y **REVOCAR** instrucciones no tienen ningún efecto en los propietarios.  
  
-   El **sa** inicio de sesión tiene todos los permisos en el dispositivo. Similar a los permisos de la propiedad, el **sa** permisos no se puede cambiar y no están visibles como permisos explícitos. El **GRANT**, **DENY**, y **REVOCAR** instrucciones no tienen ningún efecto **sa** inicio de sesión. El **sa** no se puede cambiar el nombre de inicio de sesión.  
  
-   El **USE** instrucción no requiere permisos. Pueden ejecutar todas las entidades del **USE** instrucción en cualquier base de datos.  
  
##  <a name="Examples"></a>Ejemplos: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-granting-a-server-level-permission-to-a-login"></a>A. Conceder un permiso de nivel de servidor a un inicio de sesión  
 Las dos instrucciones siguientes conceder un permiso de nivel de servidor a un inicio de sesión.  
  
```  
GRANT CONTROL SERVER TO [Ted];  
```  
  
```  
GRANT ALTER ANY DATABASE TO Mary;  
```  
  
### <a name="b-granting-a-server-level-permission-to-a-login"></a>B. Conceder un permiso de nivel de servidor a un inicio de sesión  
 El siguiente ejemplo concede un permiso de nivel de servidor en un inicio de sesión a un servidor principal (otro inicio de sesión).  
  
```  
GRANT  VIEW DEFINITION ON LOGIN::Ted TO Mary;  
```  
  
### <a name="c-granting-a-database-level-permission-to-a-user"></a>C. Conceder un permiso de nivel de base de datos a un usuario  
 El siguiente ejemplo concede un permiso de nivel de base de datos un usuario a una base de datos principal (otro usuario).  
  
```  
GRANT VIEW DEFINITION ON USER::[Ted] TO Mary;  
```  
  
### <a name="d-granting-denying-and-revoking-a-schema-permission"></a>D. Conceder, denegar y revocar un permiso de esquema  
 El siguiente **GRANT** instrucción concede Yuen la capacidad de seleccionar datos de cualquier tabla o vista en el esquema dbo.  
  
```  
GRANT SELECT ON SCHEMA::dbo TO [Yuen];  
```  
  
 El siguiente **DENY** instrucción impide que Yuen seleccionar datos de cualquier tabla o vista en el esquema dbo. Yuen no puede leer los datos, incluso si tiene permiso de alguna otra manera, como a través de una pertenencia a una función.  
  
```  
DENY SELECT ON SCHEMA::dbo TO [Yuen];  
```  
  
 El siguiente **REVOCAR** instrucción quita la **DENY** permiso. Ahora los permisos explícitos del Yuen son neutros. Yuen puede seleccionar datos de cualquier tabla a través de algunas otras permisos implícita como una pertenencia a una función.  
  
```  
REVOKE SELECT ON SCHEMA::dbo TO [Yuen];  
```  
  
### <a name="e-demonstrating-the-optional-object-clause"></a>E. Que muestra el objeto opcional:: cláusula  
 Dado que OBJECT es la clase de valor predeterminado para una instrucción de permiso, las dos instrucciones siguientes son los mismos. El **objeto::** cláusula es opcional.  
  
```  
GRANT UPDATE ON OBJECT::dbo.StatusTable TO [Ted];  
```  
  
```  
GRANT UPDATE ON dbo.StatusTable TO [Ted];  
```  
  
  

