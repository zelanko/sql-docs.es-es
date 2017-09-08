---
title: Seleccionar y configurar afectados objetos (SybaseToSQL) | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Tester Component,Affected Objects
ms.assetid: a219df74-543a-4aec-aeeb-79f90ac3e2ee
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 8e5f4fcb5af81da2b78520542e2b57bd66bc4fd1
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="selecting-and-configuring-affected-objects-sybasetosql"></a>Seleccionar y configurar afectados objetos (SybaseToSQL)
En esta página puede seleccionar tablas y claves externas, cambios en el que se deben comparar SSMA comprueba los resultados de ejecución para los objetos que haya elegido en el paso anterior. Además, puede personalizar los parámetros de comprobación.  
  
## <a name="selection-of-affected-objects"></a>Selección de objetos afectados  
En el árbol de objetos de Sybase situado en el lado izquierdo de la ventana, compruebe las tablas y las claves externas, cambios en el que se deben comparar para ser idénticos.  
  
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
  
## <a name="data"></a>Datos  
Ficha de datos muestra los datos presentes en la tabla seleccionada.  
  
## <a name="properties"></a>Propiedades  
Ficha de propiedades muestra las propiedades de la tabla seleccionada. Los campos siguientes están presentes en la ficha Propiedades:  
  
-   Creó o modificó por última vez  
  
-   Nombre de objeto  
  
## <a name="table-comparison-settings"></a>Configuración de tabla de comparación  
Establecer las reglas de comparación para la tabla en **comparaciones de tablas** página. Puede realizar las siguientes opciones.  
  
### <a name="comparison-mode"></a>Modo de comparación  
Define el contenido de la tabla en que se puede realizar la comparación.  
  
-   Si selecciona **solo cambios**, se realizará una comparación completa de filas de la tabla.  
  
-   Si selecciona **completa**, se realizará la comparación solo para las filas que se han cambiado.  
  
## <a name="column-comparison-settings"></a>Configuración de la comparación de columna  
Establecer las reglas de comparación para las columnas de tabla en **columna comparaciones** página. Puede realizar las siguientes opciones.  
  
### <a name="use-during-test-comparisons"></a>Uso durante las comparaciones de pruebas  
Determine si esta columna participará en la comprobación de resultados de la prueba.  
  
-   Si elige **True**, SSMA comparará el contenido de esta columna después de ejecutar la prueba de Sybase con el contenido de la columna en SQL Server.
  
-   Si elige **False**, la columna se excluirá de la comprobación de resultados.  
  
### <a name="use-custom-scale"></a>Usar escala personalizada  
Para las columnas de tipo de datos numérico, puede establecer una escala personalizada para la comparación.  
  
-   Si elige **True**, se debe redondear valores numéricos según la **comparar escala** valor antes de compararse.  
  
-   Si elige **False**, la comparación numérica serán exacta.  
  
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
Puede ver las instrucciones SELECT generadas por el evaluador de SSMA en el **comparar SQL** página. El evaluador comparará los conjuntos de resultados de estas instrucciones en la fila por fila. Cada fila siguiente de un conjunto de resultados de Sybase debe ser igual a la siguiente fila del conjunto de resultados generado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
Puede editar las instrucciones SELECT para proporcionar comprobación personalizada. Para guardar los cambios de Sybase y en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] instrucciones, use la **aplicar** botones en el origen y destino SQL, según corresponda.  
  
## <a name="next-step"></a>Paso siguiente  
[Personalizar el orden de las llamadas &#40; SybaseToSQL &#41;](../../ssma/sybase/customizing-calls-order-sybasetosql.md)  
  
## <a name="see-also"></a>Vea también  
[Ejecutar casos de prueba &#40; SybaseToSQL &#41;](../../ssma/sybase/running-test-cases-sybasetosql.md)  
[Pruebas migran objetos de base de datos &#40; SybaseToSQL &#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  

