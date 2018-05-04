---
title: Exportar e importar objetos de minería de datos | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- backing up databases [Analysis Services]
- exporting mining models
- exporting mining structures
- mining structures [Analysis Services], creating
- mining structures [DMX], exporting
- mining models [Analysis Services], migration
ms.assetid: 10a83b13-2640-4ff5-80c8-a35e1d692908
caps.latest.revision: 23
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 6a648eed1d1e3d46eb11f4d71bb80fbdff21764f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="export-and-import-data-mining-objects"></a>Exportar e importar objetos de minería de datos
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Además de la funcionalidad incluida en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para crear copias de seguridad, restaurar y migrar soluciones, la minería de datos de SQL Server proporciona la capacidad de transferir rápidamente estructuras y modelos de minería de datos entre servidores diferentes usando Extensiones de minería de datos (DMX).  
  
 Si la solución de minería de datos usa datos relacionales en lugar de una base de datos multidimensional, la transferencia de los modelos mediante **EXPORT** e **IMPORT** es mucho más rápida y sencilla que si se usa la restauración de la base de datos o se implementa una solución completa.  
  
 En esta sección se ofrece información general sobre cómo transferir estructuras y modelos de minería de datos mediante instrucciones DMX. Para más información sobre la sintaxis, además de ejemplos, vea [EXPORT &#40;DMX&#41;](../../dmx/export-dmx.md) e [IMPORT &#40;DMX&#41;](../../dmx/import-dmx.md).  
  
> [!NOTE]  
>  Debe ser administrador de la base de datos o del servidor para exportar o importar objetos de una base de datos de Microsoft SQL Server Analysis Services.  
  
## <a name="exporting-data-mining-structures"></a>Exportar estructuras de minería de datos  
 Al exportar una estructura de minería de datos, la instrucción EXPORT exporta automáticamente todos los modelos asociados. Si desea controlar los objetos que se exportan, debe especificar cada uno de ellos por su nombre.  
  
 Si se ha procesado la estructura de minería de datos y se han almacenado los resultados en memoria caché, que es el comportamiento predeterminado, al exportar la estructura de minería de datos, la definición contiene un resumen de los datos en los que está basada dicha estructura. Para quitar este resumen, debe borrar la caché asociada a la estructura de minería de datos realizando una operación **Process Clear Structure** . Para más información, consulte [Process a Mining Structure](../../analysis-services/data-mining/process-a-mining-structure.md).  
  
### <a name="exporting-data-mining-models"></a>Exportar modelos de minería de datos  
 Puede usar la palabra clave **WITH DEPENDENCIES** para exportar el origen de datos y la definición de vista del origen de datos junto con el modelo de minería de datos y su estructura.  
  
 Cuando se exporta un modelo de minería de datos sin exportar sus dependencias, la instrucción EXPORT exportará la definición del modelo y su estructura, pero no la definición de los orígenes de datos. Como consecuencia, después de importar el modelo, podrá examinarlo inmediatamente, pero si desea volver a procesar el modelo de minería de datos en el servidor de destino o ejecutar consultas en los datos subyacentes, debe crear un origen de datos correspondiente en el servidor de destino.  
  
## <a name="importing-data-mining-structures-and-models"></a>Importar estructuras y modelos de minería de datos  
 Cuando se importa un objeto de minería de datos, dicho objeto se importa en el servidor y la base de datos a los que se está conectado al ejecutar la instrucción IMPORT. Si el archivo de importación incluye una base de datos que no existe en el servidor, se creará la base de datos.  
  
 También puede importar una estructura o un modelo de minería de datos usando el comando **Restore** . Los modelos o las estructuras se restaurarán en la base de datos que tenga el mismo nombre que la base de datos de la que se exportaron. Para más información, consulte [Restore Options](../../analysis-services/multidimensional-models/restore-options.md).  
  
## <a name="remarks"></a>Comentarios  
 No puede importar un modelo o una estructura en un servidor si ya existe un modelo o una estructura con el mismo nombre en ese servidor. Tampoco puede exportar un objeto de minería de datos y, a continuación, modificar el nombre de dicho objeto en el archivo de exportación. Por consiguiente, para evitar conflictos de nombres, debería eliminar el objeto de minería de datos en el servidor de destino o cambiar el nombre del objeto de minería de datos antes de exportar la definición.  
  
## <a name="see-also"></a>Vea también  
 [Administración de soluciones de minería de datos y objetos](../../analysis-services/data-mining/management-of-data-mining-solutions-and-objects.md)  
  
  
