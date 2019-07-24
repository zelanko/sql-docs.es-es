---
title: Actualización a una nueva versión
titleSuffix: SQL Server big data clusters
description: Obtenga información acerca de cómo actualizar los clústeres de macrodatos SQL Server 2019 (versión preliminar) a una nueva versión.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7bdb1eb59fd36d065df9dba0f6d6879c1a294914
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419386"
---
# <a name="how-to-upgrade-sql-server-big-data-clusters"></a>Actualización de clústeres de macrodatos SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se proporcionan instrucciones sobre cómo actualizar un clúster de macrodatos de SQL Server a una nueva versión. Los pasos descritos en este artículo se aplican específicamente a la actualización entre versiones de vista previa.

## <a name="backup-and-delete-the-old-cluster"></a>Copia de seguridad y eliminación del clúster anterior

Actualmente, la única manera de actualizar un clúster de Big Data a una nueva versión es quitar manualmente y volver a crear el clúster. Cada versión tiene una versión única de **azdata** que no es compatible con la versión anterior. Además, si un clúster anterior tuviera que descargar una imagen en un nuevo nodo, es posible que la imagen más reciente no sea compatible con las imágenes anteriores del clúster. Para actualizar a la versión más reciente, siga estos pasos:

1. Antes de eliminar el clúster anterior, realice una copia de seguridad de los datos en el SQL Server instancia maestra y en HDFS. Para el SQL Server instancia maestra, puede usar [SQL Server copias de seguridad y restauración](data-ingestion-restore-database.md). Para HDFS, [puede copiar los datos con **rizo**](data-ingestion-curl.md).

1. Elimine el clúster anterior con `azdata delete cluster` el comando.

   ```bash
    azdata bdc delete --name <old-cluster-name>
   ```

   > [!Important]
   > Use la versión de **azdata** que coincida con el clúster. No elimine un clúster anterior con la versión más reciente de **azdata**.

1. Antes de la versión CTP 3,2, **azdata** se llamaba **mssqlctl**. Si tiene instaladas las versiones anteriores de **mssqlctl** o **azdata** , es importante desinstalar antes de instalar la versión más reciente de **azdata**.

   Para CTP 2,3 o posterior, ejecute el siguiente comando. Reemplace `ctp3.1` en el comando por la versión de **mssqlctl** que está desinstalando. Si la versión es anterior a CTP 3,1, agregue un guion antes del número de versión (por ejemplo `ctp-2.5`,).

   ```powershell
   pip3 uninstall -r https://mcr.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

1. Instale la versión más reciente de **azdata**. Los siguientes comandos instalan **azdata** para CTP 3,2:

   **Windows**

   ```powershell
   pip3 install -r https://aka.ms/azdata
   ```

   **Linuxun**

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!IMPORTANT]
   > En cada versión, la ruta de acceso a **azdata** cambia. Incluso si instaló anteriormente **azdata** o **mssqlctl**, debe volver a instalar desde la ruta de acceso más reciente antes de crear el nuevo clúster.

## <a id="azdataversion"></a>Comprobar la versión de azdata

Antes de implementar un nuevo clúster de Big Data, compruebe que está usando la versión más reciente de **azdata** con `--version` el parámetro:

```bash
azdata --version
```

## <a name="install-the-new-release"></a>Instalar la nueva versión

Después de quitar el clúster de Big Data anterior e instalar el **azdata**más reciente, implemente el nuevo clúster de Big Data con las instrucciones de implementación actuales. Para obtener más información, vea [cómo implementar clústeres de macrodatos SQL Server en Kubernetes](deployment-guidance.md). A continuación, restaure las bases de datos o los archivos necesarios.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre los clústeres de Big Data, consulte [¿Qué son](big-data-cluster-overview.md)los clústeres de macrodatos SQL Server.
