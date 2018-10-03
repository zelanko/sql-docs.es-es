---
title: Aumentar el tamaño de una base de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- databases [SQL Server], size
- increasing database size
- database size [SQL Server], increasing
- size [SQL Server], databases
ms.assetid: 14f4206d-3afa-4ba9-9849-23e81d63306d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7cd528c27ed34c91a076f79e0bfe8b0d1719a4a4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48069425"
---
# <a name="increase-the-size-of-a-database"></a>Aumentar el tamaño de una base de datos
  En este tema se describe cómo aumentar el tamaño de una base de datos en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. La base de datos se expande aumentando el tamaño de los datos o el archivo de registro existentes, o bien agregando un archivo nuevo a la base de datos.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para aumentar el tamaño de una base de datos, use:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   No se puede agregar o quitar un archivo mientras se está ejecutando una instrucción BACKUP.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Requiere el permiso ALTER en la base de datos.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-increase-the-size-of-a-database"></a>Para aumentar el tamaño de una base de datos  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]y, a continuación, expándala.  
  
2.  Expanda **Bases de datos**, haga clic con el botón derecho en la base de datos cuyo tamaño quiera aumentar y haga clic en **Propiedades**.  
  
3.  En **Propiedades de la base de datos**, seleccione la página **Archivos** .  
  
4.  Para aumentar el tamaño de un archivo existente, aumente el valor de la columna **Tamaño inicial (MB)** correspondiente al archivo. Debe aumentar el tamaño de la base datos en 1 megabyte como mínimo.  
  
5.  Para aumentar el tamaño de una base de datos agregando un nuevo archivo, haga clic en **Agregar** y especifique los valores de dicho archivo. Para obtener más información, consulte [Agregar archivos de datos o de registro a una base de datos](add-data-or-log-files-to-a-database.md).  
  
6.  Haga clic en **Aceptar**.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-increase-the-size-of-a-database"></a>Para aumentar el tamaño de una base de datos  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. Este ejemplo aumenta el tamaño del archivo `test1dat3`.  
  
 [!code-sql[DatabaseDDL#AlterDatabase5](../../snippets/tsql/SQL14/tsql/databaseddl/transact-sql/alterdatabase.sql#alterdatabase5)]  
  
 Para obtener más ejemplos, vea [Opciones File y Filegroup de ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-file-and-filegroup-options).  
  
## <a name="see-also"></a>Vea también  
 [Agregar archivos de datos o de registro a una base de datos](add-data-or-log-files-to-a-database.md)   
 [Reducir una base de datos](shrink-a-database.md)  
  
  
