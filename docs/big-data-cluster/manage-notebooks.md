---
title: Administración de clústeres de macrodatos SQL Server con cuadernos de Azure Data Studio
titleSuffix: Manage SQL Server Big Data Clusters with Azure Data Studio notebooks
description: Use un cuaderno de Azure Data Studio para administrar un clúster de macrodatos y solucionar problemas de este.
author: yualan
ms.author: alanyu
ms.reviewer: mikeray
ms.date: 09/09/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e22b16cf8658e53e6bdc5db0fcd82692f3730fc7
ms.sourcegitcommit: c7a202af70fd16467a498688d59637d7d0b3d1f3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/15/2019
ms.locfileid: "72313679"
---
# <a name="manage-sql-server-big-data-clusters-with-azure-data-studio-notebooks"></a>Administración de clústeres de macrodatos SQL Server con cuadernos de Azure Data Studio

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] proporciona una extensión para Azure Data Studio que incluye cuadernos. Un cuaderno proporciona documentación y código que puede usar en Azure Data Studio para administrar clústeres de macrodatos de SQL Server 2019.

Los [notebooks](notebooks-guidance.md) se han implementado en [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download)originalmente como un proyecto de código abierto. Puede usar Markdown para el texto de las celdas de texto y uno de los kernels disponibles para escribir código en las celdas de código.

Puede usar cuadernos para implementar clústeres de macrodatos para [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].

Además de los cuadernos, puede ver una colección de cuadernos, que se denomina libro Jupyter. Un libro de Jupyter proporciona una tabla de contenido para ayudarle a navegar por una colección de blocs de notas para que pueda encontrar fácilmente el cuaderno que necesita, si desea solucionar problemas SQL Server o ver el estado del clúster.

## <a name="prerequisites"></a>Requisitos previos

Necesitará estos requisitos previos para abrir un cuaderno:

* La versión más reciente de la [compilación de Azure Data Studio Insiders](https://aka.ms/azuredatastudio-rc)
* La extensión [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)], instalada en Azure Data Studio

Además de estos requisitos previos, para implementar clústeres de macrodatos SQL Server 2019, también necesita:

* [azdata](deploy-install-azdata.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [CLI de Azure](/cli/azure/install-azure-cli)

## <a name="access-troubleshooting-notebooks"></a>Acceder a los cuadernos de solución de problemas
Hay tres formas de acceder a los cuadernos de solución de problemas.

### <a name="command-palette"></a>Paleta de comandos
1. Seleccione **vista** > **paleta de comandos**.
2. Escriba @no__t 0Jupyter: SQL Server guía 2019 @ no__t-0.

Se abrirán los libros de Jupyter Viewlet con el libro Jupyter que contiene los cuadernos de solución de problemas relacionados con los clústeres de macrodatos de SQL Server.

### <a name="sql-master-dashboard"></a>Panel maestro de SQL
1. Después de instalar Azure Data Studio Insider, conéctese a una instancia de clúster de Big Data SQL Server.
2. Una vez conectado a la instancia, haga clic con el botón secundario en el nombre del servidor en **conexiones** y seleccione **administrar**.
3. En el panel, seleccione **SQL Server clúster de Big Data**. Seleccione **SQL Server guía de 2019** para abrir el libro Jupyter que contiene los cuadernos que necesita.
    @no__t notebooks de 0Jupyter en el panel @ no__t-1

1. Seleccione el cuaderno de la tarea que debe completar.

### <a name="controller-dashboard"></a>Panel del controlador
1. En la vista **conexiones** , expanda **SQL Server clústeres de Big Data**.
2. Agregue los detalles del punto de conexión del controlador.
3. Una vez conectado al controlador, haga clic con el botón derecho en el punto de conexión y seleccione **administrar**.
4. Una vez que se cargue el panel, seleccione **solucionar** problemas para abrir el libro de Jupyter guías de solución de problemas.

## <a name="use-troubleshooting-notebooks"></a>Usar cuadernos de solución de problemas
1. Busque la guía de solución de problemas que necesita en la tabla de contenido del libro de Jupyter.
1. Los cuadernos están optimizados, por lo que solo tiene que seleccionar **Ejecutar celdas**. Esta acción ejecutará cada celda del cuaderno individualmente hasta que se complete el cuaderno.
1. Si se encuentra un error, el libro Jupyter sugerirá un cuaderno que puede ejecutar para corregir el error. Siga los pasos recomendados y, a continuación, vuelva a ejecutar el Bloc de notas.

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre los cuadernos en Azure Data Studio, vea [Uso de los cuadernos en la versión preliminar de SQL Server 2019](notebooks-guidance.md).
