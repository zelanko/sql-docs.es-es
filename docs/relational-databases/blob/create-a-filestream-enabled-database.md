---
title: "Creación de una base de datos habilitada para FILESTREAM | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-blob
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FILESTREAM [SQL Server], FILESTREAM-enabled databases
ms.assetid: 0fc16356-76f7-44b8-a58b-f0b7c43694ec
caps.latest.revision: 16
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: fecfc5d5d8ac9460af07fd7cc42849aefdba2a09
ms.lasthandoff: 04/11/2017

---
# <a name="create-a-filestream-enabled-database"></a>crear una base de datos habilitada para FILESTREAM
  En este tema se muestra la forma de crear una base de datos que admite FILESTREAM. Dado que FILESTREAM utiliza un tipo especial de grupo de archivos, cuando cree la base de datos, debe especificar la cláusula CONTAINS FILESTREAM para un grupo de archivos como mínimo.  
  
 Un grupo de archivos FILESTREAM puede contener más de un archivo. Para obtener un ejemplo de código en el que se muestra cómo crear un grupo de archivos FILESTREAM que contiene varios archivos, vea [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md).  
  
### <a name="to-create-a-filestream-enabled-database"></a>Para crear una base de datos habilitada para FILESTREAM  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], haga clic en **Nueva consulta** para mostrar el Editor de consultas.  
  
2.  Copie el código [!INCLUDE[tsql](../../includes/tsql-md.md)] del ejemplo siguiente en el Editor de consultas. Este código [!INCLUDE[tsql](../../includes/tsql-md.md)] crea una base de datos habilitada para FILESTREAM denominada Archive.  
  
    > [!NOTE]  
    >  Para este script, debe existir el directorio C:\Data.  
  
3.  Para generar la base de datos, haga clic en **Ejecutar**.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo de código siguiente se crea una base de datos con el nombre de `Archive`. La base de datos contiene tres grupos de archivos: `PRIMARY`, `Arch1`y `FileStreamGroup1`. `PRIMARY` and `Arch1` son grupos de archivos normales que no pueden contener datos FILESTREAM. `FileStreamGroup1` es el grupo de archivos `FILESTREAM` .  
  
 [!code-sql[FILESTREAM#FS_CreateDB](../../relational-databases/blob/codesnippet/tsql/create-a-filestream-enab_1.sql)]  
  
 Para un grupo de archivos `FILESTREAM` , `FILENAME` hace referencia a una ruta de acceso. La ruta de acceso hasta la última carpeta debe existir y la última carpeta no debe existir. En este ejemplo, `c:\data` debe existir. Sin embargo, la subcarpeta `filestream1` no puede existir al ejecutar la instrucción `CREATE DATABASE` . Para obtener más información sobre la sintaxis, vea [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md).  
  
 Después de ejecutar el ejemplo anterior, aparecen un archivo filestream.hdr y una carpeta $FSLOG en la carpeta c:\Data\filestream1. El archivo filestream.hdr es un archivo de encabezado para el contenedor de FILESTREAM.  
  
> [!IMPORTANT]  
>  El archivo filestream.hdr es un archivo de sistema importante. Contiene información de encabezado de FILESTREAM. No quite ni modifique este archivo.  
  
 Para las bases de datos existentes, puede usar la instrucción [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) para agregar un grupo de archivos FILESTREAM.  
  
## <a name="see-also"></a>Vea también  
 [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
  
  
