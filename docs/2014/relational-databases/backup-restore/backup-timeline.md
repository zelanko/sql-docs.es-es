---
title: Escala de tiempo de copia de seguridad | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- SQL12.SWB.POINTINTIMERESTORE.F1
- sql12.swb.backuptimeline.f1
helpviewer_keywords:
- Backup Timeline
ms.assetid: ae3565f2-ddb2-4469-a992-7531d4f9ebb8
caps.latest.revision: 23
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: b1092560dc3ef1310adfcb5eec02bcf7ed124973
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36113170"
---
# <a name="backup-timeline"></a>Escala de tiempo de copia de seguridad
  Use el cuadro de diálogo **Escala de tiempo de la copia de seguridad** para buscar y especificar las copias de seguridad para restaurar una base de datos a un momento dado. El acceso al cuadro de diálogo **Escala de tiempo de la copia de seguridad** se abre haciendo clic en **Escala de tiempo** en el panel **Restaurar base de datos (página General)** . Este cuadro de diálogo permite ver una escala de tiempo de las operaciones de restauración realizadas sobre la base de datos.  
  
 El Asesor para recuperación de base de datos se asegura de que solo estén seleccionadas las copias de seguridad necesarias para restaurar a ese momento específico. Estas copias de seguridad seleccionadas componen el plan de restauraciones recomendado para la operación de restauración. Debe usar solo las copias de seguridad seleccionadas. Para obtener más información sobre el Asistente para recuperación de base de datos, vea [Información general sobre restauración y recuperación &#40;SQL Server&#41;](restore-and-recovery-overview-sql-server.md).  
  
## <a name="restore-to"></a>Restaurar en  
 La**Última copia de seguridad realizada** está seleccionada de forma predeterminada. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] seleccionará las copias de seguridad adecuadas para restaurar la base de datos y la restaurará hasta el momento de la última copia de seguridad. Haga clic en **Fecha y hora específicas** para establecer manualmente la fecha y hora (seleccionando un punto concreto en el tiempo).  
  
 **Fecha y hora específicas** permite detener la restauración en la fecha y hora específicas que seleccione. La escala de tiempo muestra una representación de las operaciones de copia de seguridad realizadas en las 24 horas anteriores y posteriores a la fecha y hora seleccionadas.  
  
 **Date**  
 Escriba o seleccione una fecha de la lista desplegable.  
  
 **Time**  
 Escriba o seleccione una fecha para designar el momento dado en que la restauración debe detenerse.  
  
 **Intervalo de escala de tiempo**  
 Muestra las opciones para los tipos de intervalo visibles en la escala de tiempo.  
  
## <a name="timeline-and-legend"></a>Escala de tiempo y leyenda  
 Use las barras de desplazamiento situadas sobre la escala de tiempo para mover el cursor hacia delante y hacia atrás a lo largo de la escala de tiempo. Haga clic en una copia de seguridad para mover la barra de desplazamiento al final de la copia de seguridad. Mantenga el mouse sobre un marcador para mostrar una Información en pantalla que proporciona información acerca del conjunto de copia de seguridad seleccionado. La información de copia de seguridad se muestra en la escala de tiempo mediante los siguientes marcadores.  
  
 Triángulo mayor  
 Representa las copias de seguridad completas realizadas sobre la base de datos, con indicación del momento concreto en el que se realizó cada copia de seguridad completa.  
  
 Triángulo menor  
 Representa las copias de seguridad diferenciales realizadas sobre la base de datos, con indicación del momento concreto en el que se realizó cada copia de seguridad diferencial.  
  
 Áreas en verde  
 Representan la cobertura de la copia de seguridad del registro de transacciones.  
  
 Línea roja  
 Solo puede colocarse a lo largo de la escala de tiempo donde es posible la restauración. Moviendo la línea roja a lo largo de la escala de tiempo se ajustará la fecha y hora mostrada en los cuadros **Fecha** y **Hora** .  
  
## <a name="see-also"></a>Vea también  
 [Restaurar la base de datos &#40;página General&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)  
  
  