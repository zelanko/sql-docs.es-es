---
title: Componente de script | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.scriptcomponentdetails.f1
helpviewer_keywords:
- Script transformation
- scripts [Integration Services], transformations
- Script component [Integration Services], about Script component
- Script component [Integration Services]
ms.assetid: 131c2d0c-2e33-4785-94af-ada5c049821e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d9a601a710531aa6905f35a2fe5ca7f02a9177f1
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62770695"
---
# <a name="script-component"></a>Componente de script
  El componente de script hospeda el script y permite a un paquete incluir y ejecutar código personalizado de script. Puede usar el componente de script en paquetes para los siguientes fines:  
  
-   Aplicar varias transformaciones a los datos en lugar de usar varias transformaciones en el flujo de datos. Por ejemplo, un script puede sumar los valores de dos columnas y luego calcular el promedio de la suma.  
  
-   Tener acceso a las reglas de negocios en un ensamblado .NET existente. Por ejemplo, un script puede aplicar una norma empresarial que especifica el intervalo de valores que son válidos en la columna `Income`.  
  
-   Usar fórmulas personalizadas y funciones, además de las funciones y operadores que proporciona la gramática de la expresión [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] . Por ejemplo, validar números de tarjeta de crédito mediante la fórmula LUHN.  
  
-   Validar datos de columna y omitir registros que contienen datos no válidos. Por ejemplo, un script puede evaluar si un valor de franqueo es razonable y omitir registros con valores extremadamente altos o bajos.  
  
 El componente de script proporciona una manera fácil y rápida de incluir funciones personalizadas en un flujo de datos. Sin embargo, si planea reutilizar el código de script en varios paquetes, quizás resulte más conveniente programar un componente personalizado en lugar de usar el componente de script. Para obtener más información, vea [Desarrollar un componente de flujo de datos personalizado](../../extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md).  
  
> [!NOTE]  
>  Si el componente de script contiene un script que intenta leer el valor de una columna que es NULL, se produce un error en el componente de script al ejecutar el paquete. Es recomendable que el script use el método <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer.IsNull%2A> para determinar si la columna es NULL antes de intentar leer el valor de la columna.  
  
 El componente de script se puede usar como origen, transformación o destino. Este componente admite una entrada y varias salidas. Según la forma en que se usa el componente, admite una entrada o salidas, o ambas cosas. El script es invocado por cada fila en la entrada o la salida.  
  
-   Si se usa como origen, el componente de script admite varias salidas.  
  
-   Si se usa como transformación, el componente de script admite una entrada y varias salidas.  
  
-   Si se usa como destino, el componente de script admite una entrada.  
  
 El componente de script no admite salidas de error.  
  
 Una vez que haya decidido que el componente de script es la opción adecuada para su paquete, tiene que configurar las entradas y salidas, desarrollar el script que el componente utiliza y configurar el propio componente.  
  
