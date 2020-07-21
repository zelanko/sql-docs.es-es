---
title: Editar una conexión de origen de datos existente (SSAS tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.selexistconn.f1
ms.assetid: 97e63f18-a01d-4c91-a411-e7e6d40a0647
author: minewiskan
ms.author: owend
ms.openlocfilehash: 1dd8ac9a27d1bcf46ba14b5f49fee3cc9b3b3b4e
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/08/2020
ms.locfileid: "84528461"
---
# <a name="edit-an-existing-data-source-connection-ssas-tabular"></a>Editar una conexión de origen de datos existente (SSAS tabular)
  Este tema describe cómo editar las propiedades de una conexión de origen de datos existente en un modelo tabular.  
  
 Después de crear una conexión a un origen de datos externo, puede modificar esa conexión posteriormente de estas maneras:  
  
-   Puede cambiar la información de conexión, incluido el archivo, fuente o base de datos utilizados como origen, sus propiedades u otras opciones de conexión específicas del proveedor.  
  
-   Puede cambiar las asignaciones de tabla y de columna, así como quitar las referencias a las columnas que ya no se utilizan.  
  
-   Puede cambiar las tablas, vistas o columnas que obtiene del origen de datos externo.  
  
## <a name="modify-a-connection"></a>Modificar una conexión  
 Este procedimiento describe cómo modificar una conexión de origen de datos de base de datos. Algunas opciones para trabajar con orígenes de datos difieren según el tipo de origen de datos; sin embargo, debería ser posible identificar fácilmente las diferencias.  
  
#### <a name="to-change-the-external-data-source-used-by-a-current-connection"></a>Para cambiar el origen de datos externo utilizado por una conexión actual  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], haga clic en el menú **Modelo** y, a continuación, en **Conexiones existentes**.  
  
2.  Seleccione la conexión de origen de datos que desea modificar y, a continuación, haga clic en **Editar**.  
  
3.  En el cuadro de diálogo **Editar conexión** , haga clic en **Examinar** para buscar otra base de datos del mismo tipo pero con un nombre o ubicación diferente.  
  
     En cuanto cambia el archivo de base de datos, un mensaje aparece indicando que tiene que guardar y actualizar las tablas para ver los nuevos datos.  
  
4.  Haga clic en **Guardar**y, a continuación, en **Cerrar**.  
  
5.  En [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], haga clic en **Modelo**, a continuación, en **Procesar**y, por último, en **Procesar todo**.  
  
     Las tablas se vuelven a procesar utilizando el nuevo origen de datos, pero con las selecciones de datos originales.  
  
    > [!NOTE]  
    >  Si el nuevo origen de datos contiene alguna tabla adicional que no se encontraba en el origen de datos original, debe volver a abrir la conexión cambiada y agregar las tablas.  
  
## <a name="edit-table-and-column-mappings-bindings"></a>Editar las asignaciones de columna y de tabla (enlaces)  
 Este procedimiento describe cómo editar las asignaciones una vez ha cambiado un origen de datos.  
  
#### <a name="to-edit-column-mappings-when-a-data-source-changes"></a>Para editar la asignación de columnas cuando se cambia un origen de datos  
  
1.  Seleccione una tabla en el diseñador de modelos.  
  
2.  Haga clic en el menú **Tabla** y, a continuación, en **Propiedades de la tabla**.  
  
     El nombre de la tabla seleccionada se muestra en el cuadro **Nombre de la tabla** . El cuadro **Nombre del origen** contiene el nombre de la tabla en el origen de datos externo. Si las columnas tienen nombres distintos en el origen y en el modelo, puede alternar entre los dos conjuntos de nombres de columnas seleccionando las opciones **Origen** o **Modelo**.  
  
3.  Para cambiar la tabla que se usa como origen de datos, en **Nombre del origen**, seleccione una tabla diferente de la actual.  
  
4.  Cambie la asignación de columnas si es necesario:  
  
    1.  Para agregar columnas que se encuentran en el origen pero no en el modelo, active la casilla situada al lado del nombre de cada columna.  
  
         Los datos reales se cargarán en el modelo la próxima vez que actualice.  
  
    2.  Si algunas columnas del modelo ya no están disponibles en el origen de datos actual, aparece un mensaje en el área de notificación con una lista de las columnas no válidas. No es necesario hacer nada más.  
  
5.  Haga clic en **Guardar** para aplicar los cambios en el modelo.  
  
     Cuando guarde el conjunto actual de propiedades de la tabla, es posible que aparezca un mensaje indicando que debe procesar las tablas. Haga clic en **Procesar** para cargar los datos actualizados en el modelo.  
  
## <a name="see-also"></a>Consulte también  
 [Procesar datos &#40;SSAS tabular&#41;](process-data-ssas-tabular.md)   
 [Orígenes de datos compatibles &#40;SSAS tabular&#41;](tabular-models/data-sources-supported-ssas-tabular.md)  
  
  
