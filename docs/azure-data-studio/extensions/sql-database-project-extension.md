---
title: Extensión SQL Database Projects
description: Instale y use la extensión SQL Database Projects para Azure Data Studio.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: dzsquared
ms.author: drskwier
ms.reviewer: maghan
ms.custom: ''
ms.date: 09/22/2020
ms.openlocfilehash: 65006891a6633a75482f9a32c328dea0d8bf76fc
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/23/2020
ms.locfileid: "91123483"
---
# <a name="sql-database-projects-extension-preview"></a>Extensión SQL Database Projects (versión preliminar)

SQL Database Projects (versión preliminar) es una extensión para desarrollar bases de datos SQL en un entorno de desarrollo basado en proyectos. 

## <a name="features"></a>Características

1. Creación del proyecto a partir de una base de datos conectada.
2. Creación de un proyecto en blanco nuevo.
3. Apertura de un proyecto creado previamente en [Azure Data Studio](sql-database-project-extension-getting-started.md) o en [SQL Server Data Tools](../../ssdt/sql-server-data-tools.md).
4. Edición del proyecto mediante la adición o eliminación de tablas, vistas, procedimientos almacenados o scripts personalizados en el proyecto.
5. Organización de archivos y scripts en carpetas.
6. Incorporación de referencias a bases de datos del sistema o dacpac del usuario.
7. Creación de un solo proyecto.
8. Implementación de un solo proyecto.
9. Carga de los detalles de conexión (autenticación de Windows de SQL) y las variables SQLCMD del perfil de implementación.

## <a name="install-the-sql-database-projects-extension"></a>Instalación de la extensión SQL Database Projects

1. Abra el administrador de extensiones para tener acceso a las extensiones disponibles.  Para ello, seleccione el icono de extensiones o **Extensiones** en el menú **Vista**.
2. Para identificar la extensión *SQL Database Projects*, escriba todo el nombre o parte de él en el cuadro de búsqueda de extensiones. Seleccione una extensión disponible para ver sus detalles.

   ![Instalación de la extensión](media/sql-database-projects-extension/install-database-projects.png)

3. Seleccione la extensión que quiera e **instálela**.
4. Seleccione **Recargar** para habilitar la extensión (solo es necesario la primera vez que se instala una extensión).
5. Seleccione el icono de archivos en la barra de actividades o **Explorer** (Explorador) en el menú **View** (Ver). Ahora hay disponible un viewlet nuevo para **Projects** (Proyectos).

   > [!NOTE]
   > El SDK de .NET Core es necesario para la funcionalidad para crear proyectos y se le pedirá que lo instale si la extensión no puede detectarlo.  El SDK de .NET Core (versión 3.1 o posterior) se puede descargar e instalar desde [https://dotnet.microsoft.com/download/dotnet-core/3.1](https://dotnet.microsoft.com/download/dotnet-core/3.1).

   > [!NOTE]
   > Se recomienda instalar la extensión [Comparación de esquemas](schema-compare-extension.md) junto con SQL Database Projects para obtener una funcionalidad completa.

## <a name="known-limitations"></a>Restricciones conocidas

1. Actualmente no se admiten la adición de referencias de proyecto ni la carga de referencias de proyecto existentes en el viewlet de Azure Data Studio.
2. Actualmente no se admite la carga de archivos como vínculo en el viewlet de Azure Data Studio. Sin embargo, los archivos se cargarán en el nivel superior del árbol y la compilación incorporará estos archivos según lo previsto.
3. No se admiten la adición ni la carga de scripts de implementación previos y posteriores en el viewlet. Sin embargo, si agrega manualmente estos archivos en el proyecto, se respetarán en tiempo de compilación.
4. Los objetos SQLCLR del proyecto no se admiten en la versión de .NET Core de DacFx.
5. El usuario no define las tareas (compilación y publicación).
6. Destinos de publicación definidos por DacFx.
7. La integración del control de código fuente y la creación de un proyecto no crean automáticamente el archivo .gitignore.
8. La compatibilidad con el entorno de WSL está limitada.

## <a name="next-steps"></a>Pasos siguientes

- [Introducción a la extensión de SQL Database Projects](sql-database-project-extension-getting-started.md)
- [Compilación y publicación de un proyecto con la extensión SQL Database Projects para Azure Data Studio](sql-database-project-extension-build.md)