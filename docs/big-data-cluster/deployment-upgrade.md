---
title: Actualización a una nueva versión
titleSuffix: SQL Server Big Data Clusters
description: Aprenda a actualizar clústeres de macrodatos de SQL Server a una nueva versión.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: f44ef17a712d0d5a19707cf94e7d3e4196a2aba3
ms.sourcegitcommit: b4ad3182aa99f9cbfd15f4c3f910317d6128a2e5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/06/2019
ms.locfileid: "73706302"
---
# <a name="how-to-upgrade-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>Cómo actualizar los [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se proporcionan instrucciones para actualizar un clúster de macrodatos de SQL Server a una nueva versión. Los pasos descritos en este artículo se aplican específicamente a la actualización de una versión preliminar a la versión de actualización del servicio de SQL Server 2019.

## <a name="backup-and-delete-the-old-cluster"></a>Copia de seguridad del clúster anterior y eliminación

Actualmente, no existe ninguna actualización local para los clústeres de macrodatos. La única manera de actualizar a una nueva versión es quitar y volver a crear manualmente el clúster. Cada versión tiene una versión única de `azdata` que no es compatible con la anterior. Además, si un clúster anterior tuviera que descargar una imagen de contenedor en un nodo nuevo, es posible que la imagen más reciente no fuera compatible con las anteriores del clúster. Tenga en cuenta que la imagen más reciente se extrae solo si se usa la etiqueta de imagen `latest` en el archivo de configuración de implementación para la configuración del contenedor. De forma predeterminada, cada versión tiene una etiqueta de imagen específica que corresponde a la versión de lanzamiento de SQL Server. Para actualizar a la versión más reciente, siga estos pasos:

1. Antes de eliminar el clúster anterior, realice una copia de seguridad de los datos en la instancia maestra de SQL Server y en HDFS. En la instancia maestra de SQL Server, puede usar [Copia de seguridad y restauración de SQL Server](data-ingestion-restore-database.md). En HDFS, se [pueden copiar los datos con `curl`](data-ingestion-curl.md).

1. Elimine el clúster anterior con el comando `azdata delete cluster`.

   ```bash
    azdata bdc delete --name <old-cluster-name>
   ```

   > [!Important]
   > Use la versión de `azdata` que coincida con el clúster. No elimine un clúster anterior con la versión más reciente de `azdata`.

   > [!Note]
   > La emisión de un comando de `azdata bdc delete` resultará en la eliminación de todos los objetos creados en el espacio de nombres identificado con el nombre del clúster de macrodatos, pero no del espacio de nombres en sí. El espacio de nombres se puede volver a utilizar para las implementaciones posteriores, siempre y cuando esté vacío y no se haya creado ninguna otra aplicación dentro del mismo.

1. Desinstale la versión anterior de `azdata`.

   ```powershell
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-rc1/requirements.txt
   ```

1. Instale la última versión de `azdata`. Los comandos siguientes instalan `azdata` desde la versión más reciente:

   **Windows:**

   ```powershell
   pip3 install -r https://aka.ms/azdata
   ```

   **Linux:**

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!IMPORTANT]
   > La ruta de acceso a la versión `n-1` de `azdata` cambia en cada versión. Aunque se haya instalado anteriormente `azdata`, se debe volver a instalar desde la ruta de acceso más reciente antes de crear el clúster nuevo.

## <a id="azdataversion"></a> Comprobar la versión de azdata

Antes de implementar un nuevo clúster de macrodatos, compruebe que se está usando la versión más reciente de `azdata` con el parámetro `--version`:

```bash
azdata --version
```

## <a name="install-the-new-release"></a>Instalar la nueva versión

Después de quitar el clúster de macrodatos anterior e instalar la versión de `azdata` más reciente, implemente el nuevo clúster de macrodatos con las instrucciones de implementación actuales. Para obtener más información, vea [Cómo implementar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] en Kubernetes](deployment-guidance.md). Luego, restaure las bases de datos o los archivos necesarios.

## <a name="next-steps"></a>Pasos siguientes

Vea [¿Qué son los [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]?](big-data-cluster-overview.md) para obtener más información sobre los clústeres de macrodatos.
