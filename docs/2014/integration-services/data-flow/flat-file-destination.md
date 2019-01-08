---
title: Destino de archivo plano | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.flatfiledest.f1
helpviewer_keywords:
- flat files
- Flat File destination
- text file writing [Integration Services]
- destinations [Integration Services], Flat File
ms.assetid: e0d6e356-8db4-48aa-ba66-029397f98f61
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ed4cb484f89d44ed31b4c82a9e1349dfab925dac
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52761757"
---
# <a name="flat-file-destination"></a>Destino de archivo plano
  El destino de archivo plano escribe datos en un archivo de texto. El archivo de texto puede tener formato delimitado, de ancho fijo, de ancho fijo con delimitador de filas o desigual a la derecha.  
  
 Puede configurar el destino de archivo plano de las maneras siguientes:  
  
-   Proporcionar un bloque de texto que se inserta en el archivo antes de escribir cualquier dato. El texto puede proporcionar información tal como encabezados de columna.  
  
-   Especificar si se deben sobrescribir datos en un archivo de destino que tenga el mismo nombre.  
  
 Este destino utiliza un administrador de conexiones de archivos planos para tener acceso al archivo de texto. Al establecer propiedades en el administrador de conexiones de archivos planos que usa el destino de archivo plano, puede especificar la manera en que el destino de archivo plano establece el formato y escribe el archivo de texto. Al configurar el administrador de conexiones de archivos planos, se especifica información sobre el archivo y sobre cada columna del archivo. Por ejemplo, puede especificar los caracteres que delimitan columnas y filas en el archivo, así como el tipo de datos y la longitud de cada columna. Para más información, consulte [Flat File Connection Manager](../connection-manager/file-connection-manager.md).  
  
 El destino de archivo plano incluye la propiedad personalizada Header. Esta propiedad se puede actualizar a través de una expresión de propiedad, al cargar el paquete. Para más información, vea [Expresiones de Integration Services &#40;SSIS&#41;](../expressions/integration-services-ssis-expressions.md), [Usar expresiones de propiedad en paquetes](../expressions/use-property-expressions-in-packages.md) y [Propiedades personalizadas de archivo plano](flat-file-custom-properties.md).  
  
 Este destino tiene una salida. No admite una salida de error.  
  
## <a name="configuration-of-the-flat-file-destination"></a>Configuración del destino de archivo plano  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el cuadro de diálogo **Editor de origen de archivos planos** , haga clic en uno de los temas siguientes:  
  
-   [Editor de destino de archivos planos &#40;página Administrador de conexiones&#41;](../flat-file-destination-editor-connection-manager-page.md)  
  
-   [Editor de destino de archivos planos &#40;página Asignaciones&#41;](../flat-file-destination-editor-mappings-page.md)  
  
 El cuadro de diálogo **Editor avanzado** indica las propiedades que se pueden establecer mediante programación. Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Common Properties](../common-properties.md)  
  
-   [Propiedades personalizadas de archivo plano](flat-file-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obtener más detalles sobre cómo establecer las propiedades de un componente de flujo de datos, vea [Establecer las propiedades de un componente de flujo de datos](set-the-properties-of-a-data-flow-component.md).  
  
## <a name="see-also"></a>Vea también  
 [Origen de archivo plano](flat-file-source.md)   
 [Flujo de datos](data-flow.md)  
  
  
