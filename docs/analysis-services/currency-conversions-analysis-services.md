---
title: Conversiones de moneda (Analysis Services) | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: misc
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- multiple currency conversions
- monetary data [SQL Server]
- currency [Analysis Services]
- converting currency
- one-to-many currency conversions
- many-to-many currency conversions [Analysis Services]
- many-to-one currency conversions [Analysis Services]
ms.assetid: e03f491c-7df8-46a0-ade9-f2e55b68db85
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f54b50833ce40a8222925ac2b43591fa89617631
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="currency-conversions-analysis-services"></a>Conversiones de moneda (Analysis Services)
  [!INCLUDE[applies](../includes/applies-md.md)] Solo multidimensional  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] usa una combinación de características, guiadas por scripts MDX (Expresiones multidimensionales), para proporcionar compatibilidad con la conversión de divisa en cubos que admiten varias divisas.  
  
## <a name="currency-conversion-terminology"></a>Terminología de conversión de monedas  
 La siguiente terminología se utiliza en [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] para describir la funcionalidad de conversión de moneda.  
  
 Moneda dinámica  
 La moneda con la que se escriben las tasas de cambio en el grupo de medida de tarifas.  
  
 Moneda local  
 La moneda que se usa para almacenar las transacciones en las que se basan las medidas que se van a convertir.  
  
 La moneda local puede identificarse por:  
  
-   Un identificador de moneda de la tabla de hechos almacenada con la transacción, como suele ser el caso de las aplicaciones bancarias en las que la propia transacción identifica la moneda que utiliza.  
  
-   Un identificador de moneda asociado con un atributo de una tabla de dimensiones que, después, se asocia con una transacción de la tabla de hechos, como suele ser el caso de las aplicaciones financieras donde una ubicación u otro identificador, como una delegación, identifica la moneda que utiliza una transacción asociada.  
  
 Moneda del informe  
 La moneda a la que se convierten las transacciones desde la moneda dinámica.  
  
> [!NOTE]  
>  En las conversiones de una moneda a varias, la moneda dinámica y la moneda del informe son la misma.  
  
 Dimensión de moneda  
 Una dimensión de base de datos definida con los siguientes parámetros:  
  
-   La propiedad **Type** de la dimensión se establece en Currency.  
  
-   La propiedad **Type** de un atributo de la dimensión se establece en CurrencyName.  
  
    > [!IMPORTANT]  
    >  Los valores de este atributo se deben utilizar en todas las columnas que deben contener un identificador de moneda.  
  
 Grupo de medida de tarifas  
 Un grupo de medida de un cubo, definido con los siguientes parámetros:  
  
-   Existe una relación de dimensión normal entre una dimensión de moneda y el grupo de medida de tarifas.  
  
-   Existe una relación de dimensión normal entre una dimensión temporal y el grupo de medida de tarifas.  
  
-   Opcionalmente, la propiedad **Type** se establece en ExchangeRate. En tanto el Asistente de Business Intelligence utiliza las relaciones con las dimensiones temporal y de moneda para identificar los grupos de medida de tarifas probables, la configuración de la propiedad **Type** en ExchangeRate permite a las aplicaciones cliente identificar más fácilmente los grupos de medida de tarifas.  
  
-   Una o más medidas, que representan las tasas de cambio que contiene el grupo de medida de tarifas.  
  
 Dimensión de moneda del informe  
 La dimensión (definida por el Asistente de Business Intelligence después de una conversión de moneda) que contiene las monedas del informe para esa conversión. La dimensión de moneda del informe se basa en una consulta con nombre (definida en la vista del origen de datos en la que se basa la dimensión de moneda asociada con el grupo de medida de tarifas) de la tabla principal de dimensión de la dimensión de moneda. La dimensión se define con los siguientes parámetros:  
  
-   La propiedad **Type** de la dimensión se establece en Currency.  
  
-   La propiedad **Type** de un atributo clave de la dimensión se establece en CurrencyName.  
  
-   La propiedad **Type** de un atributo dentro de la dimensión se establece en CurrencyDestination, y la columna enlazada con el atributo contiene los identificadores de moneda que representan las monedas del informe para esa conversión.  
  
