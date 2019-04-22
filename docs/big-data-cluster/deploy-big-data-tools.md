---
title: Instalación de herramientas de macrodatos
titleSuffix: SQL Server big data clusters
description: Obtenga información sobre cómo instalar las herramientas que se usan con los clústeres de macrodatos de 2019 de SQL Server (versión preliminar).
author: rothja
ms.author: jroth
manager: craigg
ms.date: 01/17/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: dc53bdfb71efeafd55752686ff136355bc79bd34
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "58860486"
---
# <a name="install-sql-server-2019-big-data-tools"></a>Instalar las herramientas de macrodatos de SQL Server 2019

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se describe las herramientas de cliente que se deben instalar para crear, administrar, y con SQL Server 2019 macrodatos clústeres (versión preliminar). La siguiente sección proporciona una lista de herramientas y vínculos a instrucciones de instalación. Antes de implementar un clúster de macrodatos, configure las herramientas marcadas como necesarias en Windows o Linux.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="big-data-cluster-tools"></a>Herramientas de clúster de macrodatos

En la tabla siguiente se enumera herramientas comunes de clúster de macrodatos y cómo instalarlos:

| Herramienta | Obligatorio | Descripción | Instalación |
|---|---|---|---|
| **mssqlctl** | Sí | Herramienta de línea de comandos para instalar y administrar un clúster de macrodatos. | [Instalar](deploy-install-mssqlctl.md) |
| **kubectl**<sup>1</sup> | Sí | Herramienta de línea de comandos para supervisar el clúster Kuberentes subyacente ([obtener más información](https://kubernetes.io/docs/tasks/tools/install-kubectl/)). | [Windows](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-with-powershell-from-psgallery) \| [Linux](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management) |
| **Azure Data Studio** | Sí | Herramienta gráfica multiplataforma para realizar consultas en SQL Server ([obtener más información](https://docs.microsoft.com/sql/azure-data-studio/what-is?view=sql-server-ver15)). | [Instalar](../azure-data-studio/download.md) |
| **Extensión de SQL Server 2019** | Sí | Extensión de Azure Data Studio que admite la conexión al clúster de macrodatos. También proporciona a un Asistente para la virtualización de datos. | [Instalar](../azure-data-studio/sql-server-2019-extension.md) |
| **Azure CLI**<sup>2</sup> | Para AKS | Interfaz de línea de comandos moderna para la administración de servicios de Azure. Puede usar con las implementaciones de clústeres AKS macrodatos ([obtener más información](https://docs.microsoft.com/cli/azure/?view=azure-cli-latest)). | [Instalar](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) |
| **mssql-cli** | Opcional | Interfaz de línea de comandos moderna para realizar consultas en SQL Server ([obtener más información](https://github.com/dbcli/mssql-cli/blob/master/README.rst)). | [Windows](https://github.com/dbcli/mssql-cli/blob/master/doc/installation/windows.md) \| [Linux](https://github.com/dbcli/mssql-cli/blob/master/doc/installation/linux.md) |
| **sqlcmd** | Para algunas secuencias de comandos | Herramienta de línea de comandos heredado para realizar consultas en SQL Server ([obtener más información](https://docs.microsoft.com/sql/tools/sqlcmd-utility?view=sql-server-ver15)). | [Windows](https://www.microsoft.com/download/details.aspx?id=36433) \| [Linux](../linux/sql-server-linux-setup-tools.md) |
| **curl** <sup>3</sup> | Para algunas secuencias de comandos | Herramienta de línea de comandos para la transferencia de datos con las direcciones URL. | [Windows](https://curl.haxx.se/windows/) \| Linux: paquete de instalación de curl |

<sup>1</sup> debe usar la versión de kubectl 1,10 o posterior. Además, la versión de kubectl debe ser más o menos de una versión secundaria de un clúster de Kubernetes. Si desea instalar una versión específica en el cliente kubectl, consulte [instalar kubectl binario mediante curl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-curl) (en Windows 10, use cmd.exe y no de Windows PowerShell para ejecutar curl). 

> [!TIP]
> Para usar kubectl con un clúster implementado previamente en Azure Kubernetes Service (AKS), debe establecer el contexto de clúster con el siguiente comando de CLI de Azure:
>
>    ```azurecli
>    az aks get-credentials --name <aks_cluster_name> --resource-group <azure_resource_group_name>
>    ```

<sup>2</sup> debe usar la CLI de Azure versión 2.0.4 o posterior. Ejecute `az --version` para buscar la versión si es necesario.

<sup>3</sup> si está ejecutando en Windows 10, **curl** ya está en la ruta de acceso cuando se ejecuta desde un símbolo del sistema. Para otras versiones de Windows, descargue **curl** mediante el vínculo y colóquelo en la ruta de acceso.

## <a name="which-tools-are-required"></a>¿Las herramientas que son necesarias?

La tabla anterior proporciona todas las herramientas comunes que se usan con los clústeres de datos de gran tamaño. Se requieren las herramientas que depende de su escenario. Pero en general, son más importantes para administrar, conectarse a y consultar el clúster de las siguientes herramientas:

- **mssqlctl**
- **kubectl**
- **Azure Data Studio**
- **Extensión de SQL Server 2019**

Las herramientas restantes son necesarias solo en determinados escenarios. **CLI de Azure** puede usarse para administrar los servicios de Azure asociados con implementaciones de AKS. **MSSQL-cli** es una herramienta opcional pero muy útil que le permite conectarse a la instancia principal de SQL Server en el clúster y ejecutar consultas desde la línea de comandos. Y **sqlcmd** y **curl** son necesarios si va a instalar los datos de ejemplo con el script de GitHub.

## <a name="next-steps"></a>Pasos siguientes

Después de configurar las herramientas, implemente un clúster de macrodatos de 2019 de SQL Server en Kubernetes en la nube o local. Para obtener más información, consulte los siguientes artículos de implementación:

- [Inicio rápido: Implementar el clúster de macrodatos de SQL Server en Azure Kubernetes Service (AKS)](quickstart-big-data-cluster-deploy.md)
- [Cómo implementar clústeres de macrodatos de SQL Server en Kubernetes](deployment-guidance.md)

Para obtener más información acerca de los clústeres de datos de gran tamaño, vea [¿cuáles son los clústeres de SQL Server 2019 macrodatos?](big-data-cluster-overview.md).
