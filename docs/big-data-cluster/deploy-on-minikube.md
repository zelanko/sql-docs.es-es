---
title: Configuración de Minikube
titleSuffix: SQL Server big data clusters
description: Aprenda a configurar Minikube para implementaciones de clústeres de macrodatos de SQL Server 2019 (versión preliminar) en un solo equipo.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 1991176de132062c46f36f30f4f384e483c069f9
ms.sourcegitcommit: 316c25fe7465b35884f72928e91c11eea69984d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/13/2019
ms.locfileid: "68969413"
---
# <a name="configure-minikube-for-sql-server-big-data-cluster-deployments"></a>Configuración de Minikube para implementaciones de clústeres de macrodatos de SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se explica cómo configurar **Minikube** en un solo equipo para implementaciones de clústeres de macrodatos de SQL Server 2019 (versión preliminar). Minikube es una herramienta que facilita la ejecución de Kubernetes en un solo equipo, por ejemplo uno portátil o de escritorio. Minikube ejecuta un clúster de Kubernetes de un solo nodo dentro de una máquina virtual del equipo portátil para los usuarios que quieren probar Kubernetes o desarrollar con él cada día. 

## <a name="prerequisites"></a>Requisitos previos

- 64 GB de memoria.

- Si el equipo solo tiene la memoria mínima recomendada, configure la implementación del clúster para que tenga una sola instancia de grupo de proceso, una instancia de grupo de datos y una instancia de bloque de almacenamiento. Esta configuración solo se debe usar para entornos de evaluación en los que la durabilidad y disponibilidad de los datos no importan. Vea la [documentación de implementación](deployment-guidance.md#configfile) para obtener más información sobre las variables de entorno que se deben establecer para configurar el número de réplicas de los grupos de datos, grupos de proceso y bloques de almacenamiento.

- La virtualización VT-x o AMD-v debe estar habilitada en el BIOS del equipo.

## <a name="install-dependencies"></a>Instalar dependencias

1. Instale [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/).

1. Si aún no tiene un hipervisor instalado, instale uno ahora.
   - En OS X, instale [xhyve driver](https://git.k8s.io/minikube/docs/drivers.md), [VirtualBox](https://www.virtualbox.org/wiki/Downloads) o [VMware Fusion](https://www.vmware.com/products/fusion).
   - En Linux, instale [VirtualBox](https://www.virtualbox.org/wiki/Downloads) o [KVM](https://www.linux-kvm.org/).
   - En Windows, instale [VirtualBox](https://www.virtualbox.org/wiki/Downloads) o [Hyper-V](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install). Si no tiene un conmutador externo configurado en Hyper-V, cree uno con acceso de red externo. Aprenda a [crear un conmutador externo en Hyper-V para minikube](https://blogs.msdn.microsoft.com/wasimbloch/2017/01/23/setting-up-kubernetes-on-windows10-laptop-with-minikube/).

## <a name="install-minikube"></a>Instalación de Minikube

Instale la versión de minikube según las instrucciones de la [versión v 1.3.0](https://github.com/kubernetes/minikube/releases/tag/v1.3.0). El clúster de macrodatos SQL Server 2019 (versión preliminar) solo funciona con la versión v 1.0.0 y versiones up.

## <a name="create-a-minikube-cluster"></a>Creación de un clúster de Minikube

El comando siguiente crea un clúster de minikube en una máquina virtual de Hyper-V con 8 CPU, 64 GB de memoria y un tamaño de disco de 100 GB. El tamaño de disco no es espacio reservado.  Aumenta a ese tamaño en disco según sea necesario.  Se recomienda no cambiar el espacio en disco a un valor inferior a 100 GB, ya que durante las pruebas se han experimentado problemas con eso. También especifica el conmutador de Hyper-V con acceso externo explícitamente.

Cambie parámetros como **--memory** según sea necesario en función del hardware disponible y del hipervisor que se use.  Asegúrese de que el valor del parámetro de conmutador virtual **--hyper-v** coincida con el nombre usado al crear el conmutador virtual.

```bash
minikube start --vm-driver="hyperv" --cpus 8 --memory 65536 --disk-size 100g --hyperv-virtual-switch "External"
```

Si usa Minikube con VirtualBox, el comando tendría este aspecto:

```base
minikube start --cpus 8 --memory 65536 --disk-size 100g
```

## <a name="disable-automatic-checkpoint-with-hyper-v"></a>Deshabilitar el punto de comprobación automático con Hyper-V

En Windows 10, el punto de comprobación automático está habilitado en una máquina virtual. Ejecute el comando siguiente en PowerShell para deshabilitar el punto de comprobación automático en la máquina virtual y establecer la memoria en estática.

```PowerShell
Set-VM -Name minikube -CheckpointType Disabled -AutomaticCheckpointsEnabled $false -StaticMemory
```

## <a name="next-steps"></a>Pasos siguientes

En los pasos de este artículo se ha configurado un clúster de Minikube. El siguiente paso es implementar un clúster de macrodatos de SQL Server 2019. Para obtener instrucciones, vea el siguiente artículo:

[Implementación de clústeres de macrodatos de SQL Server 2019 en Kubernetes](deployment-guidance.md#deploy)
