---
title: Roles de Integration Services (servicio SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- security [Integration Services], roles
- db_ssisoperator role
- db_ssisadmin role
- fixed database roles [Integration Services]
- packages [Integration Services], security
- roles [Integration Services]
- db_ssisltduser role
ms.assetid: 9702e90c-fada-4978-a473-1b1423017d80
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: aa7e52cd88e4eb07c0df515ebba3e10284be02b1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48132425"
---
# <a name="integration-services-roles-ssis-service"></a>Roles de Integration Services (servicio SSIS)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] incluye los tres roles fijos de nivel de base de datos, `db_ssisadmin`, **db_ssisltduser**, y **db_ssisoperator**, para controlar el acceso a los paquetes. Los roles se pueden implementar solo en los paquetes que se guardan en el `msdb` en la base de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para asignar roles a un paquete se utiliza [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Las asignaciones de roles se guardan en el `msdb` base de datos.  
  
## <a name="read-and-write-actions"></a>Acciones de lectura y escritura  
 En la tabla siguiente se describen las acciones de lectura y escritura de Windows y los roles fijos de nivel de base de datos en [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
|Rol|Acción de lectura|Acción de escritura|  
|----------|-----------------|------------------|  
|`db_ssisadmin`<br /><br /> o Administrador de configuración de<br /><br /> `sysadmin`|Enumerar los paquetes propios.<br /><br /> Enumerar todos los paquetes.<br /><br /> Ver los paquetes propios.<br /><br /> Ver todos los paquetes.<br /><br /> Ejecutar los paquetes propios.<br /><br /> Ejecutar todos los paquetes.<br /><br /> Exportar los paquetes propios.<br /><br /> Exportar todos los paquetes.<br /><br /> Ejecutar todos los paquetes del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|Importar paquetes.<br /><br /> Eliminar los paquetes propios.<br /><br /> Eliminar todos los paquetes.<br /><br /> Cambiar los roles de los paquetes propios.<br /><br /> Cambiar los roles de todos los paquetes.<br /><br /> <br /><br /> **\*\* Importante \* \***  los miembros del rol db_ssisadmin y del rol dc_admin quizá puedan elevar sus privilegios a sysadmin. Esta elevación de privilegio se puede producir porque estos roles pueden modificar los paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y los paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] los puede ejecutar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizando el contexto de seguridad de sysadmin del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para protegerse contra esta elevación de privilegio al ejecutar planes de mantenimiento, conjuntos de recopilación de datos y otros paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , configure los trabajos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que ejecutan paquetes para utilizar una cuenta de proxy con privilegios limitados o agregar solo los miembros de sysadmin a los roles dc_admin y db_ssisadmin.|  
|**db_ssisltduser**|Enumerar los paquetes propios.<br /><br /> Enumerar todos los paquetes.<br /><br /> Ver los paquetes propios.<br /><br /> Ejecutar los paquetes propios.<br /><br /> Exportar los paquetes propios.|Importar paquetes.<br /><br /> Eliminar los paquetes propios.<br /><br /> Cambiar los roles de los paquetes propios.|  
|**db_ssisoperator**|Enumerar todos los paquetes.<br /><br /> Ver todos los paquetes.<br /><br /> Ejecutar todos los paquetes.<br /><br /> Exportar todos los paquetes.<br /><br /> Ejecutar todos los paquetes del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|None|  
|**Administradores de Windows**|Ver los detalles de ejecución de todos los paquetes que se están ejecutando.|Detener todos los paquetes en ejecución en ese momento.|  
  
## <a name="sysssispackages-table"></a>Tabla Sysssispackages  
 El **sysssispackages** tabla `msdb` contiene los paquetes que se guardan en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, vea [sysssispackages &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/sysssispackages-transact-sql).  
  
 La tabla **sysssispackages** incluye columnas que contienen información sobre los roles asignados a los paquetes.  
  
-   La columna **readerrole** especifica el rol que tiene acceso de lectura al paquete.  
  
-   La columna **writerrole** especifica el rol que tiene acceso de escritura al paquete.  
  
-   La columna **ownersid** contiene el identificador de seguridad único del usuario que creó el paquete. Esta columna define el propietario del paquete.  
  
## <a name="permissions"></a>Permisos  
 De forma predeterminada, los permisos de la `db_ssisadmin` y **db_ssisoperator** roles fijos de nivel de base de datos y el identificador de seguridad único del usuario que creó el paquete se aplican al rol lector para paquetes y los permisos de el `db_ssisadmin` rol y el identificador de seguridad único del usuario que creó el paquete se aplican al rol de escritor. Un usuario debe ser miembro de la `db_ssisadmin`, **db_ssisltduser**, o **db_ssisoperator** rol para tener acceso de lectura al paquete. Un usuario debe ser miembro de la `db_ssisadmin` rol para tener acceso de escritura.  
  
## <a name="access-to-packages"></a>Acceso a paquetes  
 Los roles fijos de nivel de base de datos trabajan conjuntamente con los roles definidos por el usuario. Los roles definidos por el usuario son los que se crean en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y posteriormente se usan para asignar permisos a los paquetes. Para tener acceso a un paquete, un usuario debe ser miembro del rol definido por el usuario y del rol fijo de nivel de base de datos [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] pertinente. Por ejemplo, si los usuarios son miembros de la **AuditUsers** rol definido por el usuario que se asigna a un paquete, también deben ser miembros de `db_ssisadmin`, **db_ssisltduser**, o **db_ ssisoperator** rol para tener acceso de lectura al paquete.  
  
 Si no asigna roles definidos por el usuario a los paquetes, el acceso a dichos paquetes se determina con los roles fijos de nivel de base de datos.  
  
 Si desea usar las funciones definidas por el usuario, debe agregarlos a la `msdb` antes de poder asignar a los paquetes de la base de datos. Puede crear roles de base de datos en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 Los roles de nivel de base de datos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] conceden derechos sobre las tablas del sistema de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en la base de datos msdb.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe iniciarse (el servicio MSSQLSERVER) antes de poder conectarse al motor de base de datos y acceso el `msdb` base de datos.  
  
 Para asignar roles a paquetes, debe completar las tareas siguientes.  
  
-   **Abrir el Explorador de objetos y conectarse a Integration Services**  
  
     Antes de asignar roles a los paquetes con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], debe abrir el Explorador de objetos en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y conectarse a [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
     Debe iniciar el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] antes de conectarse a [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
-   **Asignar roles de lector y escritor a los paquetes**  
  
     Puede asignar un rol de lector y un rol de escritor a cada paquete.  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Asignar roles de lector y escritor a un paquete](../assign-a-reader-and-writer-role-to-a-package.md)  
  
-   [Crear un rol definido por el usuario](../create-a-user-defined-role.md)  
  
-   [Conectarse a Integration Services](../connect-to-integration-services.md)  
  
  
