---
title: 'Lección 2: Limpieza de datos de proveedor con la Base de conocimiento proveedores | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 215c14de-fc3f-46de-a022-bf69b9ea2a96
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 42006c68a50497034817cfe8df6c9172ea0cdc3b
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56036916"
---
# <a name="lesson-2-cleansing-supplier-data-using-the-suppliers-knowledge-base"></a>Lección 2: limpiar datos de proveedor con la base de conocimiento Proveedores
  En esta lección, limpiar los datos de proveedor en un archivo de Excel mediante el **proveedores** base de conocimiento que ha creado en la primera lección. Limpieza de datos en DQS incluye un **proceso asistido por ordenador** que analiza cómo se ajustan los datos al conocimiento en una base de conocimiento y un **proceso interactivo** que le permite revisar y modificar resultados del proceso asistido por ordenador. La característica de limpieza de datos identifica los datos incorrectos en el origen de datos y después corrige o sugiere correcciones a los datos incorrectos. También normaliza y enriquece los datos de cliente usando valores de dominio, valores iniciales de sinónimos, reglas de dominio, relaciones basadas en términos y datos de referencia. Puede aprobar o rechazar interactivamente los cambios propuestos por el proceso asistido por PC. Consulte [limpieza de datos](https://msdn.microsoft.com/library/gg524800.aspx) para obtener más detalles.  
  
 El proceso asistido por PC emplea los valores de umbral siguientes que puede configurar mediante la opción Configuración de la página principal del Cliente DQS.  
  
-   **Puntuación mínima para sugerencias:** puntuación o nivel de confianza mínimo que DQS emplea para sugerir el reemplazo de un valor.  
  
-   **Puntuación mínima de correcciones automáticas:** puntuación o nivel de confianza mínimo que DQS emplea para corregir automáticamente un valor.  
  
 Consulte [configurar los valores de umbral para la limpieza y coincidencia](https://msdn.microsoft.com/library/hh510415.aspx) para obtener más información sobre cómo configurar estas opciones.  
  
 En esta lección, realizará las tareas siguientes para limpiar los datos de entrada mediante la base de conocimiento Proveedores.  
  
1.  Crear un proyecto de calidad de datos para la limpieza, seleccionar la base de conocimiento Proveedores como base de conocimiento que se usará para analizar y limpiar los datos de origen en un archivo de Excel, y seleccionar la actividad Limpieza.  
  
2.  Asignar las columnas de Excel que desea limpiar a los dominios de DQS o dominios compuestos adecuados de la base de conocimiento.  
  
3.  Ejecutar la actividad de limpieza asistida por PC. El proceso asistido por PC muestra información sobre la calidad de los datos en el Cliente de calidad de los datos que puede usar para limpiar los datos de forma interactiva.  
  
4.  Ver y administrar los resultados de la actividad Limpieza. Puede examinar los valores que el proceso asistido por PC dice que son correctos, incorrectos pero corregidos, incorrectos con un cambio sugerido o no válidos. Puede aprobar o rechazar interactivamente los cambios, corrigiendo o invalidando la sugerencia del proceso asistido por PC mediante el campo Corregir a.  
  
5.  Exportar los resultados del proceso de limpieza a un archivo de Excel.  
  
6.  Importe los valores desde el proyecto de limpieza en dominios para aumentar el conocimiento de la base de conocimiento con nuevas reglas, valores, correcciones etcetera...  
  
## <a name="next-step"></a>Paso siguiente  
 [Tarea 1: Crear un proyecto de calidad de datos](../../2014/tutorials/task-1-creating-a-data-quality-project.md)  
  
  
