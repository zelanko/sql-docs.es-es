---
title: Administración de clústeres de macrodatos de SQL Server con cuadernos de Azure Data Studio
titleSuffix: Manage SQL Server big data cluster cluster with Azure Data Studio notebooks
description: Use un cuaderno de Azure Data Studio para administrar un clúster de macrodatos y solucionar problemas de este.
author: yualan
ms.author: alanyu
ms.reviewer: mikeray
ms.date: 09/09/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: cb2fcaf7431b5d79698af009b533ee49254777fe
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/10/2019
ms.locfileid: "70846650"
---
# <a name="manage-big-data-clusters-for-sql-server-with-azure-data-studio-notebooks"></a>Administración de clústeres de macrodatos de SQL Server con cuadernos de Azure Data Studio

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] proporciona una extensión para Azure Data Studio que incluye cuadernos. Un cuaderno incluye documentación y código que se puede usar en Azure Data Studio para administrar clústeres de macrodatos de SQL Server.

Los [cuadernos](notebooks-guidance.md), que originalmente se implementaban como un proyecto de código abierto, se han implementado en [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download). Puede usar Markdown para el texto de las celdas de texto y uno de los kernels disponibles para escribir código en las celdas de código.

Puede usar cuadernos para implementar clústeres de macrodatos para [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].

Además de los cuadernos, los usuarios pueden ver una colección de notebooks, que se denominan libros de Jupyter. Un libro de Jupyter proporciona una tabla de contenido que permite examinar una colección de cuadernos para que un usuario pueda encontrar fácilmente el cuaderno que necesita, tanto para solucionar problemas de SQL Server como para ver el estado del clúster.

## <a name="prerequisites"></a>Requisitos previos

Los siguientes requisitos previos son necesarios para poder iniciar el cuaderno:

* Versión más reciente de la [compilación Azure Data Studio Insiders](https://aka.ms/azuredatastudio-rc)
* Extensión [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] instalada en Azure Data Studio

Además de lo anterior, la implementación de clústeres de macrodatos de SQL Server 2019 también requiere:

* [azdata](deploy-install-azdata.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [CLI de Azure](/cli/azure/install-azure-cli)

## <a name="accessing-troubleshooting-notebooks"></a>Acceso a los cuadernos de solución de problemas
Hay tres formas de acceder a los cuadernos de solución de problemas.

### <a name="command-palette"></a>Paleta de comandos
1. Haga clic en **Ver** y **paleta de comandos** .
2. Escriba "Jupyter Books: SQL Server guía de 2019 "
3. Se abrirá el Jupyter Books Viewlet con el libro de Jupyter que contiene el TSG relacionado con los clústeres de macrodatos de SQL Server.

### <a name="sql-master-dashboard"></a>Panel maestro de SQL
1. Después de instalar Azure Data Studio Insiders, conéctese a una instancia de clúster de macrodatos de SQL Server.
2. Después de conectarse correctamente, haga clic con el botón derecho en el nombre del servidor en el viewlet Conexiones y haga clic en **Administrar**.
3. En el panel, haga clic en **Clúster de macrodatos de SQL Server**. Haga clic en **Guía de SQL Server 2019** para abrir el libro de Jupyter con los cuadernos que necesita.
    ![button](media/manage-notebooks/jupyter-book-button.png)

1. Se abrirá Jupyter Books Viewlet con el libro de Jupyter de TSG ya abierto.
4. Haga clic en el cuaderno de la tarea que debe completar.

### <a name="controller-dashboard"></a>Panel del controlador
1. En la vista **conexiones** , expanda **SQL Server clústeres de Big Data.**
2. Agregue los detalles del punto de conexión del controlador.
3. Después de conectarse correctamente al controlador, haga clic con el botón derecho en el extremo y haga clic en **administrar.**
4. Después de cargar el panel, haga clic en solucionar problemas para iniciar el libro de Jupyter.

## <a name="how-to-use-troubleshooting-notebooks"></a>Cómo usar cuadernos de solución de problemas
1. Examine la tabla de contenido existente del libro de Jupyter hasta encontrar el TSG que necesite.
1. Todos los notebooks están optimizados, donde el usuario solo tiene que hacer clic en **Ejecutar celdas.** Esto ejecutará cada celda del cuaderno individualmente hasta que se complete.
1. Si se genera un error, el libro Jupyter sugerirá un cuaderno que puede ejecutar para corregir el error. Siga los pasos y vuelva a ejecutar el cuaderno.

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre los cuadernos en Azure Data Studio, vea [Uso de los cuadernos en la versión preliminar de SQL Server 2019](notebooks-guidance.md).
