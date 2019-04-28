---
title: Editores de consultas y texto (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Query Editor [SQL Server Management Studio]
- Code Editor [SQL Server Management Studio], about Query Editor
- Query Editor [SQL Server Management Studio], full screen mode
- Query Editor [Database Engine], templates
- full screen mode [SQL Server Management Studio]
- SQL Server Management Studio [SQL Server], templates
- writing scripts
- modifying scripts
- SQL Server Management Studio [SQL Server], query editor
- Query Editor [SQL Server Management Studio], about Query Editor
- writing queries
- SQL Server Management Studio [SQL Server], editor
- scripts [SQL Server], SQL Server Management Studio
- queries [SQL Server], SQL Server Management Studio
ms.assetid: 062051e4-4b77-4969-98ae-d2547c24ce3e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e2f2e0f35f1d910e31bd8f3f93201660fca51c0b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62867164"
---
# <a name="query-and-text-editors-sql-server-management-studio"></a>Editores de consultas y texto (SQL Server Management Studio)
  Es posible usar uno de los editores de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para editar y probar de forma interactiva un script [!INCLUDE[tsql](../../includes/tsql-md.md)], MDX, DMX o XML/A o un archivo XML o de texto sin formato. Cada editor depende de un servicio específico del lenguaje que colorea las palabras clave y comprueba si hay errores de sintaxis y de uso. El Editor de consultas de [!INCLUDE[ssDE](../../includes/ssde-md.md)] incluye un depurador de [!INCLUDE[tsql](../../includes/tsql-md.md)] que puede usar para corregir los problemas de código [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
## <a name="sql-server-management-studio-editors"></a>Editores de SQL Server Management Studio  
 Los cuatro editores de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] comparten una arquitectura común. El editor de texto implementa el nivel base de funcionalidad y se puede usar como un editor básico para archivos de texto. Los otros tres editores, o los editores de consultas, amplían esta base de la funcionalidad mediante la inclusión de un servicio de lenguaje que define la sintaxis de uno de los lenguajes admitidos en SQL Server. Los editores de consultas también implementan niveles variables de compatibilidad con las características de editor como IntelliSense y la depuración. Los editores de consultas incluyen el editor de consultas del motor de base de datos para usarlo en la compilación de scripts que contienen instrucciones Transact-SQL y XQuery, el editor MDX del lenguaje MDX, el editor DMX para el lenguaje DMX y el editor XML/A para el lenguaje XML for Analysis.  
  
## <a name="common-components"></a>Componentes comunes  
 Todos los editores de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] comparten estos componentes:  
  
 **Panel de código**  
 Área donde se escriben las consultas o el texto. En los editores de consultas, contiene las características del generador de instrucciones disponibles para el lenguaje. El entorno de edición de texto admite las funciones de buscar y reemplazar, comentarios de forma masiva y fuentes y colores personalizados.  
  
 En el panel de código se pueden establecer opciones que afecten al comportamiento del texto y que estén relacionadas con sangrías aplicadas, tabuladores, arrastrar y colocar texto, etc. Las ventanas de consulta se pueden configurar para que funcionen como pestañas de la ventana de documento, o en documentos independientes.  
  
 **Margen de la selección**  
 Columna de espacio en blanco entre la barra indicadora al margen y el texto del código donde se puede hacer clic para seleccionar líneas de texto. Puede ocultar o mostrar el margen de selección.  
  
 **Barras de desplazamiento horizontal y vertical**  
 Le permiten desplazarse por el panel de código en sentido horizontal y vertical, de forma que pueda ver el código que se extiende más allá de los bordes visibles del panel de código.  
  
 **Numeración de línea**  
 Muestra los números de línea a la izquierda del texto o el código en el editor. Puede navegar a números de línea específicos.  
  
 **Ajuste de línea**  
 Muestra las líneas largas de texto o código como varias líneas, lo que permite ver todo el texto de la línea. El ajuste de línea no afecta al modo en que aparece el texto al ejecutarse o imprimirse. El ajuste de línea se activa desde el cuadro de diálogo **Opciones**, en **Herramientas** , ya sea en la página Editor de texto, Todos los lenguajes, General o en una página específica del editor.  
  
