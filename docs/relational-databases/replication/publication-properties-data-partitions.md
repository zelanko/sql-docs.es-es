---
title: "Propiedades de la publicaci&#243;n, Particiones de datos | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newpubwizard.pubproperties.datapartitions.f1"
ms.assetid: 5869edb7-d05f-495b-b828-b7fd5e828d20
caps.latest.revision: 20
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 20
---
# Propiedades de la publicaci&#243;n, Particiones de datos
  La página **Particiones de datos** del cuadro de diálogo **Propiedades de la publicación** le permite definir particiones de datos para publicaciones de combinación que utilizan el filtro con parámetros. Después de definir particiones, puede generar instantáneas para estas particiones, proporcionando distintos conjuntos de datos iniciales para diferentes suscriptores sobre la base de las propiedades de conexión (inicio de sesión o nombre del equipo) de los suscriptores. También puede optar por permitir que los suscriptores soliciten la entrega y la generación de instantáneas si no tienen una instantánea disponible para su partición la primera vez que realizan la sincronización. Para más información, consulte [Create a Snapshot for a Merge Publication with Parameterized Filters](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
## Opciones  
 **Agregar**  
 Haga clic en **Agregar** para definir una partición. En el **Agregar partición de datos** cuadro de diálogo, especifique valores para **HOST_NAME ()** o **SUSER_SNAME ()**, y definir una programación para actualizar las instantáneas.  
  
 **Editar**  
 Seleccione una partición existente en la cuadrícula y haga clic en **modificar** para modificar la partición.  
  
 **Delete**  
 Seleccione una partición existente en la cuadrícula y haga clic en **Eliminar** para eliminar la partición.  
  
 **Generar instantáneas seleccionadas ahora**  
 Seleccione una o varias particiones en la cuadrícula y haga clic en **generar instantáneas seleccionadas ahora** para generar instantáneas para estas particiones.  
  
 **Limpiar instantáneas existentes**  
 Seleccione una o varias particiones en la cuadrícula y haga clic en **Limpiar instantáneas existentes** para limpiar instantáneas para estas particiones.  
  
 **Definir automáticamente una partición y generar una instantánea si es necesario cuando un suscriptor nuevo intente sincronizarse**  
 Seleccione esta opción si desea permitir que los suscriptores soliciten la generación y aplicación de instantáneas. Los suscriptores podrían solicitar esta opción si no tienen una instantánea disponible para su partición la primera vez que realizan la sincronización.  
  
## Vea también  
 [Crear una publicación](../../relational-databases/replication/publish/create-a-publication.md)   
 [Ver y modificar propiedades de publicación](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Filtros de fila con parámetros](../../relational-databases/replication/merge/parameterized-row-filters.md)   
 [Publicar datos y objetos de base de datos](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Instantáneas para publicaciones de combinación con filtros con parámetros](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)  
  
  