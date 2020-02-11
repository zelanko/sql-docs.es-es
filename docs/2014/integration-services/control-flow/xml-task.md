---
title: Tarea XML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.xmltask.f1
helpviewer_keywords:
- XML [Integration Services]
- XML task [Integration Services]
ms.assetid: 9f761846-390e-46d5-9db7-858943d40849
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e89f4835b95b1fe497df32ad9f773be84ccb161b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "75232727"
---
# <a name="xml-task"></a>Tarea XML
  La tarea XML se usa para trabajar con datos XML. Mediante esta tarea, un paquete puede recuperar documentos XML, aplicar operaciones a los documentos mediante las hojas de estilos Extensible Stylesheet Language Transformations (XSLT) y expresiones XPath, combinar varios documentos, o bien validar, comparar y guardar los documentos actualizados en archivos y variables.  
  
 Esta tarea habilita un paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para modificar de forma dinámica los documentos XML en tiempo de ejecución. Puede usar la tarea XML para los siguientes objetivos:  
  
-   Cambiar el formato de un documento XML. Por ejemplo, la tarea puede obtener acceso a un informe que reside en un archivo XML y aplicar dinámicamente una hoja de estilos XSLT para personalizar la presentación del documento.  
  
-   Seleccionar secciones de un documento XML. Por ejemplo, la tarea puede obtener acceso a un informe que reside en un archivo XML y aplicar dinámicamente una expresión XPath para seleccionar una sección del documento. La operación también puede obtener y procesar valores en el documento.  
  
-   Combinar documentos de varios orígenes. Por ejemplo, la tarea puede descargar informes de varios orígenes y combinarlos dinámicamente en un solo documento XML completo.  
  
-   Validar un documento XML y, de forma opcional, obtener una salida de error detallada. Para obtener más información, vea [Validate XML with the XML Task](xml-task.md).  
  
 Puede incluir datos XML en un flujo de datos mediante un origen XML para extraer valores de un documento XML. Para más información, consulte [XML Source](../data-flow/xml-source.md).  
  
## <a name="xml-operations"></a>Operaciones XML  
 La primera acción que realiza la tarea XML es recuperar un documento XML específico. Esta acción se genera en la tarea XML y se produce automáticamente. El documento XML recuperado se usa como origen de los datos para la operación que realiza la tarea XML.  
  
 Las operaciones de XML de comparación (Diff), combinación (Merge) y revisión (Patch) requieren dos operandos. El primer operando especifica el documento XML de origen. El segundo operando también especifica un documento XML, cuyo contenido depende de los requisitos de la operación. Por ejemplo, la operación de comparación compara dos documentos: por lo tanto, el segundo operando especifica otro documento XML similar con el que se compara el documento XML de origen.  
  
 La tarea XML puede usar una variable o un administrador de conexiones de archivo como origen, o incluir los datos XML en una propiedad de tarea.  
  
 Si el origen es una variable, la variable especificada contiene la ruta del documento XML.  
  
 Si el origen es un administrador de conexiones de archivos, el administrador de conexiones de archivos especificado proporciona la información de origen. El administrador de conexiones de archivos se configura de forma independiente de la tarea XML y se hace referencia a él en la tarea XML. La cadena de conexión para el administrador de conexiones de archivos especifica la ruta del archivo XML. Para obtener más información, consulte [File Connection Manager](../connection-manager/file-connection-manager.md).  
  
 La tarea XML se puede configurar para guardar el resultado de la operación en una variable o en un archivo. Si se guarda en un archivo, la tarea XML usa un administrador de conexiones de archivos para tener acceso al archivo. También puede guardar los resultados del DiffGram generado por la operación de comparación en archivos y variables.  
  
## <a name="predefined-xml-operations"></a>Operaciones XML predefinidas  
 La tarea XML incluye un conjunto predefinido de operaciones para trabajar con documentos XML. Estas operaciones se describen en la siguiente tabla.  
  
|Operación|Descripción|  
|---------------|-----------------|  
|Diferencias|Compara dos documentos XML. Usando el documento XML de origen como documento base, la operación de comparación lo compara con otro documento XML, detecta sus diferencias y escribe las diferencias en un documento DiffGram XML. Esta operación incluye propiedades para personalizar la comparación.|  
|Merge|Combina dos documentos XML. Usando el documento XML de origen como documento base, la operación de combinación agrega el contenido de un segundo documento en el documento base. La operación puede especificar una ubicación de combinación dentro del documento base.|  
|Revisión|Aplica el resultado de la operación de comparación, denominada documento DiffGram, en un documento XML para crear un nuevo documento principal que incluye contenido del documento DiffGram.|  
|Validación|Valida el documento XML según una definición de tipo de documento (DTD) o un esquema de definición de esquema XML (XSD).|  
|XPath|Realiza consultas y evaluaciones XPath.|  
|XSLT|Realiza transformaciones XSL en documentos XML.|  
  
### <a name="diff-operation"></a>Operación de comparación  
 La operación de comparación se puede configurar para usar un algoritmo de comparación diferente dependiendo de si la comparación debe ser rápida o precisa. La operación también se puede configurar para seleccionar automáticamente una comparación rápida o precisa según el tamaño de los documentos que se comparan.  
  
 La operación de comparación incluye un conjunto de opciones que personalizan la comparación XML. Las opciones se describen en la siguiente tabla.  
  
