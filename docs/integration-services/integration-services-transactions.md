---
title: Transacciones de Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], transactions
- transactions [Integration Services], about transactions in packages
- tasks [Integration Services], transactions
- transactions [Integration Services]
ms.assetid: 3c78bb26-ddce-4831-a5f8-09d4f4fd53cc
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 46c42deda5b2b66d2979136ad6a82e0ad80042be
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/22/2020
ms.locfileid: "86917485"
---
# <a name="integration-services-transactions"></a>Transacciones de Integration Services

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


  Los paquetes utilizan transacciones para enlazar las acciones de base de datos que las tareas realizan en unidades atómicas y mantener de esta forma la integridad de los datos. Todos los tipos de contenedor de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] (los contenedores de paquetes, de bucles For y Foreach o de secuencias, así como los hosts de las tareas que encapsulan cada tarea) se pueden configurar para que usen transacciones. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] proporciona tres opciones para configurar transacciones: **NotSupported**, **Supported**y **Required**.  
  
-   **Required** indica que el contenedor inicia una transacción, a menos que el contenedor principal ya haya iniciado otra. Si ya existe una transacción, el contenedor la combina. Por ejemplo, si un paquete que no está configurado para admitir transacciones, incluye un contenedor de secuencias que utiliza la opción **Required** , el contenedor de secuencias iniciará su propia transacción. Si el paquete se hubiera configurado para utilizar la opción **Required** , el contenedor de secuencias combinaría la transacción del paquete.  
  
-   **Supported** indica que el contenedor no inicia una transacción, pero sí combina cualquier transacción iniciada por el contenedor principal. Por ejemplo, si un paquete con cuatro tareas Ejecutar SQL inicia una transacción y las cuatro tareas utilizan la opción **Supported** , las actualizaciones de la base de datos realizadas por las tareas Ejecutar SQL se revierten si se produce un error en cualquiera de las tareas. Si el paquete no inicia una transacción, las cuatro tareas Ejecutar SQL no estarán enlazadas por una transacción y no se revertirá ninguna actualización de base de datos, excepto las realizadas por la tarea que tuvo el error.  
  
-   **NotSupported** indica que el contenedor no inicia una transacción ni combina una transacción existente. Una transacción iniciada por un contenedor principal no afecta a los contenedores secundarios configurados de manera que no admitan transacciones. Por ejemplo, si un paquete está configurado para iniciar una transacción y un contenedor de bucles For del paquete utiliza la opción **NotSupported** , no se revertirá ninguna de las tareas del contenedor de bucles For aunque genere un error.  
  
 Para configurar transacciones, hay que establecer la propiedad TransactionOption en el contenedor. Puede establecer esta propiedad en la ventana **Propiedades** de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]o mediante programación.  
  
> [!NOTE]  
>  La propiedad **TransactionOption** tiene influencia sobre el hecho de que el valor de la propiedad **IsolationLevel** solicitada por un contenedor se aplique o no. Para obtener más información, vea la descripción de la propiedad **IsolationLevel** en el tema [Establecer las propiedades de paquete](../integration-services/set-package-properties.md).  
  
## <a name="configure-a-package-to-use-transactions"></a>Configurar un paquete para el uso de transacciones
Cuando configura un paquete para utilizar transacciones, tiene dos opciones:  
  
-   Tener una transacción única para el paquete. En este caso, es el propio paquete el que *inicia* esta transacción, mientras que las tareas y contenedores individuales del paquete participan en esta transacción única.  
  
-   Tener varias transacciones en el paquete. En este caso, el paquete admite transacciones, pero las tareas y contenedores individuales del paquete inician realmente las transacciones.  
  
 El procedimiento siguiente describe cómo configurar ambas opciones.  
  
### <a name="configure-a-package-to-use-a-single-transaction"></a>Configurar un paquete para usar una transacción única  
 En esta opción, el propio paquete inicia una transacción única. Configure el paquete para iniciar esta transacción estableciendo la propiedad TransactionOption del paquete en **Requerido**.  
  
 A continuación, dé de alta tareas y contenedores específicos en esta transacción única. Para dar de alta una tarea o un contenedor en una transacción, establezca la propiedad TransactionOption de esa tarea o contenedor en **Se admite**.  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene el paquete que desea configurar para usar una transacción.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  Haga clic en la pestaña **Flujo de control** .  
  
