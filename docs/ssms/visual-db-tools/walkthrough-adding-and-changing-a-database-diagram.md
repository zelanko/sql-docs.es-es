---
title: 'Tutorial: Agregar y modificar un diagrama de base de datos | Microsoft Docs'
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- database diagrams [SQL Server], about database diagrams
- database diagrams [SQL Server], designing
- database diagrams [SQL Server], creating
ms.assetid: 228caa0d-8f24-46ab-86d1-b6d8631322bc
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f2c1a211f11917f54f0f2c69bd2d1b96034cba41
ms.contentlocale: es-es
ms.lasthandoff: 08/18/2017

---
# <a name="walkthrough-adding-and-changing-a-database-diagram"></a>Visita guiada: Agregar y modificar un diagrama de base de datos
En este tutorial se muestra cómo crear y modificar un diagrama de base de datos, así como la forma de realizar cambios en la base de datos mediante el componente Diagramas de base de datos. También se explica cómo agregar tablas al diagrama, crear relaciones entre las tablas, crear restricciones e índices en las columnas y modificar el nivel de información que puede verse en cada tabla.  
  
## <a name="prerequisites"></a>Requisitos previos  
Para completar esta visita guiada, necesitará:  
  
-   Acceso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] con la base de datos de ejemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject_md.md)]  
  
-   Una cuenta con privilegios **dbo** de propietario de la base de datos  
  
> [!NOTE]  
> Si intenta realizar cambios desde una cuenta sin suficientes privilegios para realizar los cambios en las tablas, aparecerá un mensaje de error.  
  
## <a name="creating-a-diagram"></a>Crear un diagrama  
  
#### <a name="to-create-a-new-database-diagram"></a>Para crear un nuevo diagrama de base de datos  
  
1.  En el menú **Ver** , haga clic en el **Explorador de objetos**.  
  
2.  Abra el nodo Bases de datos y, luego, el nodo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject_md.md)] .  
  
3.  Haga clic con el botón derecho en el nodo Diagramas de base de datos y elija **Nuevo diagrama de base de datos**.  
  
    Si la base de datos no dispone de los objetos necesarios para crear diagramas, aparecerá el mensaje siguiente: **Esta base de datos no tiene uno o varios de los objetos de soporte necesarios para usar diagramas de base de datos. ¿Desea crearlos?** Elija **Sí**.  
  
    Aparecerá el cuadro de diálogo **Agregar tabla** .  
  
4.  Seleccione **AddressType (persona)** y **Dirección (persona)** y, luego, haga clic en **Agregar**.  
  
    Se agregan dos tablas al diagrama.  
  
5.  Cierre el cuadro de diálogo **Agregar tabla** .  
  
#### <a name="to-view-different-column-data"></a>Para visualizar datos de columna diferentes  
  
1.  Haga clic con el botón secundario en la tabla `Address` . En el menú contextual, seleccione **Vista de tabla**y, a continuación, haga clic en **Estándar**.  
  
    En la tabla con cuadrícula se muestran tres columnas: **Nombre de columna**, **Tipo de datos**y **Permitir valores NULL**.  
  
2.  Haga clic con el botón derecho en la tabla `Address` , haga clic en **Vista de tabla** y seleccione **Claves**.  
  
    En la cuadrícula de la tabla se muestra una columna, con los nombres de tabla y columna. Solo aparecen las columnas que participan en los índices.  
  
## <a name="creating-new-tables"></a>Crear nuevas tablas  
  
#### <a name="to-create-tables-within-diagram-designer"></a>Para crear tablas en el Diseñador de diagramas  
  
1.  Haga clic con el botón derecho en una zona del Diseñador de diagramas que no sea una tabla existente y elija **Nueva tabla**.  
  
2.  En el cuadro de diálogo **Elegir nombre** , haga clic en **Aceptar** para admitir el nombre predeterminado, **Table1**.  
  
    Aparecerá una nueva tabla con cuadrícula con tres columnas: **Nombre de columna**, **Tipo de datos**y **Permitir valores NULL**.  
  
