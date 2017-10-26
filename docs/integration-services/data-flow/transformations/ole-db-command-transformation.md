---
title: "Transformación comando de OLE DB | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.oledbcommandtrans.f1
helpviewer_keywords:
- statements [Integration Services]
- OLE DB Command transformation
ms.assetid: baa6735c-5acf-4759-b077-1216aca16c6c
caps.latest.revision: 55
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 4b557efa62075f7b88e6b70cf5950546444b95d8
ms.openlocfilehash: 99d34e8dd153c5ca1793d14cc9638aab6529a643
ms.contentlocale: es-es
ms.lasthandoff: 08/19/2017

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
  
 La transformación Comando de OLE DB incluye la propiedad personalizada **SQLCommand** . Esta propiedad se puede actualizar a través de una expresión de propiedad, al cargar el paquete. Para más información, vea [Expresiones de Integration Services &#40;SSIS&#41;](../../../integration-services/expressions/integration-services-ssis-expressions.md), [Usar expresiones de propiedad en paquetes](../../../integration-services/expressions/use-property-expressions-in-packages.md) y [Propiedades personalizadas de transformación](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
 Esta transformación tiene una entrada, una salida normal y una salida de error.  
  
## <a name="logging"></a>Registro  
 Puede registrar las llamadas realizadas por la transformación Comando de OLE DB a proveedores de datos externos. Puede utilizar esta capacidad de registro para solucionar problemas relacionados con las conexiones y los comandos a orígenes de datos externos realizados por la transformación Comando de OLE DB. Para registrar las llamadas que la transformación Comando de OLE DB realiza a los proveedores de datos externos, habilite el registro de paquetes y seleccione el evento **Diagnostic** en el nivel de paquete. Para más información, vea [Herramientas para solucionar problemas con la ejecución de paquetes](../../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
## <a name="related-tasks"></a>Tareas relacionadas  
 Puede configurar la transformación mediante el Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o el modelo de objetos. Vea la Guía del desarrollador para obtener información detallada sobre la configuración mediante programación de esta transformación.  
  
## <a name="configure-the-ole-db-command-transformation"></a>Configurar la transformación Comando de OLE DB
  Para agregar y configurar una transformación Comando de OLE DB, el paquete ya debe incluir por lo menos una tarea Flujo de datos y un origen tal como origen de archivo plano y un origen de OLE DB. Esta transformación normalmente se usa para ejecutar consultas con parámetros.  
  
#### <a name="to-configure-the-ole-db-command-transformation"></a>Para configurar la transformación Comando de OLE DB  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  Haga clic en la pestaña **Flujo de datos** y, a continuación, desde el **cuadro de herramientas**, arrastre la transformación Comando de OLE DB a la superficie de diseño.  
  
4.  Conecte la transformación Comando de OLE DB al flujo de datos arrastrando el conector (la flecha verde o roja) desde un origen de datos o una transformación anterior a la transformación Comando de OLE DB.  
  
5.  Haga clic con el botón derecho en el componente y seleccione Editar o Mostrar el **Editor avanzado**.  
  
6.  En la pestaña **Administradores de conexión** , seleccione un administrador de conexiones OLE DB en la lista **Administrador de conexiones** . Para más información, consulte [OLE DB Connection Manager](../../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
7.  Haga clic en la pestaña **Propiedades de componente** y haga clic en el botón de puntos suspensivos **(…)** en el cuadro **Comando SQL** .  
  
8.  En el **Editor de valores de cadena**, escriba la instrucción SQL con parámetros mediante un signo de pregunta (?) como marcador de parámetro para cada parámetro.  
  
9. Haga clic en **Actualizar**. Cuando hace clic en **Actualizar**, la transformación crea una columna para cada parámetro en la colección de columnas externas y establece la propiedad DBParamInfoFlags.  
  
10. Haga clic en la pestaña **Propiedades de entrada y salida** .  
  
11. Expanda **Entrada de comando de OLE DB**y luego expanda **Columnas externas**.  
  
12. Compruebe que **Columnas externas** enumera una columna para cada parámetro en la instrucción SQL. Los nombres de columna son **Param_0**, **Param_1**, etc.  
  
     No debe cambiar los nombres de las columnas. Si lo hace, [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] generará un error de validación para la transformación Comando de OLE DB.  
  
     Además, tampoco debe cambiar el tipo de datos. La propiedad DataType de cada columna se establece en el tipo de datos correcto.  
  
13. Si **Columnas externas** no enumera ninguna columna, debe agregarlas manualmente.  
  
    -   Haga clic en **Agregar columna** una vez por cada parámetro de la instrucción SQL.  
  
    -   Actualice los nombres de columna a **Param_0**, **Param_1**, etc.  
  
    -   Especifique un valor en la propiedad DBParamInfoFlags. El valor debe coincidir con el valor de la enumeración OLE DB DBPARAMFLAGSENUM. Para obtener más información, vea la documentación de referencia de OLE DB.  
  
    -   Especifique el tipo de datos de la columna y, según el tipo de datos, especifique la página de códigos, longitud, precisión y escala de la columna.  
  
    -   Para eliminar un parámetro sin usar, seleccione el parámetro en **Columnas externas**y luego haga clic en **Quitar columna**.  
  
    -   Haga clic en **Asignaciones de columnas** y asigne las columnas de la lista **Columnas de entrada disponibles** a parámetros de la lista **Columnas de destino disponibles** .  
  
14. Haga clic en **Aceptar**.  
  
15. Para guardar el paquete actualizado, haga clic en **Guardar** en el menú **Archivo** .  
  
## <a name="see-also"></a>Vea también  
 [Flujo de datos](../../../integration-services/data-flow/data-flow.md)   
 [Transformaciones de Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  