## <a name="code-editor-components"></a>Componentes del editor de código  
 Los editores de código contienen estas características además de las que se comparten con los editores de texto y XML:  
  
 **Resultado**  
 Esta ventana se usa para ver los resultados de una consulta. La ventana puede mostrar los resultados en una cuadrícula o en el texto, o los resultados se pueden dirigir a un archivo. Las cuadrículas de resultados se pueden mostrar como ventanas independientes con pestañas.  
  
 **IntelliSense**  
 En los Editores, en el menú **Editar** , seleccione **IntelliSense**para ver las opciones de [!INCLUDE[msCoName](../../includes/msconame-md.md)] IntelliSense.  
  
 **Código de colores**  
 Muestra diferentes colores para cada tipo de elemento de la sintaxis, lo que mejora la legibilidad de las instrucciones complejas.  
  
 **Esquematización de código**  
 Muestra grupos de código con líneas de esquematización a la izquierda del código. Los grupos de código se pueden contraer y expandir para facilitar la revisión del código.  
  
 **Plantilla**  
 Las plantillas son archivos que incluyen la estructura básica de las instrucciones necesarias para crear objetos en una base de datos. Se pueden usar para agilizar la creación de scripts.  
  
 **Mensajes**  
 Muestra los errores, advertencias y mensajes informativos que devuelve el servidor cuando se ejecuta un script. La lista de mensajes no cambia hasta que se ejecuta el script de nuevo.  
  
 **Barra de estado**  
 Muestra información del sistema asociada a la ventana del Editor de consultas, como a qué instancia está conectado el Editor de consultas.  
  
