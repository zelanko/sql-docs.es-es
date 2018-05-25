---
title: Administrar SQL Server en Linux | Documentos de Microsoft
description: Este artículo contiene vínculos a tareas comunes de administración y herramientas de SQL Server ejecutando en Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.technology: linux
ms.assetid: 6bd8eb0b-593d-467e-87ea-ab1c4dbcd1ea
ms.custom: sql-linux
ms.openlocfilehash: 89b670f6b4dd815744f505d1aa4f60a29d25bcaa
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2018
---
# <a name="choose-the-right-tool-to-manage-sql-server-on-linux"></a>Elija la herramienta adecuada para administrar SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Hay varias maneras para administrar SQL Server 2017 en Linux. La siguiente sección proporciona una introducción rápida de técnicas con punteros a más recursos y herramientas de administración diferente.

## <a name="mssql-conf"></a>MSSQL-conf 
El **mssql-conf** herramienta configura SQL Server en Linux. Para obtener más información, consulte [configurar SQL Server en Linux con mssql-conf](sql-server-linux-configure-mssql-conf.md).

## <a name="transact-sql"></a>Transact-SQL

Casi todo lo que puede hacer en una herramienta cliente también se puede lograr con las instrucciones de Transact-SQL. SQL Server proporciona [vistas de administración dinámica (DMV)](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) que consultar el estado y la configuración de SQL Server. También hay [comandos Transact-SQL](https://msdn.microsoft.com/library/bb510741.aspx) para tareas de administración de base de datos. Puede ejecutar estos comandos en cualquier herramienta de cliente que admite la conexión a SQL Server y ejecutar consultas de Transact-SQL, por ejemplo [sqlcmd](sql-server-linux-setup-tools.md) o [código de Visual Studio](sql-server-linux-develop-use-vscode.md).

## <a name="sql-server-operations-studio-preview"></a>SQL Server Operations Studio (versión preliminar)

La nueva Microsoft SQL Operations Studio (preview) es una herramienta multiplataforma para la administración de SQL Server. Para obtener más información, consulte [Microsoft SQL Operations Studio (preview)](../sql-operations-studio/what-is.md).

## <a name="sql-server-management-studio-on-windows"></a>SQL Server Management Studio en Windows

SQL Server Management Studio (SSMS) es una aplicación de Windows que proporciona una interfaz gráfica de usuario para la administración de SQL Server. Aunque actualmente se ejecuta sólo en Windows, puede usarlo para conectarse remotamente a las instancias de SQL Server de Linux. Para obtener más información sobre el uso de SSMS para administrar SQL Server, vea [utilice SSMS para administrar SQL Server en Linux](sql-server-linux-manage-ssms.md).

## <a name="mssql-cli-preview"></a>MSSQL-cli (versión preliminar)

Microsoft ha lanzado una nueva herramienta de scripting de multiplataforma para SQL Server, [mssql cli](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/). Esta herramienta está actualmente en vista previa.

## <a name="powershell"></a>PowerShell

PowerShell ofrece un entorno enriquecido de línea de comandos para administrar SQL Server en Linux. Para obtener más información, consulte [usar PowerShell para administrar SQL Server en Linux](sql-server-linux-manage-powershell.md).

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de SQL Server en Linux, consulte [SQL Server en Linux](sql-server-linux-overview.md).
