---
title: "Transformación dimensión de variación lenta | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.slowlychangingdimtrans.f1
helpviewer_keywords:
- Slowly Changing Dimension transformation
- slowly changing dimensions
- SCD transformation
- updating slowly changing dimensions
ms.assetid: f8849151-c171-4725-bd25-f2c33a40f4fe
caps.latest.revision: 55
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 59f467f9aee0637bc9463c39b51b30e47eeaff47
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="slowly-changing-dimension-transformation"></a>Transformación Dimensión de variación lenta
  La transformación Dimensión de variación lenta coordina la actualización e inserción de registros en las tablas de dimensiones de almacenamiento de datos. Por ejemplo, puede usar esta transformación para configurar las salidas de transformación que insertan y actualizan registros en la tabla DimProduct de la base de datos [!INCLUDE[ssSampleDBDWobject](../../../includes/sssampledbdwobject-md.md)] con datos de la tabla Production.Products de la base de datos OLTP AdventureWorks.  
  
> [!IMPORTANT]  
>  El Asistente para dimensiones de variación lenta solo admite las conexiones a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 La transformación Dimensión de variación lenta proporciona la siguiente funcionalidad para administrar dimensiones variables lentas:  
  
-   Hacer coincidir filas entrantes con filas de la tabla de búsqueda para identificar filas nuevas y existentes.  
  
-   Identificar las filas entrantes que contienen cambios cuando no se permiten cambios.  
  
-   Identificar registros de miembros deducidos que requieren actualización.  
  
-   Identificar filas entrantes que contienen cambios históricos que requieren la inserción de nuevos registros y la actualización de registros expirados.  
  
-   Detección de filas entrantes que contienen cambios que requieren la actualización de los registros existentes, incluyendo los expirados.  
  
 La transformación Dimensión de variación lenta admite cuatro tipos de cambios: atributo variable, atributo histórico, atributo fijo y miembro deducido.  
  
-   Los cambios de atributo variable sobrescriben los registros existentes. Este tipo de cambio es equivalente a un cambio del Tipo 1. La transformación Dimensión de variación lenta dirige estas filas a una salida llamada **Salida de actualizaciones de atributos variables**.  
  
-   Los cambios de atributo histórico crean nuevos registros en lugar de actualizar registros existentes. El único cambio que se permite en un registro existente es una actualización a una columna que indica si el registro está actualizado o expirado. Este tipo de cambio es equivalente a un cambio del tipo 2. La transformación Dimensión de variación lenta dirige estas filas a dos salidas: **Salida de inserciones de atributos históricos** y **Nueva salida**.  
  
-   Los cambios de atributo fijo indican que el valor de la columna no debe cambiar. La transformación Dimensión de variación lenta detecta cambios y puede dirigir las filas con cambios a una salida llamada **Salida de atributo fijo**.  
  
-   Un miembro deducido indica que la fila es un registro de miembro deducido en la tabla de dimensiones. Existe un miembro deducido cuando una tabla de hechos hace referencia a un miembro de dimensión que todavía no se han cargado. Un registro de miembro deducido mínimo se crea antes de los datos de dimensiones relevantes, que se proporcionan en una carga posterior de los datos de dimensiones. La transformación Dimensión de variación lenta dirige estas filas a una salida llamada **Salida de actualizaciones de miembros deducidos**. Cuando se cargan datos del miembro deducido, se puede actualizar el registro existente en lugar de crear uno nuevo.  
  
> [!NOTE]  
>  La transformación Dimensión de variación lenta no admite los cambios de tipo 3, que requieren cambios en la tabla de dimensiones. Al identificar columnas con el tipo de actualización de atributo fijo, puede capturar los valores de los datos que son candidatos para cambios del tipo 3.  
  
 En el tiempo de ejecución, la transformación Dimensión de variación lenta en primer lugar intenta hacer coincidir la fila entrante con un registro en la tabla de búsqueda. Si no se encuentran coincidencias, la fila entrante es un nuevo registro, por tanto la transformación Dimensión de variación lenta no realiza otro trabajo y dirige la fila a **Nueva salida**.  
  
 Si se encuentra una coincidencia, la transformación Dimensión de variación lenta detecta si la fila contiene cambios. Si la fila contiene cambios, la transformación Dimensión de variación lenta identifica el tipo de actualización para cada columna y dirige la fila a la **Salida de actualizaciones de atributos variables**, **Salida de atributo fijo**, **Salida de inserciones de atributos históricos**o **Salida de actualizaciones de miembros deducidos**. Si no hay cambios en la fila, la transformación Dimensión de variación lenta dirige la fila a la **Salida sin cambios**.  
  
## <a name="slowly-changing-dimension-transformation-outputs"></a>Salidas de la transformación Dimensión de variación lenta  
 La transformación Dimensión de variación lenta tiene una entrada y hasta seis salidas. Una salida dirige una fila al subconjunto del flujo de datos que corresponde a la actualización y los requisitos de inserción de la fila. Esta transformación no admite una salida de error.  
  
 La siguiente tabla describe las salidas de la transformación y los requisitos de sus flujos de datos posteriores. Los requisitos describen el flujo de datos que crea el Asistente para dimensiones variables.  
  
