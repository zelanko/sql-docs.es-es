---
title: Configurar un paquete para que utilicen transacciones | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- transactions [Integration Services], configuring packages to use
ms.assetid: 8bf14957-27b4-456b-81d9-e1a0e0ca94b7
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 8637409c0248506de68fa6615dcd6b9edbf7a5bf
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36204228"
---
# <a name="configure-a-package-to-use-transactions"></a>Configurar un paquete para el uso de transacciones
  Cuando configura un paquete para utilizar transacciones, tiene dos opciones:  
  
-   Tener una transacción única para el paquete. En este caso, es el propio paquete el que *inicia* esta transacción, mientras que las tareas y contenedores individuales del paquete participan en esta transacción única.  
  
-   Tener varias transacciones en el paquete. En este caso, el paquete admite transacciones, pero las tareas y contenedores individuales del paquete inician realmente las transacciones.  
  
 El procedimiento siguiente describe cómo configurar ambas opciones.  
  
## <a name="configuring-a-single-transaction"></a>Configurar una transacción única  
 En esta opción, el propio paquete inicia una transacción única. Configure el paquete para iniciar esta transacción estableciendo la propiedad TransactionOption del paquete en `Required`.  
  
 A continuación, dé de alta tareas y contenedores específicos en esta transacción única. Para dar de alta una tarea o contenedor en una transacción, establezca la propiedad TransactionOption de esa tarea o contenedor en `Supported`.  
  
#### <a name="to-configure-a-package-to-use-a-single-transaction"></a>Para configurar un paquete para usar una transacción única  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene el paquete que desea configurar para usar una transacción.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  Haga clic en la pestaña **Flujo de control** .  
  
4.  Haga clic con el botón derecho en cualquier parte del fondo de la superficie de diseño de flujo de control y haga clic en **Propiedades**.  
  
5.  En el **propiedades** ventana, establezca la propiedad TransactionOption `Required`.  
  
6.  En la superficie de diseño de la pestaña **Flujo de control** , haga clic con el botón derecho en la tarea o contenedor que quiere inscribir en la transacción y luego haga clic en **Propiedades**.  
  
7.  En el **propiedades** ventana, establezca la propiedad TransactionOption `Supported`.  
  
    > [!NOTE]  
    >  Para dar de alta una conexión en una transacción, inscriba las tareas que usan la conexión en la transacción. Para más información, vea [Conexiones de Integration Services &#40;SSIS&#41;](connection-manager/integration-services-ssis-connections.md).  
  
8.  Repita los pasos 6 y 7 para cada tarea y contenedor que desee inscribir en la transacción.  
  
## <a name="configuring-multiple-transactions"></a>Configurar varias transacciones  
 En esta opción, el propio paquete admite las transacciones pero no inicia una transacción. Configure el paquete para admitir transacciones estableciendo la propiedad TransactionOption del paquete en `Supported`.  
  
 A continuación, configure las tareas y contenedores deseados dentro del paquete para iniciar transacciones o participar en ellas. Para configurar una tarea o contenedor para iniciar una transacción, debe establecer la propiedad TransactionOption de esa tarea o contenedor en `Required`.  
  
#### <a name="to-configure-a-package-to-use-multiple-transactions"></a>Para configurar un paquete de modo que use varias transacciones  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene el paquete que desea configurar para usar transacciones.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  Haga clic en la pestaña **Flujo de control** .  
  
4.  Haga clic con el botón derecho en cualquier parte del fondo de la superficie de diseño de flujo de control y haga clic en **Propiedades**.  
  
5.  En el **propiedades** ventana, establezca la propiedad TransactionOption `Supported`.  
  
    > [!NOTE]  
    >  El paquete ejecuta transacciones pero las transacciones las inician tareas o contenedores del paquete.  
  
6.  En la superficie de diseño de la pestaña **Flujo de control** , haga clic con el botón derecho en la tarea o contenedor del paquete para el que quiere iniciar una transacción y luego haga clic en **Propiedades**.  
  
7.  En el **propiedades** ventana, establezca la propiedad TransactionOption `Required`.  
  
8.  Si contenedor inicia una transacción, haga clic con el botón derecho en la tarea o el contenedor que quiere inscribir en la transacción y luego haga clic en **Propiedades**.  
  
9. En el **propiedades** ventana, establezca la propiedad TransactionOption `Supported`.  
  
    > [!NOTE]  
    >  Para dar de alta una conexión en una transacción, inscriba las tareas que usan la conexión en la transacción. Para obtener más información, vea [Conexiones de Integration Services &#40;SSIS&#41;](connection-manager/integration-services-ssis-connections.md).  
  
10. Repita los pasos 6 a 9 para cada tarea y cada contenedor que inician una transacción.  
  
## <a name="see-also"></a>Vea también  
 [Transacciones de Integration Services](integration-services-transactions.md)  
  
  