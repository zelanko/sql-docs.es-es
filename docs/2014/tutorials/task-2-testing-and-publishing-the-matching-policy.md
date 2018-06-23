---
title: 'Tarea 2: Probar y publicar la directiva de coincidencia | Documentos de Microsoft'
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e1ffb6d7-fbc5-4695-b538-cc2302d1a17d
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 8f67535e5ad4969983b06fcb710c1dfce1d97cb4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36199482"
---
# <a name="task-2-testing-and-publishing-the-matching-policy"></a>Tarea 2: probar y publicar la directiva de coincidencia
  En esta tarea, probará y publicará el **quitar proveedores duplicados** directiva de coincidencia.  
  
1.  En el **resultados de búsqueda de coincidencias** página, haga clic en **iniciar** para probar toda la directiva. En su caso, solo tiene una regla en la directiva, por lo que los resultados de probar la regla y la directiva deben ser iguales.  
  
2.  Examine todos los registros coincidentes y su puntuación de coincidencia en el cuadro de lista. Un registro que tiene un **verde** icono asociado a ella es un duplicado del registro dinámico que lo precede. He aquí un par de ejemplos:  
  
    1.  El registro con **Id. de registro: 1000005** es una coincidencia del registro con **Id. de registro: 1000004** con **puntuación: 100%** porque ambos registros tienen los mismos valores para **SupplierID (requisito previo)**, **Supplier Name**, y **ContactEmailAddress columnas**. DQS elige aleatoriamente un registro como registro dinámico para un clúster.  
  
    2.  El registro **1000023** es una coincidencia del registro **1000022** con la puntuación de coincidencia: 93% porque los dos registros tienen los mismos valores para **SupplierID (requisito previo)** y  **Nombre de proveedor** columnas, pero valores diferentes para la **ContactEmailAddress** columna.  
  
    3.  Desplácese hasta la parte inferior de la lista para ver dos registros cuyos identificadores: **1000051** y **1000052**. Registro **1000052** se considera una coincidencia con la puntuación de coincidencia **91%** porque los dos registros tienen los mismos valores para la **SupplierID** y  **ContactEmailAddress** columnas, pero valores diferentes para la **Supplier Name** columna.  
  
     ![Definición de directiva - resultados de directivas de](../../2014/tutorials/media/et-testingandpublishingthematchingpolicy-01.jpg "definición de directiva - resultados de la directiva")  
  
3.  Haga doble clic en cualquier registro coincidente (con el icono verde) y haga clic en **ver detalles** para ver más detalles acerca de la coincidencia como la contribución de cada puntuación de campo a la puntuación de coincidencia total.  
  
     ![Cuadro de diálogo de detalles de puntuación de coincidencia](../../2014/tutorials/media/et-testingandpublishingthematchingpolicy-02.jpg "cuadro de diálogo de detalles de puntuación de coincidencia")  
  
4.  Haga clic en **cerrar** para cerrar el **detalles de puntuación de coincidencia** cuadro de diálogo.  
  
5.  Haga clic en **resultados de búsqueda de coincidencias** ficha en la parte inferior de la página. Esta pestaña proporciona detalles como el número de registros coincidentes, el número de registros no coincidentes, el número de clústeres con registros coincidentes, el tamaño promedio de clúster, el tamaño mínimo de clúster y el tamaño máximo de clúster. Vea [crear una directiva de coincidencia](http://msdn.microsoft.com/library/hh270290.aspx) para obtener más detalles. No puede exportar los resultados de esta actividad. Simplemente está definiendo una directiva de coincidencia usando datos de ejemplo para probar reglas y la directiva con los datos de ejemplo.  
  
     ![Pestaña de resultados de búsqueda de coincidencias](../../2014/tutorials/media/et-testingandpublishingthematchingpolicy-03.jpg "pestaña de resultados de búsqueda de coincidencias")  
  
6.  Haga clic en **finalizar** para terminar de crear la directiva de coincidencia.  
  
    > [!NOTE]  
    >  Ha definido la directiva de coincidencia aquí; por tanto, no puede exportar los resultados a un archivo de salida. Básicamente ha usado un archivo de entrada de ejemplo, ha creado reglas, y ha probado las reglas y la directiva con los datos de ejemplo con el objetivo de definir la directiva.  
  
7.  En el cuadro de diálogo Servicios de calidad de datos de SQL Server, haga clic en **publicar** y haga clic en **Aceptar** en el cuadro de mensaje. Ahora, la directiva de coincidencia que definió se publica en el **proveedores** Base de conocimiento. Puede usar la base de conocimiento para ejecutar el proceso de búsqueda de coincidencias en un archivo de entrada para identificar y quitar duplicados.  
  
## <a name="next-step"></a>Paso siguiente  
 [Tarea 3: Crear y ejecutar un proyecto de calidad de datos para buscar coincidencias](../../2014/tutorials/task-3-creating-and-running-a-data-quality-project-for-matching.md)  
  
  