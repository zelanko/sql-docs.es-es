---
title: Propiedades de flujo de datos que se pueden establecer mediante expresiones | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SQL Server Integration Services packages, property expressions
- Integration Services packages, property expressions
- packages [Integration Services], properties
- SSIS packages, property expressions
- property expressions [Integration Services]
ms.assetid: cd0e171a-08be-45d6-81dc-ed94f37698b8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f70a956834108c21dd7b17bb9f3e04db38f29bfa
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66059939"
---
# <a name="data-flow-properties-that-can-be-set-by-using-expressions"></a>Propiedades de flujo de datos que se pueden establecer utilizando expresiones
  Los valores de ciertas propiedades de objetos de flujo de datos se pueden especificar utilizando expresiones de propiedades disponibles en el contenedor de tareas Flujo de Datos.  
  
 Para obtener información sobre el uso de expresiones de propiedades, vea [Usar expresiones de propiedad en paquetes](expressions/use-property-expressions-in-packages.md).  
  
 Puede utilizar las expresiones de propiedades para personalizar las configuraciones de cada instancia implementada de un paquete. También puede usar expresiones de propiedades para especificar restricciones en tiempo de ejecución para un paquete mediante la opción **/set** con la utilidad de símbolo del sistema **dtexec** . Por ejemplo, puede restringir el `MaximumThreads` utilizado por la transformación Ordenación o bien el `MaxMemoryUsage` de las transformaciones Fuzzy Grouping y Fuzzy Lookup. Si no presentan restricciones, estas transformaciones pueden almacenar en memoria caché grandes cantidades de datos en memoria.  
  
 Para especificar una expresión de propiedades para una de las propiedades de los objetos de flujo de datos mencionados en este tema, muestre la ventana **Propiedades** para la tarea Flujo de Datos seleccionando la tarea Flujo de Datos en la superficie **Flujo de control** del diseñador o seleccionando la pestaña **Flujo de datos** del diseñador sin seleccionar ningún componente o ruta de acceso individual. Seleccione la propiedad **Expresiones** y haga clic en los puntos suspensivos (…) para mostrar el cuadro de diálogo **Editor de expresiones de propiedad** . Despliegue la lista **Propiedad** para seleccionar una propiedad y, después, escriba una expresión en el cuadro de texto **Expresión** o haga clic en los puntos suspensivos (…) para mostrar el cuadro de diálogo **Generador de expresiones** .  
  
 La lista **Propiedad** muestra las propiedades disponibles solo para aquellos objetos de flujo de datos que ya haya colocado en la superficie **Flujo de datos** del diseñador. Por consiguiente, no puede utilizar la lista **Propiedad** para ver todas las posibles propiedades de los objetos de flujo de datos que admiten expresiones de propiedades. Por ejemplo, si ha colocado un origen de ADO NET en la superficie del diseñador, la lista de **propiedades** contiene una entrada `[ADO NET Source].[SqlCommand]` para la propiedad. La lista también muestra muchas propiedades de la propia tarea Flujo de Datos.  
  
## <a name="properties-of-data-flow-objects-that-support-property-expressions"></a>Propiedades de objetos de flujo de datos que admiten las expresiones de propiedades  
 Los valores de las propiedades de la siguiente lista se pueden especificar mediante expresiones de propiedades.  
  
### <a name="data-flow-sources"></a>Orígenes de flujo de datos  
  
|Objeto Flujo de datos|Propiedad|  
|----------------------|--------------|  
|Origen ADO NET|Propiedad TableOrViewName<br /><br /> Propiedad SQLCommand|  
|Origen XML|Propiedad XMLData<br /><br /> Propiedad XMLSchemaDefinition|  
  
### <a name="data-flow-transformations"></a>Transformaciones Flujo de datos  
 Para obtener más información acerca de estas propiedades personalizadas, vea [Transformation Custom Properties](data-flow/transformations/transformation-custom-properties.md).  
  
|Objeto Flujo de datos|Propiedad|  
|----------------------|--------------|  
|División condicional, transformación|Propiedad FriendlyExpression|  
|Transformación Columna derivada|Propiedad FriendlyExpression|  
|Agrupación aproximada, transformación|Propiedad MaxMemoryUsage|  
|Búsqueda aproximada, transformación|Propiedad MaxMemoryUsage|  
|Transformación de búsqueda|Propiedad SQLCommand<br /><br /> Propiedad SqlCommandParam|  
|transformación Comando de OLE DB|Propiedad SQLCommand|  
|Muestreo de porcentaje, transformación|Propiedad SamplingValue|  
|Dinámica, transformación|Propiedad PivotKeyValue|  
|Muestreo de fila, transformación|Propiedad SamplingValue|  
|Ordenar, transformación|Propiedad MaximumThreads|  
|Anulación de dinamización, transformación|Propiedad PivotKeyValue|  
  
### <a name="data-flow-destinations"></a>Destinos de flujo de datos  
  
|Objeto Flujo de datos|Propiedad|  
|----------------------|--------------|  
|Destino ADO NET|Propiedad TableOrViewName<br /><br /> Propiedad BatchSize<br /><br /> Propiedad CommandTimeOut|  
|Destino de archivo plano|Propiedad Header|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Destino de Compact|Propiedad TableName|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]destino|Propiedad BulkInsertTableName<br /><br /> Propiedad BulkInsertFirstRow<br /><br /> Propiedad BulkInsertLastRow<br /><br /> Propiedad BulkInsertOrder<br /><br /> Propiedad Tiempo de espera|  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Agregar o cambiar una expresión de propiedad](expressions/add-or-change-a-property-expression.md)  
  
## <a name="related-content"></a>Contenido relacionado  
 Artículo técnico, sobre la [referencia rápida de expresiones de SSIS](https://pragmaticworks.com/Resources/Cheat-Sheets/SSIS-Expression-Cheat-Sheet), en pragmaticworks.com  
  
## <a name="see-also"></a>Consulte también  
 [Usar expresiones de propiedad en paquetes](expressions/use-property-expressions-in-packages.md)   
 [Propiedades comunes](../../2014/integration-services/common-properties.md)   
 [Propiedades personalizadas de la transformación](data-flow/transformations/transformation-custom-properties.md)   
 [Propiedades de la ruta de acceso](../../2014/integration-services/path-properties.md)  
  
  
