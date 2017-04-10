---
title: "Validar la informaci&#243;n de particiones para un suscriptor de mezcla | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "validación de datos de replicación de mezcla [replicación de SQL Server], particiones"
  - "filtros con parámetros [replicación de SQL Server], validar información de particiones"
  - "información de partición, validar"
ms.assetid: c059553e-df2c-4333-ba79-e8d6e2890c34
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 36
---
# Validar la informaci&#243;n de particiones para un suscriptor de mezcla
  Al definir un filtro de fila con parámetros para una publicación de combinación, se utiliza una función que hace referencia a la información del suscriptor, como el nombre de inicio de sesión del suscriptor. De manera predeterminada, la replicación valida la información del suscriptor basándose en esa función antes de cada sincronización y cada vez que se aplica una instantánea al suscriptor. El proceso de validación garantiza que los datos se dividan correctamente para cada suscriptor. Comportamiento de validación se controla mediante el **validate_subscriber_info** propiedad de publicación, que puede cambiarse mediante [sp_changemergepublication & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md) o en el **Opciones de suscripción** página de la **Propiedades de la publicación** cuadro de diálogo. Para obtener más información acerca de cómo cambiar las propiedades de la publicación, vea [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
## Cómo funciona la validación de particiones  
 Cuando se filtra una publicación, por ejemplo, mediante la función **SUSER_SNAME ()**, el agente de mezcla aplica la instantánea inicial a cada suscriptor basándose en datos que es válidos para el **SUSER_SNAME ()** expresión.  
  
 Si está habilitada la validación, cuando el suscriptor se vuelve a conectar al publicador para la siguiente sincronización, el Agente de mezcla valida la información en el suscriptor y garantiza que cada partición del suscriptor sea igual a la que se recibió en la instantánea inicial. En cada aplicación de mezcla o instantáneas posterior, el Agente de mezcla valida cada partición del suscriptor.  
  
 Si el Agente de mezcla detecta que la función utilizada en la expresión de filtro devuelve un valor distinto del que devolvía en la instantánea inicial, se producirá un error en la aplicación de mezcla o instantáneas, y es posible que sea necesario reinicializar esa suscripción en el suscriptor. La reinicialización puede ser necesaria para evitar problemas que pueden surgir si cambia la configuración de mezcla de un suscriptor, pero puede ser suficiente cambiar la información del suscriptor, como el nombre de inicio de sesión, al valor que tenía en el momento de la instantánea original.  
  
 Cuando el Agente de mezcla valida una partición, además de validarla por comparación con los valores devueltos por las funciones utilizadas en las expresiones de filtro, el agente también comprueba si la instantánea se generó antes que los cambios que la invalidan, como operaciones de limpieza de metadatos o cambios de esquema. Si una instantánea dividida es demasiado antigua, el Agente de mezcla devolverá un error y será necesario volver a generar una instantánea dividida para ese suscriptor, basándose en una instantánea normal actual.  
  
## Vea también  
 [Administración & #40; Replicación y nº 41;](../../relational-databases/replication/administration/administration-replication.md)   
 [Prácticas recomendadas para la administración de replicación](../../relational-databases/replication/administration/best-practices-for-replication-administration.md)   
 [Reinicializar suscripciones](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [Validar datos replicados](../../relational-databases/replication/validate-replicated-data.md)  
  
  