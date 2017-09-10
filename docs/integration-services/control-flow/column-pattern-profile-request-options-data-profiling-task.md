---
title: "Opciones de solicitud de perfil de patrón de columna (tarea de generación de perfiles de datos) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: 9ccb8fc5-f65e-41a2-9511-7fa55586eb8b
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 05976158e43d7dfafaf02289462d1537f5beeb36
ms.openlocfilehash: e718e67c8756d691338a614c775c2ff71df4b06c
ms.contentlocale: es-es
ms.lasthandoff: 09/08/2017

---
# <a name="column-pattern-profile-request-options-data-profiling-task"></a>Opciones de Solicitud de perfil de patrón de columnas (tarea de generación de perfiles de datos)
  Utilice el panel **Propiedades de la solicitud** de la página **Solicitudes de perfil** para establecer las opciones de **Solicitud de perfil de patrón de columnas** seleccionadas en el panel de solicitudes. Un perfil de patrón de columnas notifica un conjunto de expresiones regulares que cubren el porcentaje especificado de valores en una columna de cadenas. Este perfil puede ayudarle a identificar problemas en los datos, como cadenas no válidas, y puede sugerir expresiones regulares que se pueden utilizar en el futuro para validar los valores nuevos. Por ejemplo, un perfil de patrón de una columna de códigos postales de Estados Unidos podría generar las expresiones regulares \d{5}-\d{4}, \d{5} y \d{9}. Si ve otras expresiones regulares, es posible que los datos contengan valores no válidos o tengan un formato incorrecto.  
  
> [!NOTE]  
>  Las opciones que se describen en este tema aparecen en la página **Solicitudes de perfil** del **Editor de tareas de generación de perfiles de datos**. Para obtener más información sobre esta página del editor, vea [Editor de tareas de generación de perfiles de datos &#40;página Solicitudes de perfil&#41;](../../integration-services/control-flow/data-profiling-task-editor-profile-requests-page.md).  
  
 Para obtener más información sobre cómo usar la tarea de generación de perfiles de datos, vea [Configuración de la Tarea de generación de perfiles de datos](../../integration-services/control-flow/setup-of-the-data-profiling-task.md). Para obtener más información sobre cómo usar el Visor de perfil de datos para analizar la salida de la tarea de generación de perfiles de datos, vea [Visor de perfil de datos](../../integration-services/control-flow/data-profile-viewer.md).  
  
## <a name="understanding-the-use-of-delimiters-and-symbols"></a>Uso de delimitadores y símbolos  
 Antes de calcular los patrones para una **Solicitud de perfil de patrón de columnas**, la tarea de generación de perfiles de datos divide los datos en tokens. Es decir, la tarea separa los valores de cadena en unidades más pequeñas que se conocen como tokens. La tarea separa las cadenas en tokens según los delimitadores y los símbolos que se especifiquen para las propiedades **Delimiters** y **Symbols** :  
  
-   **Delimiters** De forma predeterminada, la lista de delimitadores contiene los caracteres siguientes: espacio, tabulador horizontal (\t), nueva línea (\n) y retorno de carro (\r). Puede especificar delimitadores adicionales, pero no puede quitar los predeterminados.  
  
-   **Símbolos** de forma predeterminada, la lista de **símbolos** contiene los siguientes caracteres: `,.;:-"'~=&/@!?()<>[]{}|#*^%`. Por ejemplo, si los símbolos son "`()-`", el valor"(425) 123-4567" se convierte en ["(", "425", ")", "123", "-", "4567", ")"].  
  
 Un carácter no puede ser delimitador y símbolo a la vez.  
  
 Todos los delimitadores se normalizan en un espacio como parte del proceso de división en tokens, mientras que los símbolos se conservan.  
  
## <a name="understanding-the-use-of-the-tag-table"></a>Uso de la tabla de etiquetas  
 Si lo desea, puede agrupar los tokens relacionados con una etiqueta única almacenando las etiquetas y los términos relacionados en una tabla especial que cree en una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . La tabla de etiquetas debe tener dos columnas de cadena, una denominada "Etiqueta" y la otra "Término". Estas columnas pueden ser de tipo **char**, **nchar**, **varchar**o **nvarchar**, pero no **text** ni **ntext**. Puede combinar varias etiquetas y los términos correspondientes en una única tabla. Una solicitud de perfil de patrón de columnas puede utilizar solo una tabla de etiquetas. Puede utilizar un administrador de conexiones de [!INCLUDE[vstecado](../../includes/vstecado-md.md)] independiente para conectarse a la tabla de etiquetas. Por consiguiente, la tabla de etiquetas se puede encontrar en una base de datos o en un servidor diferente al de los datos de origen.  
  
 Por ejemplo, podría agrupar los valores "Este", "Oeste", "Norte" y "Sur" que podrían aparecer en direcciones mediante la etiqueta única "Dirección". La tabla siguiente es un ejemplo de este tipo de tabla de etiquetas.  
  
|Etiqueta|Término|  
|---------|----------|  
|Dirección|East|  
|Dirección|West|  
|Dirección|North|  
|Dirección|South|  
  
 Podría utilizar otra etiqueta para agrupar las diferentes palabras que expresan la noción de "calle" en una dirección:  
  
|Etiqueta|Término|  
|---------|----------|  
|Calle|Calle|  
|Calle|Avenida|  
|Calle|Lugar|  
|Calle|Vía|  
  
 Según esta combinación de etiquetas, el patrón resultante para una dirección podría parecerse al siguiente:  
  
 `\d+\ LookupTag=Direction \d+\p{L}+\ LookupTag=Street`  
  
> [!NOTE]  
>  El uso de una tabla de etiquetas disminuye el rendimiento de la tarea de generación de perfiles de datos. No utilice más de 10 etiquetas o más de 100 términos por cada etiqueta.  
  
 El mismo término puede pertenecer a más de una etiqueta.  
  
## <a name="request-properties-options"></a>Opciones de Propiedades de la solicitud  
 Para cada **Solicitud de perfil de patrón de columnas**, el panel **Propiedades de la solicitud** muestra los grupos de opciones siguientes:  
  
-   **Data**, que incluye las opciones **TableOrView** y **Column**  
  
-   **General**  
  
-   **Opciones**  
  
### <a name="data-options"></a>Opciones de Data  
 **ConnectionManager**  
 Seleccione el administrador de conexiones de [!INCLUDE[vstecado](../../includes/vstecado-md.md)] existente que usa el proveedor de datos .NET para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) para conectarse a la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contiene la tabla o la vista con la que se generará el perfil.  
  
 **TableOrView**  
 Seleccione la tabla o vista existente que contenga la columna de la que se va a generar un perfil.  
  
 Para obtener más información, vea la sección "Opciones de TableorView" en este tema.  
  
 **Column**  
 Seleccione la columna existente de la que se va a generar un perfil. Seleccione **(\*)** para generar un perfil de todas las columnas.  
  
 Para obtener más información, vea la sección "Opciones de Column" en este tema.  
  
