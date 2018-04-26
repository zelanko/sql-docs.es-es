---
title: Generar script SQL (objetos de replicación) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.rep.generatesqlscript.f1
helpviewer_keywords:
- Generate SQL Script dialog box
ms.assetid: b7ccc34e-1c22-44b8-8eb5-f6423af3164e
caps.latest.revision: 24
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4f23c9232e01e476fd3d13ff7524f9ca06bc4a15
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="generate-sql-script-replication-objects"></a>Generar script SQL (Objetos de replicación)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Un script de replicación contiene los procedimientos almacenados del sistema [!INCLUDE[tsql](../../includes/tsql-md.md)] necesarios para implementar los componentes de replicación convertidos en scripts, como una publicación o una suscripción. Todos los componentes de replicación de una topología deben convertirse en script como parte de un plan de recuperación de desastres y, además, los scripts también pueden utilizarse para automatizar tareas repetitivas. La replicación ofrece dos cuadros de diálogo para crear script para los objetos de replicación:  
  
-   **Generar script SQL**, que está disponible en el menú contextual de la carpeta **Replicación** y en todas las subcarpetas de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Este cuadro de diálogo le permitirá convertir en script todos los objetos de replicación en una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   **Generar script SQL \<nombreDeObjeto>**, que está disponible en el menú contextual para publicaciones y suscripciones. Este cuadro de diálogo le permitirá convertir en script objetos individuales.  
  
 Los cuadros de diálogo convierten en script objetos en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; no se conectan a otras instancias para convertir en script los objetos relacionados.  
  
## <a name="generate-sql-script-options"></a>Opciones de Generar script SQL  
 **Propiedades del distribuidor**  
 Seleccione esta opción para convertir en script los procedimientos almacenados en: habilitar o deshabilitar el distribuidor, agregar o quitar publicadores asociados al distribuidor y crear o quitar la base de datos de distribución.  
  
 **Publicaciones en los siguientes orígenes de datos**  
 Seleccione esta opción para convertir en script los procedimientos almacenados en: habilitar o deshabilitar para publicar y crear o quitar publicaciones, artículos, suscripciones de inserción y trabajos de replicación.  
  
 **Suscripciones en los siguientes orígenes de datos**  
 Seleccione esta opción para convertir en script los procedimientos almacenados para crear o quitar suscripciones de extracción y trabajos de replicación.  
  
 **Para crear o habilitar componentes** y **Para quitar o deshabilitar componentes**  
 Especifique si desea que el script incluya comandos para crear o quitar un objeto de replicación. [!INCLUDE[msCoName](../../includes/msconame-md.md)] le recomienda utilizar el cuadro de diálogo para crear un conjunto de scripts para habilitar y deshabilitar componentes.  
  
 **Trabajos de replicación**  
 Seleccione esta opción para convertir en script trabajos de replicación y llamadas a procedimientos almacenados. Esta opción solo está disponible si genera script desde un distribuidor.  
  
 Los procedimientos almacenados de replicación crean los trabajos necesarios mientras se ejecutan, por lo que no es necesario que seleccione esta opción. Sin embargo, puede resultar útil guardar un registro de los trabajos creados por si fuese necesario volver a crear un trabajo individual.  
  
## <a name="generate-sql-script-objectname-options"></a>Opciones de Generar script SQL \<nombreDeObjeto>  
 **Para crear o habilitar componentes** y **Para quitar o deshabilitar componentes**  
 Especifique si desea que el script incluya comandos para crear o quitar un objeto de replicación. [!INCLUDE[msCoName](../../includes/msconame-md.md)] le recomienda utilizar el cuadro de diálogo para crear un conjunto de scripts para habilitar y deshabilitar componentes.  
  
 **Trabajos de replicación**  
 Está opción solo está disponible en el cuadro de diálogo **Generar script SQL** .  
  
## <a name="see-also"></a>Ver también  
 [Crear script para la replicación](../../relational-databases/replication/scripting-replication.md)  
  
  
