---
title: Expresiones de Integration Services (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- packages [Integration Services], expressions
- Integration Services packages, expressions
- SQL Server Integration Services packages, expressions
- expressions [Integration Services], packages
- SSIS packages, expressions
ms.assetid: 26d2e242-7f60-4fa9-a70d-548a80eee667
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f2e884e7a34af6cae14b4b057038e54b20255200
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "71289684"
---
# <a name="integration-services-ssis-expressions"></a>Expresiones de Integration Services (SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Una expresión es una combinación de símbolos (identificadores, literales, funciones y operadores) que produce un solo valor de datos. Las expresiones simples pueden ser una sola constante, variable o función. Es más frecuente que las expresiones sean complejas, con varios operadores y funciones, y que hagan referencia a varias columnas y variables. En [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], se pueden usar expresiones para definir condiciones para las instrucciones CASE, crear y actualizar valores de las columnas de datos, asignar valores a variables, actualizar o llenar propiedades en tiempo de ejecución, definir restricciones en las restricciones de precedencia y proporcionar las expresiones que utiliza el contenedor de bucles For.  
  
 Las expresiones se basan en un lenguaje de expresiones y en el evaluador de expresiones. El evaluador de expresiones analiza la expresión y determina si sigue las reglas del lenguaje de expresiones. Para obtener más información acerca de la sintaxis de expresiones y los literales e identificadores admitidos, vea los temas siguientes.  
  
-   [Sintaxis &#40;SSIS&#41;](../../integration-services/expressions/syntax-ssis.md)  
  
-   [Literales &#40;SSIS&#41;](../../integration-services/expressions/numeric-string-and-boolean-literals.md)  
  
-   [Identificadores &#40;SSIS&#41;](../../integration-services/expressions/identifiers-ssis.md)  
  
## <a name="components-that-use-expressions"></a>Componentes que usan expresiones  
 Los siguientes elementos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] pueden usar expresiones:  
  
-   La transformación División condicional implementa una estructura de decisión basada en expresiones para dirigir filas de datos a diferentes destinos. El resultado de evaluar las expresiones usadas en una transformación División condicional debe ser **true** o **false**. Por ejemplo, las filas que cumplen la condición de la expresión "Column1 > Column2" se pueden enrutar a una salida independiente.  
  
-   La transformación Columna derivada utiliza valores creados mediante expresiones para llenar las nuevas columnas en un flujo de datos o para actualizar columnas existentes. Por ejemplo, la expresión Column1 + " ABC" se puede utilizar para actualizar un valor o para crear uno nuevo con la cadena concatenada.  
  
-   Las variables utilizan una expresión para establecer su valor. Por ejemplo, GETDATE() establece el valor de la variable en la fecha actual.  
  
-   Las restricciones de precedencia pueden usar expresiones para especificar las condiciones que determinan si se ejecuta la tarea o el contenedor restringido de un paquete. El resultado de evaluar las expresiones usadas en una restricción de precedencia debe ser **true** o **false**. Por ejemplo, la expresión \@A > \@B compara dos variables definidas por el usuario para determinar si se ejecuta la tarea restringida.  
  
-   El contenedor de bucles For puede usar expresiones para generar las instrucciones de inicialización, evaluación e incremento utilizadas por la estructura de bucle. Por ejemplo, la expresión \@Counter = 1 inicializa el contador de bucles.  
  
 Las expresiones también se pueden utilizar para actualizar los valores de las propiedades de paquetes, contenedores de los bucles For y ForEach, tareas, administradores de conexión de paquetes y proyectos, proveedores de registro y enumeradores ForEach. Por ejemplo, con una expresión de propiedad se puede asignar la cadena "Localhost.AdventureWorks" a la propiedad ConnectionName de la tarea Ejecutar SQL. Para más información, vea [Usar expresiones de propiedad en paquetes](../../integration-services/expressions/use-property-expressions-in-packages.md).  
  
## <a name="icon-markers-for-expressions"></a>Marcadores de icono para las expresiones  
 En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], aparece un marcador de icono especial junto a los administradores de conexiones, las variables y las tareas que tienen expresiones establecidas. La propiedad de **HasExpressions** está disponible en todos los objetos SSIS que admiten expresiones, a excepción de las variables. La propiedad le permite identificar con facilidad qué objetos tienen expresiones.  
  
## <a name="expression-builder"></a>Generador de expresiones  
 El Generador de expresiones es una herramienta gráfica para generar expresiones. Está disponible en los cuadros de diálogo **Editor de transformación División condicional**y **Editor de transformación Columna derivada** , y en el cuadro de diálogo **Generador de expresiones** es una herramienta gráfica para generar expresiones.  
  
 El generador de expresiones proporciona carpetas que contienen elementos específicos del paquete y carpetas que contienen las funciones, conversiones de tipo y operadores que proporciona el lenguaje de expresiones. Los elementos específicos del paquete incluyen variables del sistema y variables definidas por el usuario. En los cuadros de diálogo **Editor de transformación División condicional** y **Editor de transformación Columna derivada** , también puede ver columnas de datos. Para crear expresiones para las transformaciones, puede arrastrar elementos de las carpetas a la columna **Condición** o **Expresión** , o bien puede escribir la expresión directamente en la columna. El generador de expresiones agrega automáticamente los elementos de sintaxis necesarios, como el prefijo \@ de los nombres de variables.  
  
> [!NOTE]  
>  Los nombres están definidos por el usuario y las variables del sistema distinguen mayúsculas y minúsculas.  
  
 Las variables tienen un ámbito y en la carpeta **Variables** del Generador de expresiones solo se muestran las variables que están en el ámbito y disponibles para su uso. Para más información, vea [Variables de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md).  
  
## <a name="related-tasks"></a>Related Tasks  
 [Usar una expresión en un componente de flujo de datos](https://msdn.microsoft.com/library/9181b998-d24a-41fb-bb3c-14eee34f910d)  
  
## <a name="related-content"></a>Contenido relacionado  
 Artículo técnico, sobre [ejemplos de expresiones SSIS](https://go.microsoft.com/fwlink/?LinkId=220761), en social.technet.microsoft.com  
  
## <a name="see-also"></a>Consulte también  
 [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)  
  
  
