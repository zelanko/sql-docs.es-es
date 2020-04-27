---
title: 'Opciones (editor de texto: pestaña Editor y página barra de estado) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.sqleditors.editorcontextsettings
- VS.ToolsOptionsPages.Text_Editor.EditorTabAndStatusBar
ms.assetid: e4815678-7885-4631-878f-c6a2b857ee05
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 01098f2181085f17788429608afb7bdda15fb504
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66089240"
---
# <a name="options-text-editor-editor-tab-and-status-bar-page"></a>Opciones (Editor de texto: pestaña Editor y página de la barra de estado)
  La **página Barra de estado y pestaña de editor** permite personalizar la información mostrada por los editores de consultas de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] . Puede especificar el nivel de información que se muestra en la pestaña y en la barra de estado de la ventana del editor de consultas y si la barra de estado debe aparecer en la parte superior o inferior de la ventana del editor.  
  
## <a name="option-settings-by-editor"></a>Configuración de las opciones de editor  
 La pestaña del editor y la barra de estado están disponibles en todos los editores de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] , pero tienen distintos niveles de funcionalidad.  
  
 El editor de consultas del motor de base de datos puede conectarse a un grupo de servidores, en cuyo caso abre las conexiones a todas las instancias del grupo de servidores y puede ejecutar simultáneamente la misma consulta en cada conexión. Puede usar este cuadro de diálogo para especificar que la barra de estado tiene diferentes colores cuando se conecta con varias instancias en lugar de una instancia. Para cambiar las opciones de resultados de varios servidores, use la página [Opciones (Resultados de la consulta/SQL Server/Multiservidor)](../../2014/database-engine/options-query-results-sql-server-multi-server.md) .  
  
## <a name="status-bar-content"></a>Contenido de la barra de estado  
 Especifica la información que aparece en la barra de estado del Editor de consultas.  
  
 **Mostrar tiempo de ejecución**  
 Incluye la hora de ejecución del script. La configuración es la siguiente:  
  
 **None**  
 La barra de estado no muestra ninguna información horaria.  
  
 **Extremo**  
 La barra de estado muestra la hora actual del día mientras se ejecuta el script. Cuando se completa el script, la pantalla muestra la hora del día a la que se ha completado el script.  
  
 **Transcurrido**  
 La barra de estado muestra la cantidad de tiempo que el script ha estado en ejecución. Cuando se completa el script, la pantalla muestra el tiempo que ha llevado ejecutarse el script.  
  
 **Incluir nombre de base de datos**  
 Incluye el nombre de la base de datos actual para la conexión. Cuando se abre el editor de consultas por primera vez, esta es la base de datos predeterminada del inicio de sesión. El contexto de la base de datos se puede cambiar posteriormente mediante la instrucción USE de Transact-SQL.  
  
 **Incluir nombre de inicio de sesión**  
 Incluye el nombre de inicio de sesión.  
  
 **Incluir recuento de filas**  
 Incluye un recuento de las filas procesadas por el script que se está ejecutando actualmente.  
  
 **Incluir nombre de servidor**  
 Incluye el nombre del servidor. Para las conexiones locales, es el nombre de instancia. Para las conexiones remotas, es el nombre del equipo remoto y el nombre de instancia.  
  
## <a name="status-bar-layout-and-colors"></a>Diseño de la barra de estado y colores  
 Especifica los colores de los elementos de la barra de estado del Editor de consultas.  
  
 **Conexiones de grupo**  
 Establezca el color de la barra de estado cuando el Editor de consultas tenga más de una conexión.  
  
 **Conexiones de servidor único**  
 Establezca el color de la barra de estado cuando el Editor de consultas tenga una conexión.  
  
 **Ubicación de la barra de estado**  
 Especifica la ubicación de la barra de estado. La configuración es la siguiente:  
  
 **Arriba**  
 La barra de estado aparece en la parte superior de la ventana del Editor de consultas.  
  
 **Descendente**  
 La barra de estado aparece en la parte inferior de la ventana del Editor de consultas.  
  
## <a name="tab-text"></a>Texto de pestaña  
 Especifica el texto que aparece en la pestaña en la parte superior de una ventana del Editor de consultas. Si el texto es demasiado largo para mostrarse, puede ver la cadena completa en una información sobre herramientas que se muestra si mantiene el mouse sobre la pestaña.  
  
 **Incluir nombre de base de datos**  
 Incluye el nombre de la base de datos actual para la conexión. Cuando se abre el editor de consultas por primera vez, esta es la base de datos predeterminada del inicio de sesión. El contexto de la base de datos se puede cambiar posteriormente mediante la instrucción USE de Transact-SQL.  
  
 **Incluir nombre de archivo**  
 Incluye el nombre del archivo donde se almacena el script.  
  
 **Incluir carpeta**  
 Incluye la ruta de acceso donde se almacena el archivo de script.  
  
 **Incluir nombre de inicio de sesión**  
 Incluye el nombre de inicio de sesión.  
  
 **Incluir nombre de servidor**  
 Incluye el nombre del servidor. Para las conexiones locales, es el nombre de instancia. Para las conexiones remotas, es el nombre del equipo remoto y el nombre de instancia.  
  
## <a name="see-also"></a>Consulte también  
 [Opciones &#40;entorno: página fuentes y colores&#41;](../ssms/menu-help/options-environment-fonts-and-colors-page.md)   
 [Codificación de colores en el Editor de consultas](../relational-databases/scripting/color-coding-in-query-editors.md)  
  
  
