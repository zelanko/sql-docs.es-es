---
title: Opciones (Entorno - página General) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-menu
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- VS.TOOLSOPTIONSPAGES.ENVIRONMENT.GENERAL
- VS.ToolsOptionsPages.Environment.SQLEnvironmentOptions
- DevLang-TSQL
ms.assetid: c32ccdb8-2cf8-4c78-b474-a3abd3dbbd13
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f7e8ba6dcb66fbf962e70cc5175b07095ffa2f5d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "33043162"
---
# <a name="options-environment---general-page"></a>Opciones (Entorno - Página General)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Use el cuadro de diálogo **Opciones** para configurar las acciones de inicio de [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)], opciones generales de administración de ventanas y otros valores de configuración generales. En el menú **Herramientas** , haga clic en **Opciones**, expanda la carpeta **Entorno** y haga clic en **General**.  
  
## <a name="uielement-list"></a>Lista de UIElement  
**Al iniciar**  
Seleccione la acción que [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] debe llevar a cabo una vez que se ha iniciado. Las opciones son:  
  
-   **Abrir el Explorador de objetos** : solicita una conexión y abre el Explorador de objetos.  
  
-   **Abrir nueva ventana de consulta** : solicita una conexión y abre el Editor de consultas de SQL.  
  
-   **Abrir el Explorador de objetos y una nueva ventana de consulta** : solicita una conexión y abre el Explorador de objetos y el Editor de consultas de SQL con dicha conexión.  
  
-   **Abrir entorno vacío** : abre [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] sin ninguna ventana del Editor de consultas de SQL y sin conectar el Explorador de objetos a un servidor.  
  
**Ocultar objetos del sistema en el Explorador de objetos**  
Seleccione esta casilla para eliminar de la vista de árbol del Explorador de objetos las bases de datos del sistema, las tablas del sistema, las vistas del sistema y los procedimientos almacenados del sistema. Las funciones del sistema y los tipos de datos del sistema no se ocultan. Esta opción solo se aplica a instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] y no afecta a los servidores que ya están conectados en el Explorador de objetos.  
  
## <a name="environment-layout"></a>Diseño del entorno  
Para poder pasar del modo organizado por pestañas al modo de interfaz de múltiples documentos (MDI), debe cerrar y volver a abrir [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] .  
  
**Organización por pestañas**  
Seleccione esta opción para mostrar ventanas de documentos que estén agrupadas por pestañas en los editores. Las ventanas organizadas por pestañas son de gran utilidad para organizar los documentos y pasar de un documento abierto a otro.  
  
**Entorno MDI**  
Seleccione esta opción para abrir documentos en un entorno MDI. Las ventanas de documento MDI son útiles para ganar espacio en la pantalla; de lo contrario, dicho espacio está ocupado por las pestañas del entorno organizado por pestañas. Si trabaja en modo MDI, para pasar de un documento a otro, presione las teclas CTRL+TAB, o utilice las opciones de organización del menú **Ventana** .  
  
## <a name="docked-tool-window-behavior"></a>Comportamiento de la ventana de herramientas acoplada  
**El botón Cerrar afecta solo a la pestaña activa**  
Si esta casilla está seleccionada, solo se cierra la ventana de herramientas activa, no todas las ventanas del conjunto de ventanas acopladas. De forma predeterminada, esta casilla está activada.  
  
**El botón Ocultar automáticamente afecta solo a la pestaña activa**  
Si esta casilla está seleccionada, solo se oculta automáticamente la ventana de herramientas activa, no todas las ventanas del conjunto de ventanas acopladas. De forma predeterminada, esta casilla no está activada.  
  
## <a name="display"></a>Pantalla  
**Mostrar n archivos de la lista de archivos recientes**  
Personaliza el número de proyectos y archivos recientes que aparecen en el menú **Archivo** . Escriba un número entre 1 y 24. El valor predeterminado es 4. Esta es una manera fácil de recuperar los proyectos de script y los proyectos de archivos y script usados recientemente.  
  
