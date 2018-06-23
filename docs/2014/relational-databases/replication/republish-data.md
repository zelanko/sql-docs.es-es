---
title: Volver a publicar datos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- republishing data
- publishing [SQL Server replication], Subscribers
- Subscribers [SQL Server replication], republishing data
ms.assetid: a1485cf4-b1c4-49e9-ab06-8ccfaad998f3
caps.latest.revision: 33
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 7348025d382a3de048906aa79fa43fe25ae35649
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36104873"
---
# <a name="republish-data"></a>Volver a publicar datos
  En un modelo de republicación, el publicador envía datos a un suscriptor y éste, a su vez, vuelve a publicar los datos en cualquier número de suscriptores. Esto es útil cuando un publicador tiene que enviar datos a suscriptores a través de un vínculo de comunicaciones lento o costoso. Si hay varios suscriptores en el otro extremo del vínculo, el uso de un republicador desplaza la mayor parte de la carga de distribución a ese extremo del vínculo.  
  
 Para republicar datos, lleve a cabo los siguientes pasos:  
  
1.  Cree una publicación en el publicador.  
  
2.  Cree una suscripción a la publicación para el suscriptor de republicación.  
  
3.  Inicialice la suscripción. La suscripción se debe inicializar antes de crear la publicación en el suscriptor de republicación; de lo contrario, se producirá un error de replicación.  
  
4.  Cree una publicación en la base de datos de suscripciones para el suscriptor de republicación.  
  
5.  Cree suscripciones a la publicación en el suscriptor de republicación para los demás suscriptores.  
  
6.  Inicialice las suscripciones.  
  
> [!NOTE]  
>  Si utiliza la replicación de mezcla en una topología de republicación, todos los suscriptores de republicación deberán utilizar las suscripciones del servidor. Para obtener más información sobre los tipos de suscripción, vea [Subscribe to Publications](subscribe-to-publications.md) (Suscribirse a publicaciones).  
  
 En la siguiente ilustración, tanto el publicador como el republicador actúan como sus propios distribuidores locales. Si estuvieran configurados para utilizar un distribuidor remoto, cada distribuidor tendría que estar en el mismo lado del vínculo de comunicaciones lento o costoso que su publicador. Los publicadores tienen que estar conectados con sus distribuidores remotos mediante vínculos de comunicaciones confiables y de alta velocidad.  
  
 ![Republishing data](media/repl-06a.gif "Republishing data")  
  
 Cualquier servidor puede funcionar como publicador y suscriptor. Por ejemplo, observe el siguiente diagrama en el que la publicación de una tabla que existe en Londres se tiene que distribuir a cuatro ciudades diferentes de los Estados Unidos: Chicago, Nueva York, San Diego y Seattle. El servidor de Nueva York es el elegido para que se suscriba a la tabla publicada de Londres, porque el sitio de Nueva York cumple estas condiciones:  
  
-   El vínculo de red de retorno a Londres es relativamente confiable.  
  
-   Los costos de comunicación entre Londres y Nueva York son aceptables.  
  
-   Hay buenas líneas de comunicación de red desde Nueva York a todos los demás sitios suscriptores de Estados Unidos.  
  
     ![Volver a publicar datos en ubicaciones dispersas](media/repl-06.gif "Volver a publicar datos en ubicaciones dispersas")  
  
 La replicación es compatible con los casos de republicación que se muestran en la tabla siguiente.  
  
|publicador|Suscriptor de publicación|Suscriptor|  
|---------------|---------------------------|----------------|  
|Publicación transaccional|Suscripción transaccional/publicación transaccional|Suscripción transaccional|  
|Publicación transaccional|Publicación de combinación/suscripción transaccional<sup>1</sup>|Suscripción de mezcla|  
|Publicación de combinación|Suscripción de mezcla/publicación de combinación|Suscripción de mezcla|  
|Publicación de combinación|Suscripción de mezcla/publicación transaccional|Suscripción transaccional|  
  
 <sup>1</sup>debe establecer el `@published_in_tran_pub` propiedad en la publicación de combinación. De forma predeterminada, la replicación transaccional espera que las tablas del suscriptor se traten como de solo lectura. Si la replicación de mezcla realiza cambios en los datos de una tabla de una suscripción transaccional, la convergencia de los datos puede no producirse. Para evitar este riesgo, se recomienda que cada tabla de este tipo se especifique como solo para descarga en la publicación de combinación. Esto evita que un suscriptor de mezcla cargue cambios de datos en la tabla. Para obtener más información, vea [Optimize Merge Replication Performance with Download-Only Articles](merge/optimize-merge-replication-performance-with-download-only-articles.md) (Optimizar el rendimiento de la replicación de mezcla con artículos de solo descarga).  
  
## <a name="see-also"></a>Vea también  
 [Configurar distribución](configure-distribution.md)   
 [Publicar datos y objetos de base de datos](publish/publish-data-and-database-objects.md)   
 [Subscribe to Publications](subscribe-to-publications.md)   
 [Initialize a Subscription](initialize-a-subscription.md)  (Inicializar una suscripción)  
 [Sincronizar datos](synchronize-data.md)  
  
  