---
title: Seguimiento (cliente de minería de datos para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- tracer
- connections
ms.assetid: 4aea3e17-cd0f-48dd-8f22-b54a6c716426
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 19a30107af159c1cd87324290844172371f02752
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "78175574"
---
# <a name="trace-data-mining-client-for-excel"></a>Seguimiento (Cliente de minería de datos para Excel)
  ![Botón Seguimiento](media/misc-trace.gif "Botón Seguimiento")

 El cuadro de diálogo **Seguimiento** le ayuda a supervisar las instrucciones que se envían a la instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que está usando para la minería de datos. Después de crear una conexión a una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], todas las interacciones entre el cliente y el servidor se registran en el panel **Seguimiento** , incluidas las instrucciones que crean estructuras, agregan modelos de minería de datos y realizan predicciones, así como algunos mensajes que devuelve el servidor.

 Dependiendo de la acción que se solicita, la instrucción puede ser una consulta de definición de datos o una consulta de manipulación de datos de Extensiones de Minería de Datos (DMX), un paquete de Analysis Services Scripting Language (ASSL), o una llamada a un procedimiento almacenado de Analysis Services. Sin embargo, no se muestran resultados numéricos ni valores de datos reales.

 **Seguimiento** solo supervisa la conexión actual; el contenido del cuadro de diálogo **Seguimiento** no se guarda.

## <a name="options"></a>Opciones
 En el panel seguimiento se enumeran todas las instrucciones enviadas desde el cliente de Excel al servidor.

 Dependiendo de la acción que se solicita, la instrucción podría ser una manipulación de datos DMX o una instrucción de definición de datos, una llamada a un procedimiento almacenado de Analysis Services o un paquete XML/A.

 **Conexión actual** Haga clic en esta opción para mostrar la definición de la conexión actual. La definición incluye el nombre de la conexión, el proveedor, el origen de datos y el catálogo, la hora en que se utilizó la conexión por última vez para una transacción y el estado actual (Abierta, Inactiva).

 **Usar modelos de sesión** Active esta casilla para almacenar estructuras y modelos de minería de datos como objetos temporales en el servidor. Los modelos y las estructuras que cree sólo estarán disponibles mientras dure la sesión actual.

 Anule la selección de esta opción si desea guardar los modelos o las estructuras en un servidor de Analysis Services.

 **Nota** : la capacidad de usar objetos temporales sólo está disponible cuando se usan las Herramientas de análisis de tabla para Excel. Las Plantillas de minería de datos para Visio y el Cliente de minería de datos para Excel requieren que las estructuras y los modelos se almacenen en el servidor.

## <a name="tracing-temporary-structures-and-models"></a>Estructuras y modelos temporales de seguimiento
 Si usa las Herramientas de análisis de tabla que, de forma predeterminada, crean estructuras y modelos temporales, se supervisará la actividad entre el servidor y el cliente, pero los modelos o las estructuras que cree no se guardarán en el servidor.

 Si desea conservar el trabajo cuando use una de las Herramientas de análisis de tabla, puede anular la selección de la opción **Usar modelos de sesión**para que los modelos se guarden permanentemente en el servidor. También puede copiar las instrucciones del panel **Seguimiento** en un archivo para que pueda volver a crear su trabajo posteriormente.

## <a name="understanding-sessions"></a>Descripción de las sesiones
 Cuando se conecta a una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], el complemento de minería de datos inicia una sesión. Cada sesión recibe un identificador de sesión que identifica una sesión existente en la instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . No obstante, un identificador de sesión no garantiza que una sesión continúe siendo válida. La sesión puede caducar si supera el tiempo de espera o se interrumpe la conexión asociada a la sesión. Si la sesión caduca y deja de ser válida, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] la finaliza y revierte cualquier transacción que esté en curso. Si se envía un mensaje con un identificador de sesión que ya no es válido, el mensaje emite un error que indica que no se puede encontrar la sesión especificada.

 Aunque algunos modelos de minería de datos se almacenan explícitamente en el servidor, los modelos y estructuras de minería de datos de sesión no lo hacen, y no se conserva ningún registro de la actividad de minería de datos de sesión. Como los modelos y estructuras de minería de datos temporales se eliminan en cuanto finaliza la sesión, no debe cerrar su libro de Excel hasta que haya guardado cualquier trabajo que desee conservar.

## <a name="changing-connections"></a>Cambiar conexiones
 El cambio de conexión no elimina los seguimientos de las conexiones anteriores. Sólo se borra la sesión si se cierra el libro.

 Si cambia de conexión mientras trabaja en un libro de Excel, el cambio no se registra en el panel **Seguimiento** . Para mostrar de manera explícita el nombre y el estado de la conexión actual, debe hacer clic en **Conexión actual**.

## <a name="understanding-statements-in-the-tracer"></a>Descripción de las instrucciones de seguimiento
 DMX es un lenguaje que puede usar para crear modelos de minería de datos en [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]y trabajar con ellos. Puede usar DMX para crear la estructura de nuevos modelos de minería de datos, para entrenar esos modelos, y para explorar, administrar y realizar predicciones con ellos. DMX se compone de instrucciones de lenguaje de definición de datos (DDL), instrucciones de lenguaje de manipulación de datos (DML), y funciones y operadores.

 Una discusión completa de las instrucciones DMX y su sintaxis queda fuera del ámbito de este tema. Sin embargo, puede usar la información del panel **Seguimiento** para buscar información detallada sobre el comportamiento de una instrucción DMX. Los Complementos de minería de datos para Excel también le permiten compilar instrucciones DMX complejas e interactuar con un servidor de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Para obtener más información, vea [&#40;de consultas SQL Server complementos de minería de datos&#41;](query-sql-server-data-mining-add-ins.md).

> [!NOTE]
>  Muchas instrucciones DMX tienen parámetros. Para los tipos simples, los valores de los parámetros aparecen bajo la instrucción. Sin embargo, para los tipos complejos, solo se indica el tipo de parámetro.

 SQL Server Analysis Services también usa el protocolo XML for Analysis (XMLA) para controlar todas las comunicaciones entre aplicaciones cliente, como el Cliente de minería de datos para Excel, y una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].

 Para obtener más información sobre la sintaxis DMX, y los comandos y elementos de XMLA, vea los Libros en pantalla de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .

 Algunas de las instrucciones enviadas al servidor pueden incluir consultas que llaman a los procedimientos almacenados en el sistema de Analysis Services. Para obtener más información, vea Libros en pantalla de SQL Server.


