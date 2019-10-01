---
title: Actualización a una nueva versión
titleSuffix: SQL Server big data clusters
description: Obtenga información acerca de cómo actualizar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] (versión preliminar) a una nueva versión.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: bb1bf33c9ccb342e6afc4d22d67463791c0d67b6
ms.sourcegitcommit: 36c3ead6f2a3628f58040acf47f049f0b0957b8a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/30/2019
ms.locfileid: "71688272"
---
# <a name="how-to-upgrade-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>Cómo actualizar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se proporcionan instrucciones para actualizar un clúster de macrodatos de SQL Server a una nueva versión. Los pasos de este artículo se aplican específicamente a la actualización entre versiones preliminares.

## <a name="backup-and-delete-the-old-cluster"></a>Copia de seguridad del clúster anterior y eliminación

Actualmente, la única manera de actualizar un clúster de macrodatos a una nueva versión es quitarlo manualmente y volver a crearlo. Cada versión tiene una versión única de `azdata` que no es compatible con la versión anterior. Además, si un clúster anterior tuviera que descargar una imagen en un nodo nuevo, es posible que la imagen más reciente no fuera compatible con las imágenes anteriores del clúster. Para actualizar a la versión más reciente, siga estos pasos:

1. Antes de eliminar el clúster anterior, realice una copia de seguridad de los datos en la instancia maestra de SQL Server y en HDFS. En la instancia maestra de SQL Server, puede usar [Copia de seguridad y restauración de SQL Server](data-ingestion-restore-database.md). Para HDFS, [puede copiar los datos con `curl`](data-ingestion-curl.md).

1. Elimine el clúster anterior con el comando `azdata delete cluster`.

   ```bash
    azdata bdc delete --name <old-cluster-name>
   ```

   > [!Important]
   > Use la versión de `azdata` que coincida con el clúster. No elimine un clúster anterior con la versión más reciente de `azdata`.

   > [!Note]
   > La emisión de un comando `azdata bdc delete` producirá la eliminación de todos los objetos creados en el espacio de nombres identificado con el nombre del clúster de Big Data, pero no el espacio de nombres en sí. El espacio de nombres se puede reutilizar para las implementaciones posteriores, siempre y cuando esté vacío y no se haya creado ninguna otra aplicación en.

1. Antes de la versión CTP 3,2, `azdata` se llamaba `mssqlctl`. Si tiene instaladas las versiones anteriores de `mssqlctl` o `azdata`, es importante desinstalar antes de instalar la versión más reciente de `azdata`.

   En CTP 2.3 o superior, ejecute el siguiente comando. Reemplace `ctp3.1` en el comando por la versión de `mssqlctl` que va a desinstalar. Si la versión es anterior a CTP 3.1, agregue un guión antes del número de versión (por ejemplo, `ctp-2.5`).

   ```powershell
   pip3 uninstall -r https://aka.ms/azdata
   ```

1. Instale la versión más reciente de `azdata`. Los siguientes comandos instalan `azdata` para el candidato de versión comercial:

   **Windows:**

   ```powershell
   pip3 install -r https://aka.ms/azdata
   ```

   **Linux:**

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!IMPORTANT]
   > En cada versión, la ruta de acceso a `azdata` cambia. Incluso si instaló anteriormente `azdata` o `mssqlctl`, debe volver a instalar desde la ruta de acceso más reciente antes de crear el nuevo clúster.

## <a id="azdataversion"></a> Comprobar la versión de azdata

Antes de implementar un nuevo clúster de Big Data, compruebe que está usando la versión más reciente de `azdata` con el parámetro `--version`:

```bash
azdata --version
```

## <a name="install-the-new-release"></a>Instalar la nueva versión

Después de quitar el clúster de Big Data anterior e instalar el `azdata` más reciente, implemente el nuevo clúster de Big Data con las instrucciones de implementación actuales. Para obtener más información, consulte [cómo implementar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] en Kubernetes](deployment-guidance.md). Luego, restaure las bases de datos o los archivos necesarios.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de los clústeres de Big Data, consulte [¿Qué son [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](big-data-cluster-overview.md).
