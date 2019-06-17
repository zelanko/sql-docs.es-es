---
title: 'Tarea 9: Creación de una jerarquía derivada mediante Master Data Manager | Microsoft Docs'
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 3bd2ec05-933f-4947-b1fe-c9226961eb7d
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 7cb2f12115e3fe743c49c2f7e69f765da4501ba2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65489544"
---
# <a name="task-9-creating-a-derived-hierarchy-using-master-data-manager"></a>Tarea 9: Creación de una jerarquía derivada mediante Master Data Manager
  En esta tarea, creará una jerarquía derivada mediante Master Data Manager. Esta jerarquía derivada se deriva de las relaciones de atributo basado en dominio entre la **proveedor** y **estado** entidades.  
  
1.  Cambie a la página principal de **Master Data Manager** haciendo **SQL Server 2012 Master Data Services** en la parte superior de la página.  
  
2.  Haga clic en **Administración del sistema** en la sección **Tareas administrativas** .  
  
3.  Mantenga el mouse sobre **administrar** en la barra de menús y haga clic en **jerarquías derivadas**.  
  
     ![Menú administrar - jerarquías derivadas seleccionadas](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-01.jpg "menú administrar - jerarquías derivadas seleccionadas")  
  
4.  Haga clic en **agregar jerarquía derivada (+)** en la barra de herramientas.  
  
     ![Botón Agregar jerarquía derivada](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-02.jpg "botón Agregar jerarquía derivada")  
  
5.  Tipo **SuppliersInState** para el **nombre de jerarquía derivada**.  
  
6.  Haga clic en **guardar** en la barra de herramientas.  
  
     ![Guardar derivada botón jerarquía](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-03.jpg "guardar derivada botón jerarquía")  
  
7.  Arrastre **proveedor** desde **niveles disponibles: SuppliersInState** a **niveles actuales: SuppliersInState**.  
  
     ![Disponibles en el entidades y jerarquías al nivel actual](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-04.jpg "disponibles en el entidades y jerarquías al nivel actual")  
  
8.  Arrastre **estado** desde **niveles disponibles: SuppliersInState** a **niveles actuales: SuppliersInState**. La pantalla debe mostrar **niveles actuales** tal como se muestra en la siguiente imagen.  
  
     ![Niveles actuales y vista previa de la jerarquía derivada](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-05.jpg "niveles actuales y vista previa de la jerarquía derivada")  
  
9. En el **Preview** ventana, expanda **NY {New York}** y debería ver un proveedor de ese estado tal como se muestra en la imagen anterior.  
  
10. Cambie a la página principal de **Master Data Manager** haciendo **SQL Server 2012 Master Data Services** en la parte superior de la página.  
  
11. Haga clic en **Explorador**.  
  
12. Mantenga el mouse sobre **jerarquías** y haga clic en **Derived: SuppliersInState**.  
  
     ![Jerarquías - derivadas: SuppliersInState menú](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-06.jpg "jerarquías - derivadas: SuppliersInState menú")  
  
13. Haga clic en cualquier **estado** nodo en el **vista de árbol** y verá los proveedores de ese estado en el panel derecho.  
  
     ![Derivado de la jerarquía en el explorador](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-07.jpg "derivados de la jerarquía en el explorador")  
  
## <a name="next-step"></a>Paso siguiente  
 [Lección 5: Automatizar la limpieza y búsqueda de coincidencias con SSIS](../../2014/tutorials/lesson-5-automating-the-cleansing-and-matching-using-ssis.md)  
  
  
