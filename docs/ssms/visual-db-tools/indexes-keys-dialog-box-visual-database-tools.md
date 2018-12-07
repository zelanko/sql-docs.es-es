---
title: Índices o claves (cuadro de diálogo, Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdtsql.chm:65539
- vdt.ppg.indexeskeys
ms.assetid: 9e4060ba-80c3-468f-bccb-e12e99f672c2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cf2d4565166dc94569a7bb3815ce3d69112116c6
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52518377"
---
# <a name="indexes---keys-dialog-box-visual-database-tools"></a>Índices o claves (cuadro de diálogo, Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Utilice este cuadro de diálogo para crear o modificar índices, claves principales y claves únicas. Para tener acceso a este cuadro de diálogo, abra la definición de la tabla que tiene el índice o la clave, haga clic con el botón derecho en la cuadrícula de la definición de tabla y, a continuación, haga clic en **Índices o claves**.  
  
> [!NOTE]  
> Si se publica la tabla para la replicación, debe modificar el esquema mediante la instrucción Transact-SQL [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) u Objetos de administración de SQL Server (SMO). Si se modifica el esquema mediante el Diseñador de tablas o el Diseñador de diagramas de base de datos, se intentará eliminar la tabla y volver a crearla. No se pueden eliminar objetos publicados, por lo que la modificación del esquema generará un error.  
  
## <a name="options"></a>Opciones  
**Índice o clave Primary/Unique seleccionados**  
Enumera los índices y las claves principales o únicas. Seleccione uno de estos elementos para ver sus propiedades en la cuadrícula que aparece a la derecha. Si la lista está vacía, no se ha definido ninguna para la tabla.  
  
**Agregar**  
Crea un nuevo índice o una nueva clave principal o única.  
  
**Eliminar**  
Elimine la clave o el índice seleccionado en la lista **Índice o clave Primary/Unique seleccionados** .  
  
**Categoría General**  
Expandido, muestra las propiedades **Columnas**, **Is Unique**y **Tipo**.  
  
**Columnas**  
Muestra los criterios de ordenación elegidos para las columnas de la clave o el índice y proporciona acceso al cuadro de diálogo en el que se pueden definir los criterios de ordenación. Para que se muestre el cuadro de diálogo, haga clic en **Columnas** y, después, en el botón de puntos suspensivos (...) situado a la derecha del campo de propiedad.  
  
**Is Unique**  
Indica si los datos especificados en el índice o en la clave deben ser únicos. Esta propiedad no está disponible en los índices XML.  
  
**Tipo**  
Especifique si el elemento seleccionado en la lista **Índice o clave Primary/Unique seleccionados** es una clave única, una clave principal o un índice. Este campo es de solo lectura para las claves principales.  
  
**Categoría Identidad**  
Expandido, muestra los campos de propiedades de **Nombre** y **Descripción**.  
  
**Nombre**  
Muestra el nombre de la clave o el índice. Cuando se crea un nuevo índice o una nueva clave, aparece un nombre predeterminado que se genera a partir de la tabla de la ventana que está activa en el Diseñador de tablas. Este nombre se puede cambiar en cualquier momento.  
  
**Descripción**  
Proporciona un espacio para describir la clave o el índice. Para escribir una descripción más detallada, haga clic en **Descripción** y, después, en el botón de puntos suspensivos (**...**) situado a la derecha del campo de propiedad. De este modo, obtendrá un área más grande en la que escribir el texto.  
  
**Categoría Diseñador de tablas**  
Expandido, muestra la información de **Crear como CLUSTERED**.  
  
**Crear como CLUSTERED**  
Crear una clave o un índice clúster. Solo se permite un índice clúster en una tabla. Los datos de la tabla se almacenan en el orden del índice clúster. Para más información, consulte [Crear índices clúster](../../relational-databases/indexes/create-clustered-indexes.md) y [Crear índices no clúster](../../relational-databases/indexes/create-nonclustered-indexes.md).  
  
**Especificación de espacio de datos**  
Expandido, muestra información sobre **(Tipo de espacio de datos)**, **Nombre de esquema de partición o grupo de archivo**y **Lista de columnas de particiones**.  
  
**(Tipo de espacio de datos)**  
Indica si este índice o esta clave pertenece a un grupo de archivos o a un esquema de partición.  
  
**Nombre de esquema de partición o grupo de archivo**  
Muestra el nombre del grupo de archivos o del esquema de partición en el que se almacena.  
  
**Lista de columnas de particiones**  
Muestra una lista separada por comas de las columnas que participan en la función de las columnas de partición. Esta propiedad no está disponible si se selecciona Grupo de archivo en el campo **(Tipo de espacio de datos)** .  
  
**Especificación de relleno**  
Expandido, muestra información sobre **Factor de relleno** y **Rellenar índice**.  
  
**Factor de relleno**  
Establece el porcentaje de páginas de nivel de hoja del índice que el sistema puede rellenar. Una vez completada una página, el sistema debe dividirla si se agregan nuevos datos, lo que afecta al rendimiento.  
  
-   El valor 100 significa que las páginas estarán llenas y que utilizarán el menor volumen posible de espacio de almacenamiento. Este valor debe utilizarse únicamente cuando no se van a efectuar cambios en los datos, como por ejemplo, en una tabla de solo lectura.  
  
-   Un valor más bajo deja más espacio vacío en las páginas de datos, lo que reduce la necesidad de dividir las páginas de datos cuando los índices aumentan, pero requiere más espacio de almacenamiento.  
  
**Rellenar índice**  
Indica si se proporciona a las páginas intermedias de este índice el mismo porcentaje de espacio vacío (relleno) especificado en **Factor de relleno** cuando crecen.  
  
**Pasar por alto claves duplicadas**  
Especifica qué ocurre cuando se inserta durante una operación de inserción masiva una fila cuyo valor de clave es igual al valor de una clave existente. Si se elige:  
  
-   **Sí** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mostrará una advertencia, omitirá la fila entrante incorrecta e intentará insertar las filas restantes.  
  
-   **No** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mostrará un mensaje de error y revertirá toda la operación de inserción masiva.  
  
**Columnas incluidas**  
Muestra una lista separada por comas de los nombres de todas las columnas que forman la clave del índice. Las columnas de subclaves solo se pueden especificar en los índices no clúster. Esta propiedad estará oculta para los índices XML.  
  
**Está deshabilitado**  
Indica si este índice está deshabilitado. Se trata de una propiedad de solo lectura. Esta propiedad solo se establecerá en **Sí** si el índice se ha deshabilitado fuera de Visual Database Tools.  
  
**Clave Es texto completo**  
Especifica si este índice es una clave de texto completo. Para obtener más información sobre las claves de texto completo, vea los Libros en pantalla de SQL Server. Esta propiedad estará oculta para los índices XML.  
  
**Bloqueos de página permitidos**  
Especifique si se permite el bloqueo de páginas en este índice. Permitir o denegar el bloqueo de página afecta al rendimiento de la base de datos. El valor recomendado es **Sí**.  
  
**Volver a calcular estadísticas**  
Especifica si [!INCLUDE[ssDE](../../includes/ssde_md.md)] que subyace calcula las nuevas estadísticas cuando se crea el índice. Al volver a calcular las estadísticas se ralentiza la generación de índices, pero es muy probable que mejore el rendimiento de las consultas.  
  
**Bloqueos de fila permitidos**  
Especifique si se permite el bloqueo de filas en este índice. Permitir o denegar el bloqueo de fila afecta al rendimiento de la base de datos. El valor recomendado es **Sí**.  
  
## <a name="see-also"></a>Ver también  
[Trabajar con restricciones (Visual Database Tools)](https://msdn.microsoft.com/637098af-2567-48f8-90f4-b41df059833e)  
[Trabajar con claves (Visual Database Tools)](https://msdn.microsoft.com/31fbcc9f-2dc5-4bf9-aa50-ed70ec7b5bcd)  
  
