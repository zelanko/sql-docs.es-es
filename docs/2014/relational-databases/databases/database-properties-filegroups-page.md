---
title: Propiedades de la base de datos (página Grupos de archivos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql12.swb.databaseproperties.filegroups.f1
ms.assetid: 8d06e859-73dd-4019-b6e8-99c5c5297697
author: stevestein
ms.author: sstein
ms.openlocfilehash: d0546a17491ed5d3b36890a605c5faa922c24fe6
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84970185"
---
# <a name="database-properties-filegroups-page"></a>Propiedades de la base de datos (página Grupos de archivos)
  Utilice esta página para ver los grupos de archivos o para agregar un nuevo grupo de archivos a la base de datos seleccionada. Los tipos de grupo de archivos se separan en grupos de archivos de *filas* , datos FILESTREAM y grupos de archivos optimizados para memoria.  
  
 Los grupos de archivos de filas contienen archivos de registro y de datos normales. Los grupos de archivos de datos de FILESTREAM contienen archivos de datos de FILESTREAM. Estos archivos de datos almacenan información sobre cómo se almacenan los datos de objetos binarios grandes (BLOB) en el sistema de archivos, cuando se utiliza el almacenamiento de FILESTREAM. Las opciones son las mismas para ambos tipos de grupos de archivos.  
  
 Si FILESTREAM no está habilitado, la sección **FILESTREAM** no estará disponible. Puede habilitar el almacenamiento de FILESTREAM mediante el cuadro de diálogo [Propiedades del servidor (página Avanzadas)](../../database-engine/configure-windows/server-properties-advanced-page.md).  
  
 Para obtener más información sobre cómo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa los grupos de archivos de filas, vea [Archivos y grupos de archivos de base de datos](database-files-and-filegroups.md). Para obtener más información sobre los grupos de archivos y datos de FILESTREAM, vea [FILESTREAM &#40;SQL Server&#41;](../blob/filestream-sql-server.md).  
  
 Los grupos de archivos optimizados para memoria son necesarios para que una base de datos pueda contener una o más tablas optimizadas para memoria.  
  
## <a name="row-and-filestream-data-filegroup-options"></a>Opciones de grupo de archivos de filas y de datos FILESTREAM  
 **Nombre**  
 Escriba el nombre del grupo de archivos.  
  
 **Archivos**  
 Muestra el recuento de archivos incluidos en el grupo de archivos.  
  
 **Solo lectura**  
 Seleccione esta opción para establecer el grupo de archivos en un estado de solo lectura.  
  
 **Valor predeterminado**  
 Seleccione esta opción para establecer este grupo de archivos como el valor predeterminado. Puede tener un grupo de archivos predeterminado para las filas y un grupo de archivos predeterminado para los datos de FILESTREAM.  
  
 **Add (Agregar)**  
 Agrega una nueva fila en blanco a la lista de grupos de archivo de la base de datos.  
  
 **Remove**  
 Quita la fila del grupo de archivos seleccionado de la cuadrícula.  
  
## <a name="memory-optimized-data-filegroup-options"></a>Opciones de grupo de archivos de datos con optimización para memoria  
 **Nombre**  
 Escriba el nombre del grupo de archivos optimizados para memoria.  
  
 **Archivos FILESTREAM**  
 Muestra el número de archivos (contenedores) en el grupo de archivos de datos optimizados para memoria. Puede agregar contenedores en la página **Archivos** .  
  
 **Add (Agregar)**  
 Agrega una nueva fila en blanco a la lista de grupos de archivo de la base de datos.  
  
 **Remove**  
 Quita la fila del grupo de archivos seleccionado de la cuadrícula.  
  
## <a name="see-also"></a>Consulte también  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
  
