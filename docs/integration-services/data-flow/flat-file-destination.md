---
title: Plano de destino de archivo | Documentos de Microsoft
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
- sql13.dts.designer.flatfiledest.f1
helpviewer_keywords:
- flat files
- Flat File destination
- text file writing [Integration Services]
- destinations [Integration Services], Flat File
ms.assetid: e0d6e356-8db4-48aa-ba66-029397f98f61
caps.latest.revision: 49
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 78a0ec526f83dcab8d7358ef5a51f1f6ccfd0a04
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

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
  
 Para obtener más información acerca de las propiedades que puede establecer en el cuadro de diálogo **Editor de origen de archivos planos** , haga clic en uno de los temas siguientes:  
  
-   [Editor de destino de archivos planos &#40;página Administrador de conexiones&#41;](../../integration-services/data-flow/flat-file-destination-editor-connection-manager-page.md)  
  
-   [Editor de destino de archivos planos &#40;página Asignaciones&#41;](../../integration-services/data-flow/flat-file-destination-editor-mappings-page.md)  
  
 El cuadro de diálogo **Editor avanzado** indica las propiedades que se pueden establecer mediante programación. Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Propiedades comunes](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propiedades personalizadas de archivo plano](../../integration-services/data-flow/flat-file-custom-properties.md)  
  
## <a name="related-tasks"></a>Tareas relacionadas  
 Para obtener más detalles sobre cómo establecer las propiedades de un componente de flujo de datos, vea [Establecer las propiedades de un componente de flujo de datos](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="see-also"></a>Vea también  
 [Origen de archivo plano](../../integration-services/data-flow/flat-file-source.md)   
 [Flujo de datos](../../integration-services/data-flow/data-flow.md)  
  
  
