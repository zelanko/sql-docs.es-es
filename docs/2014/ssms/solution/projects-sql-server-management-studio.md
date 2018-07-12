---
title: Proyectos (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: c13af859-ca66-4e43-b76a-0650ac6566c0
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 42bd9b05733ab097d09a9b9e7b8a6c18f2056c5d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37230045"
---
# <a name="projects-sql-server-management-studio"></a>Proyectos (SQL Server Management Studio)
  Un proyecto de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] es una colección de scripts y archivos relacionados lógicamente que se pueden guardar juntos para la administración y el desarrollo de bases de datos.  
  
## <a name="script-project-overview"></a>Información general del proyecto de script  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aparecen en el Explorador de soluciones de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Un proyecto de script puede contener cero o varios archivos de proyecto. Puede agregar un proyecto a una solución o combinar más de un proyecto en una solución.  
  
 Entre los proyectos se pueden incluir los siguientes:  
  
-   **Conexiones**. Una conexión, conservada en un proyecto, contendrá información lógica, el nombre del servidor, la base de datos predeterminada, el protocolo preferido, el tipo de autenticación y las propiedades de conexión. La información de conexión puede almacenarse opcionalmente con un script (vea a continuación).  
  
-   **SQLScripts**. Scripts SQL usados frecuentemente por el usuario. Si hace doble clic en un archivo .sql del proyecto, el Editor SQL abrirá el script seleccionado.  
  
-   **Scripts MDX, DMX y XMLA**. Scripts MDX usados frecuentemente por el usuario. Si hace doble clic en un archivo .mdx del proyecto, el Editor abrirá el script seleccionado.  
  
-   **Varios**. Esta carpeta se puede usar para los archivos que no encajan en ninguno de los otros tipos de nodos predeterminados, como un archivo de texto que contenga los objetivos del proyecto.  
  
 Los proyectos también pueden estar integrados en un sistema de control de código fuente.  
  
## <a name="connecting-to-an-instance-of-sql-server-from-a-script-project"></a>Conectar a una instancia de SQL Server desde un proyecto de script  
 Un proyecto de script puede contener conexiones a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Puede conectar a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un proyecto si hace clic en la conexión. Así se abrirá una ventana de script SQL conectada a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definida en la conexión seleccionada. Si abre un script [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o MDX con una conexión que use autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , se le solicitará la contraseña mediante el cuadro de diálogo **Conectar con el servidor SQL Server** una vez que el editor se haya abierto y el script se haya cargado.  
  
 La conexión se cerrará una vez que se cierre la ventana correspondiente.  
  
 Para modificar información sobre una conexión, use la ventana de propiedades de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
## <a name="project-tasks"></a>Tareas de proyecto  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Describe cómo crear un nuevo proyecto en una solución.|[Crear un proyecto](create-a-project.md)|  
|Describe cómo agregar un proyecto existente a una solución.|[Agregar un proyecto existente a una solución](add-an-existing-project-to-a-solution.md)|  
|Describe cómo cambiar la ubicación predeterminada donde se guardan los archivos de proyecto.|[Cambiar la ubicación predeterminada de los proyectos](change-the-default-location-for-projects.md)|  
|Describe cómo ver las propiedades actuales de un proyecto.|[Ver las propiedades de un proyecto](view-project-properties.md)|  
|Describe cómo agregar nuevos elementos, como conexiones o archivos de script, un proyecto.|[Agregar nuevos elementos a un proyecto](add-new-items-to-a-project.md)|  
|Describe cómo establecer la información de conexión para una consulta.|[Asociar una consulta a una conexión de un proyecto](associate-a-query-with-a-connection-in-a-project.md)|  
|Describe cómo cambiar la información de conexión para una consulta.|[Cambiar la conexión asociada a una consulta](change-the-connection-associated-with-a-query.md)|  
|Describe cómo cambiar las propiedades de conexión.|[Ver o cambiar las propiedades de una conexión en un proyecto](view-or-change-the-properties-of-a-connection-in-a-project.md)|  
  
## <a name="see-also"></a>Vea también  
 [Explorador de soluciones](solution-explorer.md)   
 [Soluciones &#40;SQL Server Management Studio&#41;](solutions-sql-server-management-studio.md)   
 [Control de código fuente del Explorador de soluciones](../../database-engine/solution-explorer-source-control.md)  
  
  
