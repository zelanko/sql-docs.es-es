---
title: Propiedades de seguimiento (pestaña General) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.pro.traceproperties.general.f1
helpviewer_keywords:
- Trace Properties dialog box
ms.assetid: 25227268-143b-477e-aac9-8268bcaf2078
caps.latest.revision: 23
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 99621b4d142e6d1686c908783ba63628109eae5e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37221945"
---
# <a name="trace-properties-general-tab"></a>Propiedades de seguimiento (pestaña General)
  Utilice la pestaña **General** del cuadro de diálogo **Propiedades de seguimiento** para ver o especificar las propiedades de un seguimiento.  
  
## <a name="options"></a>Opciones  
 **Nombre de seguimiento**  
 Especifica el nombre del seguimiento.  
  
 **Nombre del proveedor de seguimiento**  
 Muestra el nombre de la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] de la que va a realizarse un seguimiento. Este campo se rellena automáticamente con el nombre del servidor que haya especificado al conectarse. Para cambiar el nombre del proveedor de seguimiento, haga clic en **Cancelar** para cerrar el cuadro de diálogo e iniciar un nuevo seguimiento.  
  
 **Tipo de proveedor de seguimiento**  
 Muestra el tipo de proveedor que proporciona el seguimiento. El archivo de definición de seguimiento rellena el campo **Tipo de proveedor de seguimiento** automáticamente. No se puede modificar este campo.  
  
 **version**  
 Muestra la versión del servidor que proporciona el seguimiento. El archivo de definición de seguimiento rellena el campo **Versión** automáticamente. No se puede modificar este campo.  
  
 **Usar la plantilla**  
 Selecciona una plantilla del directorio de plantillas. El directorio se rellena con las plantillas predeterminadas y con cualquier tipo de plantilla definida por el usuario que se haya creado para el tipo de proveedor de seguimiento actual.  
  
 **Guardar en el archivo**  
 Captura los datos del seguimiento en un archivo .trc. Guardar los datos del seguimiento es útil para su posterior revisión y análisis.  
  
 **Establecer el tamaño máximo de archivo (MB)**  
 Si elige la opción de guardar los datos de seguimiento en un archivo, deberá especificar el tamaño máximo del mismo. El valor predeterminado es 5 megabytes (MB). El tamaño máximo está limitado únicamente por el sistema de archivos (NTFS, FAT) donde se guarde el archivo.  
  
 \<Gráfico > **Guardar como**  
 Después de seleccionar guardar, puede seleccionar este icono para cambiar el nombre de archivo.  
  
 **Habilitar sustitución incremental de archivos**  
 Seleccione esta opción para habilitar la creación de archivos adicionales, para que se acepten los datos del seguimiento cuando se alcance el tamaño máximo de archivo. Los nuevos nombres de archivo consisten en el nombre de archivo .trc original, numerado de forma secuencial. Por ejemplo, una vez que **NewTrace.trc** alcanza el tamaño máximo de archivo, se cierra, y se abre un nuevo archivo, **NewTrace_1.trc**, seguido de **NewTrace_2.trc**y así sucesivamente. La sustitución incremental de archivos está habilitada de forma predeterminada cuando se guarda un seguimiento en un archivo.  
  
 **El servidor procesa los datos de seguimiento**  
 Especifica que el servidor que ejecuta el seguimiento debe procesar los datos de seguimiento. El uso de esta opción reduce la sobrecarga de rendimiento en la que se incurre con el trazado. Si se selecciona esta opción, no se omite ningún evento, incluso en condiciones de gran demanda. Si esta casilla está desactivada, el Analizar de SQL Server se encarga del procesamiento y existe la posibilidad de que no se realice un seguimiento de algunos eventos de gran demanda.  
  
 **Guardar en la tabla**  
 Captura los datos del seguimiento en una tabla de base de datos. Guardar los datos del seguimiento es útil para su posterior revisión y análisis. Sin embargo, guardar los datos de un seguimiento en una tabla también puede aumentar de forma significativa la sobrecarga en el servidor en el que se guarda el seguimiento. Si es posible, no guarde la tabla de seguimiento en el mismo servidor del que se realiza un seguimiento.  
  
 \<Gráfico > **tabla de destino**  
 Después de seleccionar que los datos de seguimiento se guarden en una tabla de base de datos, puede seleccionar este icono para cambiar el nombre de la tabla.  
  
 **Establecer número máximo de filas (en miles)**  
 Especifica el número máximo de filas en las que guardar los datos. El valor predeterminado es 1000 filas.  
  
 **Habilitar hora de detención de seguimiento**  
 Establece la fecha y la hora de finalización y de cierre del seguimiento.  
  
## <a name="see-also"></a>Vea también  
 [Crear un seguimiento &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)  
  
  
