---
title: Crear una dimensión generando una tabla que no sea de tiempos en el origen de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data sources [Analysis Services], dimensions without data source
- dimensions [Analysis Services], standard
- dimensions [Analysis Services], creating without data source
- standard dimensions [Analysis Services]
ms.assetid: a37f7a46-7451-4582-ba19-2595196d97bc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 962df497e804011e69e2a350c24ce41f4c273b6d
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66076434"
---
# <a name="create-a-dimension-by-generating-a-non-time-table-in-the-data-source"></a>Crear una dimensión generando una tabla que no sea de tiempos en el origen de datos
  En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], puede utilizar el Asistente para dimensiones en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] para crear una dimensión sin utilizar un origen de datos existente. Para ello, debe seleccionar la opción **Generar una tabla que no sea de tiempos en el origen de datos** en la página **Seleccionar método de creación** del asistente. Para crear una tabla de dimensiones en el origen de datos subyacente, debe tener permisos para crear objetos en ese origen de datos subyacente. Al definir una dimensión sin una vista del origen de datos predefinida, puede definirla desde cero o usando una plantilla de dimensiones.  
  
 El Asistente para dimensiones proporciona plantillas de dimensiones de muestra que puede usar para generar un tipo de dimensión frecuente. Puede elegir entre los siguientes tipos de dimensiones:  
  
-   Cuenta  
  
-   Customer  
  
-   date  
  
-   Department  
  
-   Destination Currency  
  
-   Employee  
  
-   Geografía  
  
-   Internet Sales Order Details  
  
-   Organización  
  
-   Producto  
  
-   Promoción  
  
-   Reseller Sales Order Details  
  
-   Reseller  
  
-   Sales Channel  
  
-   Sales Reason  
  
-   Sales Summary Order Details  
  
-   Sales Territory  
  
-   Escenario  
  
-   Source Currency  
  
 Cada una de las plantillas estándar admite atributos que puede incluir en la dimensión. También puede agregar sus propios archivos de plantilla para dimensiones que normalmente se usan con sus datos. Las plantillas de dimensiones se ubican en la siguiente carpeta:  
  
 `C:\Program Files\Microsoft SQL Server\100\Tools\Templates\olap\1033\Dimension Templates`  
  
 Puede utilizar el Diseñador de dimensiones una vez finalizado el Asistente para dimensiones para agregar, quitar o configurar atributos y jerarquías de la dimensión.  
  
 Si va a crear una dimensión que no sea de tiempos sin utilizar un origen de datos, el Asistente para dimensiones lo guía por los pasos necesarios para especificar el tipo de dimensión, identificar el atributo clave y las dimensiones variables.  
  
## <a name="specify-dimension-type"></a>Especificar el tipo de dimensión  
 En la página **Especificar tipo de dimensión** del Asistente para dimensiones, puede especificar el tipo de dimensión. Si está generando la dimensión basada en una plantilla, el tipo de dimensión ya está definido. En esta página también puede seleccionar atributos estándar para el tipo de dimensión especificado si hay alguno disponible.  
  
 Si selecciona una plantilla que corresponde a un tipo de dimensión, esta página se llena con las opciones para este tipo de dimensión. Si no selecciona una plantilla, o bien si no hay ningún tipo de dimensión correspondiente, el tipo predeterminado de dimensión es **Normal**. Si no se encuentra ya seleccionado un tipo de dimensión, elija el más apropiado para la dimensión que se crea. Si no hay ningún tipo apropiado enumerado para **Tipo de dimensión**, use **Normal**.  
  
 Cuando se elige un tipo de dimensión, el asistente muestra los tipos de atributo que son aplicables a esta dimensión en **Atributos de dimensión**. Para seleccionar un tipo de atributo, active la casilla **Incluir** , situada junto al tipo de atributo, y escriba el nombre del atributo en **Atributo de dimensión**. El nombre predeterminado es el mismo que el **Tipo de atributo**.  
  
## <a name="identify-key-attribute-and-changing-dimensions"></a>Identificar el atributo clave y dimensiones variables  
 En la página **Especificar clave y tipo de dimensión** , seleccione el atributo que desee que sea el atributo clave para la dimensión. Normalmente, el atributo clave corresponde a la columna de clave principal en la tabla de dimensión principal, y normalmente indiza los miembros hoja de la dimensión.  
  
 Si selecciona una plantilla, y en la plantilla se define un atributo clave, ése es el atributo clave predeterminado. Si selecciona una plantilla pero no tiene definido ningún atributo clave, el atributo clave predeterminado es el primero de la lista. La lista contiene todos los atributos que seleccionó en la página **Especificar tipo de dimensión** . Puede elegir como atributo clave cualquiera de los atributos que seleccionó en la página **Especificar tipo de dimensión** . Si no ha seleccionado ningún atributo, el asistente crea automáticamente un atributo clave y lo nombra concatenando el nombre de dimensión y el "Id.".  
  
 Finalmente, especifique si esta dimensión es una dimensión variable. Los miembros de una dimensión variable se mueven con el tiempo a diferentes ubicaciones en una jerarquía. El asistente genera columnas adicionales y crea atributos que correspondan a esas columnas. Estas columnas permitirán a los usuarios consultar la dimensión de forma que se tenga en cuenta el cambio. Cualquier paquete que se cree posteriormente con el Asistente para generar esquemas administra claves suplentes basándose en las características de dimensión variable lenta de la dimensión.  
  
 Al activar la casilla **Es una dimensión variable** , el Asistente para dimensiones define los atributos indicados en la siguiente tabla:  
  
|Attribute|Tipo|  
|---------------|----------|  
|Id. original de DVL|SCDOriginalID|  
|Fecha finalización de DVL|SCDEndDate|  
|Fecha inicio de DVL|SCDStartDate|  
|Estado de SCD|SCDStatus|  
  
 La casilla **Es una dimensión variable** se activa de forma predeterminada si se usa una plantilla que tenga definidos estos atributos de dimensión de variación lenta. Si se desactiva la casilla, los atributos de dimensión variable lenta se eliminan de la dimensión.  
  
 Puede usar el Diseñador de dimensiones para configurar las propiedades de una dimensión variable lenta.  
  
## <a name="completing-the-dimension-wizard"></a>Completar el Asistente para dimensiones  
 En la página **Finalización del asistente** , escriba un nombre para la nueva dimensión y consulte la estructura de la dimensión. Active la casilla **Generar el esquema ahora** para iniciar el Asistente para generar esquemas después de hacer clic en **Finalizar**. En la mayoría de los casos, no se debe activar esta casilla si piensa crear objetos adicionales. Si no activa esta casilla, se puede usar el Diseñador de dimensiones para generar el esquema más adelante.  
  
## <a name="see-also"></a>Vea también  
 [Crear una dimensión de tiempo generando una tabla de tiempos](create-a-time-dimension-by-generating-a-time-table.md)   
 [Crear una dimensión de tiempo generando una tabla de tiempos](create-a-time-dimension-by-generating-a-time-table.md)  
  
  
