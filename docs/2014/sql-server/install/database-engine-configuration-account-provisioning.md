---
title: Configuración del motor de base de datos - aprovisionamiento de cuentas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 834b26bc-49de-4033-88d5-6aa7b1609720
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 69885ad9affb87ea160231fa6f6d42d0fef7ea6c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48099055"
---
# <a name="database-engine-configuration---account-provisioning"></a>Configuración del motor de base de datos - Aprovisionamiento de cuentas
  Use esta página para establecer el modo de seguridad en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , así como para agregar grupos o usuarios de Windows como administradores de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
## <a name="considerations-for-running-includesscurrentincludessscurrent-mdmd"></a>Consideraciones para ejecutar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 En versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se aprovisionaba el grupo **BUILTIN\Administrators** como posibilidad en el inicio de sesión de [!INCLUDE[ssDE](../../includes/ssde-md.md)] y los miembros del grupo local Administradores podían iniciar sesión con sus credenciales de administrador. El uso de permisos elevados no es una práctica recomendada. En [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , el grupo **BUILTIN\Administrators** no se aprovisiona como inicio de sesión. En consecuencia, debería crear un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para cada usuario administrativo y agregarlo al rol fijo de servidor sysadmin durante la instalación de una nueva instancia de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. También debe hacer esto para las cuentas de Windows que se utilizan para ejecutar trabajos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . También se incluyen las cuentas utilizadas para ejecutar trabajos del Agente de replicación.  
  
## <a name="options"></a>Opciones  
 **Modo de seguridad** : seleccione la autenticación de Windows o la autenticación de modo mixto para la instalación.  
  
 **Aprovisionamiento de entidad de seguridad de Windows** : en las versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el grupo local Windows Builtin\Administrator estaba ubicado en el rol de servidor sysadmin de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , con lo que se concedía a los administradores de Windows acceso a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. En [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], el grupo Builtin\Administrator no se proporciona en el rol de servidor sysadmin. En su lugar, debería aprovisionar explícitamente administradores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para las nuevas instalaciones durante la instalación.  
  
> [!IMPORTANT]  
>  Debe aprovisionar explícitamente administradores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para las nuevas instalaciones durante la instalación. El programa de instalación no le permitirá continuar hasta que complete este paso.  
  
 **Especificar administradores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**: debe especificar por lo menos una entidad de seguridad de Windows para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para agregar la cuenta en la que se ejecuta el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , haga clic en el botón **Usuario actual** . Para agregar o quitar cuentas de la lista de administradores del sistema, haga clic en **Agregar** o en **Quitar**y, a continuación, edite la lista de usuarios, grupos o equipos que tendrán privilegios de administrador para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Cuando termine de modificar la lista, haga clic en **Aceptar**y, a continuación, compruebe la lista de administradores en el cuadro de diálogo de configuración. Cuando la lista esté completa, haga clic en **Siguiente**.  
  
 Si selecciona la autenticación de modo mixto, debe proporcionar las credenciales de inicio de sesión para la cuenta de administrador de sistema (SA) de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] builtin.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
 **Modo de autenticación de Windows**  
 Cuando un usuario se conecta a través de una cuenta de usuario de Microsoft Windows, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] valida el nombre de cuenta y la contraseña con el token de la entidad de seguridad de Windows del sistema operativo. Éste es el modo de autenticación predeterminado, y es mucho más seguro que el modo mixto. La autenticación de Windows utiliza el protocolo de seguridad Kerberos, cumple la directiva de contraseñas en lo que respecta a la validación de la complejidad de las contraseñas seguras, y permite el bloqueo de las cuentas y la expiración de las contraseñas.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)] No establezca nunca una contraseña en blanco o no segura.  
  
 **Modo mixto (autenticación de Windows o autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])**  
 Permite a los usuarios conectarse con la autenticación de Windows o la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Los usuarios que se conectan mediante una cuenta de usuario de Windows pueden usar conexiones de confianza validadas por Windows.  
  
 Si tiene que elegir el modo de autenticación mixto y necesita utilizar inicios de sesión de SQL para incluir aplicaciones heredadas, debe establecer contraseñas seguras para todas las cuentas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  La autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se proporciona únicamente por motivos de compatibilidad con versiones anteriores. [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 **Escribir contraseña**  
 Escriba y confirme el inicio de sesión del administrador del sistema (sa). Las contraseñas son la primera línea de defensa contra los intrusos, por lo que establecer contraseñas seguras es esencial para la seguridad del sistema. No establezca nunca una contraseña en blanco o no segura.  
  
> [!NOTE]  
>  Las contraseñas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueden contener de 1 a 128 caracteres, incluida cualquier combinación de letras, símbolos y números. Si elige la autenticación de modo mixto, debe escribir una contraseña de sa segura antes de continuar con la siguiente página del Asistente para la instalación.  
  
 **Directrices para contraseñas seguras**  
 Las contraseñas seguras no pueden ser adivinadas con facilidad y tampoco son fácilmente vulnerables en caso de utilizar un programa informático. Las contraseñas seguras no pueden utilizar los siguientes términos o condiciones prohibidos:  
  
-   Una condición en blanco o NULL  
  
-   "Password"  
  
-   "Admin"  
  
-   "Administrator"  
  
-   "sa"  
  
-   "sysadmin"  
  
 Una contraseña segura no puede ser ninguno de los siguientes términos asociados al equipo de instalación:  
  
-   El nombre del usuario que haya iniciado actualmente la sesión en el equipo.  
  
-   El nombre del equipo.  
  
 Una contraseña segura debe tener más de 8 caracteres de longitud y satisfacer al menos tres de los siguientes criterios:  
  
-   Debe contener letras mayúsculas.  
  
-   Debe contener letras minúsculas.  
  
-   Debe contener números.  
  
-   Debe contener caracteres no alfanuméricos; por ejemplo, #, %, o ^.  
  
 Las contraseñas que se escriben en esta página deben cumplir los requisitos de las directivas de contraseñas seguras. Si tiene alguna automatización que use la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , asegúrese de que la contraseña cumple los requisitos de las directivas de contraseñas seguras.  
  
## <a name="related-content"></a>Contenido relacionado  
 Para más información sobre elegir la autenticación de Windows en lugar de la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea el tema **Elegir un modo de autenticación** en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para más información sobre elegir una cuenta para ejecutar [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], vea el tema **Configurar los permisos y las cuentas de servicio de Windows** en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] libros en pantalla.  
  
## <a name="see-also"></a>Vea también  
 [Configurar los permisos y las cuentas de servicio de Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)  
  
  
