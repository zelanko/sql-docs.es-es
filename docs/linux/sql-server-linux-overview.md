---
title: "Información general de SQL Server en Linux | Documentos de Microsoft"
description: "Este artículo describe cómo SQL Server se ejecuta en Linux y proporciona información sobre cómo obtener más información."
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/22/2018
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: 9dcc6a90-0add-42c2-815b-862e4e2a21ac
ms.workload: Active
ms.openlocfilehash: faa2898017347f59d415f7f5bf5bd6795a3f9de6
ms.sourcegitcommit: f0c5e37c138be5fb2cbb93e9f2ded307665b54ea
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/24/2018
---
# <a name="sql-server-on-linux"></a>SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

2017 de SQL Server se ejecuta ahora en Linux. Es el mismo motor de base de datos de SQL Server, con muchas características y servicios, independientemente de su sistema operativo similar.

## <a name="install"></a>Install

Para comenzar, instale a SQL Server en Linux con uno de los siguientes tutoriales:

- [Instalar en Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalar en SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar en Ubuntu](quickstart-install-connect-ubuntu.md)
- [Ejecutar en Docker](quickstart-install-connect-docker.md)
- [Aprovisionar una máquina virtual de SQL en Azure](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json)

> [!NOTE]
> Docker sí se ejecuta en varias plataformas, lo que significa que puede ejecutar la imagen de Docker en Linux, Mac y Windows.

## <a name="connect"></a>Conectar

Después de la instalación, conéctese a la instancia de SQL Server en su equipo Linux. Puede conectarse localmente o y de forma remota con una variedad de herramientas y los controladores. Los tutoriales muestran cómo usar el [sqlcmd](sql-server-linux-setup-tools.md) herramienta de línea de comandos. Otras herramientas incluyen lo siguiente:

| Herramienta | Tutorial |
|-----|-----|
| Código de Visual Studio (frente a código) | [Usar código de VS con SQL Server en Linux](sql-server-linux-develop-use-vscode.md) |
| SQL Server Management Studio (SSMS) | [Usar SSMS en Windows para conectarse a SQL Server en Linux](sql-server-linux-develop-use-ssms.md) |
| SQL Server Data Tools (SSDT) | [Usar SSDT con SQL Server en Linux](sql-server-linux-develop-use-ssdt.md) |

## <a name="explore"></a>Explorar

SQL Server 2017 tiene el mismo motor de base de datos subyacente en todas las plataformas admitidas, incluidos Linux. Por lo que muchas características y capacidades existentes funcionan de la misma forma en Linux. Esta área de la documentación expone algunas de estas características desde la perspectiva de Linux. También resalta las áreas que tienen requisitos únicos en Linux.

Si ya está familiarizado con SQL Server, revise la [notas de la versión](sql-server-linux-release-notes.md) de directrices generales y problemas conocidos de esta versión. A continuación, examine [what's new for SQL Server en Linux](sql-server-linux-whats-new.md) como [Novedades de SQL Server 2017 general](../sql-server/what-s-new-in-sql-server-2017.md). 

> [!TIP]
> Para obtener respuestas a las preguntas más frecuentes, consulte el [SQL Server en Linux preguntas más frecuentes sobre](sql-server-linux-faq.md).

[!INCLUDE[Get Help Options](../includes/paragraph-content/get-help-options.md)]
