---
title: Selección y configuración de objetos de prueba (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Selection of Objects to Test,Parameter Comparison Settings
ms.assetid: 29fb6542-5c1f-4b14-a822-87700beb7623
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: d568d1749cd54796072a108e438e448bf2a74578
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47705184"
---
# <a name="selecting-and-configuring-objects-to-test-oracletosql"></a>Selección y configuración de objetos de prueba (OracleToSQL)
En este paso, se seleccionan objetos para probar y configurar las opciones de comparación procedimientos y los funciones de parámetros de salida, así como los valores devueltos de funciones.  
  
## <a name="selection-of-objects-to-test"></a>Selección de objetos de prueba  
En el árbol de objetos de Oracle que se encuentran en el lado izquierdo de la ventana, compruebe los objetos que desea invocar durante el proceso de pruebas. Ver la lista completa de objetos puede probar en el [pruebas migrar objetos de base de datos &#40;OracleToSQL&#41; ](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md) tema.  
  
Si el evaluador de SSMA no es compatible con cualquiera de los objetos seleccionados para las pruebas, verá el vínculo con la etiqueta **algunos objetos seleccionados contienen errores** bajo el árbol de objetos. Haga clic en este vínculo para ver los motivos por qué no se puede probar estos objetos y anule la selección de objetos incorrectos.  
  
En el lado derecho puede ver varias páginas del **SQL** página muestra la definición del objeto actual. El **parámetros** página enumera los parámetros si el objeto es un procedimiento almacenado o una función. El **propiedades** página muestra características adicionales del objeto. Vea la descripción de **parámetro comparaciones** y **llamar a valores** las páginas siguientes.  
  
## <a name="parameter-comparison-settings"></a>Configuración de la comparación de parámetros  
Establecer las reglas de comparación para los parámetros output y devolver valores en el **parámetro comparaciones** página. Puede realizar las siguientes opciones.  
  
### <a name="use-during-test-comparisons"></a>Uso durante las comparaciones de pruebas  
Habilitar el uso del parámetro seleccionado en la comparación de los resultados de pruebas.  
  
-   Si elige **True**, SSMA comparará el valor de salida de este parámetro después de ejecutar el procedimiento en Oracle con el valor correspondiente en SQL Server.
  
-   Si elige**False**, el parámetro se excluirán de la comprobación de los resultados.  
  
### <a name="use-custom-scale"></a>Usar escala personalizada  
Para los parámetros de tipo de datos numérico, puede establecer una escala personalizada para la comparación.  
  
-   Si elige **True**, se debe redondear valores numéricos según la **comparar escala** valor antes de compararse.  
  
-   Si elige**False**, la comparación numérica serán exacta.  
  
### <a name="comparing-scale"></a>Comparación de escala  
Sólo está disponible si el **Use Custom Scale** opción está establecida en **True**. Se trata de la precisión de comparación numérica.  
  
### <a name="date-time-comparing"></a>Comparación de fecha hora  
Define cómo de fecha y hora se comparan los valores.  
  
-   Si selecciona **comparar todo fecha**, se realizará una comparación completa de los valores de ambas plataformas.  
  
-   Si selecciona **comparar solo fecha**, la hora se omitirá parte.  
  
-   Si selecciona **comparar tiempo solo**, la fecha se omitirá parte.  
  
-   Si selecciona **omitir milisegundos**, los resultados se compararán hasta segundos.  
  
-   Si selecciona **Omitir fecha y milisegundos**, el resultado será comparadas sólo por parte de hora y omitir partes fraccionarias de segundo.  
  
### <a name="ignore-strings-case"></a>Omitir mayúsculas y minúsculas de cadenas  
Controla las mayúsculas y minúsculas de la comparación.  
  
-   Si elige **True**, la comparación será entre mayúsculas y minúsculas.  
  
-   Si elige **False**, la comparación será distingue mayúsculas de minúsculas.  
  
### <a name="ignore-trailing-spaces"></a>Omitir espacios finales  
Controla los espacios finales de cómo se tratan durante la comparación.  
  
-   Si elige **True**, las cadenas comparadas será recortes derecha antes de comparar.  
  
-   Si elige **False**, las cadenas comparadas conservará espacios en blanco finales.  
  
## <a name="specify-input-values-for-procedures-and-functions-call-values"></a>Especifique los valores de entrada para procedimientos y funciones (llamar a valores)  
Puede especificar valores de parámetro de entrada en el **llamar a valores** página. El **agregar llamada** botón agrega una nueva llamada con los valores de parámetros vacía. El **quitar llamadas** botón quita la llamada actual.  
  
## <a name="next-step"></a>Paso siguiente  
[Selección y configuración de los objetos afectados &#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-affected-objects-oracletosql.md)  
  
## <a name="see-also"></a>Vea también  
[Pruebas con objetos de base de datos migrados &#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
