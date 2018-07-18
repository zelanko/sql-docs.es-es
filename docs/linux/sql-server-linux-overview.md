---
title: Introducción a SQL Server en Linux | Microsoft Docs
description: En este artículo se describe cómo SQL Server se ejecuta en Linux y proporciona información sobre cómo obtener más información.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 06/20/2018
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 9dcc6a90-0add-42c2-815b-862e4e2a21ac
ms.openlocfilehash: 16ea8b69f1d55e5b338931f0531bdf8a2e037707
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38020143"
---
# <a name="sql-server-on-linux"></a>SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

SQL Server 2017 ahora se ejecuta en Linux. Es el mismo motor de base de datos de SQL Server, con muchas características y servicios, independientemente de su sistema operativo similar.

## <a name="install"></a>Install

Para empezar, instale a SQL Server en Linux mediante uno de los siguientes inicios rápidos:

- [Instalación en Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalación en SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar en Ubuntu](quickstart-install-connect-ubuntu.md)
- [Ejecutar en Docker](quickstart-install-connect-docker.md)
- [Aprovisionar una máquina virtual de SQL en Azure](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json)

> [!NOTE]
> Docker sí se ejecuta en varias plataformas, lo que significa que puede ejecutar la imagen de Docker en Linux, Mac y Windows.

## <a name="connect"></a>Conectar

Después de la instalación, conéctese a la instancia de SQL Server en su equipo Linux. Puede conectarse localmente o de forma remota y con una variedad de herramientas y los controladores. Los tutoriales muestran cómo usar el [sqlcmd](sql-server-linux-setup-tools.md) herramienta de línea de comandos. Otras herramientas incluyen lo siguiente:

| Herramienta | Tutorial |
|-----|-----|
| Visual Studio Code (VS Code) | [Uso de VS Code con SQL Server en Linux](sql-server-linux-develop-use-vscode.md) |
| SQL Server Management Studio (SSMS) | [Usar SSMS en Windows para conectarse a SQL Server en Linux](sql-server-linux-manage-ssms.md) |
| SQL Server Data Tools (SSDT) | [Usar SSDT con SQL Server en Linux](sql-server-linux-develop-use-ssdt.md) |

## <a name="explore"></a>Explorar

SQL Server 2017 tiene el mismo motor de base de datos subyacente en todas las plataformas compatibles, incluidos Linux. Muchas características y capacidades existentes funcionan igual en Linux. Esta área de la documentación expone algunas de estas características desde la perspectiva de Linux. También llama a las áreas que tienen requisitos únicos en Linux.

Si ya está familiarizado con SQL Server, revise la [notas de la versión](sql-server-linux-release-notes.md) de directrices generales y problemas conocidos de esta versión. A continuación, examine [Novedades de SQL Server en Linux](sql-server-linux-whats-new.md) como [cuáles son las novedades de SQL Server 2017 general](../sql-server/what-s-new-in-sql-server-2017.md). 

> [!TIP]
> Para obtener respuestas a las preguntas más frecuentes, consulte el [SQL Server en Linux preguntas más frecuentes sobre](sql-server-linux-faq.md).

[!INCLUDE[Get Help Options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]