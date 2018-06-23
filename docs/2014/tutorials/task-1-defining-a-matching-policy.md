---
title: 'Tarea 1: Definir una directiva de coincidencia | Documentos de Microsoft'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6f89a720-fce5-4f60-bef3-a159bbc9f25c
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 0b0ccf6217899b5368cf27f93951e0a7ddc0cf48
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36111926"
---
# <a name="task-1-defining-a-matching-policy"></a>Tarea 1: definir una directiva de coincidencia
  En esta tarea, creará una directiva de coincidencia que contiene una regla. La regla tendrá un requisito previo: **Id. de proveedor**, lo que significa que debe coincidir con los identificadores de proveedor antes de utilizar los demás dominios de la regla. La regla usa otros dos dominios: **Supplier Name** con **similitud** valor establecido en **70%** y **correo electrónico de contacto** con  **Similitud** valor establecido en **30%**.  
  
1.  En la página principal de **cliente DQS**, haga clic en **flecha derecha** junto a **proveedores** knowledge base y, a continuación, seleccione **directiva de coincidencia**.  
  
     ![Menú principal de directiva de coincidencia página](../../2014/tutorials/media/et-definingamatchingpolicy-01.jpg "menú principal de directiva de coincidencia página")  
  
2.  En el **mapa** página, seleccione **archivo de Excel** para **origen de datos**.  
  
3.  Haga clic en **examinar**, asegúrese de que el filtro se establece en **libro de Excel**y seleccione **Cleansed Supplier List.xls** que exportó cuando realizó la actividad de limpieza de archivos.  
  
    > [!NOTE]  
    >  Al final de esta actividad, no puede exportar los resultados porque esta actividad se centra principalmente en la definición de una directiva de coincidencia. En la próxima lección creará un proyecto de calidad de datos para la actividad de coincidencia y lo ejecutará para quitar duplicados de la lista de proveedores usando esta directiva de coincidencia.  
  
4.  Mapa **SupplierID** columna **Id. de proveedor** dominio, **Supplier Name** columna **Supplier Name** dominio,  **ContactEmailAddress** columna **correo electrónico de contacto** dominio. Solo necesita asignar columnas de origen a los dominios que desee usar en la definición de la directiva de coincidencia. En este caso, está haciendo que los dominios Id. de proveedor, Nombre de proveedor y Correo electrónico de contacto estén disponibles para la actividad de directiva de coincidencia.  
  
     ![Asignar la página del proceso de definición de directiva de coincidencia](../../2014/tutorials/media/et-definingamatchingpolicy-02.jpg "asignar la página del proceso de definición de directiva de coincidencia")  
  
5.  Haga clic en **siguiente** para mover a la **directiva de coincidencia** página donde definirá una directiva con una regla de coincidencia en ella.  
  
6.  Haga clic en **crear una regla de coincidencia** botón en la barra de herramientas para crear una regla en la directiva.  
  
     ![Crear un botón de barra de herramientas de regla coincidente](../../2014/tutorials/media/et-definingamatchingpolicy-03.jpg "crear un botón de barra de herramientas de regla coincidente")  
  
7.  En el **detalles de la regla** panel de la derecha, escriba **quitar proveedores duplicados** para el **nombre de la regla**.  
  
8.  Haga clic en **agregar un nuevo elemento de dominio** en la barra de herramientas en el panel derecho.  
  
     ![Regla detalles - agregar un nuevo botón de elemento de dominio](../../2014/tutorials/media/et-definingamatchingpolicy-04.jpg "regla detalles - agregar un nuevo botón de elemento de dominio")  
  
9. Seleccione **Id. de proveedor** para el **dominio** y seleccione la **requisitos previos** casilla de verificación. Tenga en cuenta que **similitud** se establece automáticamente en **Exact**. Estableciendo **Id. de proveedor** como el **requisitos previos**, puede especificar que los valores para este campo en los dos registros deben devolver una coincidencia del 100%, los registros de lo contrario no se consideran una coincidencia y las demás cláusulas de la regla no se devuelven.  
  
     ![Quitar la definición de la regla de proveedores duplicados](../../2014/tutorials/media/et-definingamatchingpolicy-05.jpg "quitar la definición de la regla de proveedores duplicados")  
  
10. Haga clic en **agregar un nuevo elemento de dominio** de nuevo la barra de herramientas.  
  
11. Seleccione **Supplier Name** dominio, seleccione **Similar** para **similitud**y el tipo de **70** para el **peso**.  Aquí, está especificando que los nombres de proveedor no deben ser idénticos, sino que pueden ser similares, para que los registros se consideren una coincidencia. La ponderación indica la contribución de esta puntuación del campo a la puntuación de coincidencia total.  
  
12. Repita los dos pasos anteriores para agregar **correo electrónico de contacto** dominio con **30** para el **peso**.  
  
13. Tenga en cuenta que la **min puntuación de coincidencia** está establecido en **80%**, que es el valor que aparece en el **General** pestaña de la **configuración** página de **Administración de DQS**. Solo puede aumentar esta puntuación por encima de este valor de umbral aquí.  
  
14. Tenga en cuenta que **clústeres superpuestos** opción está seleccionada. Con esta opción, un registro puede aparecer en varios clústeres. Si cambia el valor a Clústeres no superpuestos, los clústeres que tienen registros comunes se combinan en un único clúster.  
  
15. El **iniciar** botón en esta página le permite probar cada regla en la directiva por separado, mientras que el botón de inicio en la página siguiente permite probar toda directiva (todas las reglas de la directiva).  
  
16. Haga clic en **siguiente** para cambiar a la **resultados de búsqueda de coincidencias** página.  
  
## <a name="next-step"></a>Paso siguiente  
 [Tarea 2: Probar y publicar la directiva de coincidencia](../../2014/tutorials/task-2-testing-and-publishing-the-matching-policy.md)  
  
  