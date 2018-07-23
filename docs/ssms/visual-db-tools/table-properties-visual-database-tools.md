---
title: Propiedades de tabla (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-visual-db
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- vdt.tabledesigner
- vdt.designers.properties.Table
ms.assetid: cc392987-1aab-45f5-b5af-a26be53409bf
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7ace32c9a58718e567b7b4dd77b201a3f6a60775
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/12/2018
ms.locfileid: "38981037"
---
# <a name="table-properties-visual-database-tools"></a>Propiedades de la tabla (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Estas propiedades aparecen en la ventana Propiedades cuando se hace clic con el botón secundario en el Diseñador de tablas y se selecciona Propiedades. A menos que se especifique lo contrario, podrá modificar estas propiedades en la ventana Propiedades cuando la tabla esté seleccionada.  
  
> [!NOTE]  
> Si se publica la tabla para la replicación, debe modificar el esquema mediante la instrucción Transact-SQL [ALTER TABLE](http://msdn.microsoft.com/f1745145-182d-4301-a334-18f799d361d1) u Objetos de administración de SQL Server (SMO). Si se modifica el esquema mediante el Diseñador de tablas o el Diseñador de diagramas de base de datos, se intentará eliminar la tabla y volver a crearla. No se pueden eliminar objetos publicados, por lo que la modificación del esquema generará un error.  
  
## <a name="show-table-properties-in-table-designer"></a>Mostrar las propiedades de tabla en el Diseñador de tablas  
  
> [!NOTE]  
> Las propiedades de este tema se ordenan por categoría en lugar de alfabéticamente.  
  
**Categoría Identidad**  
Se expande para mostrar las propiedades **Nombre**, **Descripción**y **Esquema**.  
  
**Nombre**  
Muestra el nombre de la tabla. Para editar el nombre, escriba en el cuadro de texto.  
  
> [!CAUTION]  
> Si las consultas, vistas, funciones definidas por el usuario, procedimientos almacenados o programas existentes hacen referencia a la tabla, la modificación del nombre hará que estos objetos dejen de ser válidos.  
  
**Nombre de la base de datos**  
Muestra el nombre del origen de datos de la tabla seleccionada.  
  
**Descripción**  
Muestra una descripción de la tabla seleccionada. Para ver o editar la descripción completa, haga clic en la descripción y después en el botón de puntos suspensivos **(…)** situado a la derecha de la propiedad.  
  
**Esquema**  
Muestra el nombre del esquema al que pertenece esta tabla (solo se aplica a Microsoft SQL Server).  
  
**Nombre de servidor**  
Muestra el nombre del servidor del origen de datos.  
  
**Categoría Diseñador de tablas**  
Se expande para mostrar las propiedades de **Columna de identidad**, **Indizable**y **Replicado**.  
  
**Columna de identidad**  
Muestra la columna utilizada como columna de identidad de la tabla. Para cambiar la columna de identidad, elija una en la lista desplegable. Solo se mostrarán en la lista columnas de tipo de datos numérico.  
  
**Indizable**  
Muestra si la tabla puede indizarse. Si la tabla no puede indizarse, puede deberse a que no es el propietario de la tabla o a que la tabla contiene columnas con tipos de datos text, ntext o image.  
  
**Replicado**  
Muestra si la columna se replica en otra ubicación  
  
**Categoría Especificación de espacio de datos normal**  
Se expande para mostrar las propiedades de **(Tipo de espacio de datos)**, **Nombre de esquema de partición o grupo de archivos**y **Lista de columnas de particiones**.  
  
**(Tipo de espacio de datos)**  
Indica si la tabla se almacena utilizando un grupo de archivos o un esquema de partición.  
  
**Nombre de esquema de partición o grupo de archivos**  
Muestra el nombre del grupo de archivos o esquema de partición.  
  
**Lista de columnas de particiones**  
Proporciona acceso al cuadro de diálogo **Lista de columnas de particiones** .  
  
**Columna de GUID de filas**  
Muestra la columna utilizada por Microsoft SQL Server como columna ROWGUID de la tabla. Para cambiar la columna ROWGUID, elija una en la lista desplegable (solo se aplica a SQL Server 7.0 o posterior).  
  
**Grupo de archivos Text/Image**  
Proporciona una lista desplegable en la que se puede elegir el grupo de archivos para columnas que tienen tipos de datos text o image. Si la tabla se almacena utilizando un esquema de partición, deje este campo en blanco.  
  
## <a name="see-also"></a>Ver también  
[Diseñar tablas (Visual Database Tools)](../../ssms/visual-db-tools/design-tables-visual-database-tools.md)  
  