## <a name="defining-currency-conversions"></a>Definir las conversiones de moneda  
 Puede utilizar el Asistente de Business Intelligence para definir la funcionalidad de conversión de moneda en un cubo o puede definir manualmente las conversiones de moneda mediante scripts MDX.  
  
### <a name="prerequisites"></a>Requisitos previos  
 Antes de que pueda definir una conversión de moneda en un cubo mediante el Asistente de Business Intelligence, debe definir, al menos, una dimensión de moneda, una dimensión temporal y un grupo de medida de tarifas. Desde estos objetos, el Asistente de Business Intelligence puede recuperar los datos y metadatos que se usan para construir la dimensión de moneda del informe y el script MDX necesarios para proporcionar la funcionalidad de conversión de moneda.  
  
### <a name="decisions"></a>Decisiones  
 Necesita tomar las siguientes decisiones antes de que el Asistente de Business Intelligence pueda construir la dimensión de moneda del informe y el script MDX necesarios para proporcionar la funcionalidad de conversión de moneda:  
  
-   Dirección de la tasa de cambio  
  
-   Miembros convertidos  
  
-   Tipo de conversión  
  
-   Monedas locales  
  
-   Monedas del informe  
  
### <a name="exchange-rate-directions"></a>Direcciones de la tasa de cambio  
 El grupo de medida de tarifas contiene medidas que representan las tasas de cambio entre las monedas locales y la moneda dinámica (a la que se hace referencia normalmente como moneda corporativa). La combinación de la dirección de la tasa de cambio y el tipo de conversión determina la operación que se realiza en las medidas que se van a convertir mediante el script MDX generado con el Asistente de Business Intelligence. La tabla siguiente describe las operaciones realizadas en función de la dirección de la tasa de cambio y el tipo de conversión, basándose en las opciones de dirección de la tasa de cambio y las direcciones de conversión disponibles en el Asistente de Business Intelligence.  
  
