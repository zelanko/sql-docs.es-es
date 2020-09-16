---
title: Ventana de comandos
description: Obtenga información sobre cómo usar la ventana Comandos del depurador de Transact-SQL para ejecutar comandos de depuración y editar comandos en el código que depura.
titleSuffix: T-SQL debugger
ms.prod: sql
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Command Window [Transact-SQL]
ms.assetid: e567ebf9-0793-451b-92c7-26193a02d9da
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 12/04/2019
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3465a430f9b9103088e08db045d1c42338c0224f
ms.sourcegitcommit: 6d53ecfdc463914f045c20eda96da39dec22acca
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/26/2020
ms.locfileid: "88901432"
---
# <a name="transact-sql-debugger---command-window"></a>Depurador de Transact-SQL: ventana Comandos

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Use la **ventana Comandos** para ejecutar comandos, como debug y edit, en el código de la ventana Editor de consultas de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que se depura actualmente. Debe estar en modo de depuración para utilizar el **Ventana de comandos**. El depurador de [!INCLUDE[tsql](../../includes/tsql-md.md)] admite muchos de los comandos que también se admiten en la ventana [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] **Comando**. Para obtener más información, vea [Ventana de comandos de Visual Studio](https://go.microsoft.com/fwlink/?LinkId=112007).  

[!INCLUDE[ssms-old-versions](../../includes/ssms-old-versions.md)]

## <a name="task-list"></a>Lista de tareas

**Para tener acceso a la Ventana de comandos**

- En el menú **Depurar** , haga clic en **Iniciar depuración**.

**Para imprimir el valor de una variable**

- En la **ventana Comandos**, escriba **Debug.Print \<VariableName>** y presione ENTRAR.

**Para mostrar información sobre el subproceso actual**

- En la **ventana Comandos**, escriba **Debug.ListThread**y pulse ENTRAR.

**Para agregar una variable a la ventana Inspección rápida**

- En la **ventana Comandos**, escriba **Debug.QuickWatch \<VariableName>** y presione ENTRAR.

## <a name="see-also"></a>Consulte también

[Depurador de Transact-SQL](../../relational-databases/scripting/transact-sql-debugger.md)
