---
title: Seleccionar y configurar los objetos a prueba (OracleToSQL) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Selection of Objects to Test,Parameter Comparison Settings
ms.assetid: 29fb6542-5c1f-4b14-a822-87700beb7623
caps.latest.revision: "8"
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: d33e430c5ecb7957e3886bf05c4fdb9d30b7614a
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="selecting-and-configuring-objects-to-test-oracletosql"></a>Seleccionar y configurar los objetos a prueba (OracleToSQL)
En este paso se seleccionan objetos para probar y configurar las opciones de comparación de funciones y procedimientos parámetros de salida, así como los valores devueltos de funciones.  
  
## <a name="selection-of-objects-to-test"></a>Selección de objetos a prueba  
En el árbol de objetos de Oracle situado en el lado izquierdo de la ventana, compruebe los objetos que desea invocar durante el proceso de prueba. Ver la lista completa de objetos pueden someterse a prueba en el [pruebas migrar objetos de base de datos &#40; OracleToSQL &#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md) tema.  
  
Si el evaluador de SSMA no admite cualquiera de los objetos seleccionados para las pruebas, verá el vínculo con la etiqueta **algunos objetos seleccionados contienen errores** bajo el árbol de objetos. Haga clic en este vínculo para ver los motivos por qué no se pueden probar estos objetos y anule la selección de objetos incorrectos.  
  
Puede ver varias páginas en el lado derecho del **SQL** página muestra la definición del objeto actual. El **parámetros** página enumera los parámetros si el objeto es un procedimiento almacenado o una función. El **propiedades** página muestra las características adicionales del objeto. Vea la descripción de **parámetro comparaciones** y **llamar a valores** páginas siguientes.  
  
## <a name="parameter-comparison-settings"></a>Configuración de la comparación de parámetro  
Establecer las reglas de comparación para los parámetros output y devolver valores en el **parámetro comparaciones** página. Puede realizar las siguientes opciones.  
  
### <a name="use-during-test-comparisons"></a>Uso durante las comparaciones de pruebas  
Habilitar el uso del parámetro seleccionado en la comparación de resultados de pruebas.  
  
-   Si elige **True**, SSMA comparará el valor de salida de este parámetro después de ejecutar el procedimiento en Oracle con el valor correspondiente en SQL Server.
  
-   Si elige**False**, el parámetro se excluirá de la comprobación de resultados.  
  
### <a name="use-custom-scale"></a>Usar escala personalizada  
Para los parámetros de tipo de datos numérico, puede establecer una escala personalizada para la comparación.  
  
-   Si elige **True**, se debe redondear valores numéricos según la **comparar escala** valor antes de compararse.  
  
-   Si elige**False**, la comparación numérica serán exacta.  
  
### <a name="comparing-scale"></a>Comparación de escala  
Sólo está disponible si la **Use Custom Scale** opción está establecida en **True**. Se trata de la precisión de comparación numérica.  
  
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
  
-   Si elige **False**, la comparación será entre mayúsculas y minúsculas.  
  
### <a name="ignore-trailing-spaces"></a>Omitir espacios finales  
Controla cómo espacios se tratan durante la comparación.  
  
-   Si elige **True**, las cadenas comparadas será recortan derecha antes de comparar.  
  
-   Si elige **False**, las cadenas comparadas conservará espacios en blanco finales.  
  
## <a name="specify-input-values-for-procedures-and-functions-call-values"></a>Especificar valores de entrada para los procedimientos y funciones (valores de llamadas)  
Puede especificar valores de parámetro de entrada en el **llamar a valores** página. El **agregar llamada** botón agrega una nueva llamada con valores de parámetros vacía. El **quitar llamadas** botón quita la llamada actual.  
  
## <a name="next-step"></a>Paso siguiente  
[Seleccionar y configurar afectados objetos &#40; OracleToSQL &#41;](../../ssma/oracle/selecting-and-configuring-affected-objects-oracletosql.md)  
  
## <a name="see-also"></a>Vea también  
[Pruebas migran objetos de base de datos &#40; OracleToSQL &#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
