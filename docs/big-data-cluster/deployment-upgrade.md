---
title: Actualización a una nueva versión
titleSuffix: SQL Server big data clusters
description: Obtenga información sobre cómo actualizar clústeres de macrodatos de 2019 de SQL Server (versión preliminar) a una nueva versión.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
manager: jroth
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 8c8b8df4dc5643febdf3ddc808f215a9c34d24fe
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67728769"
---
# <a name="how-to-upgrade-sql-server-big-data-clusters"></a>Cómo actualizar clústeres de macrodatos de SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artículo proporcionan instrucciones sobre cómo actualizar un clúster de macrodatos de SQL Server a una nueva versión. Los pasos descritos en este artículo se aplican específicamente a cómo actualizar entre versiones preliminares.

## <a name="backup-and-delete-the-old-cluster"></a>Copia de seguridad y eliminar el clúster anterior

Actualmente, la única manera de actualizar un clúster de macrodatos a una nueva versión es quitar y volver a crear el clúster manualmente. Cada versión tiene una versión única de **mssqlctl** que no es compatible con la versión anterior. Además, si un clúster anterior había que descargar una imagen en un nodo nuevo, la imagen más reciente es posible que no sea compatible con las imágenes anteriores en el clúster. Para actualizar a la versión más reciente, siga estos pasos:

1. Antes de eliminar el clúster antiguo, realizar una copia de seguridad de los datos en la instancia principal de SQL Server y en HDFS. Para la instancia principal de SQL Server, puede usar [SQL Server backup y restore](data-ingestion-restore-database.md). HDFS, le [puede copiar los datos con **curl**](data-ingestion-curl.md).

1. Eliminar el clúster antiguo con el `mssqlctl delete cluster` comando.

   ```bash
    mssqlctl bdc delete --name <old-cluster-name>
   ```

   > [!Important]
   > Use la versión de **mssqlctl** que coincide con el clúster. No elimine un clúster anterior con la versión más reciente de **mssqlctl**.

1. Si tiene cualquier versión anterior de **mssqlctl** instalado, es importante que desinstale **mssqlctl** primero antes de instalar la versión más reciente.

   Para CTP 2.3 o posterior, ejecute el siguiente comando. Reemplace `ctp3.0` en el comando con la versión de **mssqlctl** que va a desinstalar. Si la versión es anterior a la 3.0, agregue un guión antes del número de versión (por ejemplo, `ctp-2.5`).

   ```powershell
   pip3 uninstall -r  https://private-repo.microsoft.com/python/ctp3.0/mssqlctl/requirements.txt
   ```

1. Instale la versión más reciente de **mssqlctl**. El siguiente comando instala **mssqlctl** para CTP 3.1:

   **Windows:**

   ```powershell
   pip3 install -r  https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

   **Linux:**

   ```bash
   pip3 install -r  https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt --user
   ```

   > [!IMPORTANT]
   > Para cada versión, la ruta de acceso **mssqlctl** cambios. Incluso si anteriormente instaló **mssqlctl**, debe volver a instalar desde la ruta de acceso más reciente antes de crear el nuevo clúster.

## <a id="mssqlctlversion"></a> Comprobar la versión mssqlctl

Antes de implementar un nuevo clúster de macrodatos, compruebe que está usando la versión más reciente de **mssqlctl** con el `--version` parámetro:

```bash
mssqlctl --version
```

## <a name="install-the-new-release"></a>Instalar la nueva versión

Después de quitar el clúster de macrodatos anterior e instalar la versión más reciente **mssqlctl**, implementar el nuevo clúster de macrodatos mediante las instrucciones de implementación actual. Para obtener más información, consulte [de clústeres de cómo implementar grandes de datos de SQL Server en Kubernetes](deployment-guidance.md). A continuación, restaure los archivos y bases de datos necesarias.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de los clústeres de datos de gran tamaño, vea [¿cuáles son los clústeres de SQL Server macrodatos](big-data-cluster-overview.md).
