---
title: Seleccionar y configurar los objetos a prueba (SybaseToSQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Tester Component,Parameter Comparision Setting
- Tester Component,Selecting Objects
ms.assetid: 89c23aad-bfee-4917-bc16-175288390ac0
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3ee6efee5172d5261c5f8fa5e23507b9bb2b931b
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2018
---
# <a name="selecting-and-configuring-objects-to-test-sybasetosql"></a>Seleccionar y configurar los objetos a prueba (SybaseToSQL)
En este paso se seleccionan objetos para probar y configurar las opciones de comparación de funciones y procedimientos parámetros de salida, así como los valores devueltos de funciones.  
  
## <a name="selection-of-objects-to-test"></a>Selección de objetos a prueba  
En el árbol de objetos de Sybase situado en el lado izquierdo de la ventana, compruebe los objetos que desea invocar durante el proceso de prueba. Ver la lista completa de objetos pueden someterse a prueba en el [probar los objetos migrados de la base de datos &#40;SybaseToSQL&#41; ](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md) tema.  
  
Si el evaluador de SSMA no admite cualquiera de los objetos seleccionados para las pruebas, verá el vínculo con la etiqueta **algunos objetos seleccionados contienen errores** bajo el árbol de objetos. Haga clic en este vínculo para ver los motivos por qué no se pueden probar estos objetos y anule la selección de objetos incorrectos.  
  
Puede ver varias páginas en el lado derecho del **SQL** página muestra la definición del objeto actual. En el **Pre SQL** y **Post SQL** páginas pueden especificar scripts que se ejecutan antes y después de la invocación de objeto se prueba inicia. Se trata de puede ser útil cuando el objeto requiere objeto adicionales como tablas temporales o los cursores. El **parámetros** página enumera los parámetros si el objeto es un procedimiento almacenado o una función. El **propiedades** página muestra las características adicionales del objeto. Vea la descripción de **parámetros Comparsions** y **llamar a valores** páginas siguientes.  
  
## <a name="parameter-comparison-settings"></a>Configuración de la comparación de parámetro  
Establecer las reglas de comparación para los parámetros output y devolver valores en el **comparar parámetros** página. Puede realizar las siguientes opciones.  
  
### <a name="use-during-comparisons"></a>Uso durante las comparaciones  
Habilitar el uso del parámetro seleccionado en la comparación de resultados de pruebas.  
  
-   Si elige **True**, SSMA comparará el valor de salida de este parámetro después de ejecutar el procedimiento de Sybase con el valor correspondiente en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]  
  
-   Si elige**False**, el parámetro se excluirá de la comprobación de resultados.  
  
### <a name="use-custom-scale"></a>Usar escala personalizada  
Para los parámetros de tipo de datos numérico de longitud fija y aproximada, puede establecer una escala personalizada para la comparación.  
  
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
Puede especificar valores de parámetro de entrada en el **llamar a valores** página. El **agregar llamada** botón agrega una nueva llamada con valores de parámetros vacía. El **quitar llamar** botón quita la llamada actual.  
  
## <a name="next-step"></a>Paso siguiente  
[Seleccionar y configurar los objetos afectados &#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-affected-objects-sybasetosql.md)  
  
## <a name="see-also"></a>Vea también  
[Pruebas de objetos de base de datos migran &#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
