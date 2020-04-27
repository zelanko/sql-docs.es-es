---
title: Agregar proyectos al control de código fuente | Microsoft Docs
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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62791808"
---
# <a name="add-projects-to-source-control"></a>Agregar proyectos al control de código fuente
  Las soluciones de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] pueden contener varios proyectos de script. El modo en que se agregue un proyecto al control de código fuente depende de si la solución a la que pertenece el proyecto está bajo control de código fuente. Si la solución está bajo control de código fuente, al protegerla, se agrega automáticamente el proyecto al control de código fuente. Para obtener más información acerca de la protección de soluciones, consulte [proteger archivos](../../2014/database-engine/check-in-files.md).  
  
 Si la solución a la que pertenece el proyecto no está bajo control de código fuente, puede agregarla, con lo que se agregan automáticamente los proyectos de esa solución. Para obtener más información sobre cómo agregar soluciones al control de código fuente, vea [Agregar soluciones al control de código fuente](../../2014/database-engine/add-solutions-to-source-control.md).  
  
 Si no desea agregar la solución al control de código fuente, puede usar el comando **Agregar selección a control de código fuente** para agregar el proyecto manualmente.  
  
 El proveedor del control de código fuente no protege directamente los objetos de base de datos, pero puede crear scripts de los objetos de base de datos y guardarlos bajo el control de código fuente.  
  
### <a name="to-add-a-project-to-source-control"></a>Para agregar un proyecto al control de código fuente  
  
1.  En el Explorador de soluciones, seleccione un proyecto.  
  
2.  En el menú **archivo** , seleccione **control de código fuente**y, a continuación, haga clic en **Agregar proyectos seleccionados al control de código fuente**.  
  
    > [!NOTE]  
    >  Si usa el comando **Agregar proyectos seleccionados al control de código fuente** para agregar un proyecto que pertenece a una solución controlada por código fuente, se le preguntará si desea agregar el proyecto como una subcarpeta de la solución controlada por código fuente o agregar el proyecto como una carpeta independiente.  
  
3.  Si se le pide, inicie sesión en el proveedor de control de código fuente.  
  
4.  Aparecerá el cuadro de diálogo **Agregar a proyecto de SourceSafe** . El nombre del proyecto aparece en el cuadro **proyecto** .  
  
5.  En la lista **carpetas** , abra la carpeta en la que desea colocar el proyecto. Como alternativa, puede hacer clic en **crear** para crear una carpeta con el nombre que se muestra en el cuadro **proyecto** .  
  
## <a name="see-also"></a>Consulte también  
 [Agregar soluciones y proyectos al control de código fuente](../../2014/database-engine/add-solutions-and-projects-to-source-control.md)  
  
  