## <a name="database-engine-query-editor-components"></a>Componentes del editor de consultas del motor de base de datos  
 Estos componentes solo están disponibles en el editor de consultas del motor de base de datos:  
  
 **Depurador**  
 Permite pausar la ejecución de código en instrucciones concretas. A continuación, puede ver datos e información del sistema para facilitar la búsqueda de errores en el código.  
  
 **Lista de errores**  
 Muestra los errores sintácticos y semánticos que encontró IntelliSense. La lista de errores cambia dinámicamente a medida que se modifican los scripts de [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
 **Plan de presentación gráfico de**  
 Muestra los pasos lógicos integrados en el plan de ejecución de una instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
 **Estadísticas de clientes**  
 Muestra información acerca de la ejecución de una consulta agrupada en categorías. Cuando se selecciona **Incluir estadísticas de cliente** en el menú **Consulta** , se muestra una ventana **Estadísticas de clientes** al ejecutarse la consulta. Las estadísticas de ejecuciones de consultas sucesivas se muestran junto con los valores promedio. Seleccione **Restablecer estadísticas de cliente** en el menú **Consulta** para restablecer el promedio.  
  
 **Fragmentos de código**  
 Las plantillas se pueden usar como punto de partida al agregar instrucciones en el editor de consultas del motor de base de datos. Puede insertar los fragmentos de código predefinidos proporcionados con SQL Server o agregar sus propios fragmentos de código.  
  
 **Modo SQLCMD**  
 Ejecuta scripts de [!INCLUDE[tsql](../../includes/tsql-md.md)] que incluyen el conjunto de comandos admitidos por la utilidad sqlcmd. Para obtener más información, vea los [Temas de procedimientos sobre sqlcmd](../../database-engine/sqlcmd-how-to-topics.md).  
  
## <a name="editor-tasks"></a>Tareas del editor  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Describe cómo ver y usar las características básicas del editor de consultas de [!INCLUDE[ssDE](../../includes/ssde-md.md)] .|[Editor de consultas del motor de base de datos &#40;SQL Server Management Studio&#41;](database-engine-query-editor-sql-server-management-studio.md)|  
|Describe cómo ver y usar las características básicas del editor de consultas de MDX.|[Editor de consultas MDX &#40;Analysis Services: datos multidimensionales&#41;](../../analysis-services/mdx-query-editor-analysis-services-multidimensional-data.md)|  
|Describe cómo ver y usar las características básicas del editor de consultas de DMX.|[Editor de consultas DMX &#40;Analysis Services: minería de datos&#41;](../../analysis-services/dmx-query-editor-analysis-services-data-mining.md)|  
|Describe cómo ver y usar las características básicas del editor XML/A.|[Editor XML &#40;SQL Server Management Studio&#41;](xml-editor-sql-server-management-studio.md)|  
|Describe cómo configurar las opciones de los diferentes editores, como la numeración de líneas y las opciones de IntelliSense.|[Configurar editores &#40;SQL Server Management Studio&#41;](configure-editors-sql-server-management-studio.md)|  
|Describe las distintas formas en que puede abrir los editores en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].|[Abrir un editor &#40;SQL Server Management Studio&#41;](open-an-editor-sql-server-management-studio.md)|  
|Describe cómo administrar el modo de vista, como el ajuste de línea, la división de una ventana o las tabulaciones.|[Administrar el editor y el modo de vista](manage-the-editor-and-view-mode.md)|  
|Describe cómo establecer las opciones de formato, como el texto oculto o la sangría aplicada.|[Administrar formato de código](manage-code-formatting.md)|  
|Describe cómo navegar por el texto en una ventana del editor mediante características tales como la búsqueda incremental o el desplazamiento a una determinada parte.|[Navegar por código y texto](navigate-code-and-text.md)|  
|Describe cómo establecer las opciones de codificación de color para los distintos tipos de sintaxis, lo que facilita la lectura de instrucciones complejas.|[Codificación de colores en el Editor de consultas](color-coding-in-query-editors.md)|  
|Describe cómo usar la esquematización de código para ocultar partes de escrituras complejas en las que no se esté trabajando actualmente.|[Esquematización de código](code-outlining.md)|  
|Describe cómo arrastrar el texto desde una ubicación en un script y colocarlo en una nueva ubicación.|[Arrastrar y colocar texto](drag-and-drop-text.md)|  
|Describe cómo realizar una operación de búsqueda y reemplazo global, como, por ejemplo, al cambiar los nombres de columna.|[Buscar y reemplazar](search-and-replace.md)|  
|Describe cómo establecer los marcadores para encontrar más fácilmente fragmentos de código importantes.|[Administrar marcadores](../native-client-ole-db-rowsets/bookmarks.md)|  
|Describe cómo imprimir los scripts o los resultados en una ventana o cuadrícula.|[Imprimir código y resultados](print-code-and-results.md)|  
|Describe cómo usar las características sqlcmd en el editor de consultas de [!INCLUDE[ssDE](../../includes/ssde-md.md)] .|[Modificar scripts SQLCMD con el Editor de consultas](edit-sqlcmd-scripts-with-query-editor.md)|  
|Describe cómo usar las características de IntelliSense, como, por ejemplo, autocompletar nombres de objeto a medida que se escriben, o garantizar que los puntos de interrupción se colocan en ubicaciones válidas.|[IntelliSense &#40;SQL Server Management Studio&#41;](intellisense-sql-server-management-studio.md)|  
|Describe cómo usar los fragmentos de código del editor de consultas de [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Los fragmentos son plantillas para instrucciones o bloques que se usan habitualmente, y se pueden personalizar o ampliar para incluir fragmentos específicos del sitio.|[Fragmentos de código de Transact-SQL](transact-sql-code-snippets.md)|  
|Describe cómo usar el depurador de [!INCLUDE[tsql](../../includes/tsql-md.md)] para recorrer el código y consultar la información de depuración, como los valores de variables y parámetros.|[Depurador de Transact-SQL](transact-sql-debugger.md)|  
|Describe cómo definir colores personalizados para diferentes instancias de [!INCLUDE[ssDE](../../includes/ssde-md.md)]y establecerlos como el fondo de la barra de estado en las ventanas del editor de consultas de [!INCLUDE[ssDE](../../includes/ssde-md.md)] .|[Barra de estado &#40;Editor de consultas del motor de base de datos&#41;](status-bar-database-engine-query-editor.md)|  
  
## <a name="see-also"></a>Vea también  
 [Métodos abreviados de teclado de SQL Server Management Studio](../../ssms/sql-server-management-studio-keyboard-shortcuts.md)  
