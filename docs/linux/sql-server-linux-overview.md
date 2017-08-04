---
title: "Información general de SQL Server en Linux | Documentos de Microsoft"
description: "Este tema describe cómo SQL Server se ejecuta en Linux y proporciona información sobre cómo obtener más información."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 08/02/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 9dcc6a90-0add-42c2-815b-862e4e2a21ac
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: 1192afb7032f34f0af98c3c1051808e89dc22b63
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="sql-server-on-linux"></a>SQL Server en Linux

Ahora que se ejecuta SQL Server en Linux. Esta versión más reciente, SQL Server de 2017 RC2, se ejecuta en Linux y es en muchos sentidos basta con SQL Server. Es el mismo motor de base de datos de SQL Server, con muchas características y servicios, independientemente de su sistema operativo similar.

## <a name="install"></a>Install

Para comenzar, instale a SQL Server en Linux con uno de los siguientes tutoriales de inicio rápido:

- [Instalar en Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalar en SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar en Ubuntu](quickstart-install-connect-ubuntu.md)
- [Ejecutar en Docker](quickstart-install-connect-docker.md)

> [!NOTE]
> Docker sí se ejecuta en varias plataformas, lo que significa que puede ejecutar la imagen de Docker en Linux, Mac y Windows.

## <a name="connect"></a>Connect

Después de la instalación, conéctese a la instancia de SQL Server en su equipo Linux. Puede conectarse localmente o y de forma remota con una variedad de herramientas y los controladores. Los tutoriales de inicio rápido muestran cómo utilizar el [sqlcmd](sql-server-linux-setup-tools.md) herramienta de línea de comandos. Otras herramientas incluyen lo siguiente:

| Herramienta | Tutorial |
|-----|-----|
| Código de Visual Studio (frente a código) | [Usar código de VS con SQL Server en Linux](sql-server-linux-develop-use-vscode.md) |
| SQL Server Management Studio (SSMS) | [Usar SSMS en Windows para conectarse a SQL Server en Linux](sql-server-linux-develop-use-ssms.md) |
| SQL Server Data Tools (SSDT) | [Usar SSDT con SQL Server en Linux](sql-server-linux-develop-use-ssdt.md) |

## <a name="explore"></a>Explorar

SQL Server 2017 tiene el mismo motor de base de datos subyacente en todas las plataformas admitidas, incluidos Linux. Por lo que muchas características y capacidades existentes funcionan de la misma forma en Linux. Esta área de la documentación expone algunas de estas características desde la perspectiva de Linux. También resalta las áreas que tienen requisitos únicos en Linux.

Si ya está familiarizado con SQL Server, revise la [notas de la versión](sql-server-linux-release-notes.md) de directrices generales y problemas conocidos de esta versión. A continuación, examine [what's new for SQL Server en Linux](sql-server-linux-whats-new.md) como [Novedades de SQL Server 2017 general](../sql-server/what-s-new-in-sql-server-2017.md).

##  <a name="infotipmediageneralinfotippng-engage-with-the-sql-server-engineering-team"></a>![info_tip](./media/general/info_tip.png) Comunicación con el equipo de ingeniería de SQL Server

- [Cambio de la pila de DBA](https://dba.stackexchange.com/questions/tagged/sql-server): formular preguntas de administración de base de datos
- [Desbordamiento de pila](http://stackoverflow.com/questions/tagged/sql-server): formular preguntas de desarrollo
- [Foros de MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver): hacer preguntas técnicas
- [Microsoft Connect](https://connect.microsoft.com/SQLServer/Feedback): informe de errores y la característica de solicitud
- [Reddit](https://www.reddit.com/r/SQLServer/): analizar SQL Server

