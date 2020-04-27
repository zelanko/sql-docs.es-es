---
title: 'Tarea 2: probar y publicar la Directiva de coincidencia | Microsoft Docs'
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: e1ffb6d7-fbc5-4695-b538-cc2302d1a17d
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: a9957625e09bde8bb733eca6e564dfdcfbb0bd98
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "65484736"
---
# <a name="task-2-testing-and-publishing-the-matching-policy"></a>Tarea 2: Prueba y publicación de la directiva de coincidencia
  En esta tarea, probará y publicará la Directiva de coincidencia **quitar proveedores duplicados** .  
  
1.  En la página **resultados de búsqueda de coincidencias** , haga clic en **iniciar** para probar toda la Directiva. En su caso, solo tiene una regla en la directiva, por lo que los resultados de probar la regla y la directiva deben ser iguales.  
  
2.  Examine todos los registros coincidentes y su puntuación de coincidencia en el cuadro de lista. Un registro que tiene un icono **verde** asociado es un duplicado del registro dinámico que lo precede. He aquí un par de ejemplos:  
  
    1.  El registro con **ID. de registro: 1000005** es una coincidencia del registro con el **ID. de registro: 1000004** con **puntuación: 100%** porque ambos registros tienen los mismos valores para **las columnas** **IdProveedor (requisito previo)**, **nombre de proveedor**y ContactEmailAddress. DQS elige aleatoriamente un registro como registro dinámico para un clúster.  
  
    2.  El registro **1000023** es una coincidencia del registro **1000022** con la puntuación de coincidencia: 93% porque los dos registros tienen los mismos valores para las columnas **IdProveedor (requisito previo)** y **nombre de proveedor** , pero distintos valores para la columna **ContactEmailAddress** .  
  
    3.  Desplácese a la parte inferior de la lista para ver dos registros con los ID. de registro: **1000051** y **1000052**. El registro **1000052** se considera una coincidencia con la puntuación de coincidencia **91%** porque los dos registros tienen los mismos valores para las columnas **SupplierID** y **ContactEmailAddress** , pero con valores distintos para la columna **Supplier Name** .  
  
     ![Definición de directiva - Resultados de directiva](../../2014/tutorials/media/et-testingandpublishingthematchingpolicy-01.jpg "Definición de directiva - Resultados de directiva")  
  
3.  Haga clic con el botón derecho en cualquier registro coincidente (con el icono verde) y haga clic en **Ver detalles** para ver más detalles sobre la coincidencia, como la contribución de cada puntuación de campo a la puntuación de coincidencia total.  
  
     ![Cuadro de diálogo Detalles de puntuación de coincidencia](../../2014/tutorials/media/et-testingandpublishingthematchingpolicy-02.jpg "Cuadro de diálogo Detalles de puntuación de coincidencia")  
  
4.  Haga clic en **cerrar** para cerrar el cuadro de diálogo **detalles de puntuación de coincidencia** .  
  
5.  Haga clic en la pestaña **resultados de búsqueda de coincidencias** en la parte inferior de la página. Esta pestaña proporciona detalles como el número de registros coincidentes, el número de registros no coincidentes, el número de clústeres con registros coincidentes, el tamaño promedio de clúster, el tamaño mínimo de clúster y el tamaño máximo de clúster. Vea [crear una directiva de coincidencia](https://msdn.microsoft.com/library/hh270290.aspx) para obtener más detalles. No puede exportar los resultados de esta actividad. Simplemente está definiendo una directiva de coincidencia usando datos de ejemplo para probar reglas y la directiva con los datos de ejemplo.  
  
     ![Pestaña resultados de búsqueda de coincidencias](../../2014/tutorials/media/et-testingandpublishingthematchingpolicy-03.jpg "Pestaña Resultados de búsqueda de coincidencias")  
  
6.  Haga clic en **Finalizar** para terminar de crear la Directiva de coincidencia.  
  
    > [!NOTE]  
    >  Ha definido la directiva de coincidencia aquí; por tanto, no puede exportar los resultados a un archivo de salida. Básicamente ha usado un archivo de entrada de ejemplo, ha creado reglas, y ha probado las reglas y la directiva con los datos de ejemplo con el objetivo de definir la directiva.  
  
7.  En el cuadro de diálogo SQL Server Data Quality Services, haga clic en **publicar** y en **Aceptar** en el cuadro de mensaje. Ahora, la Directiva de coincidencia que definió está publicada en la base de conocimiento **proveedores** . Puede usar la base de conocimiento para ejecutar el proceso de búsqueda de coincidencias en un archivo de entrada para identificar y quitar duplicados.  
  
## <a name="next-step"></a>siguiente paso  
 [Tarea 3: Creación y ejecución de un proyecto de calidad de datos para buscar coincidencias](../../2014/tutorials/task-3-creating-and-running-a-data-quality-project-for-matching.md)  
  
  
