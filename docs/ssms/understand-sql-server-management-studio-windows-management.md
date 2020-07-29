---
title: Descripción de la administración de ventanas de SQL Server Management Studio
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- autohide [SQL Server Management Studio]
- SQL Server Management Studio [SQL Server], tool windows
- push pin [SQL Server Management Studio]
- tool windows [SQL Server Management Studio]
ms.assetid: bebf8383-dcaf-466e-84f5-63b81c9cfe52
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ee287295ca0d1e9912f5bb2f349f868734bcbc5b
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "86010802"
---
# <a name="understand-sql-server-management-studio-windows-management"></a>Descripción de la administración de ventanas de SQL Server Management Studio
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Las ventanas de herramientas de [!INCLUDE[msCoName](../includes/msconame_md.md)] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] son un sistema muy funcional, flexible y eficaz que permite:  
  
-   Maximizar el área de trabajo del usuario para desarrollo y administración.  
  
-   Reducir el número de ventanas sin utilizar que se muestran en un momento dado.  
  
-   Personalizar fácilmente el entorno del usuario.  
  
La manipulación de ventanas es vital en el entorno de [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] . Los usuarios pueden obtener acceso fácilmente a las herramientas y ventanas que usan con frecuencia. Además, pueden controlar cuánto espacio desean asignar a la distinta información. El entorno debe maximizar el espacio disponible para modificar consultas en consecuencia. Las ventanas se pueden mover a ubicaciones diferentes de la pantalla. Muchas ventanas se pueden desacoplar y arrastrar fuera del marco de [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] . Esto es muy útil cuando se utiliza más de un monitor.  
  
Para aumentar el área de edición mientras se conserva la funcionalidad, todas las ventanas ofrecen la característica Ocultar automáticamente, que muestra la ventana como una pestaña de una barra a lo largo del borde del entorno principal de [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] . Cuando el puntero se coloca sobre una de estas pestañas, se muestra la ventana subyacente. La característica Ocultar automáticamente de una ventana puede alternarse si se hace clic en el botón **Ocultar automáticamente** , situado en la esquina superior derecha de la ventana y representado por un alfiler. También existe una opción **Ocultar todo automáticamente** en el menú **Ventana** .  
  
Algunos componentes pueden configurarse en modo con pestañas, donde los componentes aparecen como pestañas en la misma ubicación acoplada, o en modo de interfaz de múltiples documentos (MDI), donde cada documento tiene su propia ventana. Para configurar esta característica, en el menú **Herramientas** , haga clic en **Opciones**, en **Entorno**y, a continuación, haga clic en **General**.  
  
> [!IMPORTANT]  
> Cuando un inicio de sesión (o un usuario de base de datos independiente) se conecta y se autentica, la conexión almacena la información de identidad del inicio de sesión. Para un inicio de sesión con autenticación de Windows, esto incluye la información sobre la pertenencia a grupos de Windows. La identidad del inicio de sesión permanecerá autenticada mientras dure la conexión. Para aplicar cambios en la identidad, como un cambio o restablecimiento de contraseña de la pertenencia al grupo de Windows, el inicio de sesión debe cerrar sesión en la entidad de autenticación (Windows o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]) y volver a iniciar sesión. Los miembros del rol fijo de servidor **sysadmin** o cualquier inicio de sesión con el permiso **ALTER ANY CONNECTION** puede usar el comando **KILL** para finalizar una conexión y hacer que el inicio de sesión se vuelva a conectar. [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] puede reutilizar la información de conexión al abrir varias conexiones en las ventanas del Explorador de objetos y del Editor de consultas. Cierre todas las conexiones para forzar una reconexión.  
  
> [!IMPORTANT]  
> Cuando un inicio de sesión (o un usuario de base de datos independiente) se conecta y se autentica, la conexión almacena en memoria caché información de identidad del inicio de sesión. Para un inicio de sesión con autenticación de Windows, esto incluye la información sobre la pertenencia a grupos de Windows. La identidad del inicio de sesión permanecerá autenticada mientras dure la conexión. Para aplicar cambios en la identidad, como un cambio o restablecimiento de contraseña de la pertenencia al grupo de Windows, el inicio de sesión debe cerrar sesión en la entidad de autenticación (Windows o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]) y volver a iniciar sesión. Los miembros del rol fijo de servidor **sysadmin** o cualquier inicio de sesión con el permiso **ALTER ANY CONNECTION** puede usar el comando **KILL** para finalizar una conexión y hacer que el inicio de sesión se vuelva a conectar. [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] puede reutilizar la información de conexión al abrir varias conexiones en las ventanas del Explorador de objetos y del Editor de consultas. Cierre todas las conexiones para forzar una reconexión.  
  
## <a name="see-also"></a>Consulte también  
[Usar SQL Server Management Studio](../ssms/use-sql-server-management-studio.md)  
[Entorno de SQL Server Management Studio](../ssms/the-sql-server-management-studio-environment.md)  
  
