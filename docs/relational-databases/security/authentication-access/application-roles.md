---
title: Roles de aplicación | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- application roles [SQL Server], about application roles
- principals [SQL Server], application roles
- credentials [SQL Server], roles
- application roles [SQL Server]
- roles [SQL Server], application
- permissions [SQL Server], roles
- users [SQL Server], application roles
- authentication [SQL Server], roles
- groups [SQL Server], roles
ms.assetid: dca18b8a-ca03-4b7f-9a46-8474d5b66f76
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 15a37c87808b5b44d59a243b2bff57ce6db5de25
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "72903789"
---
# <a name="application-roles"></a>Roles de la aplicación
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Un rol de aplicación es una entidad de seguridad de base de datos que permite que una aplicación se ejecute con sus propios permisos de usuario. Puede utilizar los roles de aplicación para permitir el acceso a datos específicos únicamente a aquellos usuarios que se conecten a través de una aplicación concreta. A diferencia de los roles de base de datos, los roles de aplicación no contienen miembros y están inactivos de manera predeterminada. Los roles de aplicación se habilitan empleando **sp_setapprole**, que requiere una contraseña. Debido a que los roles de aplicación son una entidad de seguridad de la base de datos, solo pueden obtener acceso a otras bases de datos por medio de los permisos que se conceden para dichas bases de datos a **guest**. Por tanto, cualquier base de datos en la que se haya deshabilitado **guest** no será accesible para los roles de aplicación de otras bases de datos.  
  
 En [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], los roles de aplicación no pueden tener acceso a los metadatos de nivel de servidor porque no están asociadas a una entidad de seguridad a nivel de servidor. Para deshabilitar esta restricción y permitir a los roles de aplicación tener acceso a los metadatos de nivel de servidor, defina la marca global 4616. Para obtener más información, vea [Marcas de seguimiento &#40;Transact-SQL&#41;](../../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) y [DBCC TRACEON &#40;Transact-SQL&#41;](../../../t-sql/database-console-commands/dbcc-traceon-transact-sql.md).  
  
## <a name="connecting-with-an-application-role"></a>Conectarse con un rol de aplicación  
 Los siguientes pasos muestran el proceso mediante el cual un rol de aplicación cambia de contexto de seguridad:  
  
1.  Un usuario ejecuta una aplicación cliente.  
  
2.  La aplicación cliente se conecta con una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como usuario.  
  
3.  Tras ello, la aplicación ejecuta el procedimiento almacenado **sp_setapprole** con una contraseña que solo conoce la aplicación.  
  
4.  Si el nombre y la contraseña del rol de aplicación son válidos, el rol de aplicación se habilita.  
  
5.  En este momento, la conexión pierde los permisos del usuario y asume los permisos del rol de aplicación.  

 Los permisos adquiridos durante el rol de aplicación se mantienen mientras dura la conexión.  
  
 En versiones anteriores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], la única forma de que un usuario vuelva a adquirir su contexto de seguridad original después de iniciar un rol de aplicación consiste en desconectarse y volver a conectarse a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. A partir de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], **sp_setapprole** tiene una opción que crea una cookie. La cookie contiene información sobre el contexto anterior al momento en que se habilita el rol de aplicación. **sp_unsetapprole** puede usar la cookie para revertir la sesión a su contexto original. Para obtener más información sobre esta nueva opción y obtener un ejemplo, vea [sp_setapprole &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md).  
  
> [!IMPORTANT]  
>  **SqlClient** no admite la opción **encrypt**de ODBC. Cuando transmita información confidencial a través de una red, utilice SSL (Capa de sockets seguros) o IPSec para cifrar el canal. Si necesita conservar las credenciales de la aplicación cliente, cífrelas mediante las funciones de la API de criptografía. En [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] y versiones posteriores, el parámetro *password* se almacena como un hash unidireccional.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|||  
|-|-|  
|Crear un rol de aplicación.|[Crear un rol de aplicación](../../../relational-databases/security/authentication-access/create-an-application-role.md) y [CREATE APPLICATION ROLE &#40;Transact-SQL&#41;](../../../t-sql/statements/create-application-role-transact-sql.md)|  
|Modificar un rol de aplicación.|[ALTER APPLICATION ROLE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-application-role-transact-sql.md)|  
|Eliminar un rol de aplicación.|[DROP APPLICATION ROLE &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-application-role-transact-sql.md)|  
|Usar un rol de aplicación.|[sp_setapprole &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Proteger SQL Server](../../../relational-databases/security/securing-sql-server.md)  
  
  
