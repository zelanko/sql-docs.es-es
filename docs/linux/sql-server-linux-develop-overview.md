---
title: Desarrollar aplicaciones para SQL Server en Linux
description: ''
author: VanMSFT
ms.author: vanto
manager: jroth
ms.date: 11/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 758cb738-b018-465b-9ab0-59a24b892e66
ms.openlocfilehash: 737fd2776c3320e9f71b9dfa372aa6de646516e6
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2019
ms.locfileid: "67833824"
---
# <a name="how-to-get-started-developing-applications-for-sql-server-on-linux"></a>Cómo empezar a desarrollar aplicaciones para SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Puede crear aplicaciones que se conectan a y usar SQL Server en Linux desde una variedad de lenguajes de programación como C#, Java, Node.js, PHP, Python, Ruby y C++. También puede usar marcos web más populares y marcos de trabajo de asignación relacional de objetos (ORM).

> [!VIDEO https://channel9.msdn.com/events/Connect/2017/T153/player]

> [!TIP]
> Estas mismas opciones de desarrollo también permiten a SQL Server en otras plataformas de destino. Las aplicaciones pueden tener como destino SQL Server en ejecución en el entorno local o en la nube, en Linux, Windows o Docker en macOS. O bien, puede tener como destino Azure SQL Database y Azure SQL Data Warehouse.

## <a name="try-the-tutorials"></a>Pruebe los tutoriales

Es la mejor manera de empezar a usar y crear aplicaciones con SQL Server probarlo usted mismo.

- Vaya a [tutoriales de introducción](https://aka.ms/sqldev).
- Seleccionar la plataforma de desarrollo y lenguaje.
- Pruebe los ejemplos de código.

> [!TIP]
> Si desea desarrollar para SQL Server en Docker, eche un vistazo a la **macOS** tutoriales.

## <a name="create-new-applications"></a>Crear nuevas aplicaciones

Si va a crear una nueva aplicación, eche un vistazo a una lista de los [las bibliotecas de conectividad](sql-server-linux-develop-connectivity-libraries.md) para obtener un resumen de los conectores y marcos populares disponibles para varios lenguajes de programación.

## <a name="use-existing-applications"></a>Usar las aplicaciones existentes

Si tiene una aplicación de base de datos existente, simplemente puede cambiar su cadena de conexión a SQL Server en Linux de destino. Asegúrese de que conozca el [problemas conocidos](sql-server-linux-release-notes.md) en SQL Server en Linux.

## <a name="use-existing-sql-tools-on-windows-with-sql-server-on-linux"></a>Usar las herramientas existentes de SQL en Windows con SQL Server en Linux

Las herramientas que se ejecutan actualmente en Windows, como SSMS, SSDT y PowerShell, también funcionan con SQL Server en Linux. Aunque ejecuta de forma nativa en Linux, todavía puede administrar las instancias remotas de SQL Server en Linux. 

Vea los temas siguientes para obtener más información:

- [SQL Server Management Studio (SSMS)](sql-server-linux-manage-ssms.md)
- [SQL Server Data Tools (SSDT)](sql-server-linux-develop-use-ssdt.md)
- [SQL PowerShell](sql-server-linux-manage-powershell.md)

> [!Note]
> Asegúrese de que está utilizando las versiones más recientes de estas herramientas para mejorar la experiencia.

## <a name="use-new-sql-tools-for-linux"></a>Usar nuevas herramientas SQL para Linux

Puede usar el nuevo [extensión mssql](https://aka.ms/mssql-marketplace) para [Visual Studio Code](https://code.visualstudio.com) en Linux, macOS y Windows. Para ver un tutorial paso a paso, consulte el tutorial siguiente:

- [Usar Visual Studio Code](sql-server-linux-develop-use-vscode.md)

También puede usar nuevas herramientas de línea de comandos que son nativas para Linux. Estas herramientas incluyen lo siguiente:

- [sqlcmd](../tools/sqlcmd-utility.md)
- [bcp](sql-server-linux-migrate-bcp.md)
- [mssql-conf](sql-server-linux-configure-mssql-conf.md)

## <a name="next-steps"></a>Pasos siguientes

Para empezar, instale a SQL Server en Linux mediante uno de los siguientes inicios rápidos:

- [Instalación en Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalación en SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalación en Ubuntu](quickstart-install-connect-ubuntu.md)
- [Ejecutar en Docker](quickstart-install-connect-ubuntu.md)
