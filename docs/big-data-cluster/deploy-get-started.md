---
title: Introducción
titleSuffix: SQL Server big data clusters
description: Obtenga información sobre los pasos y recursos para la implementación de clústeres de macrodatos de 2019 de SQL Server (versión preliminar).
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/18/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 69b5d9b69536243d371cb45c1c46620f5194657d
ms.sourcegitcommit: 2de5446fbc57787f18a907dd5deb02a7831ec07d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/02/2019
ms.locfileid: "58860436"
---
# <a name="get-started-with-sql-server-big-data-clusters"></a>Empezar a trabajar con clústeres grandes de datos de SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo proporciona información general sobre cómo implementar un [clúster de macrodatos (versión preliminar) de SQL Server 2019](big-data-cluster-overview.md). Está diseñada para orientarse a los conceptos y proporcionar un marco para entender los otros artículos de implementación de esta sección. Los pasos de implementación específicos varían en función de las opciones de plataforma para el cliente y servidor.

## <a id="tools"></a> herramientas de cliente

Los clústeres de datos de gran tamaño requieren un conjunto específico de las herramientas de cliente. Antes de implementar un clúster de macrodatos en Kubernetes, debe instalar las herramientas siguientes:

| Herramienta | Descripción |
|---|---|
| **mssqlctl** | Implementa y administra los clústeres de datos de gran tamaño. |
| **kubectl** | Crea y administra el clúster de Kubernetes subyacente. |
| **Azure Data Studio ** | Interfaz gráfica para el uso del clúster de macrodatos. |
| **Extensión de SQL Server 2019** | Extensión de Azure Data Studio que habilita características de clúster de macrodatos. |

Otras herramientas son necesarias para diferentes escenarios. Cada artículo debe explicar las herramientas de requisitos previos para realizar una tarea específica. Para obtener una lista completa de herramientas y vínculos de instalación, consulte [herramientas de macrodatos de instalar SQL Server 2019](deploy-big-data-tools.md).

## <a name="kubernetes"></a>Kubernetes

Los clústeres de datos de gran tamaño se implementan como una serie de contenedores interrelacionados que se administran en [Kubernetes](https://kubernetes.io/docs/home). Puede hospedar Kubernetes en una variedad de formas. Incluso si ya tiene un entorno de Kubernetes existente, debe revisar los requisitos relacionados para los clústeres de datos de gran tamaño.

- **Azure Kubernetes Service (AKS)**: AKS permite implementar un clúster de Kubernetes administrado en Azure. Solo debe administrar y mantener los nodos de agente. Con AKS, no tienes que proporcionar su propio hardware para el clúster. También es fácil de usar un clúster de macrodatos [script de implementación](quickstart-big-data-cluster-deploy.md) para crear el clúster de AKS e implementar el clúster de macrodatos en un solo paso. Para obtener más información sobre el uso de AKS con los clústeres de datos de gran tamaño, vea [configurar Azure Kubernetes Service para las implementaciones de clústeres (versión preliminar) de datos de gran tamaño de SQL Server 2019](deploy-on-aks.md).

- **Varias máquinas**: También puede implementar Kubernetes a varias máquinas de Linux, que podrían ser servidores físicos o máquinas virtuales. El [kubeadm](https://kubernetes.io/docs/setup/independent/create-cluster-kubeadm/) herramienta puede usarse para crear el clúster de Kubernetes. Este método funciona bien si ya tiene una infraestructura existente que desea usar para el clúster de macrodatos. Para obtener más información sobre el uso de **kubeadm** implementaciones con los clústeres de datos de gran tamaño, consulte [Kubernetes configurar en varios equipos para las implementaciones de clústeres (versión preliminar) de datos de gran tamaño de SQL Server 2019](deploy-with-kubeadm.md).

- **Minikube**: Minikube permite ejecutar Kubernetes localmente en un único servidor. Es una buena opción si está probando de clústeres de datos de gran tamaño o si necesita usarlo en un escenario de prueba o desarrollo. Para obtener más información sobre el uso de Minikube, consulte el [Minikube documentación](https://kubernetes.io/docs/setup/minikube/). Para conocer los requisitos específicos para usar Minikube con clústeres de datos de gran tamaño, vea [configurar minikube para las implementaciones de clústeres de SQL Server 2019 macrodatos](deploy-on-minikube.md).

## <a name="deployment-scripts"></a>Scripts de implementación

Scripts de implementación pueden ayudar a implementar Kubernetes y clústeres de datos de gran tamaño en un solo paso. Con frecuencia, también proporcionan valores predeterminados para las variables de entorno necesarias. Para obtener un ejemplo de un script de implementación para el clúster de macrodatos en Azure Kubernetes Service (AKS), consulte [implementar un clúster de macrodatos con un script de implementación (AKS) de SQL Server 2019](quickstart-big-data-cluster-deploy.md).

Puede personalizar cualquier script de implementación mediante la creación de su propia versión que configura las variables de entorno de clúster de macrodatos de manera diferente.

## <a name="deploy-a-big-data-cluster"></a>Implementación de un clúster de macrodatos

Para implementar Kubernetes y un clúster de macrodatos en AKS con una única secuencia de comandos, vea el ejemplo siguiente:

- [Implementar un clúster de macrodatos de 2019 de SQL Server con un script de implementación (AKS)](quickstart-big-data-cluster-deploy.md)

Para instrucciones detalladas para la implementación de clústeres de macrodatos con AKS, kubeadm y MiniKube, consulte el artículo siguiente:

- [Cómo implementar clústeres de macrodatos de SQL Server en Kubernetes](deployment-guidance.md)

## <a name="next-steps"></a>Pasos siguientes

Después de implementar correctamente un clúster de macrodatos, [conectarse al clúster](connect-to-big-data-cluster.md) y considere la posibilidad de [cargar datos de ejemplo](tutorial-load-sample-data.md) para su uso con diversos tutoriales.