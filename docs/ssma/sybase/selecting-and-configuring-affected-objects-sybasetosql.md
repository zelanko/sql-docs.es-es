---
title: Seleccionar y configurar objetos afectados (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Tester Component,Affected Objects
ms.assetid: a219df74-543a-4aec-aeeb-79f90ac3e2ee
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 48d5305854d214e61036e00ca23a94b85313138a
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2018
ms.locfileid: "52402269"
---
# <a name="selecting-and-configuring-affected-objects-sybasetosql"></a>Selección y configuración de objetos afectados (SybaseToSQL)
En esta página puede seleccionar tablas y claves externas, los cambios en el que se deben comparar cuando SSMA comprueba los resultados de ejecución para los objetos que haya elegido en el paso anterior. Además, puede personalizar los parámetros de comprobación.  
  
## <a name="selection-of-affected-objects"></a>Selección de objetos afectados  
En el árbol de objetos de Sybase ubicado en el lado izquierdo de la ventana, compruebe las tablas y claves externas, los cambios en el que se deben comparar por ser idénticos.  
  
Si no se puede comprobar el evaluador de SSMA cualquiera de estos objetos, verá el vínculo con la etiqueta **algunos objetos seleccionados contienen errores** bajo el árbol de objetos. Haga clic en este vínculo para ver los motivos por qué no se puede comparar estos objetos y anule la selección de objetos incorrectos.  
  
## <a name="table"></a>Table  
La pestaña de la tabla contiene la vista de cuadrícula de la tabla seleccionada. La cuadrícula contiene la siguiente información acerca de la tabla seleccionada:  
  
-   Nombre de la columna  
  
-   Tipo de datos  
  
-   Precisión  
  
-   Escala  
  
-   Regla  
  
-   Default  
  
-   identidad  
  
-   Admisión de valores NULL  
  
## <a name="sql"></a>SQL  
Pestaña SQL contiene la tabla"crear" SQL de la tabla seleccionada.  
  
## <a name="data"></a>Datos  
Pestaña de datos muestra los datos presentes en la tabla seleccionada.  
  
## <a name="properties"></a>Propiedades  
Ficha de propiedades muestra las propiedades de la tabla seleccionada. Los campos siguientes están presentes en la pestaña Propiedades:  
  
-   Creación o última modificación  
  
-   Nombre de objeto  
  
## <a name="table-comparison-settings"></a>Configuración de tabla de comparación  
Establecer las reglas de comparación para la tabla en **comparaciones de tablas** página. Puede realizar las siguientes opciones.  
  
### <a name="comparison-mode"></a>Modo de comparación  
Define el contenido de la tabla en que será realiza la comparación.  
  
-   Si selecciona **solo cambios**, se realizará una comparación completa de las filas de tabla.  
  
-   Si selecciona **completa**, se realizará la comparación solo para las filas que se han cambiado.  
  
## <a name="column-comparison-settings"></a>Configuración de la comparación de columna  
Establecer las reglas de comparación para las columnas de tabla en **columna comparaciones** página. Puede realizar las siguientes opciones.  
  
### <a name="use-during-test-comparisons"></a>Uso durante las comparaciones de pruebas  
Determinar si esta columna participará en la comprobación de los resultados de pruebas.  
  
-   Si elige **True**, SSMA comparará el contenido de esta columna después de ejecutar la prueba de Sybase con el contenido de la columna de SQL Server.
  
-   Si elige **False**, la columna se excluirán de la comprobación de los resultados.  
  
### <a name="use-custom-scale"></a>Usar escala personalizada  
Para las columnas de tipo de datos numérico, puede establecer una escala personalizada para la comparación.  
  
-   Si elige **True**, se debe redondear valores numéricos según la **comparar escala** valor antes de compararse.  
  
-   Si elige **False**, la comparación numérica serán exacta.  
  
### <a name="comparing-scale"></a>Comparación de escala  
  
-   Sólo está disponible si el **Use Custom Scale** opción está establecida en **True**. Se trata de la precisión de comparación numérica.  
  
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
  
-   Si elige **False**, la comparación se encargará de mayúsculas y minúsculas.  
  
## <a name="comparing-sql"></a>Comparación de SQL  
Puede ver las instrucciones SELECT generadas por el evaluador de SSMA en el **SQL Compare** página. La herramienta de comprobación comparará los conjuntos de resultados de estas instrucciones según una fila por fila. Cada fila siguiente de un conjunto de resultados de Sybase debe ser igual a la siguiente fila del conjunto de resultados generado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Puede editar las instrucciones SELECT para proporcionar verificación personalizados. Para guardar los cambios en Sybase y en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instrucciones, utilice el **aplicar** botones en el origen y destino SQL, según corresponda.  
  
## <a name="next-step"></a>Paso siguiente  
[Personalización del orden de las llamadas &#40;SybaseToSQL&#41;](../../ssma/sybase/customizing-calls-order-sybasetosql.md)  
  
## <a name="see-also"></a>Vea también  
[Ejecutar casos de prueba &#40;SybaseToSQL&#41;](../../ssma/sybase/running-test-cases-sybasetosql.md)  
[Pruebas con objetos de base de datos migrados &#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
