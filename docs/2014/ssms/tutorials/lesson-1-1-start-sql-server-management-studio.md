---
title: Iniciar SQL Server Management Studio | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 25ffaea6-0eee-4169-8dd0-1da417c28fc6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bd7fed6fff4ddd55ef56e4c5b342c56b6c2f462f
ms.sourcegitcommit: 66dbc3b740f4174f3364ba6b68bc8df1e941050f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/05/2019
ms.locfileid: "73632797"
---
# <a name="start-sql-server-management-studio"></a>Iniciar SQL Server Management Studio
  Para empezar este tutorial, veamos [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
## <a name="opening-sql-server-management-studio"></a>Abrir SQL Server Management Studio  
  
#### <a name="to-open-sql-server-management-studio"></a>Para abrir SQL Server Management Studio  
  
1.  En el menú **Inicio** , seleccione **Todos los programas**, [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]y, a continuación, haga clic en **SQL Server Management Studio**.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] no está instalado de forma predeterminada. Si [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] no está disponible, ejecute el programa de instalación para instalarlo. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] no está disponible con [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] Express está disponible como descarga gratuita en el [centro de descarga de Microsoft](https://www.microsoft.com/download/details.aspx?id=7593), pero tiene una interfaz de usuario diferente a la que se describe en este tutorial.  
  
2.  En el cuadro de diálogo **Conectar al servidor** , compruebe la configuración predeterminada y, después, haga clic en **Conectar**. Para conectarse, el cuadro **nombre del servidor** debe contener el nombre del equipo en el que está instalado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si el [!INCLUDE[ssDE](../../includes/ssde-md.md)] es una instancia con nombre, el cuadro **nombre del servidor** también debe contener el nombre de la instancia en el formato \<*computer_name*> *\\<instance_name*>.  
  
## <a name="management-studio-components"></a>Componentes de Management Studio  
 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] presenta la información en ventanas dedicadas a tipos de información específicos. La información de la base de datos se muestra en las ventanas de documentos y en el Explorador de objetos.  
  
-   El Explorador de objetos es una vista de árbol de todos los objetos de base de datos que contiene un servidor. Puede incluir las bases de datos de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]e [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. El Explorador de objetos incluye información de todos los servidores a los que está conectado. Al abrir [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], se le solicita que se conecte al Explorador de objetos aplicando la última configuración utilizada. Para conectarse a un servidor, no es necesario que lo registre. Solo tiene que hacer doble clic en cualquier servidor del componente Servidores registrados.  
  
-   La ventana de documento es el área de mayor tamaño de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Esta ventana puede contener editores de consulta y ventanas de explorador. De forma predeterminada, se muestra la página Resumen, conectada a la instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] del equipo actual.  
  
## <a name="showing-additional-windows"></a>Mostrar ventanas adicionales  
  
#### <a name="to-show-the-registered-servers-window"></a>Para mostrar la ventana Servidores registrados  
  
1.  En el menú **Ver** , haga clic en **Servidores registrados**.  
  
     La ventana Servidores registrados aparece encima del Explorador de objetos. Servidores registrados enumera los servidores que el usuario administra habitualmente. Puede agregar y quitar los servidores de esta lista. Solo aparecerán en la lista los servidores de las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se encuentren en el equipo donde se ejecuta [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
2.  Si el servidor no aparece, en servidores registrados, haga clic con el botón secundario en **motor de base de datos**y, a continuación, haga clic en **Actualizar registro de servidor local**.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Conectar con el Explorador de objetos y Servidores registrados](../object/object-explorer.md)  
  
  
