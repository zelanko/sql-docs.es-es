---
title: "Propiedades de la base de datos (p&#225;gina Grupos de archivos) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.databaseproperties.filegroups.f1"
ms.assetid: 8d06e859-73dd-4019-b6e8-99c5c5297697
caps.latest.revision: 31
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 31
---
# Propiedades de la base de datos (p&#225;gina Grupos de archivos)
  Utilice esta página para ver los grupos de archivos o para agregar un nuevo grupo de archivos a la base de datos seleccionada. Los tipos de grupo de archivos se separan en grupos de archivos de *filas*, datos FILESTREAM y grupos de archivos con optimización para memoria.  
  
 Los grupos de archivos de filas contienen archivos de registro y de datos normales. Los grupos de archivos de datos de FILESTREAM contienen archivos de datos de FILESTREAM. Estos archivos de datos almacenan información sobre cómo se almacenan los datos de objetos binarios grandes (BLOB) en el sistema de archivos, cuando se utiliza el almacenamiento de FILESTREAM. Las opciones son las mismas para ambos tipos de grupos de archivos.  
  
 Si FILESTREAM no está habilitado, la sección **FILESTREAM** no estará disponible. Puede habilitar el almacenamiento de FILESTREAM mediante el cuadro de diálogo [Propiedades del servidor (página Avanzadas)](../../database-engine/configure-windows/server-properties-advanced-page.md).  
  
 Para obtener más información sobre cómo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa los grupos de archivos de filas, vea [Archivos y grupos de archivos de base de datos](../../relational-databases/databases/database-files-and-filegroups.md). Para obtener más información sobre los grupos de archivos y datos de FILESTREAM, vea [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md).  
  
 Los grupos de archivos con optimización para memoria son necesarios para que una base de datos pueda contener una o más tablas con optimización para memoria.  
  
## Opciones de grupo de archivos de filas y de datos FILESTREAM  
 **Nombre**  
 Escriba el nombre del grupo de archivos.  
  
 **Archivos**  
 Muestra el recuento de archivos incluidos en el grupo de archivos.  
  
 **Solo lectura**  
 Seleccione esta opción para establecer el grupo de archivos en un estado de solo lectura.  
  
 **Valor de DB-Library**  
 Seleccione esta opción para establecer este grupo de archivos como el valor predeterminado. Puede tener un grupo de archivos predeterminado para las filas y un grupo de archivos predeterminado para los datos de FILESTREAM.  
  
 **Agregar**  
 Agrega una nueva fila en blanco a la lista de grupos de archivo de la base de datos.  
  
 **Quitar**  
 Quita la fila del grupo de archivos seleccionado de la cuadrícula.  
  
## Opciones de grupo de archivos de datos con optimización para memoria  
 **Nombre**  
 Escriba el nombre del grupo de archivos con optimización para memoria.  
  
 **Archivos FILESTREAM**  
 Muestra el número de archivos (contenedores) en el grupo de archivos de datos optimizados para memoria. Puede agregar contenedores en la página **Archivos** .  
  
 **Agregar**  
 Agrega una nueva fila en blanco a la lista de grupos de archivo de la base de datos.  
  
 **Quitar**  
 Quita la fila del grupo de archivos seleccionado de la cuadrícula.  
  
## Vea también  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
  
  