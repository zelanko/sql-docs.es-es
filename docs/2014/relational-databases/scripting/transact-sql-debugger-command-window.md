---
title: Comandos (ventana) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- VS.CommandWindow
helpviewer_keywords:
- Command Window [Transact-SQL]
ms.assetid: e567ebf9-0793-451b-92c7-26193a02d9da
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7b69735b5c2a2750ab34bc34d5a7f3c3e46bba16
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37253797"
---
# <a name="command-window"></a>Ventana de comandos
  Use la **ventana Comandos** para ejecutar comandos, como debug y edit, con el código de la ventana Editor de consultas de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que se está depurando. Debe estar en modo de depuración para utilizar el **Ventana de comandos**. El depurador de [!INCLUDE[tsql](../../includes/tsql-md.md)] admite muchos de los comandos que también se admiten en la [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] **ventana** . Para obtener más información, vea [Ventana de comandos de Visual Studio](http://go.microsoft.com/fwlink/?LinkId=112007).  
  
## <a name="task-list"></a>Lista de tareas  
 **Para tener acceso a la Ventana de comandos**  
  
-   En el menú **Depurar** , haga clic en **Iniciar depuración**.  
  
 **Para imprimir el valor de una variable**  
  
-   En la **ventana Comandos**, escriba **Debug.Print \<nombreDeVariable>** y pulse ENTRAR.  
  
 **Para mostrar información sobre el subproceso actual**  
  
-   En el **CommandWindow**, tipo `Debug.ListThread`, y, a continuación, presione ENTRAR.  
  
 **Para agregar una variable a la ventana Inspección rápida**  
  
-   En la **ventana Comandos**, escriba **Debug.QuickWatch \<nombreDeVariable** y pulse ENTRAR.  
  
## <a name="see-also"></a>Vea también  
 [Depurador de Transact-SQL](transact-sql-debugger.md)  
  
  
