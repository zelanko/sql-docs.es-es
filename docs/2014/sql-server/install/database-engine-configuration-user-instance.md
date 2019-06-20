---
title: Instancia de usuario - Configuración del motor de base de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- database engine configuration
- database engine configuration, user instance
ms.assetid: dfc27c1e-0fe2-4221-bed5-f52667ddd3c8
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ba05d426f9515793ad3a924e375ff9a6ab9f940f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66095878"
---
# <a name="database-engine-configuration---user-instance"></a>Configuración del motor de base de datos - Instancia de usuario
  Utilice la página **Instancia de usuario** para generar una instancia independiente de [!INCLUDE[ssDE](../../includes/ssde-md.md)] para usuarios sin permisos de administrador, y para agregar usuarios al rol Administrador.  
  
## <a name="option"></a>Opción  
 Habilitar instancias de usuario  
 La opción predeterminada es activado. Para deshabilitar la funcionalidad de habilitar instancias de usuario, desactive la casilla.  
  
 La instancia de usuario, también denominada instancia secundaria o cliente, es una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] generada por la instancia primaria (la instancia principal que se ejecuta como servicio, como [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]) en nombre de un usuario. La instancia de usuario se ejecuta como un proceso de usuario en el contexto de seguridad de dicho usuario. La instancia de usuario está aislada de la instancia primaria y de las demás instancias de usuario que se ejecutan en el equipo. La característica de instancias de usuario también se denomina "Ejecutar como usuario normal" (RANU).  
  
> [!NOTE]  
>  Los inicios de sesión suministrados como miembros del rol fijo de servidor **sysadmin** durante la instalación se suministran como administradores en la base de datos de plantilla. Son miembros del rol fijo de servidor **sysadmin** en la instancia de usuario a menos que se quiten.  
  
 Agregar usuario al rol Administrador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 De forma predeterminada, esta casilla está desactivada. Para agregar el usuario del programa de instalación actual al rol Administrador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , active la casilla.  
  
 Los usuarios de [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] que sean miembros de BUILTIN\Administradores no se agregan automáticamente al rol fijo de servidor sysadmin al conectarse a [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)]. Solo los usuarios de [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] que se hayan agregado de forma explícita a un rol Administrador de servidor pueden administrar [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]. Cualquier miembro del grupo BUILTIN\Users se puede conectar a la instancia de [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] , pero tendrá permisos limitados para realizar tareas de base de datos. Por este motivo, a los usuarios que hereden los privilegios de [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] de los grupos BUILTIN\Administrators y BUILTIN\Users de versiones anteriores de Windows se les debe conceder de forma explícita privilegios administrativos a las instancias de [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] que se ejecuten en [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)].  
  
 Para realizar cambios en los roles de usuario una vez finalizado este programa de instalación, utilice la Herramienta de configuración de área expuesta (SQLSAC.exe) de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] . Para actualizar la lista de usuarios del rol Administrador del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , haga clic en el vínculo **Agregar nuevo administrador** .  
  
 Asegúrese de que en el campo **Usuario para aprovisionar** aparezca el nombreDeDominio\nombreDeUsuario del usuario cuyos permisos se deben actualizar. Seleccione el rol que se debe actualizar en la lista de instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del panel **Privilegios disponibles** y, a continuación, haga clic en la flecha que señala a la derecha. Para agregar el usuario a todos los roles disponibles para todas las instancias disponibles de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y todos los roles disponibles, haga clic en la flecha doble que señala a la derecha.  
  
 Para implementar los cambios una vez completadas las selecciones, [!INCLUDE[clickOK](../../includes/clickok-md.md)]. Para cerrar la herramienta sin realizar cambios, haga clic en **Cancelar**.  
  
  
