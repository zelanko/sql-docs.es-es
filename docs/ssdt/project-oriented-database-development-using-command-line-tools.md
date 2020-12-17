---
title: Desarrollo de bases de datos orientado a proyectos mediante herramientas de la línea de comandos
description: Vea los recursos disponibles en las herramientas de línea de comandos que SQL Server Data Tools proporciona para trabajar con archivos .dacpac, como SQLPackage.exe y dbSqlPackage.
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: 9a26def9-8fbd-43e4-9e57-414840b73ed8
author: markingmyname
ms.author: maghan
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 04/26/2017
ms.openlocfilehash: f84638d0ded57fcc1312258422de522aec997b39
ms.sourcegitcommit: 866554663ca3191748b6e4eb4d8d82fa58c4e426
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/16/2020
ms.locfileid: "97559247"
---
# <a name="project-oriented-database-development-using-command-line-tools"></a>Desarrollo de bases de datos orientado a proyectos mediante herramientas de la línea de comandos

SQL Server Data Tools proporciona herramientas de línea de comandos que habilitan diversos escenarios de desarrollo de bases de datos orientado a proyectos.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Descripción|  
|-|-|  
|[SqlPackage.exe](../tools/sqlpackage/sqlpackage.md)|En este tema se describe la utilidad SQLPackage.exe que se usa para las tareas siguientes:<br /><br />-   Extraer un archivo .dacpac de una base de datos activa de SQL Server.<br />-   Publicar un archivo .dacpac en una base de datos activa de SQL Server para actualizar incrementalmente el esquema de dicha base de datos de manera que coincida con el .dacpac.<br />-   Comparar un archivo .dacpac con una base de datos activa de SQL Server y generar un script Transact\-SQL de actualización incremental sin actualizar la base de datos activa.<br />-   Comparar dos archivos .dacpac para generar un script Transact\-SQL de actualización incremental.<br />-   Generar un informe XML en el que se resuman los cambios de actualización incremental que se realizarían si la base de datos se actualizara incrementalmente.|  
|[Usar MSDeploy con el proveedor de dbSqlPackage](../ssdt/using-msdeploy-with-dbsqlpackage-provider.md)|En este tema se describe el proveedor de la [Herramienta de implementación web](https://go.microsoft.com/fwlink/?LinkId=231798) denominado dbSqlPackage que se incluye con SSDT y funciona con la Herramienta de implementación web (MSDeploy.exe) de Microsoft Internet Information Services (IIS), que se usa para las tareas siguientes:<br /><br />-   Extraer un archivo .dacpac de una base de datos remota o local de SQL Server o Azure SQL Database.<br />-   Publicar un archivo .dacpac en una base de datos remota o local de SQL Server o Azure SQL Database para actualizarlo incrementalmente.<br />-   Publicar desde una base de datos local de SQL Server en una base de datos remota de SQL Server o Azure SQL para actualizar incrementalmente la base de datos remota.<br />-   Comparar un archivo .dacpac con una base de datos remota o local de SQL Server o Azure SQL Database para generar un script Transact\-SQL de actualización incremental sin actualizar la base de datos activa.<br />-   Generar un informe XML en el que se resuman los cambios de actualización incremental que se realizarían si la base de datos se actualizara incrementalmente.|  
  
## <a name="related-sections"></a>Secciones relacionadas  
[Desarrollo de bases de datos sin conexión orientado a proyectos](../ssdt/project-oriented-offline-database-development.md)  
  