|||||  
|-|-|-|-|  
|Dirección de la tasa de cambio|**Varios a uno**|**Uno a varios**|**Varios a varios**|  
|**n moneda dinámica a 1 moneda de ejemplo**|Multiplica la medida que se va a convertir por la medida de la tasa de cambio de la moneda local, a fin de convertir la medida a la moneda dinámica.|Divide la medida que se va a convertir por la medida de la tasa de cambio de la moneda del informe, a fin de convertir la medida a la moneda del informe.|Multiplica la medida que se va a convertir por la medida de la tasa de cambio de la moneda local, a fin de convertir la medida a la moneda dinámica, y después divide la medida convertida por la medida de la tasa de cambio de la moneda del informe, a fin de convertir la medida en la moneda del informe.|  
|**n moneda de ejemplo a 1 moneda dinámica**|Divide la medida que se va a convertir por la medida de la tasa de cambio de la moneda local, a fin de convertir la medida a la moneda dinámica.|Multiplica la medida que se va a convertir por la medida de la tasa de cambio de la moneda del informe, a fin de convertir la medida a la moneda del informe.|Divide la medida que se va a convertir por la medida de la tasa de cambio de la moneda local, a fin de convertir la medida a la moneda dinámica, y después multiplica la medida convertida por la medida de la tasa de cambio de la moneda del informe, a fin de convertir la medida en la moneda del informe.|  
  
 Elija la dirección de la tasa de cambio en la página **Establecer las opciones de conversión de moneda** del Asistente de Business Intelligence. Para más información sobre cómo configurar la dirección de la conversión, vea [Establecer las opciones de conversión de moneda &#40;Asistente de Business Intelligence&#41;](http://msdn.microsoft.com/library/a49d4e1f-bdda-4a83-ab4f-ce8c500e1d6d).  
  
### <a name="converted-members"></a>Miembros convertidos  
 Puede usar el Asistente de Business Intelligence para especificar qué medidas del grupo de medida de tarifas se van a utilizar para convertir los valores de:  
  
-   Medidas en otros grupos de medida  
  
-   Miembros de una jerarquía de atributos de un atributo de cuenta en una dimensión de base de datos.  
  
-   Tipos de cuenta que usan los miembros de una jerarquía de atributos de un atributo de cuenta en una dimensión de base de datos.  
  
 El Asistente de Business Intelligence utiliza esta información dentro del script MDX generado por el asistente para determinar el ámbito de cálculo de la conversión de moneda. Para más información sobre cómo especificar miembros para la conversión de divisa, vea [Seleccionar miembros &#40;Asistente de Business Intelligence&#41;](http://msdn.microsoft.com/library/1a147461-d594-41e7-a41d-09d2d003e1e0).  
  
### <a name="conversion-types"></a>Tipos de conversión  
 El Asistente de Business Intelligence admite tres tipos diferentes de conversión de moneda:  
  
-   **Uno a varios**  
  
     Las transacciones se almacenan en la tabla de hechos de la moneda dinámica y después se convierten a una a más monedas del informe.  
  
     Por ejemplo, la moneda dinámica puede definirse como dólares norteamericanos (USD) y la tabla de hechos puede almacenar las transacciones en USD. Este tipo de conversión convierte estas transacciones de la moneda dinámica a las monedas del informe especificadas. El resultado es que las transacciones pueden almacenarse en la moneda dinámica especificada y presentarse en la moneda dinámica o en cualquiera de las monedas del informe especificadas en la dimensión de moneda del informe definida para la conversión de moneda.  
  
-   **Varios a uno**  
  
     Las transacciones se almacenan en la tabla de hechos en las monedas locales y después se convierten a la moneda dinámica. La moneda dinámica sirve como la única moneda del informe especificada en la dimensión de moneda del informe.  
  
     Por ejemplo, la moneda dinámica puede definirse como dólares norteamericanos (USD) y la tabla de hechos puede almacenar las transacciones en euros (EUR), dólares australianos (AUD) y pesos mexicanos (MXN). Este tipo de conversión convierte estas transacciones de las monedas locales especificadas a la moneda dinámica. El resultado es que las transacciones pueden almacenarse en las monedas locales especificadas y presentarse en la moneda dinámica que se ha especificado en la dimensión de moneda del informe definida para la conversión de moneda.  
  
-   **Varios a varios**  
  
     Las transacciones se almacenan en la tabla de hechos en las monedas locales. La funcionalidad de conversión de monedas convierten este tipo de transacciones a la moneda dinámica, y después a una a más monedas del informe.  
  
     Por ejemplo, la moneda dinámica puede definirse como dólares norteamericanos (USD) y la tabla de hechos puede almacenar las transacciones en euros (EUR), dólares australianos (AUD) y pesos mexicanos (MXN). Este tipo de conversión convierte estas transacciones desde sus monedas locales especificadas a la moneda dinámica, y después las transacciones convertidas se convierten de nuevo desde la moneda dinámica a las monedas del informe especificadas. El resultado es que las transacciones pueden almacenarse en las monedas locales especificadas y presentarse en la moneda dinámica o en cualquiera de las monedas del informe especificadas en la dimensión de moneda del informe definida para la conversión de moneda.  
  
 La especificación del tipo de conversión permite al Asistente de Business Intelligence definir la consulta con nombre y la estructura de la dimensión de la moneda del informe, así como la estructura del script MDX que se ha definido para la conversión de moneda.  
  
### <a name="local-currencies"></a>Monedas locales  
 Si elige un tipo de conversión varios a varios o varios a uno para su conversión de moneda, deberá especificar cómo se identifican las monedas locales para las que el script MDX generado por el Asistente de Business Intelligence realiza los cálculos de conversión de moneda. La moneda local de una transacción en una tabla de hechos puede identificarse de una de estas dos formas:  
  
-   El grupo de media contiene una relación de dimensión normal con la dimensión de moneda. Por ejemplo, en la base de datos de ejemplo [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , el grupo de medida Internet Sales tiene una relación de dimensión normal con la dimensión Currency. La tabla de hechos de ese grupo de medida contiene una columna de clave externa que hace referencia a los identificadores de moneda de la tabla de dimensiones de esa dimensión. En este caso, puede seleccionar el atributo de la dimensión de moneda a la que hace referencia el grupo de medida para identificar la moneda local de las transacciones en la tabla de hechos de ese grupo de medida. Esta situación se produce, generalmente, en las aplicaciones bancarias, donde la propia transacción determina la moneda utilizada en la transacción.  
  
-   El grupo de medida contiene una relación de dimensión referenciada con la dimensión de moneda a través de otra dimensión que hace referencia directamente a la dimensión de moneda. Por ejemplo, en la base de datos de ejemplo [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , el grupo de medida Financial Reporting tiene una relación de dimensión de referencia con la dimensión Currency a través de la dimensión Organization. La tabla de hechos de ese grupo de medida contiene una columna de clave externa que hace referencia a los miembros de la tabla de dimensiones de la dimensión Organization. A su vez, la tabla de dimensiones de la dimensión Organization contiene una columna de clave externa que hace referencia a los identificadores de moneda de la tabla de dimensiones de la dimensión Currency. Esta situación se produce, generalmente, en las aplicaciones de informes financieros, donde la ubicación o delegación de una transacción determina la moneda de esa transacción. En este caso, puede seleccionar el atributo que hace referencia a la dimensión de la moneda desde la dimensión de la entidad de empresa.  
  
### <a name="reporting-currencies"></a>Monedas del informe  
 Si elige un tipo de conversión varios a varios o uno a varios para su conversión de moneda, deberá especificar las monedas del informe en las que el script MDX generado por el Asistente de Business Intelligence realiza los cálculos de conversión de moneda. Puede especificar todos los miembros de la dimensión de moneda relacionados con el grupo de medida de tarifas o seleccionar miembros individuales de la dimensión.  
  
 El Asistente de Business Intelligence crea una dimensión de moneda del informe, basándose en una consulta con nombre generada a partir de la tabla de dimensiones de la dimensión de moneda, que usa las monedas del informe seleccionadas.  
  
> [!NOTE]  
>  Si selecciona el tipo de conversión uno a varios, también se creará una dimensión de monedas del informe. La dimensión solo contiene un miembro que representa la moneda dinámica, ya que ésta también se utiliza como moneda del informe en una conversión de moneda uno a varios.  
  
 Se define una dimensión de moneda del informe independiente por cada conversión de moneda definida en el cubo. Puede cambiar el nombre de las dimensiones de moneda del informe después de la creación, pero si lo hace también deberá actualizar el script MDX generado para esa conversión de moneda, para garantizar que el comando de script utiliza el nombre correcto cuando hace referencia a la dimensión de moneda del informe.  
  
## <a name="defining-multiple-currency-conversions"></a>Definir varias conversiones de moneda  
 Mediante el Asistente de Business Intelligence puede definir tantas conversiones de moneda como necesite para su solución de Business Intelligence. Puede sobrescribir una conversión de moneda existente o anexar una nueva conversión de moneda al script MDX de un cubo. Varias conversiones de moneda definidas en un solo cubo proporcionan flexibilidad en las aplicaciones de Business Intelligence que tienen complejos requisitos de informes, como aplicaciones de informes financieros con varios requisitos independientes de conversión para el contexto internacional.  
  
### <a name="identifying-currency-conversions"></a>Identificar las conversiones de moneda  
 El Asistente de Business Intelligence identifica cada conversión de moneda mediante la demarcación de los comandos de script para la conversión de moneda con los siguientes comentarios:  
  
 `//<Currency conversion>`  
  
 `...`  
  
 `[MDX statements for the currency conversion]`  
  
 `...`  
  
 `//</Currency conversion>`  
  
 Si cambia o quita estos comentarios, el Asistente de Business Intelligence no podrá detectar la conversión de moneda, de modo que no debe modificarlos.  
  
 El asistente también almacena metadatos en comentarios dentro de estos comentarios, incluyendo la fecha y hora de creación, el usuario y el tipo de conversión. Estos comentarios tampoco deben modificarse, ya que el Asistente de Business Intelligence utiliza estos metadatos cuando se muestran las conversiones de moneda.  
  
 Siempre que sea necesario, puede cambiar los comandos de script de una conversión de moneda. Sin embargo, si sobrescribe la conversión de moneda, estos cambios se perderán.  
  
## <a name="see-also"></a>Vea también  
 [Escenarios de globalización para Analysis Services](../analysis-services/globalization-scenarios-for-analysis-services.md)  
  
  

