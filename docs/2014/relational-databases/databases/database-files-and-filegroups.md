---
title: Archivos y grupos de archivos de base de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- databases [SQL Server], files
- filegroups [SQL Server]
- transaction logs [SQL Server], about
- transaction logs [SQL Server], files
- .mdf files
- data files [SQL Server]
- default filegroups
- files [SQL Server], about files and filegroups
- secondary files [SQL Server]
- log files [SQL Server]
- .ndf files
- files [SQL Server]
- .ldf files
- database files [SQL Server]
- databases [SQL Server], filegroups
- filegroups [SQL Server], types
- primary filegroups [SQL Server]
- user-defined filegroups [SQL Server]
- filegroups [SQL Server], about filegroups
- primary files [SQL Server]
- file types [SQL Server]
ms.assetid: 9ca11918-480d-4838-9198-cec221ef6ad0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3d75dee637a5579ca3f189e14333fbf9356623d0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62917282"
---
# <a name="database-files-and-filegroups"></a>Archivos y grupos de archivos de base de datos
  Como mínimo, todas las bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tienen dos archivos del sistema operativo: un archivo de datos y un archivo de registro. Los archivos de datos contienen datos y otros objetos, como tablas, índices, procedimientos almacenados y vistas. Los archivos de registro contienen la información necesaria para recuperar todas las transacciones de la base de datos. Los archivos de datos se pueden agrupar en grupos de archivos para su asignación y administración.  
  
## <a name="database-files"></a>Archivos de la base de datos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tienen tres tipos de archivos, tal como se muestra en la tabla siguiente.  
  
|Archivo|Descripción|  
|----------|-----------------|  
|Principal|El archivo de datos principal incluye la información de inicio de la base de datos y apunta a los demás archivos de la misma. Los datos y objetos del usuario se pueden almacenar en este archivo o en archivos de datos secundarios. Cada base de datos tiene un archivo de datos principal. La extensión recomendada para los nombres de archivos de datos principales es .mdf.|  
|Secundario|Los archivos de datos secundarios son opcionales, están definidos por el usuario y almacenan los datos del usuario. Se pueden utilizar para distribuir datos en varios discos colocando cada archivo en una unidad de disco distinta. Además, si una base de datos supera el tamaño máximo establecido para un archivo de Windows, puede utilizar los archivos de datos secundarios para permitir el crecimiento de la base de datos.<br /><br /> La extensión de nombre de archivo recomendada para los archivos de datos secundarios es .ndf.|  
|Registro de transacciones|Los archivos del registro de transacciones contienen la información de registro que se utiliza para recuperar la base de datos. Cada base de datos debe tener al menos un archivo de registro. La extensión recomendada para los nombres de archivos de registro es .ldf.|  
  
 Por ejemplo, puede crearse una base de datos sencilla denominada **Ventas** con un archivo principal que contenga todos los datos y objetos y un archivo de registro con la información del registro de transacciones. Por otra parte, puede crearse una base de datos más compleja, **Pedidos** , compuesta por un archivo principal y cinco archivos secundarios. Los datos y objetos de la base de datos se reparten entre los seis archivos, y cuatro archivos de registro adicionales contienen la información del registro de transacciones.  
  
 De forma predeterminada, los datos y los registros de transacciones se colocan en la misma unidad y ruta de acceso para administrar los sistemas de un solo disco, pero puede que esto no resulte óptimo para los entornos de producción. Se recomienda colocar los archivos de datos y de registro en distintos discos.  
  
## <a name="filegroups"></a>Grupos de archivos  
 Cada base de datos tiene un grupo de archivos principal. Este grupo de archivos contiene el archivo de datos principal y cualquier otro archivo secundario que no se encuentre en otro grupo de archivos. Se pueden crear grupos de archivos definidos por el usuario para agrupar archivos con fines administrativos y de asignación y ubicación de datos.  
  
 Por ejemplo, pueden crearse tres archivos, Datos1.ndf, Datos2.ndf y Datos3.ndf, en tres unidades de disco respectivamente para asignarlos posteriormente al grupo de archivos **grArchivos1**. A continuación, se puede crear una tabla específicamente para el grupo de archivos **grArchivos1**. Las consultas de datos de la tabla se distribuirán por los tres discos, con lo que mejorará el rendimiento. Puede obtenerse la misma mejora del rendimiento con un solo archivo creado en un conjunto de bandas RAID (matriz redundante de discos independientes). No obstante, los archivos y grupos de archivos permiten agregar fácilmente nuevos archivos a discos nuevos.  
  
 Todos los archivos de datos se almacenan en los grupos de archivos que se indican en la tabla siguiente.  
  
|Grupo de archivos|Descripción|  
|---------------|-----------------|  
|Principal|Grupo de archivos que contiene el archivo principal. Todas las tablas del sistema se asignan al grupo de archivos principal.|  
|Definidos por el usuario|Cualquier grupo de archivos creado específicamente por el usuario al crear la base de datos o al modificarla.|  
  
### <a name="default-filegroup"></a>Grupo de archivos predeterminado  
 Cuando se crean objetos en la base de datos sin especificar a qué grupo de archivos pertenecen, se asignan al grupo de archivos predeterminado. Siempre existe un grupo de archivos designado como predeterminado. Los archivos del grupo de archivos predeterminado deben ser lo suficientemente grandes como para dar cabida a todos los objetos nuevos no asignados a otros grupos de archivos.  
  
 El grupo de archivos PRINCIPAL es el predeterminado, a menos que se cambie mediante la instrucción ALTER DATABASE. Los objetos y las tablas del sistema no se asignan al nuevo grupo de archivos predeterminado, sino que siguen asignados al grupo de archivos PRIMARY.  
  
## <a name="related-content"></a>Contenido relacionado  
 [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)  
  
 [Opciones File y Filegroup de ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-file-and-filegroup-options)  
  
 [Adjuntar y separar bases de datos &#40;SQL Server&#41;](database-detach-and-attach-sql-server.md)  
  
  
