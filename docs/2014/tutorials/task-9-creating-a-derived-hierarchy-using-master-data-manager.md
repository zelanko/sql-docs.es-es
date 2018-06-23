---
title: 'Tarea 9: Crear una jerarquía derivada mediante Master Data Manager | Documentos de Microsoft'
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3bd2ec05-933f-4947-b1fe-c9226961eb7d
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 35584d33afac7a2a8f74abd013288a974cade512
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36204291"
---
# <a name="task-9-creating-a-derived-hierarchy-using-master-data-manager"></a>Tarea 9: crear una jerarquía derivada mediante Master Data Manager
  En esta tarea, creará una jerarquía derivada mediante Master Data Manager. Esta jerarquía derivada se deriva de las relaciones de atributo basado en dominio entre la **proveedor** y **estado** entidades.  
  
1.  Cambie a la página principal de **Master Data Manager** haciendo clic en **SQL Server 2012 Master Data Services** en la parte superior de la página.  
  
2.  Haga clic en **Administración del sistema** en la sección **Tareas administrativas** .  
  
3.  Mantenga el mouse sobre **administrar** en la barra de menús y haga clic en **jerarquías derivadas**.  
  
     ![Menú administrar - jerarquías derivadas seleccionadas](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-01.jpg "menú administrar - jerarquías derivadas seleccionadas")  
  
4.  Haga clic en **agregar jerarquía derivada (+)** botón en la barra de herramientas.  
  
     ![Botón Agregar jerarquía derivada](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-02.jpg "botón Agregar jerarquía derivada")  
  
5.  Tipo de **SuppliersInState** para el **nombre de jerarquía derivada**.  
  
6.  Haga clic en **guardar** botón en la barra de herramientas.  
  
     ![Guardar derivado jerarquía botón](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-03.jpg "guardar derivado botón de jerarquía")  
  
7.  Arrastre **proveedor** de **niveles disponibles: SuppliersInState** a **niveles actuales: SuppliersInState**.  
  
     ![Entidades y jerarquías en el nivel actual disponibles](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-04.jpg "entidades y jerarquías en el nivel actual disponibles")  
  
8.  Arrastre **estado** de **niveles disponibles: SuppliersInState** a **niveles actuales: SuppliersInState**. La pantalla debe mostrar **niveles actuales** tal como se muestra en la siguiente imagen.  
  
     ![Niveles actuales y vista previa de jerarquía derivada](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-05.jpg "niveles actuales y vista previa de jerarquía derivada")  
  
9. En el **vista previa** ventana, expanda **NY {New York}** y debería ver un proveedor de ese estado tal como se muestra en la imagen anterior.  
  
10. Cambie a la página principal de **Master Data Manager** haciendo clic en **SQL Server 2012 Master Data Services** en la parte superior de la página.  
  
11. Haga clic en **Explorador**.  
  
12. Mantenga el mouse sobre **jerarquías** y haga clic en **Derived: SuppliersInState**.  
  
     ![Jerarquías - derivadas: SuppliersInState menú](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-06.jpg "jerarquías - derivadas: SuppliersInState menú")  
  
13. Haga clic en cualquier **estado** nodo en el **vista de árbol** y debería ver los proveedores de ese estado en el panel derecho.  
  
     ![Deriva de la jerarquía en el Explorador de](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-07.jpg "derivadas de la jerarquía en el explorador")  
  
## <a name="next-step"></a>Paso siguiente  
 [Lección 5: Automatizar la limpieza y búsqueda de coincidencias con SSIS](../../2014/tutorials/lesson-5-automating-the-cleansing-and-matching-using-ssis.md)  
  
  