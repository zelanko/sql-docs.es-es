---
title: Extensión SQL Database Projects
description: Instale y use la extensión SQL Database Projects (versión preliminar) para Azure Data Studio
ms.custom: seodec18
ms.date: 06/25/2020
ms.reviewer: drskwier, maghan, sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: dzsquared
ms.author: drskwier
ms.openlocfilehash: 609af04cec2f6eaaaf1890e19c6d85fbd4bd5b8a
ms.sourcegitcommit: b860fe41b873977649dca8c1fd5619f294c37a58
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/29/2020
ms.locfileid: "85519174"
---
# <a name="sql-database-projects-extension-preview"></a>Extensión SQL Database Projects (versión preliminar)

SQL Database Projects (versión preliminar) es una extensión para desarrollar bases de datos SQL en un entorno de desarrollo basado en proyectos. Esta extensión se encuentra actualmente en versión preliminar y está disponible en la [compilación Azure Data Studio Insiders](https://github.com/microsoft/azuredatastudio#try-out-the-latest-insiders-build-from-main).


## <a name="install-the-sql-database-projects-extension"></a>Instalación de la extensión SQL Database Projects

1. Para abrir el administrador de extensiones y acceder a las extensiones disponibles, seleccione el icono de extensiones, o bien seleccione **Extensiones** en el menú **Ver**.
2. Para identificar la extensión *SQL Database Projects*, escriba todo el nombre o parte de él en el cuadro de búsqueda de extensiones. Seleccione una extensión disponible para ver sus detalles.

   ![Instalación de la extensión](media/extensions/sql-database-projects-extension/install-database-projects.png)

3. Seleccione la extensión que quiera e **instálela**.
4. Seleccione **Recargar** para habilitar la extensión (solo es necesario la primera vez que se instala una extensión).
5. Seleccione el icono de archivos en la barra de actividades o **Explorer** (Explorador) en el menú **View** (Ver). Ahora hay disponible un viewlet nuevo para **Projects** (Proyectos).

   > [!NOTE]
   > Se recomienda instalar la extensión [Comparación de esquemas](schema-compare-extension.md) junto con SQL Database Projects para obtener una funcionalidad completa.

## <a name="getting-started-with-database-projects"></a>Introducción a los proyectos de base de datos

* Para crear un proyecto de base de datos, vaya al viewlet **Projects** en Explorer o busque **New Database Project** (Nuevo proyecto de base de datos) en la paleta de comandos.
* Los proyectos de base de datos existentes se pueden abrir a través de **Open Database Project** (Abrir proyecto de base de datos) en la paleta de comandos.
* Comience a partir de una base de datos existente mediante **Import New Database Project** (Importar nuevo proyecto de base de datos) desde la paleta de comandos.

   ![Nuevo viewlet](media/extensions/sql-database-projects-extension/projects-viewlet.png)


### <a name="create-an-empty-database-project"></a>Creación de un proyecto vacío

 En el viewlet **Projects** de **Explorer**, haga clic en el botón **New Project** (Nuevo proyecto) y escriba un nombre de proyecto en la entrada de texto que aparece.  En el cuadro de diálogo "Select a Folder" (Seleccionar una carpeta) que aparece, seleccione un directorio para guardar la carpeta del proyecto, el archivo .sqlproj y el resto del contenido.
El proyecto vacío se abre y se ve en el viewlet **Projects** para su edición.

### <a name="open-an-existing-project"></a>Apertura de un proyecto existente

En el viewlet **Projects**, haga clic en el botón **Open Project** (Abrir proyecto) y abra un archivo *.sqlproj* existente desde el selector de archivos que aparece. Los proyectos existentes se pueden originar en Azure Data Studio o [Visual Studio SQL Server Data Tools](../ssdt/sql-server-data-tools.md).

El proyecto vacío se abre y sus contenidos se pueden ver en el viewlet **Projects** para su edición.

### <a name="create-a-database-project-from-an-existing-database"></a>Creación de un proyecto de base de datos a partir de una base de datos existente

En el viewlet **Project**, haga clic en el botón **Import Project from Database** (Importar proyecto desde una base de datos) y conéctese a una instancia de SQL Server.  Una vez que se haya establecido la conexión, seleccione una base de datos en la lista de bases de datos disponibles y establezca el nombre del proyecto.

Por último, seleccione una estructura de destino para la extracción.  El nuevo proyecto se abre y contiene scripts de SQL para el contenido de la base de datos seleccionada.

## <a name="build-and-publish"></a>Compilación y publicación

En la extensión SQL Database Projects para Azure Data Studio, la implementación del proyecto de base de datos se realiza al compilarlo en un [archivo de aplicación de capa de datos](../relational-databases/data-tier-applications/data-tier-applications.md) (DACPAC) y publicarlo en una plataforma compatible. Para obtener más información sobre este proceso, vea [Compilación y publicación de un proyecto](sql-database-project-extension-build.md).

## <a name="schema-compare"></a>Comparación de esquemas
La extensión SQL Database Projects interactúa con la extensión [Comparación de esquemas](schema-compare-extension.md), si está instalada, para comparar el contenido de un proyecto con un DACPAC o una base de datos existente.  La comparación de esquemas resultante se puede usar para ver y aplicar las diferencias entre el origen y el destino.

## <a name="next-steps"></a>Pasos siguientes

- [Compilación y publicación de un proyecto con la extensión SQL Database Projects para Azure Data Studio](sql-database-project-extension-build.md)
- [Aplicaciones de capa de datos](../relational-databases/data-tier-applications/data-tier-applications.md)