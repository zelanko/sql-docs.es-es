---
title: 'Tarea 1: definir una directiva de coincidencia | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 6f89a720-fce5-4f60-bef3-a159bbc9f25c
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 3e4777cf05e7f3eab62c389ace8b8d8a96cae304
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "65481314"
---
# <a name="task-1-defining-a-matching-policy"></a>Tarea 1: Definición de una directiva de coincidencia
  En esta tarea, creará una directiva de coincidencia que contiene una regla. La regla tendrá un requisito previo: **ID. de proveedor**, lo que significa que los identificadores de proveedor deben coincidir antes de usar los demás dominios de la regla. La regla usa otros dos dominios: el **nombre del proveedor con el** valor de **similitud** establecido en **70%** y el **correo electrónico de contacto** con el valor de **similitud** establecido en **30%**.  
  
1.  En la Página principal del **cliente DQS**, haga clic en la **flecha a la derecha** junto a la base de conocimiento **proveedores** y seleccione **Directiva de coincidencia**.  
  
     ![Menú Directiva de coincidencia en la página principal](../../2014/tutorials/media/et-definingamatchingpolicy-01.jpg "Menú Directiva de coincidencia en la página principal")  
  
2.  En la página **asignación** , seleccione **archivo de Excel** como **origen de datos**.  
  
3.  Haga clic en **examinar**, asegúrese de que filtro está establecido en **libro de Excel**y seleccione archivo **. xls de lista de proveedores limpiados** que exportó después de realizar la actividad de limpieza.  
  
    > [!NOTE]  
    >  Al final de esta actividad, no puede exportar los resultados porque esta actividad se centra principalmente en la definición de una directiva de coincidencia. En la próxima lección creará un proyecto de calidad de datos para la actividad de coincidencia y lo ejecutará para quitar duplicados de la lista de proveedores usando esta directiva de coincidencia.  
  
4.  Asigne la columna **SupplierID** al dominio **ID. de proveedor** , la columna **nombre de proveedor** al dominio nombre de **proveedor** , la columna **ContactEmailAddress** al dominio **correo electrónico de contacto** . Solo necesita asignar columnas de origen a los dominios que desee usar en la definición de la directiva de coincidencia. En este caso, está haciendo que los dominios Id. de proveedor, Nombre de proveedor y Correo electrónico de contacto estén disponibles para la actividad de directiva de coincidencia.  
  
     ![Asignar página de Proceso de definición de la directiva de coincidencia](../../2014/tutorials/media/et-definingamatchingpolicy-02.jpg "Asignar página de Proceso de definición de la directiva de coincidencia")  
  
5.  Haga clic en **siguiente** para ir a la página **Directiva de coincidencia** , donde definirá una directiva de coincidencia con una regla.  
  
6.  Haga clic en el botón **crear una regla de coincidencia** en la barra de herramientas para crear una regla en la Directiva.  
  
     ![Botón de la barra de herramientas Crear una regla de coincidencia](../../2014/tutorials/media/et-definingamatchingpolicy-03.jpg "Botón de la barra de herramientas Crear una regla de coincidencia")  
  
7.  En el panel Detalles de la **regla** de la derecha, escriba **quitar proveedores duplicados** para el nombre de la **regla**.  
  
8.  Haga clic en **Agregar un nuevo elemento de dominio** en la barra de herramientas del panel derecho.  
  
     ![Detalles de la regla - Botón Agregar un nuevo elemento de dominio](../../2014/tutorials/media/et-definingamatchingpolicy-04.jpg "Detalles de la regla - Botón Agregar un nuevo elemento de dominio")  
  
9. Seleccione **ID** . de proveedor para el **dominio** y active la casilla **requisito previo** . Observe que la **similitud** se establece automáticamente en **Exact**. Al establecer el **identificador de proveedor** como **requisito previo**, se especifica que los valores de este campo en los dos registros deben devolver una coincidencia del 100%; de lo contrario, los registros no se consideran una coincidencia y las demás cláusulas de la regla no se tienen en cuenta.  
  
     ![Eliminar la definición de regla de proveedores duplicados](../../2014/tutorials/media/et-definingamatchingpolicy-05.jpg "Eliminar la definición de regla de proveedores duplicados")  
  
10. Haga clic de nuevo en **Agregar un nuevo elemento de dominio** de la barra de herramientas.  
  
11. Seleccione **proveedor nombre** dominio, seleccione **similar** para **similitud**y escriba **70** para el **peso**.  Aquí, está especificando que los nombres de proveedor no deben ser idénticos, sino que pueden ser similares, para que los registros se consideren una coincidencia. La ponderación indica la contribución de la puntuación de este campo a la puntuación de coincidencia total.  
  
12. Repita los dos pasos anteriores para agregar el dominio de **correo electrónico de contacto** con **30** para el **peso**.  
  
13. Observe que la **puntuación de coincidencia mínima** está establecida en **80%**, que es el valor que se ve en la pestaña **General** de la página **configuración** de **Administración de DQS**. Solo puede aumentar esta puntuación por encima de este valor de umbral aquí.  
  
14. Observe que la opción **clústeres superpuestos** está seleccionada. Con esta opción, un registro puede aparecer en varios clústeres. Si cambia el valor a Clústeres no superpuestos, los clústeres que tienen registros comunes se combinan en un único clúster.  
  
15. El botón **Inicio** de esta página le permite probar cada regla de la Directiva por separado, mientras que el botón iniciar de la página siguiente le permite probar toda la Directiva (todas las reglas de la Directiva).  
  
16. Haga clic en **siguiente** para cambiar a la página **resultados de búsqueda de coincidencias** .  
  
## <a name="next-step"></a>siguiente paso  
 [Tarea 2: Prueba y publicación de la directiva de coincidencia](../../2014/tutorials/task-2-testing-and-publishing-the-matching-policy.md)  
  
  
