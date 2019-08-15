---
title: Administración de clústeres de macrodatos de SQL Server con cuadernos de Azure Data Studio
titleSuffix: Manage SQL Server big data cluster cluster with Azure Data Studio notebooks
description: Use un cuaderno de Azure Data Studio para administrar un clúster de macrodatos y solucionar problemas de este.
author: yualan
ms.author: alanyu
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7adc5c3d07b47b5310d8a45d00747d6dd6de9952
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028581"
---
# <a name="manage-big-data-clusters-for-sql-server-with-azure-data-studio-notebooks"></a>Administración de clústeres de macrodatos de SQL Server con cuadernos de Azure Data Studio

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] proporciona una extensión para Azure Data Studio que incluye cuadernos. Un cuaderno incluye documentación y código que se puede usar en Azure Data Studio para administrar clústeres de macrodatos de SQL Server.

Los [cuadernos](notebooks-guidance.md), que originalmente se implementaban como un proyecto de código abierto, se han implementado en [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download). Puede usar Markdown para el texto de las celdas de texto y uno de los kernels disponibles para escribir código en las celdas de código.

Puede usar cuadernos para implementar clústeres de macrodatos para [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].

Además de los cuadernos, los usuarios pueden ver una colección de notebooks, que se denominan libros de Jupyter. Un libro de Jupyter proporciona una tabla de contenido que permite examinar una colección de cuadernos para que un usuario pueda encontrar fácilmente el cuaderno que necesita, tanto para solucionar problemas de SQL Server como para ver el estado del clúster.

## <a name="prerequisites"></a>Requisitos previos

Los siguientes requisitos previos son necesarios para poder iniciar el cuaderno:

* Versión más reciente de la [compilación Azure Data Studio Insiders](https://github.com/microsoft/azuredatastudio#try-out-the-latest-insiders-build-from-master)
* Extensión [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] instalada en Azure Data Studio

Además de lo anterior, la implementación de clústeres de macrodatos de SQL Server 2019 también requiere:

* [azdata](deploy-install-azdata.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [CLI de Azure](/cli/azure/install-azure-cli)

## <a name="accessing-troubleshooting-notebooks"></a>Acceso a los cuadernos de solución de problemas

1. Después de instalar Azure Data Studio Insiders, conéctese a una instancia de clúster de macrodatos de SQL Server.
2. Después de conectarse correctamente, haga clic con el botón derecho en el nombre del servidor en el viewlet Conexiones y haga clic en **Administrar**.
3. En el panel, haga clic en **Clúster de macrodatos de SQL Server**. Haga clic en **Guía de SQL Server 2019** para abrir el libro de Jupyter con los cuadernos que necesita.
    ![botón](media/manage-notebooks/jupyter-book-button.png)

1. En la ventana Selector de carpetas, seleccione una ubicación para guardar el libro de Jupyter.
2. Haga clic en **Recargar** para volver a cargar Azure Data Studio a fin de ver el libro de Jupyter. Haga clic en **Abrir una nueva instancia** para abrir una nueva instancia de Azure Data Studio con el libro de Jupyter.
3. En la vista del explorador, debería ver una sección denominada **Libros**. Si no está expandida, haga clic en ella para ver los cuadernos.
4. Haga clic en el cuaderno de la tarea que debe completar.

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre los cuadernos en Azure Data Studio, vea [Uso de los cuadernos en la versión preliminar de SQL Server 2019](notebooks-guidance.md).
