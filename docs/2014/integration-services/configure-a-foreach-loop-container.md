---
title: Configurar un contenedor de bucles Foreach | Documentos de Microsoft
ms.custom: ''
ms.date: 08/22/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Foreach Loop containers
- containers [Integration Services], Foreach Loop
ms.assetid: 519c6f96-5e1f-47d2-b96a-d49946948c25
caps.latest.revision: 36
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 75c118a7d135788e4bd1c320c7f8d4b32482a31b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36200186"
---
# <a name="configure-a-foreach-loop-container"></a>Configurar un contenedor de bucles Foreach
  Este procedimiento describe cómo configurar un contenedor de bucles Foreach, incluyendo expresiones de propiedad en los niveles de enumerador y contenedor.  
  
### <a name="to-configure-the-foreach-loop-container"></a>Para configurar el contenedor de bucles Foreach  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  Haga clic en la pestaña **Flujo de control** y haga doble clic en el bucle Foreach.  
  
3.  En el cuadro de diálogo **Editor de bucles Foreach** , haga clic en **General** y, opcionalmente, modifique el nombre y descripción del bucle Foreach.  
  
4.  Haga clic en **Colección** y seleccione un tipo de enumerador de la lista **Enumerador** .  
  
5.  Especifique un enumerador y establezca las opciones del enumerador de la manera siguiente:  
  
    -   Para usar el enumerador de archivos para Foreach, proporcione la carpeta que contiene los archivos que se deben enumerar, especifique un filtro para el nombre y tipo de archivo, y especifique si es necesario devolver el nombre de archivo completo. Además, indique si se deben recorrer las subcarpetas para obtener más archivos.  
  
    -   Para usar el enumerador de elementos para Foreach, haga clic en **Columnas**y, en el cuadro de diálogo **Columnas For Each Item** , haga clic en **Agregar** para agregar columnas. Seleccione un tipo de datos de la lista **Tipo de datos** para cada columna y haga clic en **Aceptar**.  
  
         Escriba valores en las columnas o seleccione valores de las listas.  
  
        > [!NOTE]  
        >  Para agregar una nueva fila, haga clic en cualquier punto fuera de la celda en la que escribió.  
  
        > [!NOTE]  
        >  Si un valor no es compatible con el tipo de datos de la columna, el texto se resalta.  
  
    -   Para usar el enumerador Foreach ADO, seleccione una variable existente o haga clic en **Nueva variable** en la lista **Variable de origen de objeto ADO** para especificar la variable que contiene el nombre del objeto ADO que se debe enumerar, y seleccione una opción de modo de enumeración.  
  
         Si se crea una nueva variable, establezca las propiedades de la variable en el cuadro de diálogo **Agregar variable** .  
  
    -   Para usar el Enumerador de conjunto de filas del esquema para Foreach de ADO.NET, seleccione una conexión ADO.NET existente o haga clic en **Nueva conexión** en la lista **Conexión** y luego seleccione un esquema.  
  
         Si lo desea, haga clic en **Establecer restricciones** y seleccione las restricciones de esquemas, seleccione la variable que contenga el valor de restricción o escriba el valor de restricción, y haga clic en **Aceptar**.  
  
    -   Para usar el Enumerador de variable para Foreach, seleccione una variable en la lista **Variable** .  
  
    -   Para usar el enumerador NodeList para Foreach, haga clic en DocumentSourceType, seleccione el tipo de origen de la lista y, después, haga clic en DocumentSource. Según el valor seleccionado para DocumentSourceType, seleccione una variable o una conexión de archivo de la lista, cree una variable o una conexión de archivo, o bien escriba el origen XML en el **Editor de origen del documento**.  
  
         Después, haga clic en EnumerationType y seleccione el tipo de enumeración de la lista. Si EnumerationType es **Navigator, Node o NodeText**, haga clic en OuterXPathStringSourceType, seleccione el tipo de origen y, después, haga clic en OuterXPathString. Según el valor establecido para OuterXPathStringSourceType, seleccione una variable o una conexión de archivo de la lista, cree una variable o una conexión de archivo, o bien escriba la cadena de la expresión XPath (lenguaje de rutas XML) externa.  
  
         Si EnumerationType es **ElementCollection**, establezca OuterXPathStringSourceType y OuterXPathString como se ha descrito anteriormente. Después, haga clic en InnerElementType, seleccione un tipo de enumeración para los elementos internos y, después, haga clic en InnerXPathStringSourceType. Según el valor establecido para InnerXPathStringSourceType, seleccione una variable o conexión de archivo, cree una variable o una conexión de archivo, o bien escriba la cadena para la expresión XPath interna.  
  
    -   Para usar el Enumerador de SMO para Foreach, seleccione una conexión ADO.NET existente o haga clic en **Nueva conexión** en la lista **Conexión** y luego escriba la cadena que se debe usar o haga clic en **Examinar**. Si hace clic en **Examinar**, en el cuadro de diálogo **Seleccionar enumeración de SMO** , seleccione el tipo de objeto que se debe enumerar y el tipo de enumeración, y haga clic en **Aceptar**.  
  
6.  De manera opcional, haga clic en el botón Examinar ( **…** ) en el cuadro de texto **Expresiones** de la página **Colección** para crear expresiones que actualicen valores de propiedades. Para más información, vea [Agregar o cambiar una expresión de propiedad](expressions/add-or-change-a-property-expression.md).  
  
    > [!NOTE]  
    >  Las propiedades de la lista **Propiedad** varían según el enumerador.  
  
7.  Opcionalmente, haga clic en **Asignaciones de variables** para asignar propiedades de objetos al valor de la colección y luego haga lo siguiente:  
  
    1.  En la lista **Variables**, seleccione una variable o haga clic en **\<Nueva variable>** para crear una.  
  
    2.  Si agrega una nueva variable, establezca las propiedades de la variable en el cuadro de diálogo **Agregar variable** y haga clic en **Aceptar**.  
  
    3.  Si usa el enumerador Foreach Item, puede actualizar el valor de índice en la lista **Índice** .  
  
        > [!NOTE]  
        >  El valor de índice indica cuál es la columna en el elemento que se debe asignar a la variable. Solo el enumerador Foreach Item puede usar un valor de índice que no sea 0.  
  
8.  Opcionalmente, haga clic en **Expresiones** y, en la página **Expresiones** , cree expresiones de propiedades para las propiedades del contenedor de bucles Foreach. Para más información, vea [Agregar o cambiar una expresión de propiedad](expressions/add-or-change-a-property-expression.md).  
  
9. Haga clic en **Aceptar**.  
  
## <a name="see-also"></a>Vea también  
 [Contenedor de bucles ForEach](control-flow/foreach-loop-container.md)  
  
  