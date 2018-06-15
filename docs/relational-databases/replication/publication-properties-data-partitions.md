---
title: Propiedades de la publicación, Particiones de datos | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.rep.newpubwizard.pubproperties.datapartitions.f1
ms.assetid: 5869edb7-d05f-495b-b828-b7fd5e828d20
caps.latest.revision: 20
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7839c1bb3f4bf944ba230472abdca3a81fa58d38
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32961020"
---
# <a name="publication-properties-data-partitions"></a>Propiedades de la publicación, Particiones de datos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La página **Particiones de datos** del cuadro de diálogo **Propiedades de la publicación** le permite definir particiones de datos para publicaciones de combinación que utilizan el filtro con parámetros. Después de definir particiones, puede generar instantáneas para estas particiones, proporcionando distintos conjuntos de datos iniciales para diferentes suscriptores sobre la base de las propiedades de conexión (inicio de sesión o nombre del equipo) de los suscriptores. También puede optar por permitir que los suscriptores soliciten la entrega y la generación de instantáneas si no tienen una instantánea disponible para su partición la primera vez que realizan la sincronización. Para más información, consulte [Crear una instantánea para una publicación de mezcla con filtros con parámetros](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
## <a name="options"></a>Opciones  
 **Agregar**  
 Haga clic en **Agregar** para definir una partición. En el cuadro de diálogo **Agregar partición de datos** , especifique valores para **HOST_NAME()** o **SUSER_SNAME()** y defina una programación para actualizar las instantáneas.  
  
 **Editar**  
 Seleccione una partición existente en la cuadrícula y haga clic en **Editar** para editarla.  
  
 **Eliminar**  
 Seleccione una partición existente en la cuadrícula y haga clic en **Eliminar** para eliminarla.  
  
 **Generar instantáneas seleccionadas ahora**  
 Seleccione una o varias particiones en la cuadrícula y haga clic en **Generar instantáneas seleccionadas ahora** para generar instantáneas para estas particiones.  
  
 **Limpiar instantáneas existentes**  
 Seleccione una o varias particiones en la cuadrícula y haga clic en **Limpiar instantáneas existentes** para limpiar las instantáneas de estas particiones.  
  
 **Definir automáticamente una partición y generar una instantánea si es necesario cuando un suscriptor nuevo intente sincronizarse**  
 Seleccione esta opción si desea permitir que los suscriptores soliciten la generación y aplicación de instantáneas. Los suscriptores podrían solicitar esta opción si no tienen una instantánea disponible para su partición la primera vez que realizan la sincronización.  
  
## <a name="see-also"></a>Ver también  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Ver y modificar propiedades de publicación](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [Publicar datos y objetos de base de datos](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Instantáneas para publicaciones de combinación con filtros con parámetros](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)  
  
  
