---
title: Origen de archivo sin formato | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.rawfilesource.f1
- sql13.dts.designer.rawfilesourceconnectionmanager.f1
- sql13.dts.designer.rawfilesourcecolumns.f1
helpviewer_keywords:
- sources [Integration Services], Raw File
- raw data [Integration Services]
- Raw File source
ms.assetid: 5b4daea5-7f76-4674-aa77-0a79f9f97f7d
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d5a6a40ef5bee1c50ddbaf1f3424d3199e8494e3
ms.sourcegitcommit: 0638b228980998de9056b177c83ed14494b9ad74
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/14/2018
ms.locfileid: "51637659"
---
# <a name="raw-file-source"></a>archivo sin formato, origen
  El origen de archivo sin formato lee datos sin formato de un archivo. Como la representación de los datos es la nativa del origen, no es necesario traducir los datos y prácticamente no es necesario analizar el archivo. Esto significa que el origen de archivo sin formato puede leer datos más rápidamente que otros orígenes, como el origen de archivo plano o el origen de OLE DB.  
  
 El origen de archivo sin formato se usa para recuperar datos sin formato escritos previamente por el destino de archivo sin formato. También puede señalar el origen de archivo sin formato para un archivo sin formato vacío que contenga solo las columnas (archivo solo de metadatos). El destino de archivo sin formato se usa para generar el archivo de solo metadatos sin tener que ejecutar el paquete. Para más información, consulte [Raw File Destination](../../integration-services/data-flow/raw-file-destination.md).  
  
 El archivo sin formato contiene información sobre el orden. El destino de archivo sin formato guarda toda la información sobre el orden incluidas las marcas de comparación para las columnas de cadena. El origen de archivo sin formato lee y respeta la información sobre el orden. Tiene la opción de configurar el origen de archivo sin formato para omitir los marcas de orden en el archivo; para ello use el Editor avanzado. Para obtener más información acerca de las marcas de comparación, vea [Comparing String Data](../../integration-services/data-flow/comparing-string-data.md).  
  
 Para configurar el archivo sin formato, especifique el nombre del archivo leído por el origen de archivo sin formato.  
  
> [!NOTE]  
>  Este origen no usa un administrador de conexiones.  
  
 Este origen tiene una salida. No admite una salida de error.  
  
## <a name="configuration-of-the-raw-file-source"></a>Configuración del origen de archivo sin formato  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 El cuadro de diálogo **Editor avanzado** indica las propiedades que se pueden establecer mediante programación. Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propiedades personalizadas de archivo sin formato](../../integration-services/data-flow/raw-file-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 Para más información sobre cómo establecer las propiedades del componente, vea [Establecer las propiedades de un componente de flujo de datos](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="related-content"></a>Contenido relacionado  
  
-   Entrada del blog [Raw Files Are Awesome](https://www.sqlservercentral.com/blogs/stratesql/archive/2011/1/1/31-days-of-ssis-_1320_-raw-files-are-awesome-_2800_1_2F00_31_2900_.aspx), en sqlservercentral.com  
  
## <a name="raw-file-source-editor-connection-manager-page"></a>Editor de origen de archivos sin formato (página Administrador de conexiones)
  El origen de archivo sin formato lee datos sin formato de un archivo. Como la representación de los datos es la nativa del origen, no es necesario traducir los datos y prácticamente no es necesario analizar el archivo.   
## <a name="raw-file-source-editor-columns-page"></a>Editor de origen de archivos sin formato (página Columnas)
  El origen de archivo sin formato lee datos sin formato de un archivo. Como la representación de los datos es la nativa del origen, no es necesario traducir los datos y prácticamente no es necesario analizar el archivo.   
## <a name="see-also"></a>Ver también  
 [Raw File Destination](../../integration-services/data-flow/raw-file-destination.md)   
 [Flujo de datos](../../integration-services/data-flow/data-flow.md)  
  
  
