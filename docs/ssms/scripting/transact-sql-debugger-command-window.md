---
title: Comandos (ventana) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- VS.CommandWindow
helpviewer_keywords:
- Command Window [Transact-SQL]
ms.assetid: e567ebf9-0793-451b-92c7-26193a02d9da
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1ec8bc61454647bd553fa73513a1b06b71edc85b
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51701213"
---
# <a name="transact-sql-debugger---command-window"></a>Depurador de Transact-SQL: ventana Comandos
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Use la **ventana Comandos** para ejecutar comandos, como debug y edit, con el código de la ventana Editor de consultas de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que se está depurando. Debe estar en modo de depuración para utilizar el **Ventana de comandos**. El depurador de [!INCLUDE[tsql](../../includes/tsql-md.md)] admite muchos de los comandos que también se admiten en la [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] **ventana** . Para obtener más información, vea [Ventana de comandos de Visual Studio](https://go.microsoft.com/fwlink/?LinkId=112007).  
  
## <a name="task-list"></a>Lista de tareas  
 **Para tener acceso a la Ventana de comandos**  
  
-   En el menú **Depurar** , haga clic en **Iniciar depuración**.  
  
 **Para imprimir el valor de una variable**  
  
-   En la **ventana Comandos**, escriba **Debug.Print \<nombreDeVariable>** y pulse ENTRAR.  
  
 **Para mostrar información sobre el subproceso actual**  
  
-   En la **ventana Comandos**, escriba **Debug.ListThread**y pulse ENTRAR.  
  
 **Para agregar una variable a la ventana Inspección rápida**  
  
-   En la **ventana Comandos**, escriba **Debug.QuickWatch \<nombreDeVariable** y pulse ENTRAR.  
  
## <a name="see-also"></a>Ver también  
 [Depurador de Transact-SQL](../../relational-databases/scripting/transact-sql-debugger.md)  
  
  