3.  Agregue la siguiente información a **Table1**:  
  
    |**Nombre de columna**|**Tipo de datos**|**Permitir valores NULL**|  
    |-------------------|-----------------|-------------------|  
    |**T1col1**|**int**|activado|  
    |**T1col2**|**varchar(50)**|activado|  
    |**T1col3**|**float**|activado|  
  
4.  Haga clic con el botón derecho en `T1col1` y seleccione **Establecer clave principal**.  
  
    Aparecerá un icono de llave junto al nombre de columna.  
  
5.  En el menú **Archivo** , haga clic en **Guardar Diagram1**.  
  
6.  En el cuadro de diálogo **Elegir nombre**, haga clic en **Aceptar** para admitir el nombre predeterminado **Diagram1**.  
  
7.  Aparecerá el cuadro de diálogo **Guardar`Table1` con un mensaje que indica que**  se guardará en la base de datos. Haga clic en **Sí**.  
  
## <a name="modifying-table-structure"></a>Modificar la estructura de la tabla  
Se pueden agregar restricciones CHECK y crear relaciones entre las tablas en el Diseñador de diagramas.  
  
#### <a name="to-create-check-constraints"></a>Para crear restricciones CHECK  
  
1.  En `Table1`, haga clic con el botón derecho en la fila `T1col3` y elija **Comprobar restricciones**.  
  
    Aparecerá el cuadro de diálogo **Comprobar restricciones** .  
  
2.  Haga clic en **Agregar**.  
  
    Aparecerá una nueva restricción en la lista **Restricción de comprobación seleccionada** con el nombre predeterminado `CK_Table1`.  
  
3.  Seleccione la fila **Expresión** en la cuadrícula y haga clic en el botón de puntos suspensivos.  
  
    Aparecerá el cuadro de diálogo **Expresión de restricción CHECK**.  
  
4.  Escriba **T1col3 > 5** y haga clic en **Aceptar**.  
  
    `Table1` tiene ahora una restricción para que todos los valores escritos en `T1col3` sean mayores de 5.  
  
5.  Haga clic en **Cerrar**.  
  
#### <a name="to-create-relationships-between-tables"></a>Para crear relaciones entre tablas  
  
1.  Cree una nueva tabla en el Diseñador de diagramas con el nombre `Table2` y con las siguientes columnas:  
  
    |**Nombre de columna**|**Tipo de datos**|**Permitir valores NULL**|  
    |-------------------|-----------------|-------------------|  
    |**T2col1**|**int**|no seleccionado|  
    |**T2col2**|**varchar(50)**|activado|  
    |**T2col3**|**xml**|activado|  
  
    > [!NOTE]  
    > Las columnas del lado de la clave principal de una relación de clave externa deben participar en una restricción PRIMARY KEY o UNIQUE.  
  
2.  Arrastre `T2col1` hasta `T1col1`.  
  
    Aparecen dos cuadros de diálogo: **Relación de clave externa** en segundo plano y **Tablas y columnas** , en primer plano.  
  
3.  Haga clic en **Aceptar** para guardar la nueva relación.  
  
4.  Haga clic en **Aceptar** nuevamente.  
  
## <a name="creating-indexes"></a>Crear índices  
Se pueden crear índices en la mayoría de los tipos de datos, incluso en XML.  
  
#### <a name="to-create-a-standard-index"></a>Para crear un índice estándar  
  
1.  Haga clic con el botón derecho en `Table1` y elija **Índices o claves**.  
  
    Aparecerá el cuadro de diálogo **Índices o claves** .  
  
2.  Haga clic en **Agregar**.  
  
    Aparecerá un nuevo índice en la lista **Clave principal o única, o índice seleccionado** con un nombre predeterminado similar a `IX_Table1`.  
  
