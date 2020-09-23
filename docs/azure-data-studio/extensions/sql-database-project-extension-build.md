---
title: Compilación y publicación de un proyecto
description: Compilación y publicación con la extensión Proyectos de base de datos de SQL Server
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: dzsquared
ms.author: drskwier
ms.reviewer: maghan, sstein
ms.custom: ''
ms.date: 06/25/2020
ms.openlocfilehash: 4320873affdab74a31d1e666a84bc744b1c00385
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/23/2020
ms.locfileid: "91123511"
---
# <a name="build-and-publish-a-project"></a>Compilación y publicación de un proyecto

El proceso de compilación en la extensión Proyectos de base de datos de SQL para Azure Data Studio permite la creación de *dacpac* en entornos Windows, macOS y Linux. El proyecto se puede implementar en un entorno local o en la nube con el proceso de publicación.

## <a name="prerequisites"></a>Requisitos previos

- Instale y configure la [extensión Proyectos de base de datos de SQL para Azure Data Studio](sql-database-project-extension.md).

## <a name="build-a-database-project"></a>Compilación de un proyecto de base de datos

 En el viewlet **Proyectos** del **Explorador**, haga clic con el botón derecho en el nodo raíz *.sqlproj* y seleccione **Compilar**.

 El panel de salida aparecerá automáticamente con la salida del proceso de compilación.  Una compilación correcta finalizará con el mensaje siguiente: 

 ``` ... exited with code: 0 ```

## <a name="publish-a-database-project"></a>Publicación de un proyecto de base de datos

Una vez que un proyecto se compila correctamente a través del proceso de compilación, la base de datos se puede publicar en una instancia de SQL Server. Para publicar un proyecto de base de datos, en el viewlet **Proyectos** del **Explorador**, haga clic con el botón derecho en el nodo raíz *.sqlproj* y seleccione **Publicar**.

En el cuadro de diálogo **Publicar base de datos** que aparece, especifique una conexión al servidor y el nombre de la base de datos que se va a crear.

## <a name="next-steps"></a>Pasos siguientes

- [Extensión Proyectos de base de datos de SQL para Azure Data Studio](sql-database-project-extension.md)
- [Creación de proyectos de base de datos SQL desde la línea de comandos](sql-database-project-extension-build-from-command-line.md)
