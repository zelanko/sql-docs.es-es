---
title: Editor del administrador de conexiones de archivos planos (página general) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.ffileconnection.general.f1
helpviewer_keywords:
- Flat File Connection Manager Editor
ms.assetid: 77296024-5c1a-4f6a-9665-0b50d45d744c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b378d7257ddd57e97407d82feb817aa70965f598
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66058752"
---
# <a name="flat-file-connection-manager-editor-general-page"></a>Editor del administrador de conexiones de archivos planos (página General)
  Utilice la página **General** del cuadro de diálogo **Editor del administrador de conexiones de archivos planos** para seleccionar un archivo y un formato de datos. Las conexiones de archivos planos permiten que un paquete se conecte con un archivo de texto.  
  
 Para obtener más información acerca del administrador de conexiones de archivos planos, vea [Flat File Connection Manager](connection-manager/file-connection-manager.md).  
  
## <a name="options"></a>Opciones  
 **Nombre del administrador de conexiones**  
 Especifique un nombre único para la conexión de archivo plano en el flujo de trabajo. El nombre que indique se mostrará en el Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
 **Descripción**  
 Describe la conexión. Como método recomendado, describa la conexión desde el punto de vista de su propósito, para que los paquetes estén autodocumentados y sean más fáciles de mantener.  
  
 **Nombre de archivo**  
 Escriba la ruta de acceso y el nombre de archivo que utilizará en la conexión de archivos planos.  
  
 **Browse**  
 Busque el nombre de archivo que utilizará en la conexión de archivos planos.  
  
 **Configuración regional**  
 Especifique la configuración regional, que proporciona información específica del idioma para la ordenación y los formatos de fecha y hora.  
  
 **Unicode**  
 Indique si se va a utilizar Unicode. Si utiliza Unicode, no puede especificar una página de códigos.  
  
 **Página de códigos**  
 Especifique la página de códigos para el texto no Unicode.  
  
 **Aplique**  
 Indique si el archivo utiliza formato delimitado, de ancho fijo o derecho irregular.  
  
|Value|Descripción|  
|-----------|-----------------|  
|Delimitado|Las columnas se separan mediante delimitadores, que se especifican en la página **Columnas** .|  
|Ancho fijo|Las columnas tienen un ancho fijo.|  
|Derecho irregular|Los archivos de derecho irregular son archivos en los que todas las columnas tienen un ancho fijo, a excepción de la última. Se delimita mediante el delimitador de fila.|  
  
 **Calificador de texto**  
 Especifique el calificador de texto que se va a utilizar. Por ejemplo, puede indicar que los archivos de texto se delimitan con comillas.  
  
> [!NOTE]  
>  Tras seleccionar un calificador de texto, no puede volver a elegir la opción **Ninguno** . Escriba **Ninguno** para anular la selección del calificador de texto.  
  
 **Delimitador de filas de encabezado**  
 Seleccione uno de los delimitadores de filas de encabezados de la lista o escriba el texto delimitador.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**COMPRA LF**|La fila de encabezado está delimitada por una combinación de retorno de carro y avance de línea.|  
|**COMPRA**|La fila de encabezado está delimitada por un retorno de carro.|  
|**LF**|La fila de encabezado está delimitada por un avance de línea.|  
|**Punto y coma {;}**|La fila de encabezado está delimitada por un punto y coma.|  
|**Dos puntos {:}**|La fila de encabezado está delimitada por dos puntos.|  
|**Unas{,}**|La fila de encabezado está delimitada por una coma.|  
|**Tabulación {t}**|La fila de encabezado está delimitada por una tabulación.|  
|**Barra vertical {&#124;}**|La fila de encabezado está delimitada por una barra vertical.|  
  
 **Filas de encabezado que se van a omitir**  
 Especifique el número de filas de encabezado o filas de datos iniciales que se deben omitir, si es necesario.  
  
 **Nombres de columna de la primera fila de datos**  
 Indica si deben esperarse o deben especificarse nombres de columna en la primera fila de datos.  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Página &#40;columnas del editor del administrador de conexiones de archivos planos&#41;](../../2014/integration-services/flat-file-connection-manager-editor-columns-page.md)   
 [Página opciones avanzadas del editor del administrador de conexiones de archivos planos &#40;&#41;](../../2014/integration-services/flat-file-connection-manager-editor-advanced-page.md)   
 [Página de vista previa del editor del administrador de conexiones de archivos planos &#40;&#41;](../../2014/integration-services/flat-file-connection-manager-editor-preview-page.md)  
  
  
