---
title: Creación, modificación y eliminación de índices espaciales | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- indexes [SQL Server], creating
- spatial indexes [SQL Server], dropping
- spatial indexes [SQL Server], creating
- indexes [SQL Server], dropping
- indexes [SQL Server], modifying
- spatial indexes [SQL Server], modifying
ms.assetid: 00c1b927-8ec5-44cf-87c2-c8de59745735
author: MladjoA
ms.author: mlandzic
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7be26a9819fdaf5b50d6169a4d94d8c7c5b906ee
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65935479"
---
# <a name="create-modify-and-drop-spatial-indexes"></a>Crear, modificar y quitar índices espaciales
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Un índice espacial puede realizar determinadas operaciones de manera más eficaz en una columna del tipo de datos **geometry** o **geography** (una *columna espacial*). Se puede especificar más de un índice espacial en una columna espacial. Por ejemplo, esto es útil para indizar diferentes parámetros de teselación en una columna única.  
  
 Existen varias restricciones para la creación de índices espaciales. Para obtener más información, vea [Restricciones en los índices espaciales](#restrictions) más adelante en este tema.  
  
> [!NOTE]  
>  Para obtener más información sobre la relación de índices espaciales para partición y para grupos de archivos, vea la sección "Comentarios" en [CREATE SPATIAL INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-spatial-index-transact-sql.md).  
  
##  <a name="creating"></a> Crear, modificar y quitar índices espaciales  
  
###  <a name="create"></a> Para crear un índice espacial  
 **Para crear un índice espacial mediante Transact-SQL**  
 [CREATE SPATIAL INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-spatial-index-transact-sql.md)  
  
 **Para crear un índice espacial mediante el cuadro de diálogo Nuevo índice en Management Studio**  
 ##### <a name="to-create-a-spatial-index-in-management-studio"></a>Para crear un índice espacial en Management Studio  
  
1.  En el Explorador de objetos, conéctese a una instancia del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] y expándala.  
  
2.  Expanda **Bases de datos**, a continuación, la base de datos que contiene la tabla con el índice especificado y, por último, **Tablas**.  
  
3.  Expanda la tabla para la que desee crear el índice.  
  
4.  Haga clic con el botón derecho en **Índices** y seleccione **Nuevo índice**.  
  
5.  En el campo **Nombre de índice** , escriba un nombre para el índice.  
  
6.  En la lista desplegable **Tipo de índice** , seleccione **Espacial**.  
  
7.  Para especificar la columna espacial que desee indizar, haga clic en **Agregar**.  
  
8.  En el cuadro de diálogo **Seleccionar columnas de** *\<nombre tabla>* , seleccione una columna de tipo **geometry** o **geography**. Para ello, active la casilla correspondiente. Las demás columnas espaciales se convierten en no editables. Si desea seleccionar una columna espacial diferente, primero debe borrar la columna actualmente seleccionada. Cuando termine, haga clic en **Aceptar**.  
  
9. Compruebe su selección de columna en la cuadrícula **Columnas de clave de índice** .  
  
10. En el panel **Seleccionar una página** del cuadro de diálogo **Propiedades del índice** , haga clic en **Espacial**.  
  
