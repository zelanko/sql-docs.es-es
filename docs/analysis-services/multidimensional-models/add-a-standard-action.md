---
title: "Agregar una acción estándar | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ccb2928a-f75d-4acb-8ff8-fa80bb0935b2
caps.latest.revision: 7
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8f084616a0dd548fe9ee939f5e770b1f69f125f1
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="add-a-standard-action"></a>Agregar una acción estándar
  Para agregar una acción a una base de datos, use la vista de acciones del Diseñador de cubos. Se puede tener acceso a esta vista desde [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Una vez creada la acción, estará disponible para los usuarios después de volver a procesar el cubo correspondiente. Para más información, consulte [Processing Analysis Services Objects](../../analysis-services/multidimensional-models/processing-analysis-services-objects.md).  
  
### <a name="to-create-an-action"></a>Para crear una acción  
  
1.  Abra el cubo para el que desea crear una acción y, a continuación, haga clic en la pestaña **Acciones** .  
  
2.  En la barra de herramientas, haga clic en el icono **Nueva acción** y, a continuación, en el panel de expresión, haga lo siguiente:  
  
    -   En **Nombre**, escriba un nombre para la acción.  
  
    -   En la lista desplegable **Tipo de destino** , seleccione el tipo de objeto al que quiere adjuntar la acción. El objeto seleccionado en **Tipo de destino** determina los objetos disponibles y el tipo de selección que puede hacer en **Objeto de destino**. En la tabla siguiente se enumeran las selecciones válidas de **Objeto de destino** para cada tipo de destino.  
  
        |Si selecciona el tipo de destino siguiente|Realice la selección siguiente en Objeto de destino|  
        |---------------------------------------------|---------------------------------------------------|  
        |Miembros del atributo|La única selección válida es una sola jerarquía de atributo. El tipo de destino de la acción será todos los miembros del atributo dondequiera que aparezcan (es decir, la acción se aplicará también a las jerarquías definidas por el usuario).|  
        |Celdas|La única selección disponible es Todas las celdas. Si elige **Celdas** como tipo de destino, puede escribir una expresión en **Condición** para restringir las celdas con las que está asociada la acción.|  
        |Cube|La única selección disponible es CURRENTCUBE. La acción está asociada con el cubo actual.|  
        |miembros de dimensión|Seleccione una sola dimensión. La acción se asociará a todos los miembros de la dimensión.|  
        |Jerarquía|Seleccione una sola jerarquía. La acción solo se asociará con el objeto de jerarquía. Las jerarquías de atributo solo aparecen en la lista si sus propiedades **AttributeHierarchyEnabled** y **AttributeHierarchyVisible** se establecen en **True**.|  
        |Miembros de la jerarquía|Seleccione una sola jerarquía. La acción se asociará con todos los miembros de la jerarquía seleccionada. Las jerarquías de atributo solo aparecen en la lista si sus propiedades **AttributeHierarchyEnabled** y **AttributeHierarchyVisible** se establecen en **True**.|  
        |Nivel|Seleccione un solo nivel. La acción solo se asociará con el objeto de nivel.|  
        |Miembros del nivel|Seleccione un solo nivel. La acción se asociará con todos los miembros del nivel seleccionado.|  
  
    -   En **Objeto de destino**, haga clic en la flecha situada a la derecha del cuadro de texto, y en la vista de árbol que aparece, haga clic en el objeto al que desea adjuntar la acción; por último, haga clic en **Aceptar**.  
  
    -   (Opcional) En **Condición**, cree una expresión MDX para limitar el destino de la acción. Puede escribir la expresión manualmente, o puede arrastrar elementos desde las pestañas **Metadatos** y **Funciones** .  
  
    -   En la lista desplegable **Tipo** , seleccione el tipo de acción que quiere crear. En la tabla siguiente se enumeran los tipos de acciones disponibles.  
  
        |Tipo|Description|  
        |----------|-----------------|  
        |Conjunto de datos|Recupera un conjunto de datos.|  
        |Propietario|Ejecuta una operación con una interfaz que no aparece en esta tabla.|  
        |Conjunto de filas|Recupera un conjunto de filas.|  
        |.|Ejecuta un comando OLE DB.|  
        |Dirección URL|Muestra una página web en un explorador de Internet.|  
  
    -   En **Expresión de acción**, cree una expresión que defina la acción. La expresión debe evaluarse como una cadena. Puede escribir la expresión manualmente, o puede arrastrar elementos desde las pestañas **Metadatos** y **Funciones** .  
  
3.  (Opcional) Expanda **Propiedades adicionales**y, a continuación, realice uno de los pasos siguientes:  
  
    -   En la lista desplegable **Invocación**, especifique cómo se invoca la acción. La siguiente tabla describe las opciones disponibles para invocar una acción.  
  
        |Opción|Description|  
        |------------|-----------------|  
        |Interactiva|La acción la desencadena la interacción del usuario.|  
        |Lote|La acción se ejecuta como una operación por lotes.|  
        |Al abrir|La acción se ejecuta cuando un usuario abre el cubo.|  
  
    -   En **Aplicación**, escriba el nombre de la aplicación que está asociada a la acción. Por ejemplo, si crea una acción que transfiere a un usuario a un sitio web determinado, la aplicación asociada a la acción debería ser Microsoft Internet Explorer u otro explorador web.  
  
        > [!NOTE]  
        >  Las acciones de propietario no se devuelven al servidor a menos que la aplicación cliente limite explícitamente el conjunto de filas de esquema para que devuelva únicamente las acciones que coinciden con el nombre especificado en **Aplicación**.  
  
    -   En **Contenido de la acción**, si usa el tipo URL, incluya la dirección de Internet entre comillas; por ejemplo, "http://www.adventure-works.com".  
  
    -   En **Descripción**, escriba una descripción de la acción.  
  
    -   En **Título**, escriba un título o una expresión MDX que se evalúe como un título. Este título se muestra a los usuarios finales una vez iniciada la acción. Si no especifica un título, se usará el nombre de la acción en su lugar.  
  
    -   En la lista desplegable **El título es MDX** , especifique si el título es MDX. Este campo indica al servidor si debe evaluar el contenido de **Título** como una expresión MDX.  
  
  
