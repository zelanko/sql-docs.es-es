---
title: Valores de HOST_NAME | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newsubwizard.hostnamevalue.f1
ms.assetid: 21548f08-2910-4a55-baac-b911ba9afaf1
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4f8f7f1304b0d72cf59467aee16c04481fbd51ad
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62721190"
---
# <a name="hostname-values"></a>Valores de HOST_NAME
  Las publicaciones de combinación con filtros con parámetros utilizan la función SUSER_SNAME() o la función HOST_NAME() para filtrar datos. La función se especifica en el Asistente para nueva publicación o en el cuadro de diálogo **Propiedades de la publicación** .  
  
 De forma predeterminada, la función HOST_NAME() devuelve el nombre del equipo que se conecta al publicador. Cuando se utilizan filtros con parámetros, es normal reemplazar este valor suministrando otro en esta página del asistente. A continuación, la función HOST_NAME() devuelve el valor que se ha especificado en vez del nombre del equipo. Para obtener más información, vea la sección sobre cómo reemplazar el valor de HOST_NAME() de [Filtros de fila con parámetros](merge/parameterized-filters-parameterized-row-filters.md).  
  
> [!NOTE]  
>  Si reemplaza HOST_NAME(), todas las llamadas a la función HOST_NAME() devolverán el valor especificado. Asegúrese de que otras aplicaciones no dependen de HOST_NAME() al devolver el nombre del equipo.  
  
## <a name="options"></a>Opciones  
 **Propiedades de la suscripción**  
 Escriba un valor para cada suscriptor en la columna **Valor de HOST_NAME** o acepte el valor predeterminado, que es el nombre del equipo suscriptor.  
  
## <a name="see-also"></a>Vea también  
 [Crear una suscripción de extracción](create-a-pull-subscription.md)   
 [Create a Push Subscription](create-a-push-subscription.md)   
 [View and Modify Pull Subscription Properties](view-and-modify-pull-subscription-properties.md)  (Ver y modificar las propiedades de una suscripción de extracción)  
 [Ver y modificar las propiedades de una suscripción de inserción](view-and-modify-push-subscription-properties.md)   
 [HOST_NAME &#40;Transact-SQL&#41;](/sql/t-sql/functions/host-name-transact-sql)   
 [Suscribirse a publicaciones](subscribe-to-publications.md)  
  
  
