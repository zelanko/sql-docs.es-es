---
title: Índice de texto completo (cuadro de diálogo, Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.fulltextindex
ms.assetid: ef45b585-2567-4abe-b421-9fd0994e0146
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a481a3ea989ec31ea6d3e207633f102e81514940
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2018
ms.locfileid: "43809781"
---
# <a name="full-text-index-dialog-box-visual-database-tools"></a>Índice de texto completo (cuadro de diálogo, Visual Database Tools)
  Este cuadro de diálogo permite crear un índice de texto completo para realizar búsquedas de texto completo en columnas basadas en texto de las tablas de base de datos. Un índice de texto completo se basa en un índice normal, por lo que deberá crear primero este último. El índice normal debe crearse en una sola columna sin valores NULL, y es conveniente elegir una columna con valores más pequeños que una con valores más grandes.  
  
> [!NOTE]  
>  Para crear un índice de texto completo, debe crear primero un catálogo de texto completo para la base de datos mediante una herramienta externa, como [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o el Administrador corporativo.  
  
> [!NOTE]  
>  La funcionalidad de índice de texto completo no está disponible en todas las ediciones de [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="options"></a>Opciones  
 **Índice de texto completo seleccionado**  
 Muestra los índices de texto completo existentes. Seleccione un índice para mostrar sus propiedades en la cuadrícula situada a la derecha. Si la lista está vacía, no se han definido relaciones de texto completo para la tabla.  
  
 **Agregar**  
 Crea un nuevo índice de texto completo.  
  
 **Eliminar**  
 Elimina el índice de texto seleccionado en la lista **Índice de texto completo seleccionado** .  
  
 **Categoría General**  
 Expandido, muestra **Columnas** y **Nombre de catálogo de texto completo**.  
  
 **Columnas**  
 Muestra una lista separada por comas de los nombres de las columnas en las que se pueden realizar búsquedas de texto completo. Para ver la lista completa, haga clic en el botón de puntos suspensivos (**…**) que aparece a la izquierda del campo de propiedad.  
  
 **Full-Text Catalog Name**  
 Muestra el nombre del catálogo de texto completo en el que se almacena el índice de texto completo. Para guardar el índice en un catálogo diferente, haga clic en el nombre del catálogo y elija otro catálogo en la lista desplegable.  
  
> [!NOTE]  
>  El catálogo debe crearse primero en una herramienta externa, como [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o el Administrador corporativo.  
  
 **Categoría Identidad**  
 Expandido, muestra el campo de nombre de este índice.  
  
 **Nombre**  
 Muestra el nombre especificado por el sistema para este índice de texto completo.  
  
 **Categoría Diseñador de tablas**  
 Expandido, muestra las propiedades que definen la actuación del índice.  
  
 **Activo**  
 Indica si actualmente es posible realizar una búsqueda de texto completo mediante este índice de texto completo.  
  
 **Configuración de control de cambios**  
 Describe el estado del seguimiento de cambios de este índice: Manual, Automático o Desactivado.  
  
 **Rastreo completado**  
 Muestra si ha finalizado el rastreo más reciente. Si el valor de esta propiedad es No, el proceso de rastreo estará en ejecución.  
  
 **Fecha final del rastreo actual y último**  
 Muestra la fecha y la hora en que terminó el rastreo más reciente.  
  
 **Errores del rastreo actual o último**  
 Muestra el número de errores del rastreo actual o del más reciente.  
  
 **Versión de índice**  
 Muestra la versión de la tabla del esquema en el momento en que se inició el rastreo.  
  
 **Filas del rastreo actual o último**  
 Muestra el número de filas actualizadas en el rastreo actual o en el más reciente.  
  
 **Fecha de inicio y hora del rastreo actual y último**  
 Muestra la fecha y la hora en que se inició el rastreo actual o el más reciente.  
  
 **Marca de tiempo para el rastreo siguiente**  
 Muestra la fecha y la hora en que se va a iniciar el siguiente rastreo.  
  
 **Tipo de rastreo actual o último**  
 Muestra el tipo al que pertenece el rastreo actual o el más reciente: Completo, Incremental, Actualización o Autopropagación.  
  
 **Nombre de índice único**  
 Muestra una lista con todos los nombres de las columnas de esta base de datos que tienen índices únicos de una sola columna. Estas columnas se pueden utilizar para crear un índice de texto completo.  
  
## <a name="see-also"></a>Vea también  
 [Use el Asistente para indización de texto completo](../../relational-databases/search/use-the-full-text-indexing-wizard.md)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)  
  
  
