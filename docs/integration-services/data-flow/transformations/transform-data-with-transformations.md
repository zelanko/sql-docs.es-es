---
title: Transformar datos con transformaciones | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- data flow [Integration Services], transformations
- transformations [Integration Services], about transformations
- transforming data [Integration Services]
ms.assetid: e1340b6f-ef75-4b14-af6f-823586eff0ed
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 6573534c2117192efcb3a40c848e72e0a39d0426
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47610773"
---
# <a name="transform-data-with-transformations"></a>Transformar datos con transformaciones
  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] incluye tres tipos de componentes de flujo de datos: orígenes, transformaciones y destinos.  
  
 El siguiente diagrama muestra un flujo de datos simple que tiene un origen, dos transformaciones y un destino.  
  
 ![Data flow](../../../integration-services/data-flow/media/mw-dts-08.gif "Data flow")  
  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] ofrecen la siguiente funcionalidad:  
  
-   Dividir, copiar y combinar conjuntos de filas y realizar operaciones de búsqueda.  
  
-   Actualizar valores de columnas y crear nuevas columnas aplicando transformaciones tales como cambio de minúsculas por mayúsculas.  
  
-   Operaciones de inteligencia empresarial tales como limpiar datos, realizar minería de texto y ejecutar consultas de predicción de minería de datos.  
  
-   Crear nuevos conjuntos de filas que se componen de valores agregados u ordenados, datos de muestra o datos dinamizados y de anulación de dinamización.  
  
-   Realizar tareas tales como exportar e importar datos, proporcionar información de auditoría y trabajar con dimensiones de variación lenta.  
  
 Para más información, consulte [Integration Services Transformations](../../../integration-services/data-flow/transformations/integration-services-transformations.md).  
  
 También puede escribir transformaciones personalizadas. Para más información, vea [Desarrollar un componente de flujo de datos personalizado](../../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md) y [Desarrollar tipos específicos de componentes de flujo de datos](../../../integration-services/extending-packages-custom-objects-data-flow-types/developing-specific-types-of-data-flow-components.md).  
  
 Después de agregar la transformación al diseñador de flujo de datos, pero antes de configurar la transformación, debe conectar la transformación al flujo de datos conectando la salida de otra transformación u origen del flujo de datos a la entrada de esta transformación. El conector entre dos componentes de flujo de datos se denomina ruta. Para más información sobre la conexión de componentes y el trabajo con rutas, vea [Conectar componentes con rutas de acceso](http://msdn.microsoft.com/library/05633e4c-1370-4b05-802b-f36b07dd71c8).  
  
### <a name="to-add-a-transformation-to-a-data-flow"></a>Para agregar una transformación a un flujo de datos  
  
-   [Agregar o eliminar un componente en un flujo de datos](../../../integration-services/data-flow/add-or-delete-a-component-in-a-data-flow.md)  
  
### <a name="to-connect-a-transformation-to-a-data-flow"></a>Para conectar una transformación a un flujo de datos  
  
-   [Conectar componentes de un flujo de datos](../../../integration-services/data-flow/connect-components-in-a-data-flow.md)  
  
### <a name="to-set-the-properties-of-a-transformation"></a>Para establecer las propiedades de una transformación  
  
-   [Establecer las propiedades de un componente de flujo de datos](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="see-also"></a>Ver también  
 [Tarea Flujo de datos](../../../integration-services/control-flow/data-flow-task.md)   
 [Flujo de datos](../../../integration-services/data-flow/data-flow.md)   
 [Conectar componentes con rutas de acceso](http://msdn.microsoft.com/library/05633e4c-1370-4b05-802b-f36b07dd71c8)   
 [Control de errores en los datos](../../../integration-services/data-flow/error-handling-in-data.md)   
 [Flujo de datos](../../../integration-services/data-flow/data-flow.md)  
  
  
