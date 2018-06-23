---
title: Seleccione la página de bases de datos (Asistente de base de datos Asistente para agregar de nuevo grupo de disponibilidad) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.adddatabasewizard.selectdatabases.f1
- sql12.swb.newagwizard.selectdatabases.f1
ms.assetid: 929c5e15-d087-438d-b1f2-aa97c5f8bff8
caps.latest.revision: 12
author: rothja
ms.author: jroth
manager: jhubbard
ms.openlocfilehash: 304ce826a45debaf4d18a63e9d68061ef393705b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36198048"
---
# <a name="select-databases-page-new-availability-group-wizard-add-database-wizard"></a>Seleccione la página de bases de datos (Asistente de base de datos Asistente para agregar de nuevo grupo de disponibilidad)
  En este tema de Ayuda se describen las opciones de la página **Especificar bases de datos** . Esta tema se aplica a [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)] y [!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)] de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
##  <a name="PageOptions"></a> Seleccionar opciones de las bases de datos  
 La cuadrícula **Usar bases de datos en esta instancia de SQL Server** muestra cada base de datos de usuario local. Estas son sus columnas:  
  
 **Nombre**  
 Muestra el nombre de una base de datos de usuario local.  
  
 **Tamaño**  
 Muestra el tamaño de la base de datos, si el tamaño está disponible para el asistente.  
  
 **Estado**  
 Muestra un hipervínculo cuyo texto indica si una determinada base de datos cumple los requisitos previos para ser agregada a un grupo de disponibilidad. Si el estado es “**Cumple los requisitos previos**”, puede agregar la base de datos al grupo de disponibilidad. Si una base de datos no cumple todos los requisitos previos, el hipervínculo **Estado** proporciona una breve explicación de por qué la base de datos no es apta. Haga clic en el vínculo para obtener más información.  
  
 Puede dejar el asistente en la página **Seleccionar base de datos** mientras realiza acciones en una base de datos para que se cumpla un requisito previo. Cuando vuelva a la página **Seleccionar bases de datos** , haga clic en **Actualizar** para actualizar la cuadrícula.  
  
 **Actualizar**  
 Haga clic para actualizar la cuadrícula. Esto es útil después de realizar acciones en una base de datos para que se cumpla un requisito previo.  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Usar el cuadro de diálogo Nuevo grupo de disponibilidad &#40;SQL Server Management Studio&#41;](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Usar el Asistente para agregar una base de datos al grupo de disponibilidad &#40;SQL Server Management Studio&#41;](availability-group-add-database-to-group-wizard.md)  
  
## <a name="see-also"></a>Vea también  
 [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Requisitos previos, restricciones y recomendaciones para grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)  
  
  