---
title: Implementación de clústeres de macrodatos de SQL Server con cuadernos de Azure Data Studio
titleSuffix: Deploy SQL Server big data cluster cluster with Azure Data Studio notebooks
description: Use un cuaderno de Azure Data Studio para implementar un clúster de macrodatos.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 18880c6cf0590c8a10c232cd2dd9d11e5279f918
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "68470788"
---
# <a name="deploy-sql-server-big-data-cluster-with-azure-data-studio-notebooks"></a>Implementación de clústeres de macrodatos de SQL Server con cuadernos de Azure Data Studio

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] proporciona una extensión para Azure Data Studio que incluye cuadernos de implementación. Un cuaderno de implementación incluye documentación y código que se puede usar en Azure Data Studio para crear un clúster de macrodatos de SQL Server.

Los [cuadernos](notebooks-guidance.md), que originalmente se implementaban como un proyecto de código abierto, se han implementado en [Azure Data Studio](http://docs.microsoft.com/sql/azure-data-studio/download). Puede usar Markdown para el texto de las celdas de texto y uno de los kernels disponibles para escribir código en las celdas de código.

Puede usar cuadernos para implementar clústeres de macrodatos para [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].

## <a name="prerequisites"></a>Prerequisites

Los siguientes requisitos previos son necesarios para poder iniciar el cuaderno:

* Versión más reciente de [Azure Data Studio](http://docs.microsoft.com/sql/azure-data-studio/download) instalada
* Extensión [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] instalada en Azure Data Studio

Además de lo anterior, la implementación de clústeres de macrodatos de SQL Server 2019 también requiere:

* [azdata](deploy-install-azdata.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [CLI de Azure](/cli/azure/install-azure-cli)

## <a name="launch-the-notebook"></a>Inicio del cuaderno

1. Instale e inicie la [compilación de Azure Data Studio Insiders](https://github.com/microsoft/azuredatastudio#try-out-the-latest-insiders-build-from-master).

1. En la pestaña **Conexiones**, haga clic en **...** y seleccione **Implementar el clúster de macrodatos de SQL Server...**

   ![IA y AML](media/deploy-notebooks/deploy-notebooks-1.png)

1. En **Deployment Target** (Destino de implementación), en **Opciones**, seleccione **New Azure Kubernetes Cluster** (Nuevo clúster de Azure Kubernetes) o **Existing Azure Kubernetes Service cluster** (Clúster de Azure Kubernetes Service existente).

1. Seleccione **Open Notebook** (Abrir cuaderno).

Esta acción inicia el cuaderno adecuado. Para completar la implementación, siga las instrucciones del cuaderno para implementar un clúster de macrodatos para [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] en un clúster de Azure Kubernetes Service existente o nuevo.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre la implementación, consulte la [guía de implementación para los clústeres de macrodatos de SQL Server](deployment-guidance.md).
