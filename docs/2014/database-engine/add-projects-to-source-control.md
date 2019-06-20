---
title: Agregar proyectos al Control de código fuente | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- adding projects
- projects [SQL Server Management Studio], adding
ms.assetid: fd4616b2-a564-4a66-ac53-d1f5cba213c2
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c0936af9b97d08c6bcd5033e61d9fa1c9153272e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62791808"
---
# <a name="add-projects-to-source-control"></a>Agregar proyectos al control de código fuente
  Las soluciones de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] pueden contener varios proyectos de script. El modo en que se agregue un proyecto al control de código fuente depende de si la solución a la que pertenece el proyecto está bajo control de código fuente. Si la solución está bajo control de código fuente, al protegerla, se agrega automáticamente el proyecto al control de código fuente. Para obtener más información acerca de cómo proteger soluciones, consulte [los archivos en](../../2014/database-engine/check-in-files.md).  
  
 Si la solución a la que pertenece el proyecto no está bajo control de código fuente, puede agregarla, con lo que se agregan automáticamente los proyectos de esa solución. Para obtener más información sobre cómo agregar soluciones al control de código fuente, consulte [agregar soluciones al Control de código fuente](../../2014/database-engine/add-solutions-to-source-control.md).  
  
 Si no desea agregar la solución al control de código fuente, puede usar el **Agregar selección al Control de código fuente** comando para agregar el proyecto manualmente.  
  
 El proveedor del control de código fuente no protege directamente los objetos de base de datos, pero puede crear scripts de los objetos de base de datos y guardarlos bajo el control de código fuente.  
  
### <a name="to-add-a-project-to-source-control"></a>Para agregar un proyecto al control de código fuente  
  
1.  En el Explorador de soluciones, seleccione un proyecto.  
  
2.  En el **archivo** menú, elija **Control de código fuente**y, a continuación, haga clic en **agregar proyectos seleccionados al Control de código fuente**.  
  
    > [!NOTE]  
    >  Si usas el **agregar proyectos seleccionados al Control de código fuente** de comando para agregar un proyecto al que pertenece a una solución controlados por código fuente, se le pregunte si desea agregar el proyecto como una subcarpeta de la solución controlados por código fuente o para agregar el proyecto como una carpeta independiente.  
  
3.  Si se le pide, inicie sesión en el proveedor de control de código fuente.  
  
4.  El **agregar a un proyecto de SourceSafe** aparece el cuadro de diálogo. El nombre del proyecto aparece en el **proyecto** cuadro.  
  
5.  En el **carpetas** lista, abra la carpeta donde desea colocar el proyecto. Como alternativa, puede hacer clic en **crear** para crear una carpeta con el nombre mostrado en el **proyecto** cuadro.  
  
## <a name="see-also"></a>Vea también  
 [Agregar soluciones y proyectos al control de código fuente](../../2014/database-engine/add-solutions-and-projects-to-source-control.md)  
  
  
