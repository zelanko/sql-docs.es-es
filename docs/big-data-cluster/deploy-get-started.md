---
title: Introducción
titleSuffix: SQL Server Big Data Clusters
description: Conozca los pasos y recursos para implementar clústeres de macrodatos de SQL Server.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 0f6600b6578abe0a9b72dff8fee2d815b0771c0c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "82178136"
---
# <a name="get-started-with-big-data-clusters-2019-deployment"></a>Introducción a la implementación de [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se ofrece información general sobre cómo implementar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]. En este artículo se presentan los conceptos y se ofrece un marco para comprender los escenarios de implementación. Los pasos de implementación específicos varían en función de las opciones de plataforma para el cliente y el servidor. Para obtener una introducción sobre [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], vea [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]](big-data-cluster-overview.md).

Para otros escenarios de implementación de SQL Server, vea:

- [Windows](../database-engine/install-windows/install-sql-server.md)
- [Linux](../linux/sql-server-linux-setup.md)
- [Contenedores de Docker](../linux/sql-server-linux-configure-docker.md)

## <a name="quick-introduction"></a>Introducción rápida 

Vea este vídeo de 9 minutos para obtener información general sobre cómo implementar clústeres de macrodatos:

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Big-Data-Clusters-deployment-overview/player?WT.mc_id=dataexposed-c9-niner]


> [!TIP]
> Para lograr rápidamente un entorno con Kubernetes y un clúster de macrodatos implementados que le ayude a aumentar sus capacidades, use uno de los scripts de ejemplo de la [sección de scripts](#scripts). Después de la implementación, para administrar el clúster, use las [herramientas de cliente](#tools) de la sección siguiente.


## <a name="client-tools"></a><a id="tools"></a> Herramientas de cliente

Los clústeres de macrodatos requieren un conjunto específico de herramientas de cliente. Antes de implementar un clúster de macrodatos en Kubernetes, debe instalar las herramientas siguientes:

| Herramienta | Descripción |
|---|---|
| **azdata** | Implementa y administra clústeres de macrodatos. |
| **kubectl** | Crea y administra el clúster de Kubernetes subyacente. |
| **Azure Data Studio** | Interfaz gráfica para usar el clúster de macrodatos. |
| **Extensión de SQL Server 2019** | Extensión de Azure Data Studio que habilita las características de clúster de macrodatos. |

Se requieren otras herramientas para distintos escenarios. Cada artículo debe explicar las herramientas de requisitos previos para realizar una tarea específica. Para obtener una lista completa de las herramientas y los vínculos de instalación, consulte [Instalación de herramientas de macrodatos de SQL Server 2019](deploy-big-data-tools.md).

## <a name="kubernetes"></a>Kubernetes

Los clústeres de macrodatos se implementan como una serie de contenedores interrelacionados que se administran en [Kubernetes](https://kubernetes.io/docs/home). Puede hospedar Kubernetes de varias maneras. Incluso si ya tiene un entorno de Kubernetes existente, debe revisar los requisitos relacionados con los clústeres de macrodatos.

- **Azure Kubernetes Service (AKS)** : AKS le permite implementar un clúster de Kubernetes administrado en Azure. Usted solo administra y mantiene los nodos del agente. Con AKS, no tiene que aprovisionar su propio hardware para el clúster. También es fácil usar un [script de Python](quickstart-big-data-cluster-deploy.md) o un [cuaderno de implementación](notebooks-deploy.md) para crear el clúster de AKS e implementar el clúster de macrodatos en un solo paso. Para obtener más información sobre la configuración de AKS para una implementación de clúster de macrodatos, vea [Configuración de Azure Kubernetes Service para implementaciones de [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]](deploy-on-aks.md).

- **Varias máquinas**: También puede implementar Kubernetes en varias máquinas Linux, que podrían ser servidores físicos o máquinas virtuales. La herramienta [kubeadm](https://kubernetes.io/docs/setup/independent/create-cluster-kubeadm/) se puede usar para crear el clúster de Kubernetes. Puede usar un [script de Bash](deployment-script-single-node-kubeadm.md) para automatizar este tipo de implementación. Este método funciona bien si ya tiene una infraestructura existente que quiere usar para el clúster de macrodatos. Para obtener más información sobre el uso de implementaciones de **kubeadm** con clústeres de macrodatos, vea [Configuración de Kubernetes en varios equipos para implementaciones de [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]](deploy-with-kubeadm.md).

## <a name="deploy-a-big-data-cluster"></a>Implementación de un clúster de macrodatos

Después de configurar Kubernetes, implemente un clúster de macrodatos con el comando `azdata bdc create`. Al implementar, puede adoptar varios enfoques diferentes.

- Si va a implementar en un entorno de desarrollo y pruebas, puede optar por usar una de las [configuraciones predeterminadas](deployment-guidance.md#deploy) que proporciona **azdata**.

- Para personalizar la implementación, puede crear y usar sus propios [archivos de configuración de implementación](deployment-guidance.md#configfile).

- En el caso de una instalación completamente desatendida, puede pasar todas las demás configuraciones en variables de entorno. Para obtener más información, consulte [implementaciones desatendidas](deployment-guidance.md#unattended).


## <a name="deployment-scripts"></a><a id="scripts"></a> Scripts de implementación

Los scripts de implementación pueden ayudar a implementar clústeres de Kubernetes y de macrodatos en un solo paso. También suelen proporcionar valores predeterminados para la configuración del clúster de macrodatos. Puede personalizar cualquier script de implementación creando una versión que configure de forma diferente la implementación del clúster de macrodatos.

Actualmente los están disponibles los siguientes scripts de implementación:

- [Script de Python: implementación de un clúster de macrodatos en Azure Kubernetes Service (AKS)](quickstart-big-data-cluster-deploy.md)
- [Script de Bash: implementación de un clúster de macrodatos en un clúster de kubeadm de un solo nodo](deployment-script-single-node-kubeadm.md)

## <a name="deployment-notebooks"></a>Cuadernos de implementación

También puede implementar un clúster de macrodatos mediante la ejecución de un cuaderno Azure Data Studio. Para obtener más información sobre cómo usar un cuaderno para implementaciones en AKS, vea el artículo siguiente:

- [Implementación de un clúster de macrodatos con cuadernos de Azure Data Studio](notebooks-deploy.md).

## <a name="next-steps"></a>Pasos siguientes

Después de implementar correctamente un clúster de macrodatos, [conéctese al clúster](connect-to-big-data-cluster.md) y considere la posibilidad de [cargar datos de ejemplo](tutorial-load-sample-data.md) para su uso con varios tutoriales.
