---
title: Selección y configuración de objetos de prueba (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
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
ms.openlocfilehash: 09103b9294754a7634a1d28109f3129286acae94
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/14/2018
ms.locfileid: "40392810"
---
# <a name="selecting-and-configuring-objects-to-test-sybasetosql"></a>Selección y configuración de objetos de prueba (SybaseToSQL)
En este paso, se seleccionan objetos para probar y configurar las opciones de comparación procedimientos y los funciones de parámetros de salida, así como los valores devueltos de funciones.  
  
## <a name="selection-of-objects-to-test"></a>Selección de objetos de prueba  
En el árbol de objetos de Sybase ubicado en el lado izquierdo de la ventana, compruebe los objetos que desea invocar durante el proceso de pruebas. Ver la lista completa de objetos puede probar en el [pruebas migrar objetos de base de datos &#40;SybaseToSQL&#41; ](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md) tema.  
  
Si el evaluador de SSMA no es compatible con cualquiera de los objetos seleccionados para las pruebas, verá el vínculo con la etiqueta **algunos objetos seleccionados contienen errores** bajo el árbol de objetos. Haga clic en este vínculo para ver los motivos por qué no se puede probar estos objetos y anule la selección de objetos incorrectos.  
  
En el lado derecho puede ver varias páginas del **SQL** página muestra la definición del objeto actual. En el **Pre SQL** y **Post SQL** páginas pueden especificar scripts que se ejecutan antes y después de la invocación de guías de objeto de prueba. Se trata de puede ser útil cuando el objeto requiere objetos adicionales, como tablas temporales o los cursores. El **parámetros** página enumera los parámetros si el objeto es un procedimiento almacenado o una función. El **propiedades** página muestra características adicionales del objeto. Vea la descripción de **parámetros Comparsions** y **llamar a valores** las páginas siguientes.  
  
## <a name="parameter-comparison-settings"></a>Configuración de la comparación de parámetros  
Establecer las reglas de comparación para los parámetros output y devolver valores en el **comparar parámetros** página. Puede realizar las siguientes opciones.  
  
### <a name="use-during-comparisons"></a>Uso durante las comparaciones  
Habilitar el uso del parámetro seleccionado en la comparación de los resultados de pruebas.  
  
-   Si elige **True**, SSMA comparará el valor de salida de este parámetro después de ejecutar el procedimiento de Sybase con el valor correspondiente en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Si elige**False**, el parámetro se excluirán de la comprobación de los resultados.  
  
### <a name="use-custom-scale"></a>Usar escala personalizada  
Para los parámetros de tipo de datos numérico de longitud fija y aproximada, puede establecer una escala personalizada para la comparación.  
  
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
Puede especificar valores de parámetro de entrada en el **llamar a valores** página. El **agregar llamada** botón agrega una nueva llamada con los valores de parámetros vacía. El **quitar llamar** botón quita la llamada actual.  
  
## <a name="next-step"></a>Paso siguiente  
[Selección y configuración de los objetos afectados &#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-affected-objects-sybasetosql.md)  
  
## <a name="see-also"></a>Vea también  
[Pruebas con objetos de base de datos migrados &#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