#### <a name="tableorview-options"></a>Opciones de TableOrView  
 **Esquema**  
 Especifica el esquema al que pertenece la tabla seleccionada. Esta opción es de solo lectura.  
  
 **Table**  
 Muestra el nombre de la tabla seleccionada. Esta opción es de solo lectura.  
  
#### <a name="column-options"></a>Opciones de Column  
 **IsWildCard**  
 Especifica si se ha seleccionado el carácter comodín **(\*)**. Esta opción está establecida en **True** si ha seleccionado **(\*)** para generar un perfil de todas las columnas. Es **False** si ha seleccionado una columna individual para la que generar un perfil. Esta opción es de solo lectura.  
  
 **ColumnName**  
 Muestra el nombre de la columna seleccionada. Esta opción está en blanco si ha seleccionado **(\*)** para generar un perfil de todas las columnas. Esta opción es de solo lectura.  
  
 **StringCompareOptions**  
 Esta opción no se aplica al perfil de patrón de columnas.  
  
### <a name="general-options"></a>Opciones de General  
 **IdSolicitud**  
 Escriba un nombre descriptivo para identificar esta solicitud de perfil. Generalmente, no tiene que cambiar el valor generado automáticamente.  
  
### <a name="options"></a>Opciones  
 **MaxNumberOfPatterns**  
 Especifique el número máximo de patrones que desea que calcule el perfil. El valor predeterminado de esta opción es 10. El valor máximo es 100.  
  
 **PercentageDataCoverageDesired**  
 Especifique el porcentaje de los datos que desea que abarquen los patrones calculados. El valor predeterminado de esta opción es 95 (por ciento).  
  
 **CaseSensitive**  
 Indica si los patrones deberían distinguir entre mayúsculas y minúsculas. El valor predeterminado de esta opción es **False**.  
  
 **Delimiters**  
 Muestra los caracteres que se deben tratar como equivalente de espacios entre las palabras al dividir el texto en tokens. De forma predeterminada, la lista **Delimiters** contiene los caracteres siguientes: espacio, tabulador horizontal (\t), nueva línea (\n) y retorno de carro (\r). Puede especificar delimitadores adicionales, pero no puede quitar los predeterminados.  
  
 Para obtener más información al respecto, vea "Uso de delimitadores y símbolos" anteriormente en este tema.  
  
 **Symbols**  
 Muestra los símbolos que se deberían conservar como parte de los patrones. Algunos ejemplos podrían incluir "/" para las fechas, ":" para las horas  y "@" para las direcciones de correo electrónico. De forma predeterminada, la lista **Symbols** contiene los caracteres siguientes: `,.;:-"'`~=&/@!?()<>[]{}|#*^%`.  
  
 Para obtener más información al respecto, vea "Uso de delimitadores y símbolos" anteriormente en este tema.  
  
 **TagTableConnectionManager**  
 Seleccione el administrador de conexiones de [!INCLUDE[vstecado](../../includes/vstecado-md.md)] existente que usa el Proveedor de datos .NET para que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) se conecte a la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contiene la tabla de etiquetas.  
  
 Para obtener más información al respecto, vea "Uso de la tabla de etiquetas" anteriormente en este tema.  
  
 **TagTableName**  
 Seleccione la tabla de etiquetas existente, que debe tener dos columnas de cadenas denominadas Etiqueta y Término.  
  
 Para obtener más información al respecto, vea "Uso de la tabla de etiquetas" anteriormente en este tema.  
  
## <a name="see-also"></a>Vea también  
 [Editor de tareas de generación de perfiles de datos &#40;página General&#41;](../../integration-services/control-flow/data-profiling-task-editor-general-page.md)   
 [Formulario de perfil rápido de tabla única &#40; datos de generación de perfiles de tarea &#41;](../../integration-services/control-flow/single-table-quick-profile-form-data-profiling-task.md)  
  
  