## <a name="understanding-the-script-component-modes"></a>Descripción de los modos del componente de script  
 En el Diseñador [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , el componente de script tiene dos modos: modo de diseño de metadatos y modo de diseño de código. En el modo de diseño de metadatos, se pueden agregar y modificar las entradas y salidas de componente de script, pero no se puede escribir código. Una vez configuradas todas las entradas y salidas, se cambia al modo de diseño de código para escribir el script. El componente de script genera automáticamente código base a partir de los metadatos de entradas y salidas. Si cambia los metadatos después de que el componente de script genere el código de base, es posible que su código ya no pueda compilarse porque el código base actualizado puede ser incompatible con su código.  
  
## <a name="writing-the-script-that-the-component-uses"></a>Escribir el script que el componente utiliza  
 El componente de script usa [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools para aplicaciones (VSTA) como entorno para escribir los scripts. Puede tener acceso a VSTA en el **Editor de transformación Script**. Para obtener más información, vea [Editor de transformación Script &#40;página Script&#41;](../../script-transformation-editor-script-page.md).  
  
 El componente de script proporciona un proyecto de VSTA que incluye una clase autogenerada, llamada ScriptMain, que representa los metadatos del componente. Por ejemplo, si el componente de script se usa como una transformación que tiene tres salidas, ScriptMain incluye un método para cada salida. ScriptMain es el punto de entrada al script.  
  
 VSTA incluye todas las características estándar del entorno [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] , como el editor de [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] con códigos de color, IntelliSense y el Explorador de objetos. El script que usa el componente de script se almacena en la definición de paquete. Al diseñar el paquete, el código de script se escribe temporalmente en un archivo de proyecto.  
  
 VSTA es compatible con los lenguajes de programación de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# y [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic.  
  
 Para obtener información acerca de cómo programar el componente de script, vea [Ampliar el flujo de datos con el componente de script](script-component.md). Para obtener información más específica acerca de cómo configurar el componente de script como origen, transformación o destino, vea [Developing Specific Types of Script Components](../../extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md). Para consultar ejemplos adicionales, como un destino ODBC, que ilustran el uso del componente de script, vea [Additional Script Component Examples](../../extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md).  
  
> [!NOTE]  
>  A diferencia de las versiones anteriores en las que podía indicar si se precompilaban los scripts, todos los scripts se precompilan en [!INCLUDE[ssISversion10](../../../includes/ssisversion10-md.md)] y versiones posteriores. Al precompilar el script, no se carga el motor del lenguaje en tiempo de ejecución, por lo que el paquete se ejecuta con mayor rapidez. Sin embargo, los archivos binarios precompilados utilizan una cantidad considerable de espacio en disco.  
  
## <a name="configuring-the-script-component"></a>Configurar el componente de script  
 Puede configurar el componente de script de las maneras siguientes:  
  
-   Seleccionar las columnas de entrada a las que hacer referencia.  
  
    > [!NOTE]  
    >  Puede configurar solo una entrada al usar el Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] .  
  
-   Proporcionar el script que ejecuta el componente.  
  
-   Especificar el lenguaje de script.  
  
-   Proporcionar listas separadas por comas de variables de solo lectura y de lectura/escritura.  
  
-   Agregue más salidas, así como columnas de salida en las que el script realiza asignaciones.  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación.  
  
### <a name="configuring-the-script-component-in-the-designer"></a>Configurar el componente de script en el Diseñador  
 Para obtener más información sobre las propiedades que se pueden establecer en el cuadro de diálogo **Editor de transformación Script** , haga clic en uno de los siguientes temas:  
  
-   [Editor de transformación Script &#40;página Columnas de entrada&#41;](../../script-transformation-editor-input-columns-page.md)  
  
-   [Editor de transformación Script &#40;página Entradas y salidas&#41;](../../script-transformation-editor-inputs-and-outputs-page.md)  
  
-   [Editor de transformación Script &#40;página Script&#41;](../../script-transformation-editor-script-page.md)  
  
-   [Editor de transformación Script &#40;página Administradores de conexión&#41;](../../script-transformation-editor-connection-managers-page.md)  
  
 Para obtener más información sobre cómo establecer estas propiedades en el Diseñador [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , haga clic en el siguiente tema:  
  
-   [Establecer las propiedades de un componente de flujo de datos](../set-the-properties-of-a-data-flow-component.md)  
  
### <a name="configuring-the-script-component-programmatically"></a>Configurar el componente de script mediante programación  
 Para obtener más información sobre las propiedades que se pueden establecer en la ventana **Propiedades** o mediante programación, haga clic en uno de los siguientes temas:  
  
-   [Propiedades comunes](../../common-properties.md)  
  
-   [Propiedades personalizadas de transformación](transformation-custom-properties.md)  
  
 Para obtener más información sobre cómo establecer valores de propiedades, haga clic en uno de los temas siguientes:  
  
-   [Establecer las propiedades de un componente de flujo de datos](../set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-content"></a>Contenido relacionado  
 [Transformaciones de Integration Services](integration-services-transformations.md)  
  
 [Ampliar el flujo de datos con el componente de script](script-component.md)  
  
  