|Salida|Description|Requisitos de flujo de datos|  
|------------|-----------------|----------------------------|  
|**Salida de actualizaciones de atributos variables**|El registro de la tabla de búsqueda se actualiza. Esta salida se usa para filas de atributos variables.|Una transformación Comando de OLE DB actualiza el registro mediante una instrucción UPDATE.|  
|**Salida de atributo fijo**|Los valores en las filas que no deben cambiar no coinciden con los valores de la tabla de búsqueda. Esta salida se usa para filas de atributos fijos.|No se crea un flujo de datos predeterminado. Si la transformación se configura para continuar después de encontrar cambios en columnas de atributos fijos, debe crear un flujo de datos que capture estas filas.|  
|**Salida de inserciones de atributos históricos**|La tabla de búsqueda contiene como mínimo una fila coincidente. La fila marcada como "actual" se debe marcar ahora como "expirada". Esta salida se usa para filas de atributos históricos.|Las transformaciones de Columna derivada crean columnas para la fila expirada y los indicadores de fila actual. Una transformación Comando de OLE DB actualiza el valor que se debe marcar como "expirado". La fila con los nuevos valores de columna se dirige a Nueva salida, en la que la fila se inserta y marca como "actual".|  
|**Salida de actualizaciones de miembros deducidos**|Se insertan filas para miembros de dimensión deducidos. Esta salida se usa para filas de miembros deducidos.|Una transformación Comando de OLE DB actualiza el registro mediante una instrucción SQL UPDATE.|  
|**Nueva salida**|La tabla de búsqueda no contiene filas coincidentes. La fila se agrega a la tabla de dimensiones. Esta salida se usa para nuevas filas y cambios en las filas de atributos históricos.|Una transformación Columna derivada establece el indicador de fila actual, y un destino de OLE DB inserta la fila.|  
|**Salida sin cambios**|Los valores de la tabla de búsqueda coinciden con los valores de la fila. Esta salida se usa para filas sin cambios.|No se crea un flujo de datos predeterminado porque la transformación Dimensión de variación lenta no realiza ningún trabajo. Si desea capturar estas filas, debe crear un flujo de datos para esta salida.|  
  
## <a name="business-keys"></a>Claves empresariales  
 La transformación Dimensión de variación lenta requiere por lo menos una columna de clave empresarial.  
  
 La transformación Dimensión de variación lenta no admite claves empresariales con valor NULL. Si los datos incluyen filas en las que la columna de clave empresarial tiene un valor NULL, estas filas deben quitarse del flujo de datos. Puede usar la transformación División condicional para filtrar filas cuyas columnas de clave empresarial contengan valores NULL. Para más información, consulte [Conditional Split Transformation](../../../integration-services/data-flow/transformations/conditional-split-transformation.md).  
  
## <a name="optimizing-the-performance-of-the-slowly-changing-dimension-transformation"></a>Optimizar el rendimiento de la transformación Dimensión de variación lenta  
 Para obtener sugerencias sobre cómo mejorar el rendimiento de la transformación Dimensión de variación lenta, vea [Características de rendimiento de flujo de datos](../../../integration-services/data-flow/data-flow-performance-features.md).  
  
## <a name="troubleshooting-the-slowly-changing-dimension-transformation"></a>Solucionar problemas de la transformación Dimensión de variación lenta  
 Puede registrar las llamadas realizadas por la transformación Dimensión de variación lenta a proveedores de datos externos. Puede utilizar esta capacidad de registro para solucionar problemas relacionados con las conexiones, los comandos y las consultas a orígenes de datos externos realizados por la transformación Dimensión de variación lenta. Para registrar las llamadas que la transformación Dimensión de variación lenta realiza a proveedores de datos externos, habilite el registro de paquetes y seleccione el evento **Diagnostic** en el nivel de paquete. Para más información, vea [Herramientas para solucionar problemas con la ejecución de paquetes](../../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
## <a name="configuring-the-slowly-changing-dimension-transformation"></a>Configurar la transformación Dimensión de variación lenta  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Propiedades comunes](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propiedades personalizadas de transformación](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Para más información sobre cómo establecer propiedades, vea [Establecer las propiedades de un componente de flujo de datos](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="configuring-the-slowly-changing-dimension-transformation-outputs"></a>Configurar las salidas de la transformación Dimensión de variación lenta  
 Coordinar la actualización e inserción de registros en las tablas de dimensiones puede ser una tarea compleja, especialmente si se usan datos de tipo 1 y 2. [!INCLUDE[ssIS](../../../includes/ssis-md.md)] ofrece dos maneras de configurar las dimensiones de variación lenta:  
  
-   El cuadro de diálogo **Editor avanzado** , en el que se selecciona una conexión, se establecen propiedades de componentes comunes y personalizados, se eligen columnas de entrada y se establecen propiedades de columnas en las seis salidas. Para completar la tarea de configuración de una dimensión de variación lenta, debe crear manualmente el flujo de datos para las salidas que usa la transformación Dimensión de variación lenta. Para más información, consulte [Data Flow](../../../integration-services/data-flow/data-flow.md).  
  
-   Cargar el Asistente para dimensiones, que lo guía por los pasos necesarios para configurar la transformación Dimensión de variación lenta y generar el flujo de datos para las salidas de la transformación. Para cambiar la configuración de las dimensiones de variación lenta, vuelva a ejecutar el Asistente para cargar dimensión. Para más información, vea [Configurar salidas mediante el Asistente para dimensión de variación lenta](../../../integration-services/data-flow/transformations/configure-outputs-using-the-slowly-changing-dimension-wizard.md).  
  
## <a name="related-tasks"></a>Tareas relacionadas  
 [Establecer las propiedades de un componente de flujo de datos](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-content"></a>Contenido relacionado  
  
-   La entrada del blog sobre cómo [optimizar el Asistente para dimensiones de variación lenta](http://go.microsoft.com/fwlink/?LinkId=199481), en blogs.msdn.com.  
  
  

