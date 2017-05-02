---
title: "Optimizar el rendimiento de la replicación de mezcla con seguimiento condicional de eliminaciones | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- conditional delete tracking [SQL Server replication]
- merge replication [SQL Server replication], conditional delete tracking
- articles [SQL Server replication], conditional delete tracking
ms.assetid: 58f120a3-ea3a-4e97-93f0-0eb4e580ecf2
caps.latest.revision: 23
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 61f3c832be62fb53a82713182dc026d7a6fc3fb5
ms.lasthandoff: 04/11/2017

---
# <a name="optimize-merge-replication-performance-with-conditional-delete-tracking"></a>Optimizar el rendimiento de la replicación de mezcla con seguimiento condicional de eliminaciones
    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 En la replicación de mezcla, puede especificar que los desencadenadores de replicación y las tablas del sistema no realicen el seguimiento de las eliminaciones de uno o varios artículos. Si se especifica esta opción para un artículo, no se realiza el seguimiento ni la replicación de las eliminaciones del publicador ni de ningún suscriptor. Esta opción está disponible para admitir una serie de casos de aplicación y para proporcionar una optimización del rendimiento para los casos en los que la replicación de eliminaciones no es necesaria o deseable. El rendimiento se mejora de tres maneras: los metadatos de las eliminaciones no se almacenan, las eliminaciones no se enumeran durante la sincronización, y las eliminaciones no se replican ni se aplican en el suscriptor.  
  
> [!NOTE]  
>  Para utilizar artículos de solo descarga, el nivel de compatibilidad de la publicación debe ser como mínimo de 90RTM.  
  
 La opción se puede especificar al crear una publicación, o bien se puede activar o desactivar si la aplicación requiere que algunas eliminaciones se repliquen y otras no, como las eliminaciones por lotes. En los siguientes ejemplos se ilustra de qué maneras se puede utilizar esta opción en una aplicación:  
  
-   Normalmente, una aplicación para personal de ventas móvil tiene tablas como **SalesOrderHeader**, **SalesOrderDetail** y **Product**. Los pedidos se pasan al suscriptor y después se replican en el publicador, que suele proporcionar los datos a un sistema de cumplimentación de pedidos. Muchos trabajadores móviles utilizan dispositivos de mano que tienen un almacenamiento limitado: una vez recibido el pedido en el publicador, dicho pedido puede eliminarse del suscriptor. La eliminación no se propaga al publicador porque el pedido sigue activo en el sistema.  
  
     En esta situación, no se realiza el seguimiento de las eliminaciones para las tablas **SalesOrderHeader** y **SalesOrderDetail** . Se realiza el seguimiento de las eliminaciones para la tabla **Product** , ya que si se elimina un producto en el publicador, la eliminación debe enviarse al suscriptor para que la lista de productos se mantenga actualizada.  
  
-   Una aplicación puede almacenar datos históricos en una tabla como **TransactionHistory**, de la que periódicamente se purgan los registros cuya antigüedad es superior a un año. La tabla se puede filtrar para que los suscriptores reciban solo los datos de las transacciones del mes en curso. Las eliminaciones mensuales de lotes en el publicador que purgan datos antiguos no son relevantes para los suscriptores, pero aun así se realiza un seguimiento de las mismas y se enumeran de forma predeterminada.  
  
     En esta situación, antes de que tenga lugar el procesamiento por lotes, la actividad podría detenerse en el sistema y la aplicación podría deshabilitar el seguimiento de las eliminaciones. Una vez completado el procesamiento, el seguimiento podría volver a habilitarse.  
  
> [!IMPORTANT]  
>  Si siguen llevándose a cabo otras actividades en el publicador, deberá asegurarse de que no se producen eliminaciones que se deban propagar a los suscriptores mientras el seguimiento de eliminaciones está deshabilitado.  
  
 **Para especificar que no se realice el seguimiento de las eliminaciones**  
  
-   Programación [!INCLUDE[tsql](../../../includes/tsql-md.md)] de la replicación: [especificar que no se debe realizar un seguimiento de las eliminaciones para los artículos de mezcla &#40;programación de la replicación con Transact-SQL&#41;](../../../relational-databases/replication/publish/specify-that-deletes-should-not-be-tracked-for-merge-articles.md)  
  
## <a name="see-also"></a>Vea también  
 [Opciones de artículos para replicación de mezcla](../../../relational-databases/replication/merge/article-options-for-merge-replication.md)   
 [Optimizar el rendimiento de la replicación de mezcla con artículos de solo descarga](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)  
  
  
