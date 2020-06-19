---
title: Ventana de comandos
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Command Window [Transact-SQL]
ms.assetid: e567ebf9-0793-451b-92c7-26193a02d9da
author: rothja
ms.author: jroth
ms.openlocfilehash: 1313ff25791c285e1bd1f8ccb69a75700ae62be1
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85063371"
---
# <a name="command-window"></a>Ventana de comandos
  Use la **ventana Comandos** para ejecutar comandos, como debug y edit, con el código de la ventana Editor de consultas de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que se está depurando. Debe estar en modo de depuración para utilizar el **Ventana de comandos**. El depurador de [!INCLUDE[tsql](../../includes/tsql-md.md)] admite muchos de los comandos que también se admiten en la ventana [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] **Comando**. Para obtener más información, vea [Ventana de comandos de Visual Studio](https://go.microsoft.com/fwlink/?LinkId=112007).  
  
## <a name="task-list"></a>Lista de tareas  
 **Para tener acceso a la Ventana de comandos**  
  
-   En el menú **Depurar** , haga clic en **Iniciar depuración**.  
  
 **Para imprimir el valor de una variable**  
  
-   En el tipo de **CommandWindow**, escriba **Debug \<VariableName> . Print **y presione Entrar.  
  
 **Para mostrar información sobre el subproceso actual**  
  
-   En el tipo **CommandWindow**, escriba `Debug.ListThread` y, a continuación, presione Entrar.  
  
 **Para agregar una variable a la ventana Inspección rápida**  
  
-   En el tipo de **CommandWindow**, escriba **Debug \<VariableName> . Inspección rápida **y, a continuación, presione Entrar.  
  
## <a name="see-also"></a>Consulte también  
 [Depurador de Transact-SQL](transact-sql-debugger.md)  
