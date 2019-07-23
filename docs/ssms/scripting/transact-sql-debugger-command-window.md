---
title: Comandos (ventana) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Command Window [Transact-SQL]
ms.assetid: e567ebf9-0793-451b-92c7-26193a02d9da
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 25b83d46a1223f9af01233a60527bd492638399d
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68253874"
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
  
## <a name="see-also"></a>Consulte también  
 [Depurador de Transact-SQL](../../relational-databases/scripting/transact-sql-debugger.md)  
