---
title: Introducción
titleSuffix: SQL Server big data clusters
description: Conozca los pasos y los recursos para la [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] implementación (versión preliminar).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 323394f9590551528ce9e9dfdf1fb97c7d1c2225
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653391"
---
# <a name="get-started-with-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>Introducción[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se proporciona información general sobre cómo [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]](big-data-cluster-overview.md)implementar. Está diseñado para darle una idea sobre los conceptos y proporcionar un marco para comprender los demás artículos de implementación de esta sección. Los pasos de implementación específicos varían en función de las opciones de plataforma para el cliente y el servidor.

> [!TIP]
> Para obtener rápidamente un entorno con Kubernetes y un clúster de Big Data implementado para ayudarle a aumentar sus capacidades, use uno de los scripts de ejemplo señalados en [la sección scripts](#scripts). Después de la implementación, para administrar el clúster, use las [herramientas de cliente](#tools) de la sección siguiente.

## <a id="tools"></a> Herramientas de cliente

Los clústeres de macrodatos requieren un conjunto específico de herramientas de cliente. Antes de implementar un clúster de macrodatos en Kubernetes, debe instalar las herramientas siguientes:

| Herramienta | Descripción |
|---|---|
| **azdata** | Implementa y administra clústeres de macrodatos. |
| **kubectl** | Crea y administra el clúster de Kubernetes subyacente. |
| **Azure Data Studio** | Interfaz gráfica para usar el clúster de macrodatos. |
| **Extensión de SQL Server 2019** | Extensión de Azure Data Studio que habilita las características de clúster de macrodatos. |

Se requieren otras herramientas para distintos escenarios. Cada artículo debe explicar las herramientas de requisitos previos para realizar una tarea específica. Para obtener una lista completa de las herramientas y los vínculos de instalación, consulte [Instalación de herramientas de macrodatos de SQL Server 2019](deploy-big-data-tools.md).

## <a name="kubernetes"></a>Kubernetes

Los clústeres de macrodatos se implementan como una serie de contenedores interrelacionados que se administran en [Kubernetes](https://kubernetes.io/docs/home). Puede hospedar Kubernetes de varias maneras. Incluso si ya tiene un entorno de Kubernetes existente, debe revisar los requisitos relacionados con los clústeres de macrodatos.

- **Azure Kubernetes Service (AKS)** : AKS le permite implementar un clúster de Kubernetes administrado en Azure. Usted solo administra y mantiene los nodos del agente. Con AKS, no tiene que aprovisionar su propio hardware para el clúster. También es fácil usar un [script de Python](quickstart-big-data-cluster-deploy.md) o un [cuaderno de implementación](deploy-notebooks.md) para crear el clúster de AKS e implementar el clúster de macrodatos en un solo paso. Para obtener más información sobre la configuración de AKS para una implementación de clúster de Big Data, consulte [configuración de Azure Kubernetes [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] Service for Deployments](deploy-on-aks.md).

- **Varias máquinas**: También puede implementar Kubernetes en varias máquinas Linux, que podrían ser servidores físicos o máquinas virtuales. La herramienta [kubeadm](https://kubernetes.io/docs/setup/independent/create-cluster-kubeadm/) se puede usar para crear el clúster de Kubernetes. Puede usar un [script de Bash](deployment-script-single-node-kubeadm.md) para automatizar este tipo de implementación. Este método funciona bien si ya tiene una infraestructura existente que quiere usar para el clúster de macrodatos. Para más información sobre el uso de implementaciones de **kubeadm** con clústeres de macrodatos, consulte [configuración de [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] Kubernetes en varias máquinas para implementaciones](deploy-with-kubeadm.md).

- **Minikube**: Minikube le permite ejecutar Kubernetes localmente en un solo servidor. Es una buena opción si está probando clústeres de macrodatos o necesita usarlo en un escenario de prueba o desarrollo. Para obtener más información sobre cómo utilizar Minikube, vea la [documentación de Minikube](https://kubernetes.io/docs/setup/minikube/). Para conocer los requisitos específicos del uso de Minikube con clústeres de macrodatos, consulte [Configuración de Minikube para implementaciones de clústeres de macrodatos de SQL Server 2019](deploy-on-minikube.md).

## <a name="deploy-a-big-data-cluster"></a>Implementación de un clúster de macrodatos

Después de configurar Kubernetes, implemente un clúster de macrodatos con el comando `azdata bdc create`. Al implementar, puede adoptar varios enfoques diferentes.

- Si va a implementar en un entorno de desarrollo y pruebas, puede optar por usar una de las [configuraciones predeterminadas](deployment-guidance.md#deploy) que proporciona **azdata**.

- Para personalizar la implementación, puede crear y usar sus propios [archivos de configuración de implementación](deployment-guidance.md#configfile).

- En el caso de una instalación completamente desatendida, puede pasar todas las demás configuraciones en variables de entorno. Para obtener más información, consulte [implementaciones desatendidas](deployment-guidance.md#unattended).


## <a id="scripts"></a>Scripts de implementación

Los scripts de implementación pueden ayudar a implementar clústeres de Kubernetes y de macrodatos en un solo paso. También suelen proporcionar valores predeterminados para la configuración del clúster de macrodatos. Puede personalizar cualquier script de implementación creando una versión que configure de forma diferente la implementación del clúster de macrodatos.

Actualmente los están disponibles los siguientes scripts de implementación:

- [Script de Python: implementación de un clúster de macrodatos en Azure Kubernetes Service (AKS)](quickstart-big-data-cluster-deploy.md)
- [Script de Bash: implementación de un clúster de macrodatos en un clúster de kubeadm de un solo nodo](deployment-script-single-node-kubeadm.md)

## <a name="deployment-notebooks"></a>Cuadernos de implementación

También puede implementar un clúster de macrodatos mediante la ejecución de un cuaderno Azure Data Studio. Para obtener más información sobre cómo usar un cuaderno para implementaciones en AKS, vea el artículo siguiente:

- [Implementación de un clúster de macrodatos con cuadernos de Azure Data Studio](deploy-notebooks.md).

## <a name="next-steps"></a>Pasos siguientes

Después de implementar correctamente un clúster de macrodatos, [conéctese al clúster](connect-to-big-data-cluster.md) y considere la posibilidad de [cargar datos de ejemplo](tutorial-load-sample-data.md) para su uso con varios tutoriales.
