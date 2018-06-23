---
title: Opciones (resultados de SQL Server-resultados de la consulta a la página de texto) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- VS.ToolsOptionsPages.QueryResults.SqlServer.SQLResultsToText
ms.assetid: 2ccbdf17-e14f-42f1-a836-ca999a3432c9
caps.latest.revision: 19
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 190d508cc4e1e637d95516a8c9daf148692aa2df
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36113878"
---
# <a name="options-query-results-sql-server-results-to-text-page"></a>Opciones (resultados de SQL Server-resultados de la consulta a la página de texto)
  Utilice esta página para especificar las opciones para mostrar el conjunto de resultados de una consulta en formato de texto. Los cambios que se realicen en estas opciones solo se aplicarán a las nuevas consultas de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para cambiar las opciones de las consultas actuales, haga clic en **Opciones de consulta** en el menú **Consulta** o haga clic con el botón derecho en la ventana Consulta de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y seleccione **Opciones de consulta**. En el cuadro de diálogo **Opciones de consulta** , en **Resultados**, haga clic en **Texto**.  
  
## <a name="uielement-list"></a>Lista de UIElement  
 **Formato de salida**  
 De manera predeterminada, la salida se muestra en columnas que se han creado rellenando de espacios los resultados. Otras de las opciones son el uso de comas, tabulaciones o espacios para separar las columnas. Seleccione **Delimitador personalizado** en esta lista desplegable para especificar un carácter delimitador distinto en el cuadro de texto **Delimitador personalizado**.  
  
 **Delimitador personalizado**  
 Especifique el carácter que desee para separar las columnas. Este cuadro de texto solo estará disponible si se ha hecho clic en Delimitador personalizado en el cuadro de lista desplegable **Formato de salida**.  
  
 **Incluir encabezados de columna del conjunto de resultados**  
 Desactive esta casilla si no desea que cada columna tenga una etiqueta con un título de columna.  
  
 **Incluir la consulta en el conjunto de resultados**  
 Active esta casilla para incluir el texto de la consulta que se ejecuta en el panel de resultados antes de los resultados de la consulta.  
  
 **Desplazarse a medida que se reciben resultados**  
 Active esta casilla para mantener el foco de visualización en los registros devueltos más recientemente al final del conjunto de resultados. Desactive esta casilla para mantener el foco de visualización en las primeras filas recibidas.  
  
 **Alinear los valores numéricos a la derecha**  
 Active esta casilla para alinear los valores numéricos a la derecha de la columna. Esto puede ser de ayuda a la hora de revisar números con un número fijo de posiciones decimales.  
  
 **Descartar resultados tras la ejecución**  
 Active esta casilla para descartar los resultados de la consulta después de que se hayan mostrado en el panel de resultados de la ventana de consulta.  
  
 **Mostrar los resultados en una pestaña independiente**  
 Active esta casilla para mostrar el conjunto de resultados en una nueva ventana de documento, en lugar de en la parte inferior de la ventana de documento de la consulta.  
  
 **Cambiar a la pestaña de resultados tras ejecutar la consulta**  
 Active esta casilla para establecer automáticamente el foco de la pantalla en el conjunto de resultados.  
  
 **Número máximo de caracteres mostrados en cada columna**  
 El valor predeterminado es 256. Aumente este valor para poder mostrar conjuntos de resultados mayores sin truncamientos. El valor máximo es 8,192.  
  
 **Restablecer valores predeterminados**  
 Restablece todos los valores de esta página a los valores predeterminados originales.  
  
  