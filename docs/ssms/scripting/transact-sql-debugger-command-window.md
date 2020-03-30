---
title: Ventana de comandos
titleSuffix: T-SQL debugger
ms.prod: sql
ms.technology: scripting
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
ms.openlocfilehash: 226acc4696b5edacde3b6950c10c8b5370e29b42
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "75243432"
---
# <a name="transact-sql-debugger---command-window"></a>Depurador de Transact-SQL: ventana Comandos

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Use la **ventana Comandos** para ejecutar comandos, como debug y edit, con el código de la ventana Editor de consultas de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que se está depurando. Debe estar en modo de depuración para utilizar el **Ventana de comandos**. El depurador de [!INCLUDE[tsql](../../includes/tsql-md.md)] admite muchos de los comandos que también se admiten en la ventana [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] **Comando**. Para obtener más información, vea [Ventana de comandos de Visual Studio](https://go.microsoft.com/fwlink/?LinkId=112007).  

[!INCLUDE[ssms-old-versions](../../includes/ssms-old-versions.md)]

## <a name="task-list"></a>Lista de tareas

**Para tener acceso a la Ventana de comandos**

- En el menú **Depurar** , haga clic en **Iniciar depuración**.

**Para imprimir el valor de una variable**

- En la **ventana Comandos**, escriba **Debug.Print \<nombreDeVariable>** y pulse ENTRAR.

**Para mostrar información sobre el subproceso actual**

- En la **ventana Comandos**, escriba **Debug.ListThread**y pulse ENTRAR.

**Para agregar una variable a la ventana Inspección rápida**

- En la **ventana Comandos**, escriba **Debug.QuickWatch \<nombreDeVariable** y pulse ENTRAR.

## <a name="see-also"></a>Consulte también

[Depurador de Transact-SQL](../../relational-databases/scripting/transact-sql-debugger.md)
