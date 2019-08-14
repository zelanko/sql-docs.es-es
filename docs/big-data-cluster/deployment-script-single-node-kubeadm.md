---
title: Implementación con un script de bash en un clúster de kubeadm de un solo nodo
titleSuffix: SQL Server big data clusters
description: Use un script de implementación de Bash para implementar un clúster de macrodatos de SQL Server 2019 (versión preliminar) en un clúster de kubeadm de un solo nodo.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 37017221b636146a003f8af8890c655ed605bca9
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "68473077"
---
# <a name="deploy-with-a-bash-script-to-a-single-node-kubeadm-cluster"></a>Implementación con un script de bash en un clúster de kubeadm de un solo nodo

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este tutorial, usará un script de implementación de bash de ejemplo para implementar un clúster de Kubernetes de un solo nodo con kubeadm y un clúster de macrodatos SQL Server en él.  

## <a name="prerequisites"></a>Prerequisites

- Una máquina virtual de **servidor** de Vanilla Ubuntu 18.04 o 16.04. El script, que se ejecuta desde la máquina virtual, configura todas las dependencias.

  > [!NOTE]
  > Todavía no se admite el uso de máquinas virtuales de Azure.

- La máquina virtual debe tener al menos 8 CPU, 64 GB de RAM y 100 GB de espacio en disco. Después de extraer todas las imágenes de Docker del clúster de macrodatos, le quedarán 50 GB para los datos y los registros de todos los componentes.

## <a name="instructions"></a>Instructions

1. Descargue el script en la máquina virtual que planea usar para la implementación.

   ```bash
   curl --output setup-bdc.sh https://raw.githubusercontent.com/microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu-single-node-vm/setup-bdc.sh
   ```

2. Ejecute el script con el siguiente comando.

   ```bash
   chmod +x setup-bdc.sh
   ```

3. Ejecute el script con **sudo**.

   ```bash
   sudo ./setup-bdc.sh
   ```

   Cuando se le solicite, proporcione la contraseña que se va a usar para los siguientes puntos de conexión externos: controlador, SQL Server maestro y puerta de enlace. De forma predeterminada, el nombre de usuario del controlador es *admin*.

4. Configure un alias para la herramienta **azdata**.

   ```bash
   source ~/.bashrc
   ```

5. Compruebe que el alias funciona.

   ```bash
   azdata --version
   ```

## <a name="next-steps"></a>Pasos siguientes

Siga [este tutorial](tutorial-load-sample-data.md) para empezar a usar el clúster de macrodatos.
