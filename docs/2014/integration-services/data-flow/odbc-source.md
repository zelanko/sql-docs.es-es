---
title: Origen ODBC | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.ssis.designer.odbcsource.f1
ms.assetid: abcf34eb-9140-4100-82e6-b85bccd22abe
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: b9b3ee40399f6fa3507e27e3d6cb98b63627dcb8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36203456"
---
# <a name="odbc-source"></a>Origen ODBC
  El origen ODBC extrae los datos de una base de datos con ODBC mediante una tabla de base de datos, una vista o una instrucción SQL.  
  
 El origen ODBC tiene los modos de acceso a datos siguientes para extraer datos:  
  
-   Una tabla o vista.  
  
-   Los resultados de una instrucción SQL.  
  
 El origen utiliza un administrador de conexiones ODBC, que especifica el proveedor que usar.  
  
 Un origen ODBC incluye las columnas de salida de datos de origen. Cuando las columnas de salida se asignan en el destino ODBC a las columnas de destino, pueden aparecer errores si no se ha asignado ninguna columna de salida a las columnas de destino. Se pueden asignar columnas de tipos diferentes, sin embargo, si los datos de salida no son compatibles con el destino, se produce un error en tiempo de ejecución. En función de la opción de comportamiento del error, se omitirá el error, se producirá un error o la fila se enviará a la salida de error.  
  
 El origen ODBC tiene una salida normal y una salida de error.  
  
## <a name="error-handling"></a>Tratamiento de errores  
 El origen ODBC tiene una salida de error. La salida de error del componente incluye las columnas de salida siguientes:  
  
-   **Código de error**: número que corresponde al error actual. Vea la documentación de la base de datos con ODBC que usa para obtener una lista de errores. Para obtener una lista de códigos de errores de SSIS, vea la referencia Código de errores y mensajes de SSIS.  
  
-   **Columna de error**: columna de origen que produce el error (para los errores de conversión).  
  
-   Columnas estándar de datos de salida.  
  
 Según la configuración del comportamiento de los errores, el origen ODBC permite devolver los errores (conversión de datos, truncamiento) que aparecerán durante el proceso de extracción en la salida de error. Para obtener más información, vea [Editor de destino de ODBC &#40;página Administrador de conexiones&#41;](../odbc-destination-editor-connection-manager-page.md).  
  
## <a name="data-type-support"></a>Compatibilidad con tipos de datos  
 Para obtener información acerca de los tipos de datos admitidos por el origen ODBC, vea Connector for Open Database Connectivity (ODBC) de Attunity.  
  
## <a name="extract-options"></a>Opciones de extracción  
 El origen ODBC funciona en modo **Lote** o **Fila a fila** . La propiedad **FetchMethod** determina el modo usado. En la lista siguiente, se describen los modos.  
  
-   **Lote**: el componente intenta usar el método más eficaz de búsqueda en función de las capacidades del proveedor ODBC percibidas. Para la mayoría de los proveedores ODBC modernos, es SQLFetchScroll con enlace de matriz (donde el tamaño de la matriz se determina mediante la propiedad **BatchSize** ). Si selecciona **Lote** y el proveedor no admite este método, el destino ODBC cambia automáticamente al modo **Fila a fila** .  
  
-   **Fila a fila**: el componente usa SQLFetch para recuperar las filas de una en una.  
  
 Para obtener más información acerca de la la propiedad **FetchMethod** , vea [ODBC Source Custom Properties](odbc-source-custom-properties.md).  
  
## <a name="parallelism"></a>Parallelism  
 No hay límite en el número de componentes de origen ODBC que se pueden ejecutar en paralelo en la misma tabla o en tablas diferentes, en el mismo equipo o en equipos diferentes (que no sean los límites normales de la sesión global).  
  
 Sin embargo, las limitaciones del proveedor ODBC que se usa pueden restringir el número de conexiones simultáneas a través del proveedor. Estas limitaciones limitan el número de instancias en paralelo admitidas posibles para el origen ODBC. El desarrollador de SSIS debe tener en cuenta las limitaciones de cualquier proveedor ODBC que se vaya a usar y tomarlas en cuenta al generar paquetes SSIS.  
  
## <a name="troubleshooting-the-odbc-source"></a>Solucionar problemas del origen de ODBC  
 Puede registrar las llamadas que el origen ODBC realiza a proveedores de datos externos. Puede usar esta capacidad de registro para solucionar los problemas relacionados con la carga de datos de orígenes de datos externos que realiza el origen ODBC. Para registrar las llamadas realizadas por el origen ODBC a proveedores de datos externos, habilite el seguimiento del administrador de controladores ODBC. Para obtener más información, vea la documentación de Microsoft sobre *cómo generar un seguimiento ODBC con el administrador de orígenes de datos.*  
  
## <a name="configuring-the-odbc-source"></a>Configurar el origen ODBC  
 Puede configurar el origen ODBC mediante programación o través del Diseñador SSIS.  
  
 Para obtener más información, vea uno de los siguientes temas:  
  
-   [Editor de origen ODBC &#40;página Administrador de conexiones&#41;](../odbc-source-editor-connection-manager-page.md)  
  
-   [Editor de origen ODBC &#40;página columnas&#41;](../odbc-source-editor-columns-page.md)  
  
-   [Editor de origen ODBC &#40;página de salida de Error&#41;](../odbc-source-editor-error-output-page.md)  
  
 El cuadro de diálogo **Editor avanzado** contiene las propiedades que se pueden establecer mediante programación.  
  
 Para abrir el cuadro de diálogo **Editor avanzado** :  
  
-   En la pantalla **Flujo de datos** del proyecto de [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] , haga clic con el botón secundario en el origen ODBC y seleccione **Mostrar editor avanzado**.  
  
 Para obtener más información acerca de las propiedades que se pueden establecer en el cuadro de diálogo Editor avanzado, vea [ODBC Source Custom Properties](odbc-source-custom-properties.md).  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Editor de origen ODBC &#40;página de salida de Error&#41;](../odbc-source-editor-error-output-page.md)  
  
-   [Editor de origen ODBC &#40;página columnas&#41;](../odbc-source-editor-columns-page.md)  
  
-   [Editor de origen ODBC &#40;página Administrador de conexiones&#41;](../odbc-source-editor-connection-manager-page.md)  
  
-   [Extraer datos mediante el origen ODBC](odbc-source.md)  
  
-   [Propiedades personalizadas del origen ODBC](odbc-source-custom-properties.md)  
  
  