4.  Haga clic con el botón derecho en cualquier parte del fondo de la superficie de diseño de flujo de control y haga clic en **Propiedades**.  
  
5.  En la ventana **Propiedades** , establezca la propiedad TransactionOption en **Requerido**.  
  
6.  En la superficie de diseño de la pestaña **Flujo de control** , haga clic con el botón derecho en la tarea o contenedor que quiere inscribir en la transacción y luego haga clic en **Propiedades**.  
  
7.  En la ventana **Propiedades** , establezca la propiedad TransactionOption en **Se admite**.  
  
    > [!NOTE]  
    >  Para dar de alta una conexión en una transacción, inscriba las tareas que usan la conexión en la transacción. Para más información, vea [Conexiones de Integration Services &#40;SSIS&#41;](../integration-services/connection-manager/integration-services-ssis-connections.md).  
  
8.  Repita los pasos 6 y 7 para cada tarea y contenedor que desee inscribir en la transacción.  
  
### <a name="configure-a-package-to-use-multiple-transactions"></a>Configurar un paquete de modo que use varias transacciones  
 En esta opción, el propio paquete admite las transacciones pero no inicia una transacción. Configure el paquete para admitir transacciones estableciendo la propiedad TransactionOption del paquete en **Se admite**.  
  
 A continuación, configure las tareas y contenedores deseados dentro del paquete para iniciar transacciones o participar en ellas. Para configurar una tarea o un contenedor para iniciar una transacción, establezca la propiedad TransactionOption de esa tarea o contenedor en **Requerido**.   
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene el paquete que desea configurar para usar transacciones.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  Haga clic en la pestaña **Flujo de control** .  
  
4.  Haga clic con el botón derecho en cualquier parte del fondo de la superficie de diseño de flujo de control y haga clic en **Propiedades**.  
  
5.  En la ventana **Propiedades** , establezca la propiedad TransactionOption en **Se admite**.  
  
    > [!NOTE]  
    >  El paquete ejecuta transacciones pero las transacciones las inician tareas o contenedores del paquete.  
  
6.  En la superficie de diseño de la pestaña **Flujo de control** , haga clic con el botón derecho en la tarea o contenedor del paquete para el que quiere iniciar una transacción y luego haga clic en **Propiedades**.  
  
7.  En la ventana **Propiedades** , establezca la propiedad TransactionOption en **Requerido**.  
  
8.  Si contenedor inicia una transacción, haga clic con el botón derecho en la tarea o el contenedor que quiere inscribir en la transacción y luego haga clic en **Propiedades**.  
  
9. En la ventana **Propiedades** , establezca la propiedad TransactionOption en **Se admite**.  
  
    > [!NOTE]  
    >  Para dar de alta una conexión en una transacción, inscriba las tareas que usan la conexión en la transacción. Para más información, vea [Conexiones de Integration Services &#40;SSIS&#41;](../integration-services/connection-manager/integration-services-ssis-connections.md).  
  
10. Repita los pasos 6 a 9 para cada tarea y cada contenedor que inician una transacción.  

## <a name="multiple-transactions-in-a-package"></a>Varias transacciones en un paquete
Un paquete puede incluir transacciones no relacionadas en un paquete de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Cuando un contenedor situado en medio de una jerarquía de contenedores anidados no admite transacciones, los contenedores situados en un nivel superior o inferior de la jerarquía inician transacciones independientes, si están configurados para admitir transacciones. Las transacciones se confirman o se revierten en orden, desde la tarea más interna en la jerarquía de contenedores anidados hasta el paquete. Sin embargo, una vez confirmada la transacción interna, no se revierte aunque se anule una transacción externa.  
  
### <a name="example-of-multiple-transactions-in-a-package"></a>Ejemplo de varias transacciones en un paquete 
 Por ejemplo, un paquete tiene un contenedor de secuencias con dos contenedores de bucles Foreach y cada contenedor incluye dos tareas Ejecutar SQL. El contenedor de secuencias y las tareas Ejecutar SQL admiten transacciones, pero los contenedores de bucles Foreach no las admiten. En este ejemplo, cada tarea Ejecutar SQL iniciaría su propia transacción, que no se revertiría aunque se anulara la tarea de secuencia.  
  
 Las propiedades de TransactionOption del contenedor de secuencias, el contenedor de bucles Foreach y las tareas Ejecutar SQL se establecen de la siguiente forma:  
  
-   La propiedad TransactionOption del contenedor de secuencias se establece en **Required**.  
  
-   Las propiedades TransactionOption de los contenedores de bucles Foreach se establecen en **NotSupported**.  
  
-   Las propiedades de TransactionOption las tareas Ejecutar SQL se establecen en **Required**.  
  
 En el diagrama siguiente se muestran las cinco transacciones no relacionadas del paquete. El contenedor de secuencias inicia una transacción y las tareas Ejecutar SQL inician las otras cuatro.  
  
 ![Implementación de varias transacciones](../integration-services/media/mw-dts-trans2.gif "Implementación de varias transacciones")  
 
## <a name="inherited-transactions"></a>Transacciones heredadas
 Un paquete puede ejecutar otro paquete, utilizando la tarea Ejecutar paquete. El paquete secundario, que es el que ejecuta la tarea Ejecutar paquete, puede crear su propia transacción de paquete o heredar la del paquete primario.  
  
 Un paquete secundario hereda la transacción de paquete primario si se cumplen las dos condiciones siguientes:  
  
-   Una tarea Ejecutar paquete invoca al paquete.  
  
-   La tarea Ejecutar paquete que invocó al paquete también se combina con la transacción del paquete primario.  
  
 Los contenedores y tareas del paquete secundario no se pueden combinar con la transacción del paquete primario, a menos que el propio paquete secundario se combine con la transacción.  
  
### <a name="example-of-inherited-transactions"></a>Ejemplo de transacciones heredadas  
 En el diagrama siguiente, hay tres paquetes que utilizan transacciones. Cada paquete contiene varias tareas. Para resaltar el comportamiento de las transacciones, solo se muestran las tareas Ejecutar paquete. El paquete A ejecuta los paquetes B y C. A su vez, el paquete B ejecuta los paquetes D y E, y el paquete C ejecuta el paquete F.  
  
 Los paquetes y las tareas tienen los siguientes atributos de transacción:  
  
-   **TransactionOption** se establece en **Required** en los paquetes A y C  
  
-   **TransactionOption** se establece en **Supported** en los paquetes B y D, y en las tareas Ejecutar paquete B, Ejecutar paquete D y Ejecutar paquete F.  
  
-   **TransactionOption** se establece en **NotSupported** en el paquete E y en las tareas Ejecutar paquete C y Ejecutar paquete E.  
  
 ![Flujo de transacciones heredadas](../integration-services/media/mw-dts-executepack.gif "Flujo de transacciones heredadas")  
  
 Solo los paquetes B, D y F pueden heredar transacciones de sus paquetes primarios.  
  
 Los paquetes B y D heredan la transacción iniciada por el paquete A.  
  
 El paquete F hereda la transacción iniciada por el paquete C.  
  
 Los paquetes A y C controlan sus propias transacciones.  
  
 El paquete E no utiliza transacciones.  
 
  
## <a name="external-resources"></a>Recursos externos  
  
-   Entrada de blog, [Cómo usar transacciones en SQL Server Integration Services (SSIS)](https://go.microsoft.com/fwlink/?LinkId=157783)(en inglés), en www.mssqltips.com  
  
## <a name="see-also"></a>Consulte también  
 [Transacciones heredadas](https://msdn.microsoft.com/library/90db5564-d41e-4cfe-8c9e-4e68d41eff1c)   
 [Varias transacciones](https://msdn.microsoft.com/library/c3664a94-be89-40c0-a3a0-84b74a7fedbe)  
  
  
