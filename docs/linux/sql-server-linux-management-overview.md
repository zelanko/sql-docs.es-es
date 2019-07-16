---
title: Administrar SQL Server en Linux
description: Este artículo contiene vínculos a tareas comunes de administración y herramientas para SQL Server que se ejecutan en Linux.
author: VanMSFT
ms.author: vanto
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 6bd8eb0b-593d-467e-87ea-ab1c4dbcd1ea
ms.openlocfilehash: e38e51eb1db6c335175b2fc55636532df88ac27d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68000058"
---
# <a name="choose-the-right-tool-to-manage-sql-server-on-linux"></a>Elija la herramienta adecuada para administrar SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Hay varias maneras para administrar SQL Server en Linux. La siguiente sección proporciona una introducción rápida de las técnicas de punteros a más recursos y herramientas de administración diferentes.

## <a name="mssql-conf"></a>mssql-conf 

El **mssql-conf** herramienta configura SQL Server en Linux. Para obtener más información, consulte [configurar SQL Server en Linux con mssql-conf](sql-server-linux-configure-mssql-conf.md).

## <a name="transact-sql"></a>Transact-SQL

Casi todo lo que puede hacer en una herramienta de cliente también se puede lograr con las instrucciones Transact-SQL. SQL Server proporciona [vistas de administración dinámica (DMV)](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) que consultan el estado y la configuración de SQL Server. También hay [comandos Transact-SQL](../t-sql/language-reference.md) para tareas de administración de base de datos. Puede ejecutar estos comandos en cualquier herramienta de cliente que admite la conexión a SQL Server y ejecutar consultas de Transact-SQL, por ejemplo [sqlcmd](sql-server-linux-setup-tools.md) o [Visual Studio Code](sql-server-linux-develop-use-vscode.md).

## <a name="azure-data-studio"></a>Azure Data Studio

El nuevo Azure Data Studio es una herramienta multiplataforma para administrar SQL Server. Para obtener más información, consulte [Azure Data Studio](../azure-data-studio/what-is.md).

## <a name="sql-server-management-studio-on-windows"></a>SQL Server Management Studio en Windows

SQL Server Management Studio (SSMS) es una aplicación de Windows que proporciona una interfaz gráfica de usuario para la administración de SQL Server. Aunque actualmente sólo se ejecuta en Windows, puede usarlo para conectarse remotamente a las instancias de Linux con SQL Server. Para obtener más información sobre el uso de SSMS para administrar SQL Server, vea [Use SSMS para administrar SQL Server en Linux](sql-server-linux-manage-ssms.md).

## <a name="mssql-cli-preview"></a>MSSQL-cli (versión preliminar)

Microsoft ha lanzado una nueva herramienta de secuencias de comandos multiplataforma para SQL Server, [mssql-cli](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/). Esta herramienta está actualmente en versión preliminar.

## <a name="powershell"></a>PowerShell

PowerShell proporciona un entorno enriquecido de línea de comandos para administrar SQL Server en Linux. Para obtener más información, consulte [usar PowerShell para administrar SQL Server en Linux](sql-server-linux-manage-powershell.md).

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de SQL Server en Linux, consulte [SQL Server en Linux](sql-server-linux-overview.md).
