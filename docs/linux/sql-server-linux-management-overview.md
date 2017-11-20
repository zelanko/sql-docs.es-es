---
title: Administrar SQL Server en Linux | Documentos de Microsoft
description: "Este tema proporciona vínculos a tareas comunes de administración y herramientas de SQL Server ejecutando en Linux."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: linux
ms.suite: sql
ms.technology: database-engine
ms.assetid: 6bd8eb0b-593d-467e-87ea-ab1c4dbcd1ea
ms.custom: 
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: 4639379a65fc28c363f6510c1a393df8840dc7f8
ms.contentlocale: es-es
ms.lasthandoff: 10/02/2017

---
# <a name="choose-the-right-tool-to-manage-sql-server-on-linux"></a>Elija la herramienta adecuada para administrar SQL Server en Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Hay varias maneras para administrar SQL Server 2017 en Linux. En la siguiente sección proporciona una introducción rápida de técnicas con punteros a más recursos y herramientas de administración diferente.

## <a name="mssql-conf"></a>MSSQL-conf 
El **mssql-conf** herramienta configura SQL Server en Linux. Para obtener más información, consulte [configurar SQL Server en Linux con mssql-conf](sql-server-linux-configure-mssql-conf.md).

## <a name="transact-sql"></a>Transact-SQL

Casi todo lo que puede hacer en una herramienta cliente también se puede lograr con las instrucciones de Transact-SQL. SQL Server proporciona [vistas de administración dinámica (DMV)](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) que consultar el estado y la configuración de SQL Server. También hay [comandos Transact-SQL](https://msdn.microsoft.com/library/bb510741.aspx) para tareas de administración de base de datos. Puede ejecutar estos comandos en cualquier herramienta de cliente que admite la conexión a SQL Server y ejecutar consultas Transact-SQL. Algunos ejemplos son [sqlcmd](sql-server-linux-setup-tools.md), [código de Visual Studio](sql-server-linux-develop-use-vscode.md), y [SQL Server Management Studio](sql-server-linux-manage-ssms.md).

## <a name="sql-server-management-studio-on-windows"></a>SQL Server Management Studio en Windows

SQL Server Management Studio (SSMS) es una aplicación de Windows que proporciona una interfaz gráfica de usuario para la administración de SQL Server. Aunque actualmente se ejecuta sólo en Windows, puede usarlo para conectarse remotamente a las instancias de SQL Server de Linux. Para obtener más información sobre el uso de SSMS para administrar SQL Server, vea [utilice SSMS para administrar SQL Server en Linux](sql-server-linux-manage-ssms.md).

## <a name="powershell"></a>PowerShell

PowerShell ofrece un entorno enriquecido de línea de comandos para administrar SQL Server en Linux. Para obtener más información, consulte [usar PowerShell para administrar SQL Server en Linux](sql-server-linux-manage-powershell.md).

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de SQL Server en Linux, consulte [SQL Server en Linux](sql-server-linux-overview.md).

