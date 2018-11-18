---
title: Destino de archivo plano | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.flatfiledest.f1
- sql13.dts.designer.flatfiledestadapter.connection.f1
- sql13.dts.designer.flatfiledestadapter.mappings.f1
helpviewer_keywords:
- flat files
- Flat File destination
- text file writing [Integration Services]
- destinations [Integration Services], Flat File
ms.assetid: e0d6e356-8db4-48aa-ba66-029397f98f61
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 6e6fa3edeeff19f7ddf9fde79114586ba7588324
ms.sourcegitcommit: 0638b228980998de9056b177c83ed14494b9ad74
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/14/2018
ms.locfileid: "51641322"
---
# <a name="flat-file-destination"></a>Destino de archivo plano
  El destino de archivo plano escribe datos en un archivo de texto. El archivo de texto puede tener formato delimitado, de ancho fijo, de ancho fijo con delimitador de filas o desigual a la derecha.  
  
 Puede configurar el destino de archivo plano de las maneras siguientes:  
  
-   Proporcionar un bloque de texto que se inserta en el archivo antes de escribir cualquier dato. El texto puede proporcionar información tal como encabezados de columna.  
  
-   Especificar si se deben sobrescribir datos en un archivo de destino que tenga el mismo nombre.  
  
 Este destino utiliza un administrador de conexiones de archivos planos para tener acceso al archivo de texto. Al establecer propiedades en el administrador de conexiones de archivos planos que usa el destino de archivo plano, puede especificar la manera en que el destino de archivo plano establece el formato y escribe el archivo de texto. Al configurar el administrador de conexiones de archivos planos, se especifica información sobre el archivo y sobre cada columna del archivo. Por ejemplo, puede especificar los caracteres que delimitan columnas y filas en el archivo, así como el tipo de datos y la longitud de cada columna. Para más información, consulte [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
 El destino de archivo plano incluye la propiedad personalizada Header. Esta propiedad se puede actualizar a través de una expresión de propiedad, al cargar el paquete. Para más información, vea [Expresiones de Integration Services &#40;SSIS&#41;](../../integration-services/expressions/integration-services-ssis-expressions.md), [Usar expresiones de propiedad en paquetes](../../integration-services/expressions/use-property-expressions-in-packages.md) y [Propiedades personalizadas de archivo plano](../../integration-services/data-flow/flat-file-custom-properties.md).  
  
 Este destino tiene una salida. No admite una salida de error.  
  
## <a name="configuration-of-the-flat-file-destination"></a>Configuración del destino de archivo plano  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 El cuadro de diálogo **Editor avanzado** indica las propiedades que se pueden establecer mediante programación. Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propiedades personalizadas de archivo plano](../../integration-services/data-flow/flat-file-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obtener más detalles sobre cómo establecer las propiedades de un componente de flujo de datos, vea [Establecer las propiedades de un componente de flujo de datos](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="flat-file-destination-editor-connection-manager-page"></a>Editor de destino de archivos planos (página Administrador de conexiones)
  Utilice la página **Administrador de conexiones** del cuadro de diálogo **Editor de destino de archivos planos** para seleccionar la conexión de archivos planos del destino y para especificar si se debe sobrescribir o anexar en el archivo de destino existente. El destino de archivo plano escribe datos en un archivo de texto. Este archivo de texto puede tener los formatos: delimitado, ancho fijo, ancho fijo con delimitadores de fila o derecho irregular.  
  
### <a name="options"></a>Opciones  
 **Administrador de conexiones de archivos planos**  
 Seleccione un administrador de conexiones existente en el cuadro de lista o haga clic en **Nueva**para crear una conexión.  
  
 **Nueva**  
 Cree una conexión con los cuadros de diálogo **Formato del archivo plano** y **Editor del administrador de conexiones de archivos planos** .  
  
 Además de los formatos estándar de archivo plano delimitado, ancho fijo y desigual a la derecha, el cuadro de diálogo **Formato de archivo plano** tiene una cuarta opción, **Ancho fijo con delimitadores de fila**. Esta opción representa un caso especial del formato derecho desigual en el que [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] agrega una columna ficticia como última columna de datos. Esta columna ficticia sirve para garantizar que la última columna tenga un ancho fijo.  
  
 La opción **Ancho fijo con delimitadores de fila** no está disponible en el **Editor del administrador de conexiones de archivos planos**. Si es necesario, puede emular esta opción en el editor. Para emular esta opción, en la página **General** del **Editor del administrador de conexiones de archivos planos**seleccione **Desigual a la derecha**en **Formato**, . A continuación en la página **Avanzadas** del editor, agregue una nueva columna ficticia como última columna de datos.  
  
 **Sobrescribir los datos del archivo**  
 Indique si desea sobrescribir un archivo existente o anexar datos en él.  
  
 **Encabezado**  
 Escriba un bloque de texto para insertarlo en el archivo antes de que se escriban datos. Utilice esta opción para incluir información adicional, como encabezados de columna.  
  
 **Vista previa**  
 Muestra una vista previa de los resultados mediante el cuadro de diálogo **Vista de datos** . La vista previa puede mostrar hasta 200 filas.  
  
## <a name="flat-file-destination-editor-mappings-page"></a>Editor de destino de archivos planos (página Asignaciones)
  Utilice la página **Asignaciones** del cuadro de diálogo **Editor de destino de archivos planos** para asignar columnas de entrada a columnas de destino.  
  
### <a name="options"></a>Opciones  
 **Columnas de entrada disponibles**  
 Muestra la lista de columnas de entrada disponibles. Utilice una operación de arrastrar y colocar para asignar columnas de entrada disponibles a columnas de destino.  
  
 **Columnas de destino disponibles**  
 Muestra la lista de columnas de destino disponibles. Utilice una operación de arrastrar y colocar para asignar columnas de destino disponibles a columnas de entrada.  
  
 **Columna de entrada**  
 Muestra las columnas de entrada seleccionadas anteriormente en este tema. Puede cambiar las asignaciones utilizando la lista de **Columnas de entrada disponibles**. Seleccione **\<omitir>** para excluir la columna de los resultados.  
  
 **Columna de destino**  
 Muestra las columnas de destino disponibles, independientemente de si están asignadas o no.  
  
## <a name="see-also"></a>Ver también  
 [Origen de archivo plano](../../integration-services/data-flow/flat-file-source.md)   
 [Flujo de datos](../../integration-services/data-flow/data-flow.md)  
  
  
