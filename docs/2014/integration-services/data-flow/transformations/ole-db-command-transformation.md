---
title: Transformación Comando de OLE DB | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.oledbcommandtrans.f1
helpviewer_keywords:
- statements [Integration Services]
- OLE DB Command transformation
ms.assetid: baa6735c-5acf-4759-b077-1216aca16c6c
caps.latest.revision: 55
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 3903585642605114cca4441ea2192d69ef74c1fd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36108383"
---
# <a name="ole-db-command-transformation"></a>transformación Comando de OLE DB
  La transformación Comando de OLE DB ejecuta una instrucción SQL para cada fila en un flujo de datos. Por ejemplo, puede ejecutar una instrucción SQL que inserte, actualice o elimine filas en una tabla de base de datos.  
  
 Puede configurar el administrador de conexiones OLE DB de las maneras siguientes:  
  
-   Proporcionar la instrucción SQL que la transformación ejecuta para cada fila.  
  
-   Especifica la cantidad de segundos que tienen que transcurrir antes de que la instrucción SQL agote el tiempo de espera.  
  
-   Especificar la página de códigos predeterminada.  
  
 Normalmente, la instrucción SQL incluye parámetros. Los valores de parámetro se almacenan en columnas externas en la entrada de transformación y al asignar una columna de entrada a una columna externa se asigna una columna de entrada a un parámetro. Por ejemplo, para buscar filas en la tabla **DimProduct** por el valor de su columna **ProductKey** y luego eliminarlas, puede asignar la columna externa denominada **Param_0** a la columna de entrada denominada **ProductKey** y luego ejecutar la instrucción SQL `DELETE FROM DimProduct WHERE ProductKey = ?`. La transformación Comando de OLE DB proporciona los nombres de parámetro y no puede modificarlos. Los nombres de parámetro son **Param_0**, **Param_1**y así sucesivamente.  
  
 Si configura la transformación Comando de OLE DB mediante el cuadro de diálogo **Editor avanzado** , los parámetros de la instrucción SQL se pueden asignar automáticamente a las columnas externas en la entrada de transformación y las características de cada parámetro se definen haciendo clic en el botón **Actualizar** . Sin embargo, si el proveedor OLE DB que usa la transformación Comando de OLE DB no admite la derivación de la información de parámetros del parámetro, debe configurar las columnas externas manualmente. Esto significa que debe agregar una columna por cada parámetro a la entrada externa a la transformación, actualizar los nombres de columna para que usen nombres como **Param_0**, especificar el valor de la propiedad DBParamInfoFlags y asignar las columnas de entrada que contienen valores de parámetro a las columnas externas.  
  
 El valor de DBParamInfoFlags representa las características del parámetro. Por ejemplo, el valor **1** especifica que el parámetro es un parámetro de entrada, y el valor **65** especifica que el parámetro es un parámetro de entrada y puede contener un valor NULL. Los valores deben coincidir con los valores de la enumeración OLE DB DBPARAMFLAGSENUM. Para obtener más información, vea la documentación de referencia de OLE DB.  
  
 La transformación Comando de OLE DB incluye la propiedad personalizada `SQLCommand`. Esta propiedad se puede actualizar a través de una expresión de propiedad, al cargar el paquete. Para más información, vea [Expresiones de Integration Services &#40;SSIS&#41;](../../expressions/integration-services-ssis-expressions.md), [Usar expresiones de propiedad en paquetes](../../expressions/use-property-expressions-in-packages.md) y [Propiedades personalizadas de transformación](transformation-custom-properties.md).  
  
 Esta transformación tiene una entrada, una salida normal y una salida de error.  
  
## <a name="logging"></a>Registro  
 Puede registrar las llamadas realizadas por la transformación Comando de OLE DB a proveedores de datos externos. Puede utilizar esta capacidad de registro para solucionar problemas relacionados con las conexiones y los comandos a orígenes de datos externos realizados por la transformación Comando de OLE DB. Para registrar las llamadas que la transformación Comando de OLE DB realiza a los proveedores de datos externos, habilite el registro de paquetes y seleccione el evento **Diagnostic** en el nivel de paquete. Para obtener más información, vea [Herramientas para solucionar problemas con la ejecución de paquetes](../../troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
## <a name="related-tasks"></a>Related Tasks  
 Puede configurar la transformación mediante el Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o el modelo de objetos. Para obtener detalles sobre cómo configurar la transformación mediante el Diseñador [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , vea  [Configurar la transformación Comando de OLE DB](../../configure-the-ole-db-command-transformation.md). Vea la Guía del desarrollador para obtener información detallada sobre la configuración mediante programación de esta transformación.  
  
## <a name="see-also"></a>Vea también  
 [Flujo de datos](../data-flow.md)   
 [Transformaciones de Integration Services](integration-services-transformations.md)  
  
  