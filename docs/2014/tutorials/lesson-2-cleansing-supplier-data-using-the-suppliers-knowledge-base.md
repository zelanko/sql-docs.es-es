---
title: 'Lección 2: limpiar datos de proveedor mediante la base de conocimiento proveedores | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 215c14de-fc3f-46de-a022-bf69b9ea2a96
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 3186cbac127244131f45e2cbe7e3131b2e6d4895
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85063983"
---
# <a name="lesson-2-cleansing-supplier-data-using-the-suppliers-knowledge-base"></a>Lección 2: Limpieza de datos de proveedor con la base de conocimiento Proveedores
  En esta lección, limpiará los datos de proveedor en un archivo de Excel con la base de conocimiento **proveedores** que creó en la primera lección. La limpieza de datos en DQS incluye un **proceso asistido por PC** que analiza cómo se ajustan los datos a la información de una base de conocimiento y un **proceso interactivo** que permite revisar y modificar los resultados del proceso asistido por PC. La característica de limpieza de datos identifica los datos incorrectos en el origen de datos y después corrige o sugiere correcciones a los datos incorrectos. También normaliza y enriquece los datos de cliente usando valores de dominio, valores iniciales de sinónimos, reglas de dominio, relaciones basadas en términos y datos de referencia. Puede aprobar o rechazar interactivamente los cambios propuestos por el proceso asistido por PC. Vea [limpieza de datos](https://msdn.microsoft.com/library/gg524800.aspx) para obtener más detalles.  
  
 El proceso asistido por PC emplea los valores de umbral siguientes que puede configurar mediante la opción Configuración de la página principal del Cliente DQS.  
  
-   **Puntuación mínima para sugerencias:** Puntuación mínima o nivel de confianza que utiliza DQS para sugerir el reemplazo de un valor.  
  
-   **Puntuación mínima para las correcciones automáticas:** Puntuación mínima o nivel de confianza que utiliza DQS para corregir automáticamente un valor.  
  
 Vea [configurar los valores de umbral para la limpieza y la búsqueda de coincidencias](https://msdn.microsoft.com/library/hh510415.aspx) para obtener más información sobre cómo configurar estas opciones.  
  
 En esta lección, realizará las tareas siguientes para limpiar los datos de entrada mediante la base de conocimiento Proveedores.  
  
1.  Crear un proyecto de calidad de datos para la limpieza, seleccionar la base de conocimiento Proveedores como base de conocimiento que se usará para analizar y limpiar los datos de origen en un archivo de Excel, y seleccionar la actividad Limpieza.  
  
2.  Asignar las columnas de Excel que desea limpiar a los dominios de DQS o dominios compuestos adecuados de la base de conocimiento.  
  
3.  Ejecutar la actividad de limpieza asistida por PC. El proceso asistido por PC muestra información sobre la calidad de los datos en el Cliente de calidad de los datos que puede usar para limpiar los datos de forma interactiva.  
  
4.  Ver y administrar los resultados de la actividad Limpieza. Puede examinar los valores que el proceso asistido por PC dice que son correctos, incorrectos pero corregidos, incorrectos con un cambio sugerido o no válidos. Puede aprobar o rechazar interactivamente los cambios, corrigiendo o invalidando la sugerencia del proceso asistido por PC mediante el campo Corregir a.  
  
5.  Exportar los resultados del proceso de limpieza a un archivo de Excel.  
  
6.  Importe los valores del proyecto de limpieza a los dominios para aumentar el conocimiento de la base de conocimiento con nuevas reglas, valores, correcciones, etc.  
  
## <a name="next-step"></a>siguiente paso  
 [Tarea 1: Creación de un proyecto de calidad de datos](../../2014/tutorials/task-1-creating-a-data-quality-project.md)  
  
  
