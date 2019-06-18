---
title: Depurar un controlador de lógica de negocios | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- merge replication business logic handlers [SQL Server replication]
- business logic handlers [SQL Server replication]
- BusinessLogicModule class
ms.assetid: edd0d17a-0e9c-4c28-8395-a7d47e8ce3d6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 90d1fc5d6dd4eb972e15ae942822418aba30573e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62721505"
---
# <a name="debug-a-business-logic-handler-replication-programming"></a>Depurar un controlador de lógica de negocios (programación de la replicación)
  Use un controlador de lógica de negocios para invocar la lógica de negocios personalizada cuando se sincroniza una suscripción de mezcla. Para obtener más información, vea [Execute Business Logic During Merge Synchronization](merge/execute-business-logic-during-merge-synchronization.md) (Ejecutar lógica de negocios durante la sincronización de mezcla).  
  
 El Reconciliador de replicación de mezcla (replrec.dll) llama al ensamblado de código administrado que contiene la lógica de negocios. En la mayoría de los casos, replrec.dll y la lógica de negocios personalizada se ejecuta en el equipo donde el Agente de mezcla se ejecuta (en el suscriptor para una suscripción de extracción o en el distribuidor para una suscripción de inserción). En el caso de la sincronización web o en el caso de un suscriptor de [!INCLUDE[ssEW](../../includes/ssew-md.md)] , el reconciliador y la lógica de negocios personalizada se ejecuta en el servidor web.  
  
### <a name="to-debug-a-business-logic-handler-on-a-local-computer"></a>Para depurar un controlador de lógica de negocios en un equipo local  
  
1.  Configure la publicación y la distribución, cree una publicación y cree una suscripción a la publicación. Para más información, vea [Configuración de la publicación y la distribución](configure-publishing-and-distribution.md) y [Creación de una publicación](publish/create-a-publication.md).  
  
2.  Cree y registre un controlador de lógica de negocios Para más información, consulte [Implementar un controlador de lógica de negocios para un artículo de mezcla](implement-a-business-logic-handler-for-a-merge-article.md).  
  
3.  Cree un proyecto de Replication Management Objects (RMO) en [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio que mediante programación inicie sincrónicamente el Agente de mezcla. Para obtener más información, consulte [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md).  
  
4.  Establezca un punto de interrupción en el código del controlador de lógica de negocios, ya sea en el método que se depura o en el constructor de clase. Para obtener más información acerca de los métodos que se pueden implementar en un controlador de lógica de negocios, vea el tema de métodos <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> .  
  
5.  Genere el controlador de lógica de negocios en modo de depuración e implemente el archivo de símbolos de ensamblado y depuración (.pdb) en la ubicación registrada en el paso 1.  
  
    > [!NOTE]  
    >  Para simplificar la depuración, cree una solución de Visual Studio .NET que contenga el proyecto del controlador de lógica de negocios y el proyecto que sincronice la suscripción. En este caso, establezca el proyecto de sincronización como el proyecto de inicio y configure el entorno de la compilación para implementar el ensamblado de lógica de negocios en la ubicación registrada en el paso 1 durante la depuración.  
  
6.  Ejecute los comandos de inserción, actualización o eliminación en la base de datos de suscripciones o de publicación. La ubicación del comando y de la ejecución depende del método que se depura.  
  
7.  Inicie el proyecto del paso 3 en modo de depuración para sincronizar la suscripción.  
  
8.  Suponiendo que no se establezcan otros puntos de interrupción y que se repliquen los comandos adecuados, la ejecución se detiene cuando llega al punto de interrupción en el controlador de lógica de negocios.  
  
### <a name="to-debug-a-business-logic-handler-on-a-web-server-using-web-synchronization-or-for-a-sql-server-compact-subscriber"></a>Para depurar un controlador de lógica de negocios en un servidor web con la sincronización web, o para un suscriptor de SQL Server Compact  
  
1.  Configure la publicación y la distribución, cree una publicación y cree una suscripción de extracción a la publicación. La publicación debe admitir la sincronización web o los suscriptores de [!INCLUDE[ssEW](../../includes/ssew-md.md)] .  
  
2.  Cree y registre un controlador de lógica de negocios Para más información, consulte [Implementar un controlador de lógica de negocios para un artículo de mezcla](implement-a-business-logic-handler-for-a-merge-article.md).  
  
3.  Establezca un punto de interrupción en el código del controlador de lógica de negocios, ya sea en el método que se depura o en el constructor de clase. Para obtener más información acerca de los métodos que se pueden implementar en un controlador de lógica de negocios, vea el tema de métodos <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> .  
  
4.  Genere el controlador de lógica de negocios en modo de depuración e implemente el archivo de símbolos de ensamblado y depuración (.pdb) en el servidor web, en la ubicación registrada en el paso 1.  
  
    > [!NOTE]  
    >  Si el controlador de lógica de negocios no se genera porque se está usando el ensamblado, escriba el comando `iisreset` en el símbolo del sistema del servidor web para restablecer dicho servidor.  
  
5.  Sincronice la suscripción con la sincronización web habilitada. Durante la sincronización, el servidor web carga el ensamblado registrado.  
  
6.  Con el depurador de Visual Studio .NET, adjúntese a uno de los procesos siguientes del servidor web:  
  
    -   w3wp.exe - Windows Server 2003.  
  
    -   inetinfo.exe - Windows 2000 y Windows XP.  
  
7.  En la ventana **Salida** , compruebe la depuración generada para comprobar que los símbolos del ensamblado registrado se cargaron correctamente. Si no se cargaron los símbolos, asegúrese de que el archivo .pdb correcto se copió en el paso 4, y repita el paso 5.  
  
8.  Ejecute los comandos de inserción, actualización o eliminación en la base de datos de suscripciones o de publicación. La ubicación del comando y de la ejecución depende del método que se depura.  
  
9. Con el depurador de Visual Studio, adjúntese al proceso w3wp.exe.  
  
10. Vuelva a sincronizar la suscripción con la sincronización web.  
  
11. Suponiendo que no se establezcan otros puntos de interrupción y que se repliquen los comandos adecuados, la ejecución se detiene cuando llega al punto de interrupción en el controlador de lógica de negocios.  
  
## <a name="see-also"></a>Vea también  
 [Implementar un controlador de lógica de negocios para un artículo de mezcla](implement-a-business-logic-handler-for-a-merge-article.md)  
  
  
