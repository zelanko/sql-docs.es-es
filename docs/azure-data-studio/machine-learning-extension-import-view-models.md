---
title: Importación o consulta de modelos con la extensión Machine Learning
titleSuffix: Azure Data Studio
description: Obtenga información sobre cómo usar la extensión Machine Learning para Azure Data Studio a fin de importar un modelo ONNX o ver los ya importados en la base de datos.
ms.date: 06/09/2020
ms.reviewer: sstein
ms.prod: azure-data-studio
ms.technology: machine-learning
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 62eb0a2c4eb4db7c86f4c5ff486a0088a20e8244
ms.sourcegitcommit: 48d60fe6b6991303a88936fb32322c005dfca2d8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/25/2020
ms.locfileid: "85352412"
---
# <a name="import-or-view-models-with-machine-learning-extension-preview-for-azure-data-studio"></a>Importación o consulta de modelos con la extensión Machine Learning (versión preliminar) para Azure Data Studio

Obtenga información sobre cómo usar la [extensión Machine Learning para Azure Data Studio](machine-learning-extension.md) a fin de importar un modelo ONNX o ver los ya importados en la base de datos.

> [!IMPORTANT]
> La importación y la consulta de una base de datos con la extensión Machine Learning actualmente solo admite [Machine Learning Services en Azure SQL Managed Instance](/azure/azure-sql/managed-instance/machine-learning-services-overview) y [Azure SQL Edge con ONNX](/azure/azure-sql-edge/onnx-overview).

## <a name="prerequisites"></a>Requisitos previos

- Instale y configure la [extensión Machine Learning para Azure Data Studio](machine-learning-extension.md). Debe especificar las [rutas de acceso de la instalación de Python en la configuración de la extensión](machine-learning-extension.md#settings).

- Los paquetes de Python **onnxruntime**, **mlflow** y **mlflow-dbstore**. Si los paquetes todavía no estás instalados, la extensión Machine Learning le pedirá que los instale.

## <a name="view-models"></a>Ver modelos

Siga los pasos que se indican a continuación para ver los modelos de ONNX almacenados en la base de datos.

1. Haga clic en **Importar o ver modelos**.

1. Si se le pide que instale **onnxruntime**, **mlflow** y **mlflow-dbstore**, haga clic en **Sí**.

1. Seleccione la **base de datos de modelos** y la **tabla de modelos** donde se almacenen los modelos.

Esto mostrará una lista de los modelos. Puede editar el nombre y la descripción del modelo, o eliminar uno de la lista.

## <a name="import-a-new-model"></a>Importación de un modelo nuevo

Siga los pasos que se indican a continuación para importar un modelo de ONNX en la base de datos.

1. Haga clic en **Importar o ver modelos**.

1. Si se le pide que instale **onnxruntime**, **mlflow** y **mlflow-dbstore**, haga clic en **Sí**.

1. Haga clic en **Importar modelos**.

1. Seleccione la **base de datos de modelos** donde quiera almacenar el modelo importado.

1. Seleccione la **tabla de modelos** donde quiera almacenar el modelo importado. Puede elegir una **tabla existente** o crear una **nueva tabla**. Haga clic en **Next**.

1. Seleccione dónde se encuentra el modelo y haga clic en **Siguiente**. Puede usar:
    - **Carga de archivos**. Elija esta opción para usar un modelo a partir de un archivo. Seleccione el archivo de modelo en **Archivos de origen** y haga clic en **Siguiente**.
    - **Azure Machine Learning**. Elija esta opción para usar un modelo de Azure Machine Learning. En primer lugar, **inicie sesión en Azure**. Después, seleccione la **cuenta de Azure**, la **suscripción de Azure**, el **grupo de recursos de Azure** y el **área de trabajo de Azure ML**. Seleccione el modelo que quiere usar y, después, haga clic en **Siguiente**.

1. Escriba el **nombre** y la **descripción** del modelo, y haga clic en **Implementar** para almacenar el modelo en la base de datos.

> [!NOTE]
> La extensión Azure Machine Learning está actualmente en versión preliminar. Por lo tanto, el esquema de tabla donde se almacenan los modelos podría cambiar en el futuro.

## <a name="next-steps"></a>Pasos siguientes

- [Extensión Machine Learning in Azure Data Studio](machine-learning-extension.md)
- [Administración de paquetes en la base de datos](machine-learning-extension-manage-packages.md)
- [Realización de predicciones](machine-learning-extension-predictions.md)
- [Importación y consulta de modelos](machine-learning-extension-import-view-models.md)
- [Documentación del aprendizaje automático en SQL](../machine-learning/index.yml)
- [Machine Learning Services en Azure SQL Managed Instance](/azure/azure-sql/managed-instance/machine-learning-services-overview)
- [Aprendizaje automático e IA con ONNX en SQL Edge (versión preliminar)](/azure/azure-sql-edge/onnx-overview)
