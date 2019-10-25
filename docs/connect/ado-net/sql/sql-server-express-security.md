---
title: Seguridad de SQL Server Express
description: Describe cuestiones de seguridad relacionadas con SQL Server Express.
ms.date: 09/26/2019
ms.assetid: cf9cf6d9-4b05-43e9-ac7b-6cefbfcd6d4e
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 9d6b711109f7d94e3bca8d9cf2bda6d2c124c798
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452020"
---
# <a name="sql-server-express-security"></a>Seguridad de SQL Server Express

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Descargar ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Microsoft SQL Server Express Edition (SQL Server Express) se basa en Microsoft SQL Server y es compatible con la mayoría de las características del motor de base de datos. Está diseñado para que las características no esenciales y la conectividad de red estén desactivadas de forma predeterminada. Esto reduce el área expuesta disponible para los ataques por parte de un usuario malintencionado.  
  
Normalmente SQL Server Express se instala como una instancia con nombre. El nombre predeterminado de la instancia es `SQLExpress`. Una instancia con nombre se identifica mediante el nombre de red del equipo más el nombre de instancia que especifique durante la instalación.  
  
## <a name="network-access"></a>Acceso de red  
Por razones de seguridad, los protocolos de red están deshabilitados de forma predeterminada en SQL Server Express. Esto evita ataques de usuarios externos que podrían poner en peligro el equipo que hospeda la instancia de SQL Server Express. Debe habilitar explícitamente la conectividad de red e iniciar el servicio SQL Server Browser para conectarse a una instancia de SQL Server Express desde otro equipo.  
  
Una vez habilitada la conectividad de red, una instancia de SQL Server Express tiene los mismos requisitos de seguridad que las otras ediciones de SQL Server.  
  
## <a name="user-instances"></a>Instancias de usuario  
Una instancia de usuario es una instancia independiente del motor de base de datos de SQL Server Express generada por una instancia primaria de SQL Server Express. El objetivo principal de una instancia de usuario es permitir a los usuarios que ejecutan Windows con una cuenta de usuario con privilegios mínimos tener privilegios de administrador del sistema (`sysadmin`) en la instancia de SQL Server Express en su equipo local. Las instancias de usuario no están destinadas a los usuarios que son administradores del sistema en sus propios equipos.  
  
Una instancia de usuario se genera a partir de una instancia principal de SQL Server o SQL Server Express en nombre de un usuario. Se ejecuta como un proceso de usuario en el contexto de seguridad de Windows del usuario, no como un servicio. No se permiten los inicios de sesión de SQL Server. solo se admiten inicios de sesión de Windows. Esto evita que el software que se ejecuta en una instancia de usuario realice cambios en todo el sistema para los que el usuario no tendría permisos. Una instancia de usuario también se conoce como instancia secundaria o de cliente y a veces se hace referencia a ella mediante el acrónimo RANU ("ejecutar como usuario normal").  
  
Cada instancia de usuario está aislada de su instancia primaria y de otras instancias de usuario que se ejecutan en el mismo equipo. Las bases de datos instaladas en instancias de usuario se abren solo en modo de usuario único; varios usuarios no se pueden conectar a ellos. La replicación, las consultas distribuidas y las conexiones remotas están deshabilitadas para las instancias de usuario. Cuando se conecta a una instancia de usuario, los usuarios no tienen ningún privilegio especial en la instancia de SQL Server Express primaria.  
  
## <a name="external-resources"></a>Recursos externos  
Para obtener más información acerca de SQL Server Express, vea los siguientes recursos.  
  
|||  
|-|-|  
|[Libros en pantalla de Microsoft SQL Server 2005 Express Edition](https://docs.microsoft.com/previous-versions/sql/sql-server-2005/ms165706(v=sql.90))|Documentación completa de SQL Server 2005 Express Edition.|  
|[Instancias de usuario para usuarios que no son administradores](https://docs.microsoft.com/previous-versions/sql/sql-server-2008/ms143684(v=sql.100)) en los Libros en pantalla de SQL Server|Describe cómo crear e implementar instancias de usuario.|  
|[Instancias de usuario de SQL Server Express](sql-server-express-user-instances.md)|Describe las capacidades de la instancia de usuario en una aplicación ADO.NET. Proporciona información sobre cómo habilitar una instancia de usuario, conectarse a una instancia de usuario mediante un <xref:Microsoft.Data.SqlClient.SqlConnection>, la duración de la instancia de usuario y escenarios de instancias de usuario.|  
  
## <a name="next-steps"></a>Pasos siguientes
- [Seguridad de SQL Server](sql-server-security.md)
- [Instancias de usuario de SQL Server Express](sql-server-express-user-instances.md)
