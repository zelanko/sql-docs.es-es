---
title: Administración del acceso al clúster de macrodatos en el modo de Active Directory
description: Administración del acceso al clúster de macrodatos
author: NelGson
ms.author: negust
ms.reviewer: mikeray
ms.date: 12/06/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9f9cca7e761b8f8ec3f5b87e9a195a0eb8b5da6d
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "76259463"
---
# <a name="manage-big-data-cluster-access-in-active-directory-mode"></a>Administración del acceso al clúster de macrodatos en el modo de Active Directory

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se describe cómo actualizar los grupos de Active Directory que se proporcionan durante la implementación para clusterAdmins y clusterUsers.

## <a name="two-overarching-roles-in-the-big-data-cluster"></a>Dos roles generales en el clúster de macrodatos

Los grupos de Active Directory se pueden proporcionar en la sección de seguridad del perfil de implementación como parte de dos roles generales para la autorización dentro del clúster de macrodatos:

* `clusterAdmins`: este parámetro toma un grupo de Active Directory. Los miembros de este grupo obtienen permisos de administrador para todo el clúster. Tienen permisos de *sysadmin* en SQL Server, permisos de *superuser* en el Sistema de archivos distribuido Hadoop (HDFS) y Spark y derechos de *administrador* en el controlador.

* `clusterUsers`: estos grupos de Active Directory son usuarios normales sin permisos de administrador en el clúster. Tienen permisos para iniciar sesión en la instancia maestra de SQL Server pero, de forma predeterminada, no tienen permisos para los objetos o los datos.

Una manera de conceder permisos de grupos de Active Directory adicionales al clúster de macrodatos después de la implementación es agregar usuarios y grupos adicionales a los grupos ya designados durante la implementación. 

Sin embargo, puede que no siempre sea factible que los administradores modifiquen las pertenencias a grupos dentro de Active Directory. Para conceder permisos de grupos de Active Directory adicionales sin modificar las pertenencias a grupos en Active Directory, complete los procedimientos que aparecen en las secciones siguientes.

## <a name="grant-administrator-permissions-to-additional-active-directory-groups"></a>Concesión de permisos de administrador a grupos de Active Directory adicionales

>[!IMPORTANT]
>Este procedimiento no concede a los grupos de Active Directory adicionales acceso de administrador a los componentes de Hadoop, como HDFS y Spark, en el clúster de macrodatos. Estos componentes solo permiten un grupo de Active Directory como grupo de superusuario. Esta restricción significa que el grupo que se especifica en `clusterAdmins` durante la implementación sigue siendo el grupo de superusuario, incluso después de este paso.

Al seguir los procedimientos de esta sección, puede conceder acceso de administrador tanto al controlador como a la instancia maestra de SQL Server.

### <a name="create-a-login-for-the-active-directory-user-or-group-in-the-sql-server-master-instance"></a>Creación de un inicio de sesión para el usuario o el grupo de Active Directory en la instancia maestra de SQL Server 

1. Conéctese al punto de conexión de SQL maestro mediante su cliente SQL favorito. Use cualquier inicio de sesión de administrador (por ejemplo, `AZDATA_USERNAME`, que se proporcionó durante la implementación). Como alternativa, podría ser cualquier cuenta de Active Directory que pertenezca al grupo de Active Directory que se proporciona como `clusterAdmins` en la configuración de seguridad.

1. Para crear un inicio de sesión para el usuario o grupo de Active Directory, ejecute el comando TSQL siguiente:

   ```sql
   CREATE LOGIN [<domain>\<principal>] FROM WINDOWS;
   ```

   Si va a conceder permisos de administrador en la instancia de SQL Server, conceda también el permiso siguiente:

   ```sql
   ALTER SERVER ROLE sysadmin ADD MEMBER [<domain>\<principal>];
   GO
   ```

### <a name="add-the-active-directory-user-or-group-to-the-roles-table-in-the-controller-database"></a>Incorporación del usuario o grupo de Active Directory a la tabla de roles en la base de datos del controlador 

1. Ejecute estos comandos para obtener las credenciales de SQL Server del controlador:

   a. Ejecute este comando como administrador de Kubernetes:

   ```bash
   kubectl get secret controller-sa-secret -n <cluster name> -o yaml | grep password
   ```

   b. Descodifique el secreto en Base64:

   ```bash
   echo <password from kubectl command>  | base64 --decode && echo
   ```

1. En una ventana de comandos independiente, exponga el puerto del servidor de base de datos del controlador:

   ```bash
   kubectl port-forward controldb-0 1433:1433 --address 0.0.0.0 -n <cluster name>
   ```

1. Use la conexión anterior para insertar una fila en la tabla de roles. Escriba el valor *REALM* en mayúsculas.

   Si va a conceder permisos de administrador, use el rol *bdcAdmin* en el *\<nombre del rol>* . Para los usuarios que no son administradores, use el rol *bdcUser*.

   ```sql
   USE controller;
   GO

   INSERT INTO [controller].[auth].[roles] VALUES (N'<user or group name>@<REALM>', N'<role name>')
   GO
   ```

1. Para comprobar que los miembros del grupo que ha agregado tienen permisos de administrador de clúster de macrodatos, inicie sesión en el punto de conexión del controlador y ejecute el comando siguiente:

   ```bash
   azdata bdc config show
   ```

1. Para los usuarios que no son administradores, puede comprobar el acceso mediante la autenticación en la instancia maestra de SQL o en el controlador mediante `azdata login`.

## <a name="next-steps"></a>Pasos siguientes

- [Conceptos de seguridad de los Clústeres de macrodatos de SQL Server 2019](concept-security.md)
