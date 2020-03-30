---
title: 'Administrar: Azure Data Studio Notebooks'
titleSuffix: SQL Server Big Data Clusters
description: Use un cuaderno de Azure Data Studio para administrar un clúster de macrodatos y solucionar problemas de este.
author: yualan
ms.author: alanyu
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 12/13/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d2a051e297b48ed8d813fce0e0e8ffa748a84d16
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "75252018"
---
# <a name="manage-sql-server-big-data-clusters-with-azure-data-studio-notebooks"></a>Administración de clústeres de macrodatos de SQL Server con cuadernos de Azure Data Studio

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] proporciona una extensión para Azure Data Studio que incluye cuadernos. Un cuaderno proporciona documentación y código que se puede usar en Azure Data Studio para administrar clústeres de macrodatos de SQL Server 2019.

Los [cuadernos](notebooks-guidance.md), que originalmente se implementaban como un proyecto de código abierto, se han incorporado a [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download). Puede usar Markdown para el texto de las celdas de texto y uno de los kernels disponibles para escribir código en las celdas de código.

Puede usar cuadernos para implementar clústeres de macrodatos para [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].

Además de los cuadernos, puede ver una colección de cuadernos, que se denomina "libro de Jupyter". Un libro de Jupyter proporciona una tabla de contenido que le permite examinar una colección de cuadernos para que pueda encontrar fácilmente el cuaderno que necesita, tanto para solucionar problemas de SQL Server como para ver el estado del clúster.

## <a name="prerequisites"></a>Prerrequisitos

Deberá cumplir estos requisitos previos para abrir un cuaderno:

* La versión más reciente de la [compilación Azure Data Studio Insiders](https://aka.ms/azuredatastudio-rc)
* La extensión [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] instalada en Azure Data Studio

Además de estos requisitos previos, para implementar clústeres de macrodatos de SQL Server 2019, también necesitará:

* [azdata](deploy-install-azdata.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [CLI de Azure](/cli/azure/install-azure-cli)

## <a name="access-troubleshooting-notebooks"></a>Acceso a los cuadernos de solución de problemas
Hay tres formas de acceder a los cuadernos de solución de problemas.

### <a name="command-palette"></a>Paleta de comandos
1. Seleccione **Ver** > **Paleta de comandos**.
2. Escriba **Libros de Jupyter: Guía de SQL Server 2019**.

Se abrirá el viewlet Libros de Jupyter con el libro de Jupyter que contiene los cuadernos de solución de problemas relacionados con los clústeres de macrodatos de SQL Server.

### <a name="sql-master-dashboard"></a>Panel maestro de SQL
1. Después de instalar Azure Data Studio Insiders, conéctese a una instancia de clúster de macrodatos de SQL Server.
2. Una vez que se haya conectado a la instancia, haga clic con el botón derecho en el nombre del servidor en **CONEXIONES** y seleccione **Administrar**.
3. En el panel, seleccione **Clúster de macrodatos de SQL Server**. Seleccione **Guía de SQL Server 2019** para abrir el libro de Jupyter que contiene los cuadernos que necesita.
    ![Cuadernos de Jupyter en el panel](media/manage-notebooks/jupyter-book-button.png)

1. Seleccione el cuaderno de la tarea que debe completar.

### <a name="controller-dashboard"></a>Panel del controlador
1. En la vista **Conexiones**, expanda **Clúster de macrodatos de SQL Server**.
2. Agregue los detalles del punto de conexión del controlador.
3. Una vez que se haya conectado al controlador, haga clic con el botón derecho en el punto de conexión y seleccione **Administrar**.
4. Una vez que se haya cargado el panel, seleccione **Solucionar problemas** para abrir las guías de solución de problemas de los libros de Jupyter.

## <a name="use-troubleshooting-notebooks"></a>Uso de los cuadernos de solución de problemas
1. Busque la guía de solución de problemas que necesite en la tabla de contenido del libro de Jupyter.
1. Los cuadernos están optimizados, por lo que solo tiene que seleccionar **Ejecutar celdas**. Esta acción ejecutará cada celda del cuaderno de forma individual hasta que se haya completado el cuaderno.
1. Si se encuentra un error, el libro de Jupyter sugerirá un cuaderno que puede ejecutar para corregir el error. Siga los pasos recomendados y, a continuación, vuelva a ejecutar el cuaderno.

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre los cuadernos en Azure Data Studio, vea [Uso de los cuadernos en SQL Server](notebooks-guidance.md).
