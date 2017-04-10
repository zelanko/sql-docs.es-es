---
title: "Depurar un controlador de l&#243;gica de negocios (programaci&#243;n de la replicaci&#243;n) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
helpviewer_keywords: 
  - "controladores de lógica de negocios de replicación de mezcla [replicación de SQL Server]"
  - "controladores de lógica de negocios [replicación de SQL Server]"
  - "BusinessLogicModule, clase"
ms.assetid: edd0d17a-0e9c-4c28-8395-a7d47e8ce3d6
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 34
---
# Depurar un controlador de l&#243;gica de negocios (programaci&#243;n de la replicaci&#243;n)
  Use un controlador de lógica de negocios para invocar la lógica de negocios personalizada cuando se sincroniza una suscripción de mezcla. Para obtener más información, consulte [ejecutar lógica de negocios durante la sincronización mezcla](../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md).  
  
 El Reconciliador de replicación de mezcla (replrec.dll) llama al ensamblado de código administrado que contiene la lógica de negocios. En la mayoría de los casos, replrec.dll y la lógica de negocios personalizada se ejecuta en el equipo donde el Agente de mezcla se ejecuta (en el suscriptor para una suscripción de extracción o en el distribuidor para una suscripción de inserción). En el caso de la sincronización web o en el caso de un suscriptor de [!INCLUDE[ssEW](../../includes/ssew-md.md)] , el reconciliador y la lógica de negocios personalizada se ejecuta en el servidor web.  
  
### Para depurar un controlador de lógica de negocios en un equipo local  
  
1.  Configure la publicación y la distribución, cree una publicación y cree una suscripción a la publicación. Para obtener más información, consulte [Configurar publicación y distribución](../../relational-databases/replication/configure-publishing-and-distribution.md) y [crear, modificar y eliminar publicaciones y artículos y Nº 40; Replicación y nº 41;](../../relational-databases/replication/publish/create-modify-and-delete-publications-and-articles-replication.md).  
  
2.  Cree y registre un controlador de lógica de negocios Para más información, consulte [Implement a Business Logic Handler for a Merge Article](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md).  
  
3.  Cree un proyecto de Replication Management Objects (RMO) en [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio que mediante programación inicie sincrónicamente el Agente de mezcla. Para más información, consulte [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md).  
  
4.  Establezca un punto de interrupción en el código del controlador de lógica de negocios, ya sea en el método que se depura o en el constructor de clase. Para obtener más información acerca de los métodos que se pueden implementar en un controlador de lógica de negocios, consulte el <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> tema de métodos.  
  
5.  Genere el controlador de lógica de negocios en modo de depuración e implemente el archivo de símbolos de ensamblado y depuración (.pdb) en la ubicación registrada en el paso 1.  
  
    > [!NOTE]  
    >  Para simplificar la depuración, cree una solución de Visual Studio .NET que contenga el proyecto del controlador de lógica de negocios y el proyecto que sincronice la suscripción. En este caso, establezca el proyecto de sincronización como el proyecto de inicio y configure el entorno de la compilación para implementar el ensamblado de lógica de negocios en la ubicación registrada en el paso 1 durante la depuración.  
  
6.  Ejecute los comandos de inserción, actualización o eliminación en la base de datos de suscripciones o de publicación. La ubicación del comando y de la ejecución depende del método que se depura.  
  
7.  Inicie el proyecto del paso 3 en modo de depuración para sincronizar la suscripción.  
  
8.  Suponiendo que no se establezcan otros puntos de interrupción y que se repliquen los comandos adecuados, la ejecución se detiene cuando llega al punto de interrupción en el controlador de lógica de negocios.  
  
### Para depurar un controlador de lógica de negocios en un servidor web con la sincronización web, o para un suscriptor de SQL Server Compact  
  
1.  Configure la publicación y la distribución, cree una publicación y cree una suscripción de extracción a la publicación. La publicación debe admitir la sincronización web o los suscriptores de [!INCLUDE[ssEW](../../includes/ssew-md.md)] .  
  
2.  Cree y registre un controlador de lógica de negocios Para más información, consulte [Implement a Business Logic Handler for a Merge Article](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md).  
  
3.  Establezca un punto de interrupción en el código del controlador de lógica de negocios, ya sea en el método que se depura o en el constructor de clase. Para obtener más información acerca de los métodos que se pueden implementar en un controlador de lógica de negocios, consulte el <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> tema de métodos.  
  
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
  
## Vea también  
 [Implementar un controlador de lógica de negocios para un artículo de mezcla](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)  
  
  