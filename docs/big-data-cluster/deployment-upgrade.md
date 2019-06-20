---
title: Actualización a una nueva versión
titleSuffix: SQL Server big data clusters
description: Obtenga información sobre cómo actualizar clústeres de macrodatos de 2019 de SQL Server (versión preliminar) a una nueva versión.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 3af688d607e8ec2d9dad7efe0d2275840c48cba8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66782243"
---
# <a name="how-to-upgrade-sql-server-big-data-clusters"></a>Cómo actualizar clústeres de macrodatos de SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artículo proporcionan instrucciones sobre cómo actualizar un clúster de macrodatos de SQL Server a una nueva versión. Los pasos descritos en este artículo se aplican específicamente a cómo actualizar entre versiones preliminares.

## <a name="backup-and-delete-the-old-cluster"></a>Copia de seguridad y eliminar el clúster anterior

Actualmente, la única manera de actualizar un clúster de macrodatos a una nueva versión es quitar y volver a crear el clúster manualmente. Cada versión tiene una versión única de **mssqlctl** que no es compatible con la versión anterior. Además, si un clúster anterior había que descargar una imagen en un nodo nuevo, la imagen más reciente es posible que no sea compatible con las imágenes anteriores en el clúster. Para actualizar a la versión más reciente, siga estos pasos:

1. Antes de eliminar el clúster antiguo, realizar una copia de seguridad de los datos en la instancia principal de SQL Server y en HDFS. Para la instancia principal de SQL Server, puede usar [SQL Server backup y restore](data-ingestion-restore-database.md). HDFS, le [puede copiar los datos con **curl**](data-ingestion-curl.md).

1. Eliminar el clúster antiguo con el `mssqlctl delete cluster` comando.

   ```bash
    mssqlctl cluster delete --name <old-cluster-name>
   ```

   > [!Important]
   > Use la versión de **mssqlctl** que coincide con el clúster. No elimine un clúster anterior con la versión más reciente de **mssqlctl**.

1. Si tiene cualquier versión anterior de **mssqlctl** instalado, es importante que desinstale **mssqlctl** primero antes de instalar la versión más reciente.

   Si está desinstalando **mssqlctl** correspondiente a CTP 2.2 o ejecución inferior:

   ```powershell
   pip3 uninstall mssqlctl
   ```

   Para CTP 2.3 o posterior, ejecute el siguiente comando. Reemplace `ctp-2.5` en el comando con la versión de **mssqlctl** que va a desinstalar:

   ```powershell
   pip3 uninstall -r  https://private-repo.microsoft.com/python/ctp-2.5/mssqlctl/requirements.txt
   ```

1. Instale la versión más reciente de **mssqlctl**. El siguiente comando instala **mssqlctl** para CTP 3.0:

   **Windows:**

   ```powershell
   pip3 install -r  https://private-repo.microsoft.com/python/ctp3.0/mssqlctl/requirements.txt
   ```

   **Linux:**

   ```bash
   pip3 install -r  https://private-repo.microsoft.com/python/ctp3.0/mssqlctl/requirements.txt --user
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