3.  Seleccione la fila **Columnas** y haga clic en el botón de puntos suspensivos.  
  
    Aparecerá el cuadro de diálogo **Columnas de índice** .  
  
4.  Haga clic en la flecha de lista desplegable situada bajo **Nombre de columna** y seleccione `T1col2`.  
  
    > [!NOTE]  
    > Puede agregar columnas adicionales a este índice si selecciona la celda situada bajo `T1col2` y elige otro nombre de columna.  
  
5.  Haga clic en **Aceptar** para guardar el índice.  
  
6.  Haga clic en **Cerrar** en el cuadro de diálogo **Índices o claves** .  
  
#### <a name="to-create-an-xml-index"></a>Para crear un índice XML  
  
1.  Haga clic con el botón derecho en `T2col1` y elija **Establecer clave principal**.  
  
    > [!NOTE]  
    > Para poder agregar un índice XML, se debe establecer otra columna de la tabla como clave principal agrupada.  
  
2.  Haga clic con el botón derecho en la fila `T2col3` en `Table2` y seleccione **Índices XML**.  
  
    Aparecerá el cuadro de diálogo **Índices XML** .  
  
3.  Haga clic en **Agregar**.  
  
    Se agregará un índice XML con valores predeterminados a la lista **Índice XML seleccionado** .  
  
4.  Haga clic en **Cerrar**.  
  
    > [!NOTE]  
    > Los índices XML se crean por cada columna. El primer índice XML es el principal y cualquier otro índice es secundario.  
  
## <a name="saving-the-diagram"></a>Guardar el diagrama  
Todos los cambios realizados en el diagrama no se publican en la base de datos hasta que lo guarde. Si hay problemas o conflictos, aparecerá un cuadro de diálogo con más información.  
  
#### <a name="to-save-a-database-diagram"></a>Para guardar el diagrama de base de datos  
  
1.  En el menú **Archivo** , seleccione **Guardar Diagram1**.  
  
    Aparecerá el cuadro de diálogo **Guardar** . Si selecciona la opción **Advertir sobre las tablas afectadas** , se proporcionará información acerca de las tablas nuevas o modificadas.  
  
2.  Haga clic en **Aceptar**.  
  
3.  Si se produce algún error, aparecerá el cuadro de diálogo **Notificaciones después de guardar** con los errores y las causas. Solucione los errores y guarde el diagrama de nuevo.  
  
## <a name="next-steps"></a>Pasos siguientes  
Este diagrama es básico, únicamente con dos tablas existentes y otras dos nuevas, pero muestra el potencial de la creación de diagramas en una base de datos existente o de la creación de un nuevo esquema visual. Algunas sugerencias de investigación adicional son:  
  
-   Crear nuevos diagramas que incluyan grupos de tablas relacionadas  
  
-   Personalizar el volumen de información que aparece en cada tabla  
  
-   Modificar el diseño y agregar anotaciones  
  
-   Copiar el diagrama en un mapa de bits  
  
## <a name="see-also"></a>Vea también  
[Personalizar la cantidad de información mostrada en los diagramas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/customize-the-amount-of-information-displayed-in-diagrams-visual-database-tools.md)  
[Configurar el Diseñador de diagramas de base de datos &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/set-up-database-diagram-designer-visual-database-tools.md)  
[Agregar tablas a diagramas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/add-tables-to-diagrams-visual-database-tools.md)  
[Crear relaciones entre tablas en un diagrama &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-relationships-between-tables-on-a-diagram-visual-database-tools.md)  
[Crear índices XML](http://msdn.microsoft.com/en-us/6ecac598-355d-4408-baf7-1b2e8d4cf7c1)  
[Copiar una imagen del diagrama de base de datos en el Portapapeles &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/copy-an-image-of-a-database-diagram-to-the-clipboard-visual-database-tools.md)  
[Trabajar con el diseño de diagramas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/work-with-diagram-layout-visual-database-tools.md)  
  

