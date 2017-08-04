---
title: "Editor del Administrador de conexiones (página General) varios archivos planos | Documentos de Microsoft"
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
- sql13.dts.designer.multifile.general.f1
helpviewer_keywords:
- Multiple Flat Files Connection Manager Editor
ms.assetid: 00129d43-2772-413b-bdf8-ac5de81cf4a5
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 84e8e23d349266c6c1195a10410085654548c64f
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="multiple-flat-files-connection-manager-editor-general-page"></a>Editor del administrador de conexiones de varios archivos planos (página General)
  Utilice la página **General** del cuadro de diálogo **Editor del administrador de conexiones de varios archivos planos** para seleccionar un grupo de archivos que tengan el mismo formato de datos y para especificar su formato de datos. Una conexión de varios archivos planos permite que un paquete se conecte a un grupo de archivos de texto que tengan el mismo formato.  
  
 Para obtener más información acerca del administrador de conexiones de varios archivos planos, vea [Multiple Flat Files Connection Manager](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md).  
  
## <a name="options"></a>Opciones  
 **Nombre del administrador de conexiones**  
 Especifique un nombre único para la conexión de varios archivos planos en el flujo de trabajo. El nombre que indique se mostrará en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 **Description**  
 Describe la conexión. Como método recomendado, describa la conexión desde el punto de vista de su propósito, para que los paquetes estén autodocumentados y sean más fáciles de mantener.  
  
 **Nombres de archivos**  
 Escriba la ruta de acceso y los nombres de los archivos que se van a utilizar en la conexión de varios archivos planos. Puede especificar varios archivos mediante el uso de caracteres comodín, como en el ejemplo "C:\\*.txt", o mediante el uso del carácter de barra vertical (|) para separar varios nombres de archivo. Todos los archivos deben tener el mismo formato de datos.  
  
 **Examinar**  
 Busque los nombres de los archivos que se van a utilizar en la conexión de varios archivos planos. Puede seleccionar varios archivos. Todos los archivos deben tener el mismo formato de datos.  
  
 **Configuración regional**  
 Especifique la ubicación para proporcionar información de ordenación y de conversión de fecha y hora.  
  
 **Unicode**  
 Indique si se va a utilizar Unicode. El uso de Unicode impide especificar una página de códigos.  
  
 **Página de códigos**  
 Especifique la página de códigos para el texto no Unicode.  
  
 **Formato**  
 Indique si se utiliza formato delimitado, de ancho fijo o derecho irregular. Todos los archivos deben tener el mismo formato de datos.  
  
|Value|Description|  
|-----------|-----------------|  
|Delimitado|Las columnas se separan mediante delimitadores, que se especifican en la página **Columnas** .|  
|Ancho fijo|Las columnas tienen un ancho fijo, que se especifica arrastrando líneas de marcador en la página **Columnas** .|  
|Derecho irregular|Los archivos de derecho irregular son los archivos en los que todas las columnas tienen un ancho fijo, a excepción de la última, que está delimitada por el delimitador de filas, que se especifica en la página **Columnas** .|  
  
 **Calificador de texto**  
 Especifique el calificador de texto que se va a utilizar. Por ejemplo, puede especificar que el texto se incluya entre comillas.  
  
 **Delimitador de filas de encabezados**  
 Seleccione uno de los delimitadores de filas de encabezados de la lista o escriba el texto delimitador.  
  
|Value|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|La fila de encabezado está delimitada por una combinación de retorno de carro y avance de línea.|  
|**{CR}**|La fila de encabezado está delimitada por un retorno de carro.|  
|**{LF}**|La fila de encabezado está delimitada por un avance de línea.|  
|**Punto y coma {;}**|La fila de encabezado está delimitada por un punto y coma.|  
|**Dos puntos {:}**|La fila de encabezado está delimitada por dos puntos.|  
|**Coma {,}**|La fila de encabezado está delimitada por una coma.|  
|**Tabulación {t}**|La fila de encabezado está delimitada por una tabulación.|  
|**Barra vertical {&#124;}**|La fila de encabezado está delimitada por una barra vertical.|  
  
 **Filas de encabezados que se omitirán**  
 Especifica el número de filas de encabezados que se van a omitir, en caso de que esto ocurra.  
  
 **Nombres de columna de la primera fila de datos**  
 Indica si deben esperarse o deben especificarse nombres de columna en la primera fila de datos.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de errores y mensajes de Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor del Administrador de conexiones de varios archivos planos &#40; Página columnas &#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-columns-page.md)   
 [Editor del Administrador de conexiones de varios archivos planos &#40; Página avanzadas &#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-advanced-page.md)   
 [Editor del Administrador de conexiones de varios archivos planos &#40; Página de vista previa &#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-preview-page.md)  
  
  
