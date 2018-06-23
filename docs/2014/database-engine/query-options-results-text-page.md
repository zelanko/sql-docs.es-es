---
title: Opciones de consulta de resultados (página texto) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.query.text.f1
ms.assetid: fd2fb409-58f9-4ede-8349-ce007126b68d
caps.latest.revision: 15
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 51e1a98f00bc4d33e0609f1b03ceca928bded049
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36201656"
---
# <a name="query-options-results-text-page"></a>Resultados de Opciones de consulta (página Texto)
  Utilice esta página para especificar las opciones para mostrar el conjunto de resultados de una consulta en formato de texto. La configuración de esta página también se aplica cuando está seleccionada la opción **Resultados a archivo** .  
  
 **Formato de salida**  
 De manera predeterminada, la salida se muestra en columnas que se han creado rellenando de espacios los resultados. Otras de las opciones son el uso de comas, tabulaciones o espacios para separar las columnas. Seleccione el cuadro de diálogo **Delimitador personalizado** para especificar un carácter delimitador diferente en el cuadro **Delimitador personalizado** .  
  
 **Delimitador personalizado**  
 Especifique el carácter que desee para separar las columnas. Esta opción solo se encuentra disponible si está seleccionada la casilla **Delimitador personalizado** en el cuadro **Formato de salida** .  
  
 **Incluir encabezados de columna del conjunto de resultados**  
 Desactive esta casilla si no desea que cada columna tenga una etiqueta con un título de columna.  
  
 **Desplazarse a medida que se reciben resultados**  
 Active esta casilla para mantener el foco de visualización en los registros devueltos más recientemente en la parte inferior. Desactive esta casilla para mantener el foco de visualización en las primeras filas recibidas.  
  
 **Alinear los valores numéricos a la derecha**  
 Active esta casilla para alinear los valores numéricos a la derecha de la columna. Esto puede ser de ayuda a la hora de revisar números con un número fijo de posiciones decimales.  
  
 **Descartar resultados tras la ejecución**  
 Si descarta los resultados de la consulta después de que la pantalla los reciba, liberará memoria.  
  
 **Mostrar los resultados en una pestaña independiente**  
 Active esta casilla para mostrar el conjunto de resultados en una nueva ventana de documento, en lugar de en la parte inferior de la ventana de documento de la consulta.  
  
 **Cambiar a la pestaña de resultados tras ejecutar la consulta**  
 Haga clic en esta opción para establecer automáticamente el foco de pantalla en el conjunto de resultados.  
  
 **Número máximo de caracteres mostrados en cada columna**  
 El valor predeterminado es 256. Aumente este valor para poder mostrar conjuntos de resultados mayores sin truncamientos.  
  
 **Restablecer valores predeterminados**  
 Restablece todos los valores de esta página a los valores predeterminados originales.  
  
## <a name="saving-a-text-result-set-with-headers"></a>Guardar un conjunto de resultados de texto con encabezados  
 Para guardar los resultados de la consulta como un archivo de texto con encabezados, seleccione la casilla **Incluir encabezados de columna en el conjunto de resultados** y un formato de salida delimitado. El archivo de informes contendrá encabezados si hace clic en **Resultados a archivo** de la barra de herramientas, o bien si hace clic con el botón derecho en cualquier resultado de la búsqueda, selecciona **Guardar resultados como**, escribe un nombre de archivo y hace clic en **Guardar**.  
  
  