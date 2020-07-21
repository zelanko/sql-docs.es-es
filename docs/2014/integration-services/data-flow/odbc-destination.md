---
title: Destino ODBC | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.odbcdest.f1
ms.assetid: bffa63e0-c737-4b54-b4ea-495a400ffcf8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e398766c827f7611432f5ecd94353f1168e136b4
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85431902"
---
# <a name="odbc-destination"></a>Destino ODBC
  El destino ODBC carga de forma masiva los datos en tablas de base de datos que admiten ODBC. El destino ODBC usa un administrador de conexiones ODBC para conectarse al origen de datos.  
  
 Un destino ODBC incluye asignaciones entre las columnas de entrada y las columnas en el origen de datos de destino. No es necesario asignar columnas de entrada a todas las columnas de destino pero, según las propiedades de las columnas de destino, pueden producirse errores si no se asignan columnas de entrada a las columnas de destino. Por ejemplo, si una columna de destino no permite valores NULL, se debe asignar una columna de entrada a esa columna. Además, se pueden asignar columnas de tipos diferentes, sin embargo, si los datos de entrada no son compatibles con el tipo de las columnas de destino, se produce un error en tiempo de ejecución. En función de la opción de comportamiento del error, se omitirá el error, se producirá un error o la fila se enviará a la salida de error.  
  
 El destino ODBC tiene una salida normal y una salida de error.  
  
##  <a name="load-options"></a><a name="BKMK_odbcdestination_loadoptions"></a> Opciones de carga  
 El destino ODBC puede usar uno de dos módulos de de carga de acceso. Establezca el modo en el [Editor de orígenes ODBC &#40;página Administrador de conexiones&#41;](../odbc-source-editor-connection-manager-page.md). Los dos modos son:  
  
-   **Lote**: en este modo, el destino ODBC intenta usar el método más eficaz de inserción en función de las capacidades del proveedor ODBC percibidas. Para la mayoría de los proveedores ODBC modernos, esto significaría preparar una instrucción INSERT con parámetros y usar después un enlace de parámetros de matriz en las filas (donde el tamaño de la matriz está controlado por la propiedad **BatchSize** ). Si selecciona **Lote** y el proveedor no admite este método, el destino ODBC cambia automáticamente los modificadores al modo **Fila a fila** .  
  
-   **Fila a fila**: en este modo, el destino ODBC prepara una instrucción INSERT con parámetros y usa **Execute de SQL** para insertar las filas de una en una.  
  
## <a name="error-handling"></a>Tratamiento de errores  
 El destino ODBC tiene una salida de error. La salida de error del componente incluye las columnas de salida siguientes:  
  
-   **Código de error**: número que corresponde al error actual. Vea la documentación de la base de datos de origen para obtener una lista de errores. Para obtener una lista de códigos de errores de SSIS, vea la referencia Código de errores y mensajes de SSIS.  
  
-   **Columna de error**: columna de origen que produce el error (para los errores de conversión).  
  
-   Columnas estándar de datos de salida.  
  
 Según la configuración del comportamiento de los errores, el destino ODBC permite devolver los errores (conversión de datos, truncamiento) que aparecerán durante el proceso de extracción en la salida de error. Para obtener más información, vea [Editor de origen de ODBC &#40;página Salida de error&#41;](../odbc-source-editor-error-output-page.md).  
  
## <a name="parallelism"></a>Paralelismo  
 No hay límite en el número de componentes de destino ODBC que se pueden ejecutar en paralelo en la misma tabla o en tablas diferentes, en el mismo equipo o en equipos diferentes (que no sean los límites normales de la sesión global).  
  
 Sin embargo, las limitaciones del proveedor ODBC que se usa pueden restringir el número de conexiones simultáneas a través del proveedor. Estas limitaciones limitan el número de instancias en paralelo admitidas posibles para el destino ODBC. El desarrollador de SSIS debe tener en cuenta las limitaciones de cualquier proveedor ODBC que se vaya a usar y tomarlas en cuenta al generar paquetes SSIS.  
  
 También debe tener en cuenta que la carga simultánea en la misma tabla puede reducir el rendimiento debido al bloqueo de registros estándar. Esto depende de los datos que se cargan y de la organización de las tablas.  
  
## <a name="troubleshooting-the-odbc-destination"></a>Solucionar problemas del destino ODBC  
 Puede registrar las llamadas que el origen ODBC realiza a proveedores de datos externos. Puede usar esta nueva capacidad de registro para solucionar los problemas que tengan que ver con guardar datos en orígenes de datos externos que realiza el destino ADO NET. Para registrar las llamadas realizadas por el destino ODBC a proveedores de datos externos, habilite el seguimiento del administrador de controladores ODBC. Para obtener más información, vea la documentación de Microsoft sobre *cómo generar un seguimiento ODBC con el administrador de orígenes de datos*.  
  
## <a name="configuring-the-odbc-destination"></a>Configuración del destino ODBC  
 Puede configurar el destino ODBC mediante programación o mediante el Diseñador SSIS  
  
 Para obtener más información, vea uno de los siguientes temas:  
  
-   [Editor de destino de ODBC &#40;página Administrador de conexiones&#41;](../odbc-destination-editor-connection-manager-page.md)  
  
-   [Editor de destino de ODBC &#40;página Asignaciones&#41;](../odbc-destination-editor-mappings-page.md)  
  
-   [Editor de destinos de ODBC &#40;página Salida de error&#41;](../odbc-destination-editor-error-output-page.md)  
  
 El cuadro de diálogo **Editor avanzado** contiene las propiedades que se pueden establecer mediante programación.  
  
 Para abrir el cuadro de diálogo **Editor avanzado** :  
  
-   En la pantalla **Flujo de datos** del proyecto de [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] , haga clic con el botón secundario en el destino ODBC y seleccione **Mostrar editor avanzado**.  
  
 Para obtener más información acerca de las propiedades que se pueden establecer en el cuadro de diálogo Editor avanzado, vea [ODBC Destination Custom Properties](odbc-destination-custom-properties.md).  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Editor de destinos de ODBC &#40;página Salida de error&#41;](../odbc-destination-editor-error-output-page.md)  
  
-   [Editor de destino de ODBC &#40;página Asignaciones&#41;](../odbc-destination-editor-mappings-page.md)  
  
-   [Editor de destino de ODBC &#40;página Administrador de conexiones&#41;](../odbc-destination-editor-connection-manager-page.md)  
  
-   [Cargar datos mediante el destino de ODBC](odbc-destination.md)  
  
-   [ODBC Destination Custom Properties](odbc-destination-custom-properties.md)  
  
  
