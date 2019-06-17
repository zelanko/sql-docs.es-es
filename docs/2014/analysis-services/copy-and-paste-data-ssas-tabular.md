---
title: Copiar y pegar datos (SSAS Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.pastepreviewdb.f1
ms.assetid: 2f8d8b3d-810b-4c31-98f2-341015e13da8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ad25ecae16a9b5e5f32554350a315156e9818241
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66086966"
---
# <a name="copy-and-paste-data-ssas-tabular"></a>Copiar y pegar datos (SSAS tabular)
  Puede copiar los datos de tabla de las aplicaciones externas y pegarlos en una tabla nueva o en una ya existente en el diseñador de modelos. Los datos que pega del Portapapeles deben estar en formato HTML, como los datos que se copian de Excel o Word. El diseñador de modelos detectará y aplicará automáticamente tipos de datos a los datos pegados. También puede modificar el tipo de datos o el formato para mostrar de una columna de forma manual.  
  
 A diferencia de las tablas con una conexión de origen de datos, las tablas pegadas no tienen una propiedad de nombre de conexión o de datos de origen. Los datos pegados se guardan en el archivo Model.bim. Los datos pegados se guardan junto con el proyecto o el archivo Model.bim.  
  
 Al implementar un modelo, los datos pegados también se implementan con él, independientemente de si el modelo se procesa con la implementación.  
  
 Secciones de este tema:  
  
-   [Requisitos previos](#bkmk_prerequisites)  
  
-   [Pegar datos](#bkmk_paste_data)  
  
-   [Cuadro de diálogo Vista previa de pegado](#bkmk_paste_preview)  
  
##  <a name="bkmk_prerequisites"></a> Requisitos previos  
 Hay algunas restricciones al pegar los datos:  
  
-   Las tablas pegadas no pueden tener más de 10.000 filas.  
  
-   Las tablas pegadas no deben estar particionadas.  
  
-   Las tablas pegadas no se admiten en el modo DirectQuery.  
  
-   Las opciones **Pegar y anexar** y **Pegar y reemplazar** solo están disponibles al trabajar con una tabla que se creó inicialmente pegando datos del Portapapeles. No se puede usar **Pegar datos anexados** ni **Pegar datos reemplazados** al agregar datos a una tabla de datos importados de otro tipo de origen de datos.  
  
-   Al usar **Pegar datos anexados** o **Pegar datos reemplazados**, los nuevos datos deben contener exactamente el mismo número de columnas que los originales. Si es posible, las columnas de datos que se pegan o anexan también deberían ser de los mismos tipos de datos que los de la tabla de destino, o ser de un tipo de datos compatible. En algunos casos puede usar un tipo de datos diferente, pero es posible que se muestre un error de **coincidencia de tipos** .  
  
##  <a name="bkmk_paste_data"></a> Pegar datos  
  
#### <a name="to-paste-data-into-the-designer"></a>Para pegar datos en el diseñador  
  
-   En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], haga clic en el menú **Editar** y, a continuación, haga clic en una de las opciones siguientes:  
  
    -   Haga clic en **Pegar** para pegar el contenido del Portapapeles en una tabla nueva.  
  
    -   Haga clic en **Pegar datos anexados** para pegar el contenido del Portapapeles como filas adicionales en la tabla seleccionada. Las nuevas filas se agregarán al final de la tabla.  
  
    -   Haga clic en **Pegar datos reemplazados** para reemplazar la tabla seleccionada con el contenido del Portapapeles. Todos los nombres de encabezado de columna existentes permanecerán en la tabla y se conservarán las relaciones.  
  
##  <a name="bkmk_paste_preview"></a> Cuadro de diálogo Vista previa de pegado  
 El cuadro de diálogo **Vista previa de pegado** le permite ver una vista previa de los datos que se copian en la ventana del diseñador y asegurarse de que se copian correctamente. Para obtener acceso a este cuadro de diálogo, copie datos basados en tabla en formato HTML en el diseñador, haga clic en el menú **Editar** y, después, en **Pegar**, **Pegar y anexar**o **Pegar y reemplazar**. Las opciones **Pegar y anexar** y **Pegar y reemplazar** solo están disponibles al agregar o reemplazar datos en una tabla creada copiando y pegando mediante el Portapapeles. No se puede usar **Pegar y anexar** ni **Pegar y reemplazar** para agregar datos en una tabla de datos importados.  
  
 Las opciones de este cuadro de diálogo son diferentes en función de que los datos se peguen en una tabla completamente nueva, en una tabla existente y reemplacen a los datos existentes, o se agreguen al final de una tabla existente.  
  
### <a name="paste-to-new-table"></a>Pegar en una nueva tabla  
 **Nombre de la tabla**  
 Especifique el nombre de la tabla que se creará en el diseñador.  
  
 **Datos que se van a pegar**  
 Muestra un ejemplo del contenido del Portapapeles que se agregará a la tabla de destino.  
  
### <a name="paste-append"></a>Pegar y anexar  
 **Datos existentes en la tabla**  
 Muestra un ejemplo de los datos existentes en la tabla para que pueda comprobar las columnas, tipos de datos, etc.  
  
 **Datos que se van a pegar**  
 Muestra un ejemplo del contenido del Portapapeles. Estos datos se anexarán a los datos existentes.  
  
### <a name="paste-replace"></a>Pegar y reemplazar  
 **Datos existentes en la tabla**  
 Muestra un ejemplo de los datos existentes en la tabla para que pueda comprobar las columnas, tipos de datos, etc.  
  
 **Datos que se van a pegar**  
 Muestra un ejemplo del contenido del Portapapeles. Se eliminarán los datos existentes en la tabla de destino y se incrustarán las nuevas filas en la tabla.  
  
## <a name="see-also"></a>Vea también  
 [Importar datos &#40;SSAS tabular&#41;](import-data-ssas-tabular.md)   
 [Orígenes de datos compatibles &#40;SSAS tabular&#41;](tabular-models/data-sources-supported-ssas-tabular.md)   
 [Establecer el tipo de datos de una columna &#40;SSAS tabular&#41;](tabular-models/set-the-data-type-of-a-column-ssas-tabular.md)  
  
  
