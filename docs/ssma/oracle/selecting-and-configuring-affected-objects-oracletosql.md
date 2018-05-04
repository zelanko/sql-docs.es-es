---
title: Seleccionar y configurar afectados objetos (OracleToSQL) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-oracle
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Columns Comparison Settings
- Selection of Affected Objects
ms.assetid: 545eeda2-9829-4187-a858-619a96b4b71d
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 238db38f3dbb3497dc88f870edf96e8d36c00a9f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="selecting-and-configuring-affected-objects-oracletosql"></a>Seleccionar y configurar afectados objetos (OracleToSQL)
En esta página puede seleccionar tablas y claves externas, cambios en el que se deben comparar SSMA comprueba los resultados de ejecución para los objetos que haya elegido en el paso anterior. Además, puede personalizar los parámetros de comprobación.  
  
## <a name="selection-of-affected-objects"></a>Selección de objetos afectados  
En el árbol de objetos de Oracle situado en el lado izquierdo de la ventana, compruebe las tablas y las claves externas, cambios en el que se deben comparar para ser idénticos.  
  
Si no se puede comprobar el evaluador de SSMA cualquiera de estos objetos, verá el vínculo con la etiqueta **algunos objetos seleccionados contienen errores** bajo el árbol de objetos. Haga clic en este vínculo para ver los motivos por qué no se pueden comparar estos objetos y anule la selección de objetos incorrectos.  
  
## <a name="table"></a>Table  
La pestaña de la tabla contiene la vista de cuadrícula de la tabla seleccionada. La cuadrícula contiene la siguiente información acerca de la tabla seleccionada:  
  
-   Nombre de la columna  
  
-   Tipo de datos  
  
-   Precisión  
  
-   Escala  
  
-   Regla  
  
-   Predeterminado  
  
-   Identidad  
  
-   Admisión de valores NULL  
  
## <a name="sql"></a>SQL  
Pestaña SQL contiene la "crear una tabla" SQL de la tabla seleccionada.  
  
## <a name="data"></a>data  
Ficha de datos muestra los datos presentes en la tabla seleccionada.  
  
## <a name="properties"></a>Propiedades  
Ficha de propiedades muestra las propiedades de la tabla seleccionada. Los campos siguientes están presentes en la ficha Propiedades:  
  
-   Creó o modificó por última vez  
  
-   Nombre de objeto  
  
## <a name="columns-comparison-settings"></a>Configuración de la comparación de columnas  
Establecer las reglas de comparación para las columnas de tabla en **comparación de las columnas** página. Puede realizar las siguientes opciones.  
  
### <a name="use-during-test-comparisons"></a>Uso durante las comparaciones de pruebas  
Determine si esta columna participará en la comprobación de resultados de la prueba.  
  
-   Si elige **True**, SSMA comparará el contenido de esta columna después de ejecutar la prueba en Oracle con el contenido de la columna en SQL Server. 
  
-   Si elige**False**, la columna se excluirá de la comprobación de resultados.  
  
### <a name="use-custom-scale"></a>Usar escala personalizada  
Para las columnas de tipo de datos numérico, puede establecer una escala personalizada para la comparación.  
  
-   Si elige **True**, se debe redondear valores numéricos según la **comparar escala** valor antes de compararse.  
  
-   Si elige**False**, la comparación numérica serán exacta.  
  
### <a name="comparing-scale"></a>Comparación de escala  
  
-   Sólo está disponible si la **Use Custom Scale** opción está establecida en **True**. Se trata de la precisión de comparación numérica.  
  
### <a name="date-time-comparing"></a>Comparación de fecha hora  
Define la fecha y hora se comparan valores.  
  
-   Si selecciona **comparar todo fecha**, se realizará la comparación completa de los valores de ambas plataformas.  
  
-   Si selecciona **comparar solo fecha**, la hora parte se pasará por alto.  
  
-   Si selecciona **comparar solo hora**, la fecha en la parte se pasará por alto.  
  
-   Si selecciona **milisegundos omitir**, los resultados se compararán hasta segundos.  
  
-   Si selecciona **Omitir fecha y milisegundos**, el resultado será comparados sólo por parte de hora y omitir partes fraccionarias de segundo.  
  
### <a name="ignore-strings-case"></a>Omitir mayúsculas y minúsculas cadenas  
Controla la distinción entre mayúsculas y de la comparación.  
  
-   Si elige **True**, la comparación será entre mayúsculas y minúsculas.  
  
-   Si elige **False**, la comparación tendrá en cuenta mayúsculas y minúsculas.  
  
## <a name="comparing-sql"></a>Comparación de SQL  
Puede ver las instrucciones SELECT generadas por el evaluador de SSMA en el **comparar SQL** página. El evaluador comparará los conjuntos de resultados de estas instrucciones en la fila por fila. Cada fila siguiente de un conjunto de resultados de Oracle debe ser igual a la siguiente fila del conjunto de resultados generado en SQL Server.
  
Puede editar las instrucciones SELECT para proporcionar comprobación personalizada. Para guardar los cambios en Oracle y en las instrucciones de SQL Server, use la **aplicar** botones en el origen y destino SQL, según corresponda.  
  
## <a name="next-step"></a>Paso siguiente  
[Personalizar el orden de las llamadas &#40;OracleToSQL&#41;](../../ssma/oracle/customizing-calls-order-oracletosql.md)  
  
## <a name="see-also"></a>Vea también  
[Finalizar la preparación del caso de prueba &#40;OracleToSQL&#41;](../../ssma/oracle/finishing-test-case-preparation-oracletosql.md)  
[Ejecutar casos de prueba &#40;OracleToSQL&#41;](../../ssma/oracle/running-test-cases-oracletosql.md)  
[Pruebas de objetos de base de datos migran &#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
