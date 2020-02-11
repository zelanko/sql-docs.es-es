---
title: Editor de consultas MDX (Analysis Services-datos multidimensionales) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.startpage.mdx.f1
helpviewer_keywords:
- Query Editor [MDX]
- MDX Query Editor
ms.assetid: 777f2c23-1c1c-4b72-9d19-48a4866551f8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 579af162998ffaa7c9483a6e6d29a87f98e96fac
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66077879"
---
# <a name="mdx-query-editor-analysis-services---multidimensional-data"></a>Editor de consultas MDX (Analysis Services - Datos multidimensionales)
  Use el Editor de consultas MDX para diseñar y ejecutar instrucciones y scripts escritos en lenguaje de expresiones multidimensionales (MDX).  
  
## <a name="features"></a>Características  
  
-   Escriba los scripts en el panel del editor de consultas del Editor de consultas MDX.  
  
-   Para ejecutar scripts, presione **F5**o haga clic en **Ejecutar** en la barra de herramientas, o haga clic en **Ejecutar** en el menú **Consulta**. Si se selecciona un fragmento del código, solamente se ejecutará dicho fragmento. Si no se selecciona ningún código, se ejecutará todo el contenido del Editor de consultas MDX.  
  
-   Vea los metadatos para cubos y otros objetos contenidos en una base de datos [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] en el panel de metadatos.  
  
-   Para obtener ayuda sobre la sintaxis de MDX, seleccione una palabra clave en el Editor de consultas MDX y haga clic en **F1**.  
  
-   Para obtener ayuda dinámica sobre la sintaxis de MDX, en el menú **Ayuda** haga clic en **Ayuda dinámica**para abrir el componente Ayuda dinámica. En Ayuda dinámica, los temas de ayuda se muestran en la ventana **Ayuda dinámica** al escribir las palabras clave en el Editor de consultas.  
  
## <a name="sql-server-analysis-services-editors-toolbar"></a>Barra de herramientas Editores de SQL Server Analysis Services  
 Al abrir el Editor de consultas MDX, se mostrará la barra de herramientas de los editores de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] con los botones que se incluyen en la siguiente tabla.  
  
|Término|Definición|  
|----------|----------------|  
|**Conectar**|Abre el cuadro de diálogo **Conectar a servidor** para establecer una conexión a una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .|  
|**Conecto**|Desconecta el Editor de consultas MDX de una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .|  
|**Cambiar conexión**|Abre el cuadro de diálogo **Conectar a servidor** para establecer una conexión a una instancia distinta de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .|  
|**Nueva consulta con conexión actual**|Abre una nueva ventana del Editor de consultas MDX y usa la información de conexión de la ventana actual del Editor de consultas MDX.|  
|**Bases de datos disponibles**|Cambie la conexión a una base de datos distinta de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] en la misma instancia.|  
|**Ejecut**|Ejecuta el código seleccionado y, si no se ha seleccionado ningún código, ejecuta todo el código del Editor de consultas MDX.|  
|**Analizar**|Comprueba la sintaxis del código seleccionado. Si no se selecciona ningún código, comprueba la sintaxis de toda la ventana del Editor de consultas MDX.|  
|**Cancelar la ejecución de la consulta**|Envía una solicitud de cancelación al servidor. Algunas consultas no pueden cancelarse inmediatamente, sino que deben esperar a una condición de cancelación adecuada. Al cancelar las consultas, podrían producirse retrasos mientras se revierten las transacciones.|  
  
## <a name="mdx-query-editor-window"></a>Ventana Editor de consultas MDX  
 Las opciones incluidas en la siguiente tabla están disponibles en el Editor de consultas MDX.  
  
|Término|Definición|  
|----------|----------------|  
|**Ventana del editor de consultas**|Escriba las instrucciones y scripts MDX que debe ejecutar el Editor de consultas MDX.<br /><br /> El menú contextual del editor de consultas proporciona las siguientes opciones:<br /><br /> **Cortar**: copia la selección actual en el portapapeles y quita la selección de la ventana del editor de consultas.<br /><br /> **Copiar**: copia la selección actual en el portapapeles.<br /><br /> **Pegar**: pega el contenido del portapapeles en la selección actual.<br /><br /> **Conectar**: abre el cuadro de diálogo **conectar con el servidor** para establecer una conexión a [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] una instancia de.<br /><br /> **Desconectar**: desconecta el editor de consultas actual de una [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] instancia de.<br /><br /> **Desconectar todas las consultas**: desconecta todos los editores de consultas abiertos actualmente.<br /><br /> **Cambiar conexión**: abre el cuadro de diálogo **conectar con el servidor** para establecer una conexión a una [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] instancia diferente.<br /><br /> **Abrir servidor en explorador de objetos**: abre la [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] instancia de a la que está conectado el editor de consultas actual en **Explorador de objetos**.<br /><br /> **Ejecutar**: ejecuta el código seleccionado o, si no se selecciona ningún código, ejecuta todo el código en el editor de consultas actual.<br /><br /> **Ventana Propiedades**: muestra la ventana **propiedades** de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para la ventana de consulta actual.<br /><br /> **Opciones de consulta**: muestra el cuadro de diálogo **Opciones de consulta** .|  
|**Ventana Metadatos**|Muestra los metadatos para la base de datos conectada de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .|  
|**BD**|Seleccione un cubo en la base de datos conectada de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] para mostrar los metadatos asociados al cubo en la pestaña **Metadatos** .|  
|**Metadatos**|Muestra los metadatos para el cubo seleccionado en **Cubo**, incluidos los grupos de medida y las medidas, los indicadores clave de rendimiento, las dimensiones, las jerarquías, los niveles, los miembros y las propiedades de los miembros. Para recuperar la clave completa de un objeto:<br /><br /> Arrastre el objeto desde la pestaña **Metadatos** hasta el panel de consultas.<br /><br /> Haga clic con el botón derecho en el objeto y seleccione **Copiar** y, después, haga clic con el botón derecho en el panel de consultas y seleccione **Pegar**.|  
|**Funciones**|Muestra los metadatos para las funciones MDX disponibles para la base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], una vez recuperados del conjunto de filas de esquema MDSCHEMA_FUNCTIONS. Para recuperar la sintaxis de una función:<br /><br /> Arrastre el objeto desde la pestaña **Funciones** hasta el panel de consultas.<br /><br /> Haga clic con el botón derecho en la función y seleccione **Copiar** y, luego, haga clic con el botón derecho en el panel de consultas y seleccione **Pegar**.|  
|**Ventana Resultados**|Muestra los resultados de una instrucción o script MDX en una cuadrícula.|  
|**Ventana Mensajes**|Muestra información sobre cómo ejecutar una instrucción o script MDX. Por ejemplo, esta ventana muestra todos los errores encontrados durante la ejecución o el número de celdas recuperadas tras la ejecución.|  
  
  