11. En la página **Espacial** , especifique los valores que desee usar para las propiedades espaciales del índice.  
  
     Al crear un índice en una columna de tipo **geometry** , debe especificar las coordenadas **(** _X mínima_ **,** _Y mínima_ **)** y **(** _X máxima_ **,** _Y máxima_ **)** del cuadro de límite. Para un índice de una columna de tipo **geography** , los campos de cuadro de límite se vuelven de solo lectura después de especificar el esquema de teselación **Cuadrícula geográfica** , porque la teselación de cuadrícula de geografía no usa un cuadro de límite.  
  
     Opcionalmente, puede especificar valores no predeterminados para el campo **Celdas por objeto** y para la densidad de cuadrícula en cualquier nivel del esquema de teselación. El número predeterminado de celdas por objeto es 16 para [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] u 8 para [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] o posterior y la densidad de cuadrícula predeterminada es **Media** para [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
     Puede seleccionar GEOMETRY_AUTO_GRID o GEOGRAPHY_AUTO_GRID para el esquema de teselación en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cuando se seleccionan GEOMETRY_AUTO_GRID o GEOGRAPHY_AUTO_GRID, se deshabilitan las opciones de densidad de cuadrícula Nivel 1, Nivel 2, Nivel 3 Nivel 4.  
  
     Para obtener más información acerca de estas propiedades, vea [Index Properties F1 Help](../../relational-databases/indexes/index-properties-f1-help.md).  
  
12. Haga clic en **Aceptar**.  
  
> [!NOTE]  
>  Para crear otro índice espacial en la misma columna o en otra columna espacial diferente, repita los pasos anteriores.  
  
  
 **Para crear un índice espacial mediante el Diseñador de tablas en Management Studio**  
 ##### <a name="to-create-a-spatial-index-in-table-designer"></a>Para crear un índice espacial en el Diseñador de tablas  
  
1.  En el Explorador de objetos, haga clic con el botón derecho en la tabla para la que quiere crear un índice espacial y luego haga clic en **Diseño**.  
  
     La tabla se abre en el Diseñador de tablas.  
  
2.  Seleccione una columna **geometry** o **geography** para el índice.  
  
3.  En el menú **Diseñador de tablas** , haga clic en **Índice espacial**.  
  
4.  En el cuadro de diálogo **Índices espaciales** , haga clic en **Agregar**.  
  
5.  Seleccione el nuevo índice en la lista **Índice espacial seleccionado** y configure las propiedades del índice espacial en la cuadrícula de la derecha. Para obtener información sobre las propiedades, vea [Cuadro de diálogo Índices espaciales &#40;Visual Database Tools&#41;](https://msdn.microsoft.com/library/4d84239a-68c7-4aa2-8602-2b51dd07260f).  
  
  
###  <a name="alter"></a> Para modificar un índice espacial  
  
-   [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)  
  
    > [!IMPORTANT]  
    >  Para cambiar opciones específicas de un índice espacial, como BOUNDING_BOX o GRID, puede usar una instrucción CREATE SPATIAL INDEX que especifica DROP_EXISTING = ON, o quitar el índice espacial y crear uno nuevo. Para ver un ejemplo, consulte [CREATE SPATIAL INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-spatial-index-transact-sql.md).  
  
-   [Modificar un índice](../../relational-databases/indexes/modify-an-index.md)  
  
-   [Mover un índice existente a un grupo de archivos diferente](../../relational-databases/indexes/move-an-existing-index-to-a-different-filegroup.md)  
  
  
###  <a name="drop"></a> Para quitar un índice espacial  
 **Para quitar un índice espacial mediante Transact-SQL**  
 [DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)  
  
 **Para quitar un índice mediante Management Studio**  
 [Eliminar un índice](../../relational-databases/indexes/delete-an-index.md)  
  
 **Para quitar un índice espacial mediante el Diseñador de tablas en Management Studio**  
 ##### <a name="to-drop-a-spatial-index-in-table-designer"></a>Para quitar un índice espacial en el Diseñador de tablas  
  
1.  En el Explorador de objetos, haga clic con el botón derecho en la tabla cuyo índice espacial quiere eliminar y elija **Diseño**.  
  
     La tabla se abre en el Diseñador de tablas.  
  
2.  En el menú **Diseñador de tablas** , haga clic en **Índice espacial**.  
  
     Se abrirá el cuadro de diálogo **Índice espacial** .  
  
3.  Haga clic en el índice que desee eliminar en la columna **Índice espacial seleccionado** .  
  
4.  Haga clic en **Eliminar**.  
  
  
##  <a name="restrictions"></a> Restricciones en los índices espaciales  
 Un índice espacial solamente puede crearse en una columna de tipo **geometría** o **geografía**.  
  
### <a name="table-and-view-restrictions"></a>Restricciones de las vistas y tablas  
 Los índices espaciales solo se pueden definir en una tabla que tenga una clave principal. El número máximo de columnas de clave principal en la tabla es de 15.  
  
 El tamaño máximo de los registros de clave de índice es 895 bytes. Los tamaños mayores producen un error.  
  
> [!NOTE]  
>  No se pueden cambiar los metadatos de clave principal mientras un índice espacial está definido en una tabla.  
  
 Los índices espaciales no se pueden especificar en vistas indizadas.  
  
### <a name="multiple-spatial-index-restrictions"></a>Varias restricciones de los índices espaciales  
 Puede crear hasta 249 índices espaciales en cualquiera de las columnas espaciales de una tabla admitida. Crear más de un índice espacial en la misma columna espacial puede ser útil, por ejemplo, para indizar parámetros de teselación diferentes en una única columna.  
  
 Solo puede crear un índice espacial al mismo tiempo.  
  
### <a name="spatial-indexes-and-process-parallelism"></a>Índices espaciales y paralelismo del proceso  
 Una generación de índices puede usar el paralelismo de procesos disponible.  
  
### <a name="version-restrictions"></a>Restricciones de versión  
 Las teselaciones espaciales incluidas en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] no se pueden replicar en [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] ni en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]. Debe usar las teselaciones espaciales de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] para los índices espaciales cuando la compatibilidad con versiones anteriores con las bases de datos de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] sea un requisito.  
  
  
## <a name="see-also"></a>Consulte también  
 [Información general sobre los índices espaciales](../../relational-databases/spatial/spatial-indexes-overview.md)  
  
  
