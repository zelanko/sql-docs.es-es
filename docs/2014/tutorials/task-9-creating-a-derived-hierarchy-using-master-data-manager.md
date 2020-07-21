---
title: 'Tarea 9: crear una jerarquía derivada mediante Master Data Manager | Microsoft Docs'
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 3bd2ec05-933f-4947-b1fe-c9226961eb7d
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 56e3d832fccbab849d0646c761964aee9266181e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85006207"
---
# <a name="task-9-creating-a-derived-hierarchy-using-master-data-manager"></a>Tarea 9: Creación de una jerarquía derivada mediante Master Data Manager
  En esta tarea, creará una jerarquía derivada mediante Master Data Manager. Esta jerarquía derivada se deriva de las relaciones de atributo basado en dominio entre las entidades **proveedor** y **Estado** .  
  
1.  Cambie a la Página principal de **Master Data Manager** haciendo clic en **SQL Server 2012 Master Data Services** en la parte superior de la página.  
  
2.  Haga clic en **Administración del sistema** en la sección **Tareas administrativas** .  
  
3.  Mantenga el mouse sobre **administrar** en la barra de menús y haga clic en **jerarquías derivadas**.  
  
     ![Menú Administrar - Jerarquías derivadas seleccionadas](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-01.jpg "Menú Administrar - Jerarquías derivadas seleccionadas")  
  
4.  Haga clic en el botón **Agregar jerarquía derivada (+)** de la barra de herramientas.  
  
     ![Botón Agregar jerarquía derivada](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-02.jpg "Botón Agregar jerarquía derivada")  
  
5.  Escriba **SuppliersInState** para el **nombre de la jerarquía derivada**.  
  
6.  Haga clic en el botón **Guardar** en la barra de herramientas.  
  
     ![Botón Guardar jerarquía derivada](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-03.jpg "Botón Guardar jerarquía derivada")  
  
7.  Arrastre **proveedor** desde **niveles disponibles: SuppliersInState** a **niveles actuales: SuppliersInState**.  
  
     ![Entidades y jerarquías disponibles en el nivel actual](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-04.jpg "Entidades y jerarquías disponibles en el nivel actual")  
  
8.  Arrastre **Estado** desde **niveles disponibles: SuppliersInState** a **niveles actuales: SuppliersInState**. La pantalla debe tener los **niveles actuales** , tal como se muestra en la siguiente imagen.  
  
     ![Niveles actuales y vista previa de la jerarquía derivada](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-05.jpg "Niveles actuales y vista previa de la jerarquía derivada")  
  
9. En la ventana de **vista previa** , expanda **NY {Nueva York}** y debería ver un proveedor en ese estado, tal como se muestra en la imagen anterior.  
  
10. Cambie a la Página principal de **Master Data Manager** haciendo clic en **SQL Server 2012 Master Data Services** en la parte superior de la página.  
  
11. Haga clic en **Explorador**.  
  
12. Mantenga el mouse sobre las **jerarquías** y haga clic en **derived: SuppliersInState**.  
  
     ![Jerarquías- Menú Derived:SuppliersInState](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-06.jpg "Jerarquías- Menú Derived:SuppliersInState")  
  
13. Haga clic en cualquier nodo de **Estado** en la **vista de árbol** y debería ver los proveedores en ese estado en el panel derecho.  
  
     ![Jerarquía derivada en el Explorador](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-07.jpg "Jerarquía derivada en el Explorador")  
  
## <a name="next-step"></a>siguiente paso  
 [Lección 5: Automatización de la limpieza y la búsqueda de coincidencias con SSIS](../../2014/tutorials/lesson-5-automating-the-cleansing-and-matching-using-ssis.md)  
  
  
