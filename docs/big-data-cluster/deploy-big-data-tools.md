---
title: Instalación de herramientas de macrodatos
titleSuffix: SQL Server big data clusters
description: Obtenga información sobre cómo instalar herramientas usadas con clústeres de macrodatos de SQL Server 2019 (versión preliminar).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 757209ff89fd40dcc737b65d3b19f2a7d4ef247b
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419461"
---
# <a name="install-sql-server-2019-big-data-tools"></a>Instalación de herramientas de macrodatos SQL Server 2019

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se describen las herramientas de cliente que se deben instalar para crear, administrar y usar clústeres de macrodatos SQL Server 2019 (versión preliminar). En la siguiente sección se proporciona una lista de herramientas y vínculos a instrucciones de instalación. Antes de implementar un clúster de Big Data, configure las herramientas marcadas como necesarias en Windows o Linux.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="big-data-cluster-tools"></a>Herramientas de clúster de Big Data

En la tabla siguiente se enumeran las herramientas de clúster de Big Data comunes y cómo instalarlas:

| Herramienta | Obligatorio | Descripción | Instalación |
|---|---|---|---|
| **Python** | Sí | Python es un lenguaje de programación interpretado, orientado a objetos y de alto nivel con semántica dinámica. Muchas partes de los clústeres de macrodatos para SQL Server usan Python. | [Instalación de Python](#python)|
| **azdata** | Sí | Herramienta de línea de comandos para instalar y administrar un clúster de Big Data. | [Instalar](deploy-install-azdata.md) |
| **kubectl** <sup>1</sup> | Sí | Herramienta de línea de comandos para supervisar el clúster de Kuberentes subyacente ([más información](https://kubernetes.io/docs/tasks/tools/install-kubectl/)). | [Windows](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-with-powershell-from-psgallery) \| [Linux](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management) |
| **Azure Data Studio (Insider)** | Sí | Herramienta gráfica multiplataforma para consultar SQL Server ([más información](https://docs.microsoft.com/sql/azure-data-studio/what-is?view=sql-server-ver15)). | [Instalar](https://aka.ms/azdata-insiders) |
| **SQL Server extensión 2019** | Sí | Extensión de Azure Data Studio que admite la conexión al clúster de Big Data. También proporciona un asistente para la virtualización de datos. | [Instalar](../azure-data-studio/sql-server-2019-extension.md) |
| **CLI de Azure** <sup>2</sup> | Para AKS | Interfaz de línea de comandos moderna para administrar servicios de Azure. Se usa con implementaciones de clúster de macrodatos de AKS ([más información](https://docs.microsoft.com/cli/azure/?view=azure-cli-latest)). | [Instalar](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) |
| **mssql-cli** | Opcional | Interfaz de línea de comandos moderna para consultar SQL Server ([más información](https://github.com/dbcli/mssql-cli/blob/master/README.rst)). | [Windows](https://github.com/dbcli/mssql-cli/blob/master/doc/installation/windows.md) \| [Linux](https://github.com/dbcli/mssql-cli/blob/master/doc/installation/linux.md) |
| **sqlcmd** | Para algunos scripts | Herramienta de línea de comandos heredada para consultar SQL Server ([más información](https://docs.microsoft.com/sql/tools/sqlcmd-utility?view=sql-server-ver15)). | [Windows](https://www.microsoft.com/download/details.aspx?id=36433) \| [Linux](../linux/sql-server-linux-setup-tools.md) |
| **rizo** <sup>3</sup> | Para algunos scripts | Herramienta de línea de comandos para transferir datos con direcciones URL. | [Windows](https://curl.haxx.se/windows/) \| Linux: instalación de un paquete de rizo |

<sup>1</sup> debe usar la versión 1,10 de kubectl o posterior. Además, la versión de kubectl debe ser más o menos una versión secundaria del clúster de Kubernetes. Si quiere instalar una versión específica en el cliente de kubectl, consulte [instalación del archivo binario de kubectl mediante rizo](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-curl) (en Windows 10, uso de cmd. exe y no de Windows PowerShell para ejecutar rizo). 

> [!TIP]
> Para usar kubectl con un clúster implementado previamente en Azure Kubernetes Service (AKS), debe establecer el contexto de clúster con el siguiente comando de CLI de Azure:
>
>    ```azurecli
>    az aks get-credentials --name <aks_cluster_name> --resource-group <azure_resource_group_name>
>    ```

<sup>2</sup> debe usar CLI de Azure versión 2.0.4 o posterior. Ejecute `az --version` para encontrar la versión si es necesario.

<sup>3</sup> si se ejecuta en Windows 10, el **rizo** ya está en la ruta de acceso cuando se ejecuta desde un símbolo del sistema. Para otras versiones de Windows, descargue **rizo** con el vínculo y colóquelo en la ruta de acceso.

## <a name="which-tools-are-required"></a>¿Qué herramientas son necesarias?

En la tabla anterior se proporcionan todas las herramientas comunes que se usan con los clústeres de Big Data. Las herramientas necesarias dependen de su escenario. Pero en general, las siguientes herramientas son más importantes para administrar, conectarse y consultar el clúster:

- **azdata**
- **kubectl**
- **Azure Data Studio**
- **SQL Server extensión 2019**

Las herramientas restantes solo son necesarias en ciertos escenarios. **CLI de Azure** se puede usar para administrar los servicios de Azure asociados a las implementaciones de AKS. **MSSQL-CLI** es una herramienta opcional pero útil que le permite conectarse al SQL Server instancia maestra del clúster y ejecutar consultas desde la línea de comandos. Y **sqlcmd** y **doblez** son necesarios si tiene previsto instalar datos de ejemplo con el script de github.

### <a id="python"></a>Instalación de Python sin conexión

1. En una máquina con acceso a Internet, descargue uno de los siguientes archivos comprimidos que contienen Python:

   | Sistema operativo | Descargar |
   |---|---|
   | Windows | [https://go.microsoft.com/fwlink/?linkid=2074021](https://go.microsoft.com/fwlink/?linkid=2074021) |
   | Linux   | [https://go.microsoft.com/fwlink/?linkid=2065975](https://go.microsoft.com/fwlink/?linkid=2065975) |
   | OSX     | [https://go.microsoft.com/fwlink/?linkid=2065976](https://go.microsoft.com/fwlink/?linkid=2065976) |

1. Copie el archivo comprimido en el equipo de destino y extráigalo en una carpeta de su elección.

1. Solo para Windows, ejecute `installLocalPythonPackages.bat` desde esa carpeta y pase la ruta de acceso completa a la misma carpeta que un parámetro.

   ```PowerShell
   installLocalPythonPackages.bat "C:\python-3.6.6-win-x64-0.0.1-offline\0.0.1"
   ```

## <a name="next-steps"></a>Pasos siguientes

Después de configurar las herramientas, implemente un clúster de macrodatos SQL Server 2019 en Kubernetes en la nube o de forma local. Para obtener más información, consulte los siguientes artículos de implementación:

- [Inicio rápido: Implementación de SQL Server clúster de macrodatos en Azure Kubernetes Service (AKS)](quickstart-big-data-cluster-deploy.md)
- [Cómo implementar clústeres de macrodatos SQL Server en Kubernetes](deployment-guidance.md)

Para obtener más información sobre los clústeres de Big Data, consulte [¿Qué son los clústeres de macrodatos SQL Server 2019?](big-data-cluster-overview.md).
