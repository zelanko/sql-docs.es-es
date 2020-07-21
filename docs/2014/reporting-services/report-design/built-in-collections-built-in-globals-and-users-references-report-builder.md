---
title: Referencias a campos globales y de usuario integrados (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 5f5e1149-c967-454d-9a63-18ec4a33d985
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ef0438dfa0750c2a516a801a2d81b5d1c0b49721
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66106437"
---
# <a name="built-in-globals-and-users-references-report-builder-and-ssrs"></a>Referencias a campos globales y de usuario integrados (Generador de informes y SSRS)
  La colección de campos integrados, que incluye las colecciones `Globals` y `User`, representa valores globales proporcionados por Reporting Services al procesar un informe. La colección `Globals` proporciona valores como el nombre del informe, la hora a la que comenzó el procesamiento del informe y el número de la página actual para el encabezado o el pie de página del informe. La colección `User` proporciona el identificador de usuario y la configuración de idioma. Estos valores se pueden usar en expresiones para filtrar los resultados de un informe.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="using-the-globals-collection"></a>Usar la colección Globals  
 La colección `Globals` contiene las variables globales del informe. En la superficie de diseño, estas variables aparecen con el prefijo & (y comercial); por ejemplo, `[&ReportName]`. En la siguiente tabla, se describen los miembros de la colección `Globals`.  
  
|**Miembro**|**Tipo**|**Descripción**|  
|----------------|--------------|---------------------|  
|ExecutionTime|`DateTime`|Fecha y hora en que se empezó a ejecutar el informe.|  
|PageNumber|`Integer`|Número de página actual relativo a los saltos de página que restablecieron el número de página. Al principio del procesamiento del informe, el valor inicial está establecido en 1. El número de página aumenta en cada página representada.<br /><br /> Para numerar las páginas dentro de los saltos de página para un rectángulo, una región de datos, un grupo de regiones de datos o un mapa, en la `True`propiedad PageBreak, establezca la propiedad ResetPageNumber en. No se admite en grupos de jerarquías de columnas de Tablix.<br /><br /> PageNumber solo se puede usar en una expresión en un encabezado o pie de página.|  
|ReportFolder|`String`|Ruta de acceso completa a la carpeta en la que se halla el informe. No incluye la dirección URL del servidor de informes.|  
|ReportName|`String`|Nombre del informe tal como se almacena en la base de datos del servidor de informes.|  
|ReportServerUrl|`String`|Dirección URL del servidor de informes en el que se ejecuta el informe.|  
|TotalPages|`Integer`|Número total de páginas relativo a los saltos de página que restablecen PageNumber. Si no se establece ningún salto de página, este valor es igual que OverallTotalPages.<br /><br /> TotalPages solo se puede usar en una expresión en un encabezado o pie de página.|  
|PageName|`String`|Nombre de la página. Al comenzar el procesamiento del informe, el valor inicial se establece desde InitialPageName, una propiedad de informe. Cuando se procesa cada elemento de informe, el valor correspondiente de PageName reemplaza este valor de un rectángulo, una región de datos, un grupo de regiones de datos o una asignación. No se admite en grupos de jerarquías de columnas de Tablix.<br /><br /> PageName solo se puede usar en una expresión en un encabezado o pie de página.|  
|OverallPageNumber|`Integer`|Número de página de la página actual para el informe completo. ResetPageNumber no afecta a este valor.<br /><br /> OverallPageNumber solo se puede usar en una expresión en un encabezado o pie de página.|  
|OverallTotalPages|`Integer`|Número total de páginas de todo el informe. ResetPageNumber no afecta a este valor.<br /><br /> OverallTotalPages solo se puede usar en una expresión en un encabezado o pie de página.|  
|RenderFormat|`RenderFormat`|Información sobre la solicitud de representación actual.<br /><br /> Para obtener más información, vea la sección "RenderFormat" más adelante.|  
  
 Los miembros de la colección `Globals` devuelven datos de tipo variant. Si desea usar un miembro de esta colección en una expresión que requiere un tipo de datos específico, primero deberá convertir la variable. Por ejemplo, para convertir los datos de tipo variant de la fecha y hora de ejecución a formato de fecha, utilice `=CDate(Globals!ExecutionTime)`. Para obtener más información, vea [Tipos de datos en expresiones &#40;Generador de informes y SSRS&#41;](expressions-report-builder-and-ssrs.md).  
  
### <a name="renderformat"></a>RenderFormat  
 En esta tabla se describen los miembros de `RenderFormat`.  
  
|Member|Tipo|Descripción|  
|------------|----------|-----------------|  
|Nombre|`String`|Nombre del representador como está registrado en el archivo de configuración de RSReportServer.<br /><br /> Está disponible durante el ciclo de procesamiento o representación de partes concretas del informe.|  
|IsInteractive|`Boolean`|Si la solicitud de representación actual utiliza un formato de representación interactivo.|  
|DeviceInfo|Colección nombre/valor de solo lectura|Pares clave/valor para los parámetros de deviceinfo para la solicitud de representación actual.<br /><br /> Los valores de cadena se pueden especificar utilizando la clave o un índice en la colección.|  
  
### <a name="examples"></a>Ejemplos  
 En los ejemplos siguientes se muestra cómo usar una referencia a la colección `Globals` en una expresión:  
  
-   Esta expresión, ubicada en un cuadro de texto en el pie de página de un informe, devuelve el número de página y el número total de páginas del informe:  
  
     `=Globals.PageNumber & " of " & Globals.TotalPages`  
  
-   Esta expresión devuelve el nombre del informe y la hora a la que se ejecutó. A la hora se le aplica [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] formato con la cadena de formato para la fecha corta:  
  
     `=Globals.ReportName & ", dated " & Format(Globals.ExecutionTime, "d")`  
  
-   Esta expresión, ubicada en el cuadro de diálogo **Visibilidad de columna** para una columna seleccionada, muestra la columna solo cuando el informe se exporta a Excel. De lo contrario, la columna está oculta.  
  
     `EXCELOPENXML` hace referencia al formato de Excel que se incluye en Office 2007. `EXCEL` hace referencia al formato de Excel que se incluye en Office 2003.  
  
     `=IIF(Globals!RenderFormat.Name = "EXCELOPENXML" OR Globals!RenderFormat.Name = "EXCEL", false, true)`  
  
## <a name="using-the-user-collection"></a>Usar la colección User  
 La colección `User` contiene datos acerca del usuario que ejecuta el informe. Puede usar esta colección para filtrar los datos que aparecen en un informe; por ejemplo, para mostrar solo los datos del usuario actual o para mostrar el identificador de usuario (UserID) en el título de un informe. En la superficie de diseño, estas variables aparecen con el prefijo & (y comercial); por ejemplo, `[&UserID]`.  
  
 En la siguiente tabla, se describen los miembros de la colección `User`.  
  
|**Member**|**Tipo**|**Descripción**|  
|----------------|--------------|---------------------|  
|`Language`|`String`|Idioma del usuario que ejecuta el informe. Por ejemplo: `en-US`.|  
|`UserID`|`String`|Identificador del usuario que ejecuta el informe. Si está utilizando la autenticación de Windows, este valor será la cuenta de dominio del usuario actual. El valor viene determinado por la extensión de seguridad de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , que puede utilizar la autenticación de Windows o una autenticación personalizada.|  
  
 Para obtener más información sobre el uso de varios idiomas en un informe, vea "Consideraciones de diseño de soluciones para las implementaciones plurilingües o globales" en la documentación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en los [Libros en pantalla de SQL Server](https://go.microsoft.com/fwlink/?LinkId=120955).  
  
### <a name="using-locale-settings"></a>Usar la configuración regional  
 Para determinar la apariencia de un informe, puede usar expresiones que hagan referencia a la configuración regional en un equipo cliente mediante el valor de `User.Language`. Por ejemplo, puede crear un informe que utilice una expresión de consulta diferente basada en el valor de configuración regional. La consulta puede cambiar para obtener información traducida de otra columna según el idioma devuelto. También se puede utilizar una expresión en la configuración de idioma del informe o elementos del informe basados en esta variable.  
  
> [!NOTE]  
>  Aunque es posible cambiar la configuración de idioma de un informe, es preciso ser muy consciente de los problemas de visualización que esto puede provocar. Por ejemplo, si se cambia la configuración regional de un informe, puede cambiar no solo el formato de fecha del informe, sino también el formato de moneda. A menos que exista algún proceso de conversión de moneda, este cambio puede provocar que el informe muestre un símbolo de moneda incorrecto. Para evitar esta situación, establezca la información de idioma en cada uno de los elementos que desee cambiar, o establezca el elemento con los datos de moneda en un idioma determinado.  
  
### <a name="identifying-userid-for-snapshot-or-history-reports"></a>Identificar el identificador de usuario para informes de historial o instantánea  
 En algunas ocasiones, los informes que incluyen la variable *User!UserID* no podrán mostrar los datos de informe específicos del usuario que está viendo el informe en ese momento.  
  
## <a name="see-also"></a>Consulte también  
 [Expresiones &#40;Generador de informes y SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Cuadro de diálogo expresión &#40;Generador de informes&#41;](../expression-dialog-box-report-builder.md)   
 [Tipos de datos en expresiones &#40;Generador de informes y SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Aplicar formato a números y fechas &#40;Generador de informes y SSRS&#41;](formatting-numbers-and-dates-report-builder-and-ssrs.md)   
 [Ejemplos de expresiones &#40;Generador de informes y SSRS&#41;](expression-examples-report-builder-and-ssrs.md)  
  
  
