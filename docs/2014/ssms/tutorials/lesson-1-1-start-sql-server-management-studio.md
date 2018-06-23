---
title: Iniciar SQL Server Management Studio | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 25ffaea6-0eee-4169-8dd0-1da417c28fc6
caps.latest.revision: 43
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 2f928645fb89757b2284628d0400847cf5f3a1f2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36104162"
---
# <a name="start-sql-server-management-studio"></a>Iniciar SQL Server Management Studio
  Para empezar este tutorial, veamos [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
## <a name="opening-sql-server-management-studio"></a>Abrir SQL Server Management Studio  
  
#### <a name="to-open-sql-server-management-studio"></a>Para abrir SQL Server Management Studio  
  
1.  En el **iniciar** menú, elija **todos los programas**, seleccione [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]y, a continuación, haga clic en **SQL Server Management Studio**.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] no está instalado de forma predeterminada. Si [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] no está disponible, ejecute el programa de instalación para instalarlo. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] no está disponible con [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] Express está disponible como descarga gratuita en el [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkID=37075&clcid=0x409), pero tiene una interfaz de usuario diferente que se describe en este tutorial.  
  
2.  En el cuadro de diálogo **Conectar al servidor** , compruebe la configuración predeterminada y, después, haga clic en **Conectar**. Para conectarse, el **nombre del servidor** cuadro debe contener el nombre del equipo donde [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está instalado. Si el [!INCLUDE[ssDE](../../includes/ssde-md.md)] es una instancia con nombre, el **nombre del servidor** cuadro también debe contener el nombre de instancia en el formato \< *computer_name* > \\ < *instance_name*>.  
  
## <a name="management-studio-components"></a>Componentes de Management Studio  
 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] presenta la información en ventanas dedicadas a tipos de información específicos. La información de la base de datos se muestra en las ventanas de documentos y en el Explorador de objetos.  
  
-   El Explorador de objetos es una vista de árbol de todos los objetos de base de datos que contiene un servidor. Puede incluir las bases de datos de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]e [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. El Explorador de objetos incluye información de todos los servidores a los que está conectado. Al abrir [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], se le solicita que se conecte al Explorador de objetos aplicando la última configuración utilizada. Para conectarse a un servidor, no es necesario que lo registre. Solo tiene que hacer doble clic en cualquier servidor del componente Servidores registrados.  
  
-   La ventana de documento es el área de mayor tamaño de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Esta ventana puede contener editores de consulta y ventanas de explorador. De forma predeterminada, se muestra la página Resumen, conectada a la instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] del equipo actual.  
  
## <a name="showing-additional-windows"></a>Mostrar ventanas adicionales  
  
#### <a name="to-show-the-registered-servers-window"></a>Para mostrar la ventana Servidores registrados  
  
1.  En el menú **Ver** , haga clic en **Servidores registrados**.  
  
     La ventana Servidores registrados aparece encima del Explorador de objetos. Servidores registrados enumera los servidores que el usuario administra habitualmente. Puede agregar y quitar los servidores de esta lista. Solo aparecerán en la lista los servidores de las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se encuentren en el equipo donde se ejecuta [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
2.  Si el servidor no aparece, en servidores registrados, haga clic en **motor de base de datos**y, a continuación, haga clic en **actualizar registro de servidor Local**.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Conectar con el Explorador de objetos y Servidores registrados](../object/object-explorer.md)  
  
  