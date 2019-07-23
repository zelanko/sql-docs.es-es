---
title: Aumentar el tamaño de una base de datos | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- databases [SQL Server], size
- increasing database size
- database size [SQL Server], increasing
- size [SQL Server], databases
ms.assetid: 14f4206d-3afa-4ba9-9849-23e81d63306d
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 400d04da6865ca0bd8ebc6fc7d700dbeeedd378b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67934455"
---
# <a name="increase-the-size-of-a-database"></a>Aumentar el tamaño de una base de datos
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  En este tema se describe cómo aumentar el tamaño de una base de datos en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. La base de datos se expande aumentando el tamaño de los datos o el archivo de registro existentes, o bien agregando un archivo nuevo a la base de datos.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para aumentar el tamaño de una base de datos, use:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   No se puede agregar o quitar un archivo mientras se está ejecutando una instrucción BACKUP.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Requiere el permiso ALTER en la base de datos.  
  
##  <a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-increase-the-size-of-a-database"></a>Para aumentar el tamaño de una base de datos  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]y, a continuación, expándala.  
  
2.  Expanda **Bases de datos**, haga clic con el botón derecho en la base de datos cuyo tamaño quiera aumentar y haga clic en **Propiedades**.  
  
3.  En **Propiedades de la base de datos**, seleccione la página **Archivos** .  
  
4.  Para aumentar el tamaño de un archivo existente, aumente el valor de la columna **Tamaño inicial (MB)** correspondiente al archivo. Debe aumentar el tamaño de la base datos en 1 megabyte como mínimo.  
  
5.  Para aumentar el tamaño de una base de datos agregando un nuevo archivo, haga clic en **Agregar** y especifique los valores de dicho archivo. Para obtener más información, consulte [Agregar archivos de datos o de registro a una base de datos](../../relational-databases/databases/add-data-or-log-files-to-a-database.md).  
  
6.  Haga clic en **Aceptar**.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-increase-the-size-of-a-database"></a>Para aumentar el tamaño de una base de datos  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. Este ejemplo aumenta el tamaño del archivo `test1dat3`.  
  
 [!code-sql[DatabaseDDL#AlterDatabase5](../../relational-databases/databases/codesnippet/tsql/increase-the-size-of-a-d_1.sql)]  
  
 Para obtener más ejemplos, vea [Opciones File y Filegroup de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md).  
  
## <a name="see-also"></a>Consulte también  
 [Agregar archivos de datos o de registro a una base de datos](../../relational-databases/databases/add-data-or-log-files-to-a-database.md)   
 [Reducir una base de datos](../../relational-databases/databases/shrink-a-database.md)  
  
  
