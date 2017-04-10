---
title: "Valores de HOST_NAME | Microsoft Docs"
ms.custom: ""
ms.date: "03/06/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newsubwizard.hostnamevalue.f1"
ms.assetid: 21548f08-2910-4a55-baac-b911ba9afaf1
caps.latest.revision: 20
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 20
---
# Valores de HOST_NAME
  Las publicaciones de combinación con filtros con parámetros utilizan la función SUSER_SNAME() o la función HOST_NAME() para filtrar datos. La función se especifica en el Asistente para nueva publicación o en el cuadro de diálogo **Propiedades de la publicación** .  
  
 De forma predeterminada, la función HOST_NAME() devuelve el nombre del equipo que se conecta al publicador. Cuando se utilizan filtros con parámetros, es normal reemplazar este valor suministrando otro en esta página del asistente. A continuación, la función HOST_NAME() devuelve el valor que se ha especificado en vez del nombre del equipo. Para obtener más información, consulte la sección "Reemplazar el valor de HOST_NAME ()" de [filtros de fila parametrizados](../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
> [!NOTE]  
>  Si reemplaza HOST_NAME(), todas las llamadas a la función HOST_NAME() devolverán el valor especificado. Asegúrese de que otras aplicaciones no dependen de HOST_NAME() al devolver el nombre del equipo.  
  
## Opciones  
 **Propiedades de la suscripción**  
 Escriba un valor para cada suscriptor en la **valor de HOST_NAME** columna o acepte el predeterminado, que es el nombre del equipo del suscriptor.  
  
## Vea también  
 [Crear una suscripción de extracción](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Crear una suscripción de inserción](../../relational-databases/replication/create-a-push-subscription.md)   
 [Ver y modificar las propiedades de una suscripción de extracción](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [Ver y modificar las propiedades de una suscripción de inserción](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [HOST_NAME & #40; Transact-SQL & #41;](../../t-sql/functions/host-name-transact-sql.md)   
 [Suscribirse a publicaciones](../../relational-databases/replication/subscribe-to-publications.md)  
  
  