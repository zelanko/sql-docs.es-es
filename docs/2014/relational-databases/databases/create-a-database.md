---
title: Creacíón de una base de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- databases [SQL Server], creating
- database creation [SQL Server], SQL Server Management Studio
- creating databases
ms.assetid: 4c4beea2-6cbc-4352-9db6-49ea8130bb64
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7f527d9767a6e821d0d4d5527fcad70e37f16e3c
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52799117"
---
# <a name="create-a-database"></a>Crear una base de datos
  En este tema se describe cómo crear una base de datos en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Requisitos previos](#Prerequisites)  
  
     [Recomendaciones](#Recommendations)  
  
     [Seguridad](#Security)  
  
-   **Para crear una base de datos, use:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   En una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]se pueden especificar 32.767 bases de datos como máximo.  
  
###  <a name="Prerequisites"></a> Requisitos previos  
  
-   La instrucción CREATE DATABASE debe ejecutarse en modo de confirmación automática (el modo predeterminado de administración de transacciones) y no se permite en una transacción explícita o implícita.  
  
###  <a name="Recommendations"></a> Recomendaciones  
  
-   Cada vez que se crea, modifica o quita una base de datos de usuario, se debe hacer una copia de seguridad de la base de datos [maestra](master-database.md) .  
  
-   Cuando cree una base de datos, defina el mayor tamaño posible para los archivos de datos según la cantidad de datos máxima prevista para la base datos.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Requiere el permiso CREATE DATABASE en la base de datos maestra, o los permisos CREATE ANY DATABASE o ALTER ANY DATABASE.  
  
 Para mantener el control del uso del disco en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el permiso para crear bases de datos suele limitarse a un número reducido de cuentas de inicio de sesión.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-create-a-database"></a>Para crear una base de datos  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] y expándala.  
  
2.  Haga clic con el botón derecho en **Bases de datos**y luego haga clic en **Nueva base de datos**.  
  
3.  En **Nueva base de datos**, especifique un nombre de base de datos.  
  
4.  Si desea crear la base de datos aceptando todos los valores predeterminados, haga clic en **Aceptar**; de lo contrario, continúe con siguientes los pasos opcionales.  
  
5.  Para cambiar el nombre del propietario, haga clic en (**...**) para seleccionar otro.  
  
    > [!NOTE]  
    >  La opción **Usar indexación de texto completo** siempre está activada y atenuada porque, a partir de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], todas las bases de datos de usuario están habilitadas para texto completo.  
  
6.  Para cambiar los valores predeterminados de los archivos de datos y de registro de transacciones principales, en la cuadrícula **Archivos de la base de datos** , haga clic en la celda correspondiente y especifique el nuevo valor. Para obtener más información, consulte [Agregar archivos de datos o de registro a una base de datos](add-data-or-log-files-to-a-database.md).  
  
7.  Para cambiar la intercalación de la base de datos, seleccione la página **Opciones** y una intercalación de la lista.  
  
8.  Para cambiar el modelo de recuperación, seleccione la página **Opciones** y un modelo de recuperación de la lista.  
  
9. Para cambiar opciones de base de datos, seleccione la página **Opciones** y modifique las opciones de la base de datos. Para obtener una descripción de cada opción, vea [Opciones de ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options).  
  
10. Para agregar un nuevo grupo de archivos, haga clic en la página **Grupos de archivos** . Haga clic en **Agregar** y especifique los valores para el grupo de archivos.  
  
11. Para agregar una propiedad extendida a la base de datos, seleccione la página **Propiedades extendidas** .  
  
    1.  En la columna **Nombre** , escriba un nombre para la propiedad extendida.  
  
    2.  En la columna **Valor** , escriba el texto de la propiedad extendida. Por ejemplo, especifique una o varias instrucciones que describan la base de datos.  
  
12. Para crear la base de datos, haga clic en **Aceptar**.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-create-a-database"></a>Para crear una base de datos  
  
1.  Conéctese al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. Este ejemplo crea la base de datos `Sales`. Debido a que no se usa la palabra clave PRIMARY, el primer archivo (`Sales`_`dat`) se convierte en el archivo principal. Como no se especifica MB ni KB en el parámetro SIZE del archivo `Sales`\_`dat` , se utiliza MB y el tamaño se asigna en megabytes. Cada vez que se crea, modifica o quita una base de datos de usuario, se debe hacer una copia de seguridad de la base de datos `Sales`\_`log` se asigna en megabytes porque el sufijo `MB` se ha indicado explícitamente en el parámetro `SIZE` .  
  
```tsql  
USE master ;  
GO  
CREATE DATABASE Sales  
ON   
( NAME = Sales_dat,  
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA\saledat.mdf',  
    SIZE = 10,  
    MAXSIZE = 50,  
    FILEGROWTH = 5 )  
LOG ON  
( NAME = Sales_log,  
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA\salelog.ldf',  
    SIZE = 5MB,  
    MAXSIZE = 25MB,  
    FILEGROWTH = 5MB ) ;  
GO  
```  
  
 Para obtener más ejemplos, vea [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql).  
  
## <a name="see-also"></a>Vea también  
 [Archivos y grupos de archivos de base de datos](database-files-and-filegroups.md)   
 [Adjuntar y separar bases de datos &#40;SQL Server&#41;](database-detach-and-attach-sql-server.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [Agregar archivos de datos o de registro a una base de datos](add-data-or-log-files-to-a-database.md)  
  
  