|Opción|Descripción|  
|------------|-----------------|  
|**IgnoreComments**|Valor que especifica si se comparan los nodos de comentarios.|  
|**IgnoreNameSpaces**|Valor que especifica si se comparan el identificador uniforme de recursos (URI) de espacio de nombres de un elemento y sus nombres de atributos. Si esta opción se establece en `true`, dos elementos que tienen el mismo nombre local pero un espacio de nombres diferente se consideran idénticos.|  
|**IgnorePrefixes**|Valor que especifica si se comparan los prefijos de nombres de elementos y atributos. Si esta opción se establece en `true,` dos elementos que tienen el mismo nombre local pero un URI y un prefijo de espacio de nombres diferentes se consideran idénticos.|  
|**IgnoreXMLDeclaration**|Un valor que especifica si se comparan las declaraciones XML.|  
|**IgnoreOrderOfChildElements**|Valor que especifica si se compara el orden de los elementos secundarios. Si esta opción se establece en `true`, los elementos secundarios que solo difieren en su posición en una lista de elementos del mismo nivel se consideran idénticos.|  
|**IgnoreWhiteSpaces**|Valor que especifica si se comparan los espacios en blanco.|  
|**IgnoreProcessingInstructions**|Valor que especifica si se comparan las instrucciones de procesamiento.|  
|**IgnoreDTD**|Valor que especifica si se pasa por alto el DTD.|  
  
### <a name="merge-operation"></a>Operación de combinación  
 Al utilizar una instrucción XPath para identificar la ubicación de la combinación en el documento de origen, se espera que esta instrucción devuelva un único nodo. Si la instrucción devuelve varios nodos, solo se utiliza el primero. El contenido del segundo documento se combina bajo el primer nodo que devuelve la consulta de XPath.  
  
### <a name="xpath-operation"></a>Operación XPath  
 La operación XPath se puede configurar para usar diferentes tipos de funcionalidad de XPath.  
  
-   Seleccione la opción **Evaluación** para implementar funciones XPath tales como sum().  
  
-   Seleccione la opción **Lista de nodos** para devolver los nodos seleccionados como un fragmento XML.  
  
-   Seleccione la opción **Valores** para devolver el valor de texto interno de todos los nodos seleccionados, concatenados en una cadena.  
  
### <a name="validation-operation"></a>Operación de validación  
 La operación de validación se puede configurar para usar una Definición de tipo de documento (DTD) o un esquema de definición del esquema XML (XSD).  
  
 Habilite `ValidationDetails` para obtener una salida de error detallada. Para obtener más información, vea [Validate XML with the XML Task](xml-task.md).  
  
## <a name="xml-document-encoding"></a>Codificación de documentos XML  
 La tarea XML únicamente admite la mezcla de documentos Unicode. Esto significa que la tarea puede aplicar la operación de combinación únicamente a documentos con una codificación Unicode. El uso de otras codificaciones hará que la tarea XML genere un error.  
  
> [!NOTE]  
>  Las operaciones de comparación y revisión incluyen una opción para omitir la declaración XML en los datos XML del segundo operando, lo que permite usar documentos que tienen otras codificaciones en estas operaciones.  
  
 Para comprobar que se puede usar el documento XML, revise la declaración XML. La declaración debe especificar explícitamente UTF-8, que indica una codificación Unicode de 8 bits.  
  
 La etiqueta siguiente muestra la codificación Unicode de 8 bits.  
  
 `<?xml version="1.0" encoding="UTF-8"?>`  
  
## <a name="custom-logging-messages-available-on-the-xml-task"></a>Mensajes de registro personalizados disponibles en la tarea XML  
 La siguiente tabla contiene las entradas del registro personalizadas para la tarea XML. Para más información, vea [Registro de Integration Services &#40;SSIS&#41;](../performance/integration-services-ssis-logging.md) y [Mensajes personalizados para registro](../custom-messages-for-logging.md).  
  
|Entrada del registro|Descripción|  
|---------------|-----------------|  
|`XMLOperation`|Proporciona información sobre la operación que la tarea realiza.|  
  
## <a name="configuration-of-the-xml-task"></a>Configuración de la tarea XML  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en uno de los temas siguientes:  
  
-   [Editor de la tarea XML &#40;página general&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [Validar XML con la tarea XML](xml-task.md)  
  
-   [Página Expresiones](../expressions/expressions-page.md)  
  
 Para obtener más información sobre cómo establecer propiedades en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el tema siguiente:  
  
-   [Establecer las propiedades de tareas o contenedores](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="programmatic-configuration-of-the-xml-task"></a>Configuración mediante programación de la tarea XML  
 Para obtener más información sobre cómo establecer estas propiedades mediante programación, haga clic en el tema siguiente:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.XMLTask.XMLTask>  
  
## <a name="related-tasks"></a>Related Tasks  
 [Establecer las propiedades de tareas o contenedores](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="related-content"></a>Contenido relacionado  
  
-   Entrada del blog sobre el [Componente script de destino XML](http://agilebi.com/jwelch/2007/06/02/xml-destination-script-component/), en agilebi.com  
  
-   Ejemplo en CodePlex, [ejemplo de proceso de paquete de datos XML](https://msftisprodsamples.codeplex.com/wikipage?title=SS2008!Process%20XML%20Data%20Package%20Sample&version=10&ProjectName=msftisprodsamples), en www.codeplex.com  
  
