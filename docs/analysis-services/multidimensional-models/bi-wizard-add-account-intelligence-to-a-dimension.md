---
title: Agregar inteligencia de cuentas a una dimensión | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5021d10832028f46d1d0b1a8f33dc01a75df5985
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34023472"
---
# <a name="bi-wizard---add-account-intelligence-to-a-dimension"></a>Asistente de BI - agregar inteligencia de cuentas a una dimensión
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Agregue la mejora de inteligencia de cuentas a un cubo o dimensión para asignar las clasificaciones de cuenta estándar, como ingresos y gastos, a los miembros de un atributo de cuenta. Esta mejora también identifica los tipos de cuenta (como Asset y Liability) y asigna la agregación adecuada a cada tipo de cuenta. [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] puede usar las clasificaciones para agregar cuentas con el tiempo.  
  
> [!NOTE]  
>  La inteligencia de cuentas solo está disponible en dimensiones basadas en los orígenes de datos existentes. En las dimensiones que se crearon sin utilizar un origen de datos, debe ejecutar el Asistente para generar esquemas para crear una vista del origen de datos antes de agregar la inteligencia de cuentas.  
  
 Se aplica la inteligencia de cuentas a una dimensión que especifica la información de una cuenta (por ejemplo, nombre de cuenta, número de cuenta y tipo de cuenta). Para agregar una inteligencia de cuentas, debe utilizar el Asistente de Business Intelligence y seleccionar la opción **Definir la inteligencia de cuentas** en la página **Elegir mejora** . El asistente le mostrará los pasos necesarios para seleccionar la dimensión en la que desee aplicar la inteligencia de cuentas, identificar los atributos de cuenta en la dimensión de cuenta seleccionada y asignar los tipos de cuenta de la tabla de dimensión a los tipos de cuenta reconocidos por [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
## <a name="selecting-a-dimension"></a>Seleccionar una dimensión  
 En la primera página **Definir la inteligencia de cuentas** del asistente, deberá especificar la dimensión en la que desee aplicar la inteligencia de cuentas. La mejora de inteligencia de cuentas agregada a esta dimensión seleccionada provocará cambios en la dimensión. Estos cambios son heredados por todos los cubos que incluyan la dimensión seleccionada.  
  
## <a name="specifying-account-attributes"></a>Especificar atributos de cuenta  
 En la página **Configurar los atributos de dimensión** del asistente, deberá especificar los atributos de cuenta en la dimensión de cuenta seleccionada. En primer lugar, en la columna **Incluir** , active la casilla junto a los tipos de atributo de cuenta que desee asignar a un atributo de dimensión en la dimensión. A continuación, en la columna **Atributo de dimensión** , expanda la lista desplegable y seleccione el atributo en la dimensión que se corresponda con el tipo de atributo seleccionado. Al seleccionar el atributo de la lista, se establece la propiedad de atributo **Type** para los atributos de cuenta.  
  
## <a name="mapping-account-types"></a>Asignar tipos de cuenta  
 La segunda página de **Definir la inteligencia de cuentas** asigna los valores de tipos de cuenta de la tabla de dimensión a los tipos de cuenta reconocidos por [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Solo se mostrará esta página si incluye el atributo de dimensión **Tipo de cuenta** en la dimensión. Para incluir la dimensión **Tipo de cuenta** , en la página **Definir configuración de la inteligencia de cuentas** del asistente, active la casilla junto a **Tipo de cuenta**y seleccione el atributo adecuado.  
  
 En la segunda página de **Definir la inteligencia de cuentas** , se muestran dos columnas:  
  
-   La columna **Tipos de cuenta de tabla de origen** muestra los tipos de cuenta que obtiene el asistente de la tabla de dimensión.  
  
-   La columna **Tipos de cuenta de servidor** identifica el tipo de cuenta correspondiente que reconoce [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . La siguiente tabla muestra los tipos de cuenta que reconoce [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y la agregación predeterminada de cada tipo. Las selecciones se realizan automáticamente si la tabla de dimensión utiliza los mismos nombres de tipo de cuenta que [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
    |Tipo de cuenta de servidor|Agregación|Description|  
    |-------------------------|-----------------|-----------------|  
    |**Estadísticas**|**Ninguno**|Proporción calculada de algo o recuento de algo que no se agrega a lo largo del tiempo. Este tipo de cuenta no convierte distintas monedas con reglas de conversión.|  
    |**Liability**|**LastNonEmpty**|Dinero o valor de cosas debidas en un momento dado. Este tipo de cuenta no se acumula a lo largo del tiempo, por lo que no se agrega de forma natural a lo largo del tiempo. Por ejemplo, la cantidad Year es el valor del último mes con datos. Este tipo de cuenta convierte monedas con la tasa del final del período.|  
    |**Asset**|**LastNonEmpty**|Dinero o valor de cosas mantenidas en un momento dado. Este tipo de cuenta se acumula a lo largo del tiempo, por lo que no se agrega de forma natural a lo largo del tiempo. Por ejemplo, la cantidad Year es el valor del último mes con datos. Este tipo de cuenta convierte monedas con la tasa del final del período.|  
    |**Equilibrio**|**LastNonEmpty**|Recuento de algo en un momento dado. Este tipo de cuenta se acumula pero no se agrega de forma natural a lo largo del tiempo. Por ejemplo, la cantidad Year es el valor del último mes con datos.|  
    |**Flow**|**Sum**|Recuento incremental de algo. Este tipo de cuenta se agrega como una **Sum** a lo largo del tiempo pero no convierte con reglas de conversión de monedas.|  
    |**Expense**|**Sum**|Dinero o valor de cosas gastadas. Este tipo de cuenta se agrega como una **Sum** a lo largo del tiempo y convierte monedas con una tasa media.|  
    |**Income**|**Sum**|Dinero o valor de cosas recibidas. Este tipo de cuenta se agrega como una **Sum** a lo largo del tiempo y convierte monedas con una tasa media.|  
  
    > [!NOTE]  
    >  De ser adecuado, se puede asignar más de un tipo de cuenta de la dimensión a un tipo de cuenta de servidor determinado.  
  
 Para cambiar las agregaciones predeterminadas asignadas a cada tipo de cuenta de una base de datos, puede utilizar el Diseñador de bases de datos.  
  
1.  En el Explorador de soluciones, haga clic con el botón derecho en el proyecto de Analysis Services y haga clic en **Editar base de datos**.  
  
2.  En el cuadro **Asignación de tipo de cuenta** , seleccione un tipo de cuenta en el **Nombre**.  
  
3.  En el cuadro de texto **Alias** , escriba un alias para este tipo de cuenta.  
  
4.  En el cuadro de lista desplegable **Función de agregación** , cambie la función de agregación predeterminada para este tipo de cuenta.  
  
  
