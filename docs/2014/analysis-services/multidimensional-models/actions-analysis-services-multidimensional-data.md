---
title: Acciones (Analysis Services-datos multidimensionales) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- actions [Analysis Services]
- actions [Analysis Services], about actions
- MDX [Analysis Services], actions
- cubes [Analysis Services], actions
- OLAP objects [Analysis Services], actions
ms.assetid: 07229bb2-805c-427e-8455-69c9ca5d01e0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3ff4e330950a3fca54ba8ab08456157156836c0f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66077587"
---
# <a name="actions-analysis-services---multidimensional-data"></a>Acciones (Analysis Services - Datos multidimensionales)
  Las acciones pueden ser de tipos diferentes y se deben crear como corresponda. Las acciones pueden ser:  
  
-   Acciones de obtención de detalles, que devuelven el conjunto de filas que representa los datos subyacentes de las celdas seleccionadas del cubo donde se produce la acción.  
  
-   Acciones de elaboración de informes, que devuelven un informe de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] asociado con la sección seleccionada del cubo donde se produce la acción.  
  
-   Acciones estándar, que devuelven el elemento de acción (URL, HTML, DataSet, RowSet y otros elementos) asociado a la sección seleccionada del cubo donde se produce la acción.  
  
 La aplicación cliente usa una interfaz de consulta, como ADOMD.NET, para recuperar y exponer las acciones al usuario final. Para obtener más información, vea [Desarrollar con ADOMD.NET](https://docs.microsoft.com/bi-reference/adomd/developing-with-adomd-net).  
  
 Un objeto <xref:Microsoft.AnalysisServices.Action> simple se compone de la información básica, el destino donde se va a producir la acción, una condición para limitar el ámbito de acción y el tipo. La información básica incluye el nombre de la acción, la descripción de la acción, la sugerencia de título para la acción y otros elementos.  
  
 El destino es la ubicación real del cubo donde se va a producir la acción. El destino está compuesto por un tipo de destino y un objeto de destino. El tipo de destino representa el tipo de objeto, en el cubo, donde se va a habilitar la acción. El tipo de destino puede ser un miembro del nivel, una celda, una jerarquía, un miembro de la jerarquía u otros. El objeto de destino es un objeto concreto del tipo de destino; si el tipo de destino es la jerarquía, el objeto de destino es cualquiera de las jerarquías definidas en el cubo.  
  
 La condición es una expresión MDX de tipo `Boolean` que se evalúa en el evento de la acción. La acción se ejecuta si la condición se evalúa como `true`. En caso contrario, no se ejecuta la acción.  
  
 El tipo es el tipo de acción que se va a ejecutar. <xref:Microsoft.AnalysisServices.Action> es una clase abstracta y, por lo tanto, para usarla es necesario usar una de las clases derivadas. Existen dos tipos de acciones predefinidas: obtención de detalles y elaboración de informes. Estos tienen clases derivadas correspondientes: <xref:Microsoft.AnalysisServices.DrillThroughAction> y <xref:Microsoft.AnalysisServices.ReportAction>. Otras acciones se realizan con la clase <xref:Microsoft.AnalysisServices.StandardAction> .  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] En [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], una acción es una instrucción MDX almacenada que se puede presentar y emplear en aplicaciones cliente. En otras palabras, una acción es un comando cliente que se define y se almacena en el servidor. Una acción también contiene información que especifica cuándo y cómo debe la aplicación cliente mostrar y controlar la instrucción MDX. La operación que se especifica con la acción puede iniciar una aplicación, utilizando la información de la acción como parámetro, o bien recuperar información en función de criterios que proporciona la acción.  
  
 Las acciones permiten a los usuarios corporativos actuar sobre los resultados de sus análisis. Al guardar y volver a utilizar acciones, los usuarios finales pueden llegar más lejos que con el análisis tradicional, que suele finalizar con la presentación de datos, e iniciar soluciones para problemas y deficiencias que se hayan detectado, ampliando así la aplicación de Business Intelligence más allá del cubo. Las acciones pueden transformar la aplicación cliente de una sofisticada herramienta de representación de datos en una parte integral del sistema operativo de la empresa. En lugar de centrarse en enviar datos como entrada para aplicaciones operativas, los usuarios finales pueden "cerrar el ciclo" en el proceso de toma de decisiones. Esta posibilidad de transformar datos analíticos en decisiones es fundamental para la correcta aplicación de Business Intelligence.  
  
 Por ejemplo, un usuario corporativo que examine un cubo observa que las existencias actuales de un determinado producto son bajas. La aplicación cliente proporciona al usuario corporativo una lista de acciones, todas relacionadas con el valor de existencias bajas del producto, que se recuperan de la base de datos de Analysis Services. El usuario corporativo selecciona la acción Order para el miembro del cubo que representa el producto. La acción Order inicia un nuevo pedido al llamar a un procedimiento almacenado de la base de datos operativa. El procedimiento almacenado genera la información correspondiente para enviarla al sistema de entrada de pedidos.  
  
 Puede ser flexible al crear acciones; una acción puede, por ejemplo, iniciar una aplicación o recuperar información de una base de datos. Puede configurar una acción para que se desencadene desde prácticamente cualquier parte de un cubo, como dimensiones, niveles, miembros y celdas, o bien crear varias acciones para una misma parte de un cubo. También puede pasar parámetros de cadena a las aplicaciones iniciadas y especificar los títulos que se muestran a los usuarios finales cuando se ejecuta la acción.  
  
> [!IMPORTANT]  
>  Para que un usuario corporativo utilice acciones, la aplicación cliente empleada por dicho usuario debe admitir acciones.  
  
## <a name="types-of-actions"></a>Tipos de acciones  
 En la tabla siguiente se enumeran los tipos de acciones que se incluyen en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]:  
  
|Tipo de acción|Descripción|  
|-----------------|-----------------|  
|CommandLine|Ejecuta un comando en el símbolo del sistema.|  
|Dataset|Devuelve un conjunto de datos a una aplicación cliente.|  
|Obtención de detalles|Devuelve una instrucción de obtención de detalles como una expresión, que el cliente ejecuta para devolver un conjunto de filas.|  
|Html|Ejecuta un script HTML en un explorador de Internet.|  
|Propietario|Ejecuta una operación con una interfaz que no aparece en esta tabla.|  
|Informe|Envía una solicitud parametrizada basada en una dirección URL a un servidor de informes y devuelve un informe a una aplicación cliente.|  
|Conjunto de filas|Devuelve un conjunto de filas a una aplicación cliente.|  
|.|Ejecuta un comando OLE DB.|  
|URL|Muestra una página web dinámica en un explorador de Internet.|  
  
## <a name="resolving-and-executing-actions"></a>Resolver y ejecutar acciones  
 Cuando un usuario corporativo obtiene acceso al objeto para el que se define el objeto de comando, la instrucción asociada a la acción se resuelve automáticamente, lo que la pone a disposición de la aplicación cliente, pero la acción no se ejecuta automáticamente. La acción se ejecuta solo cuando el usuario corporativo realiza la operación específica del cliente que inicia la acción. Por ejemplo, las aplicaciones cliente pueden presentar una lista de acciones como menú emergente cuando el usuario corporativo hace clic con el botón secundario en un miembro o una celda concretos.  
  
## <a name="see-also"></a>Consulte también  
 [Acciones en modelos multidimensionales](actions-in-multidimensional-models.md)  
  
  
