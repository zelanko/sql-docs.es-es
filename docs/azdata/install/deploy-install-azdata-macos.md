---
title: Instalación de azdata para macOS
titleSuffix: ''
description: Obtenga información sobre cómo instalar la herramienta azdata en macOS.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 01/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: c812600394546cba8adb0eacab59fa450b7c4bd2
ms.sourcegitcommit: d56f1eca807c55cf606a6316f3872585f014fec1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/22/2020
ms.locfileid: "90914912"
---
# <a name="install-azdata-on-macos"></a>Instalación de `azdata` en macOS

Para la plataforma macOS, puede instalar la `azdata-cli` mediante el administrador de paquetes de Homebrew. El paquete de la CLI se ha probado en distintas versiones de macOS: 
* 10.13 High Sierra
* 10.14 Mojave
* 10.15 Catalina

## <a name="install-with-homebrew"></a>Instalación con Homebrew

```bash
brew tap microsoft/azdata-cli-release
brew update
brew install azdata-cli
```

>[!IMPORTANT]
>La `azdata-cli` tiene una dependencia en los paquetes `python3`, `freetds`, `unixodbc`, `zeromq` de Homebrew y los instalará. Se garantiza que la `azdata-cli` será compatible con la versión más reciente de estas dependencias publicadas en Homebrew.

## <a name="verify-install"></a>Comprobación de la instalación

```bash
azdata
azdata --version
```

## <a name="update"></a>Actualizar

Debe actualizar la información del repositorio local y, a continuación, actualizar el paquete `azdata-cli`.

```bash
brew tap microsoft/azdata-cli-release
brew update
brew upgrade azdata-cli
```

## <a name="uninstall"></a>Desinstalación

Use Homebrew para desinstalar el paquete `azdata-cli`.

```bash
brew uninstall azdata-cli
```

## <a name="next-steps"></a>Pasos siguientes

Vea [¿Qué son los [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ver15.md)]?](../../big-data-cluster/big-data-cluster-overview.md) para obtener más información sobre los clústeres de macrodatos.

Use azdata con [Servicios de datos habilitados por Azure Arc](/azure/azure-arc/data/)
