---
title: 'Tarea 2: Probar y publicar la directiva de coincidencia | Microsoft Docs'
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.topic: conceptual
ms.assetid: e1ffb6d7-fbc5-4695-b538-cc2302d1a17d
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 17723cfd2c1c694f21130e985b6bd65736f90236
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/13/2018
ms.locfileid: "53373945"
---
# <a name="task-2-testing-and-publishing-the-matching-policy"></a>Tarea 2: probar y publicar la directiva de coincidencia
  En esta tarea, probará y publicará el **quitar proveedores duplicados** directiva de coincidencia.  
  
1.  En el **resultados coincidentes** página, haga clic en **iniciar** para probar la directiva completa. En su caso, solo tiene una regla en la directiva, por lo que los resultados de probar la regla y la directiva deben ser iguales.  
  
2.  Examine todos los registros coincidentes y su puntuación de coincidencia en el cuadro de lista. Un registro que tiene un **verde** icono asociado a ella es un duplicado del registro dinámico que lo precede. He aquí un par de ejemplos:  
  
    1.  El registro que tiene **Id. de registro: 1000005** es una coincidencia del registro con **Id. de registro: 1000004** con **puntuación: 100%** porque ambos registros tienen los mismos valores para **SupplierID (requisito previo)**, **Supplier Name**, y **ContactEmailAddress columnas**. DQS elige aleatoriamente un registro como registro dinámico para un clúster.  
  
    2.  El registro **1000023** es una coincidencia del registro **1000022** con la puntuación de coincidencia: 93% porque los dos registros tienen los mismos valores para **SupplierID (requisito previo)** y **Supplier Name** columnas, pero valores diferentes para el **ContactEmailAddress** columna.  
  
    3.  Desplácese hasta la parte inferior de la lista para ver dos registros cuyos identificadores son **1000051** y **1000052**. Registro **1000052** se considera una coincidencia con la puntuación de coincidencia **91%** porque los dos registros tienen los mismos valores para el **SupplierID** y  **ContactEmailAddress** columnas, pero valores diferentes para el **Supplier Name** columna.  
  
     ![Definición de directiva - resultados de directivas de](../../2014/tutorials/media/et-testingandpublishingthematchingpolicy-01.jpg "definición de directiva - resultados de directivas")  
  
3.  Haga doble clic en cualquier registro coincidente (con el icono verde) y haga clic en **ver detalles** para ver más detalles acerca de la coincidencia como la contribución de cada puntuación de campo a la puntuación de coincidencia total.  
  
     ![Cuadro de diálogo de detalles de puntuación de coincidencia](../../2014/tutorials/media/et-testingandpublishingthematchingpolicy-02.jpg "cuadro de diálogo de detalles de puntuación de coincidencia")  
  
4.  Haga clic en **cerrar** para cerrar el **detalles de puntuación de coincidencia** cuadro de diálogo.  
  
5.  Haga clic en **resultados coincidentes** ficha en la parte inferior de la página. Esta pestaña proporciona detalles como el número de registros coincidentes, el número de registros no coincidentes, el número de clústeres con registros coincidentes, el tamaño promedio de clúster, el tamaño mínimo de clúster y el tamaño máximo de clúster. Consulte [crear una directiva de coincidencia](https://msdn.microsoft.com/library/hh270290.aspx) para obtener más detalles. No puede exportar los resultados de esta actividad. Simplemente está definiendo una directiva de coincidencia usando datos de ejemplo para probar reglas y la directiva con los datos de ejemplo.  
  
     ![Pestaña de resultados de coincidencia](../../2014/tutorials/media/et-testingandpublishingthematchingpolicy-03.jpg "coincidentes de la pestaña de resultados")  
  
6.  Haga clic en **finalizar** para terminar de crear la directiva de coincidencia.  
  
    > [!NOTE]  
    >  Ha definido la directiva de coincidencia aquí; por tanto, no puede exportar los resultados a un archivo de salida. Básicamente ha usado un archivo de entrada de ejemplo, ha creado reglas, y ha probado las reglas y la directiva con los datos de ejemplo con el objetivo de definir la directiva.  
  
7.  En el cuadro de diálogo de SQL Server Data Quality Services, haga clic en **publicar** y haga clic en **Aceptar** en el cuadro de mensaje. Ahora, se publica la directiva de coincidencia que definió en el **proveedores** Knowledge Base. Puede usar la base de conocimiento para ejecutar el proceso de búsqueda de coincidencias en un archivo de entrada para identificar y quitar duplicados.  
  
## <a name="next-step"></a>Paso siguiente  
 [Tarea 3: Crear y ejecutar un proyecto de calidad de datos para buscar coincidencias](../../2014/tutorials/task-3-creating-and-running-a-data-quality-project-for-matching.md)  
  
  
