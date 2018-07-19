---
title: Desarrollo de bases de datos orientado a proyectos mediante herramientas de la línea de comandos | Microsoft Docs
ms.custom:
- SSDT
ms.date: 04/26/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9a26def9-8fbd-43e4-9e57-414840b73ed8
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 482e777563e825c7d5d76d7f04b11c6b46be708f
ms.sourcegitcommit: 2f07d285824a8982c279f3816b220e61a2d91b06
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/29/2018
ms.locfileid: "37094653"
---
# <a name="project-oriented-database-development-using-command-line-tools"></a>Desarrollo de bases de datos orientado a proyectos mediante herramientas de la línea de comandos
SQL Server Data Tools proporciona herramientas de línea de comandos que habilitan diversos escenarios de desarrollo de bases de datos orientado a proyectos.  
  
## <a name="in-this-section"></a>En esta sección  
  
|||  
|-|-|  
|[SqlPackage.exe](../tools/sqlpackage.md)|En este tema se describe la utilidad SQLPackage.exe que se usa para las tareas siguientes:<br /><br />-   Extraer un archivo .dacpac de una base de datos activa de SQL Server.<br />-   Publicar un archivo .dacpac en una base de datos activa de SQL Server para actualizar incrementalmente el esquema de dicha base de datos de manera que coincida con el .dacpac.<br />-   Comparar un archivo .dacpac con una base de datos activa de SQL Server y generar un script Transact\-SQL de actualización incremental sin actualizar la base de datos activa.<br />-   Comparar dos archivos .dacpac para generar un script Transact\-SQL de actualización incremental.<br />-   Generar un informe XML en el que se resuman los cambios de actualización incremental que se realizarían si la base de datos se actualizara incrementalmente.|  
|[Usar MSDeploy con el proveedor de dbSqlPackage](../ssdt/using-msdeploy-with-dbsqlpackage-provider.md)|En este tema se describe el proveedor de la [Herramienta de implementación web](http://go.microsoft.com/fwlink/?LinkId=231798) denominado dbSqlPackage que se incluye con SSDT y funciona con la Herramienta de implementación web (MSDeploy.exe) de Microsoft Internet Information Services (IIS), que se usa para las tareas siguientes:<br /><br />-   Extraer un archivo .dacpac de una base de datos remota o local de SQL Server o SQL Azure.<br />-   Publicar un archivo .dacpac en una base de datos remota o local de SQL Server o SQL Azure para actualizarlo incrementalmente.<br />-   Publicar desde una base de datos local de SQL Server en una base de datos remota de SQL Server o SQL Azure para actualizar incrementalmente la base de datos remota.<br />-   Comparar un archivo .dacpac con una base de datos remota o local de SQL Server o SQL Azure para generar un script Transact\-SQL de actualización incremental sin actualizar la base de datos activa.<br />-   Generar un informe XML en el que se resuman los cambios de actualización incremental que se realizarían si la base de datos se actualizara incrementalmente.|  
  
## <a name="related-sections"></a>Secciones relacionadas  
[Desarrollo de bases de datos sin conexión orientado a proyectos](../ssdt/project-oriented-offline-database-development.md)  
  
