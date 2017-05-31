---
title: "Instalar y configurar la búsqueda semántica | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-search
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- semantic search [SQL Server], installing
- semantic search [SQL Server], configuring
ms.assetid: 2cdd0568-7799-474b-82fb-65d79df3057c
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 5a59c184fc5229797ad83d5334fbb03169b64374
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="install-and-configure-semantic-search"></a>Instalar y configurar la búsqueda semántica
  Describe los requisitos previos de la búsqueda semántica estadística y cómo instalarlos o comprobarlos.  
  
## <a name="install-semantic-search"></a>Instalar la búsqueda semántica  
  
###  <a name="HowToCheckInstalled"></a> Comprobar si la búsqueda semántica está instalada  
 Consulte la propiedad **IsFullTextInstalled** de la función de metadatos [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md).  
  
 Un valor devuelto de 1 indica que la búsqueda de texto completo y la búsqueda semántica están instaladas; un valor devuelto de 0 indica que no lo están.  
  
```tsql  
SELECT SERVERPROPERTY('IsFullTextInstalled');  
GO  
```  
  
###  <a name="BasicsSemanticSearch"></a> Instalar la búsqueda semántica  
 Para instalar la búsqueda semántica, seleccione **Extracciones de texto completo y semánticas de búsqueda** en la página **Características que se van a instalar** durante la instalación de SQL Server.  
  
 La búsqueda semántica estadística depende de la búsqueda de texto completo. Estas dos características opcionales de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se instalan conjuntamente.  
  
## <a name="install-the-semantic-language-statistics-database"></a>Instalar la base de datos de estadísticas de lenguaje semántico  
 La búsqueda semántica tiene una dependencia externa adicional que se denomina base de datos de estadísticas semánticas de lenguaje. Esta base de datos contiene modelos estadísticos de idioma que requiere la búsqueda semántica. Una sola base de datos de estadísticas semánticas de lenguaje contiene los modelos de idioma de todos los idiomas compatibles con la indización semántica.  
  
###  <a name="HowToCheckDatabase"></a> Comprobar si está instalada la base de datos de estadísticas de lenguaje semántico  
 Consulte la vista de catálogo [sys.fulltext_semantic_language_statistics_database &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-semantic-language-statistics-database-transact-sql.md).  
  
 Si la base de datos de estadísticas semánticas de lenguaje está instalada y registrada para la instancia, los resultados de la consulta contienen una sola fila de información acerca de la base de datos.  
  
```tsql  
SELECT * FROM sys.fulltext_semantic_language_statistics_database;  
GO  
```  
  
###  <a name="HowToInstallModel"></a> Instalar, adjuntar y registrar la base de datos de estadísticas semánticas de lenguaje  
 La base de datos de estadísticas de lenguaje semántico no se instala con el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para configurar la base de datos de estadísticas semánticas de lenguaje como requisito previo para la indización semántica, realice las siguientes tareas:  
  
 **1. Instale la base de datos de estadísticas de lenguaje semántico.**  
 
 1.  Busque la base de datos semántica de estadísticas de idioma en el disco de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o descárguela de web.  
  
        1.  Busque el paquete de Windows installer denominado **SemanticLanguageDatabase.msi** en el disco de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
        2.  Descargue el paquete del instalador de la página [Estadísticas de semántica de lenguaje de Microsoft® SQL Server® 2016](https://www.microsoft.com/en-us/download/details.aspx?id=52681) en el Centro de descarga de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
2.  Ejecute el paquete de Windows Installer **SemanticLanguageDatabase.msi** para extraer la base de datos y el archivo de registro.  
  
     También puede cambiar el directorio de destino. De forma predeterminada, el instalador extrae los archivos en una carpeta denominada **Base de datos de lenguaje semántico de Microsoft** en la carpeta Archivos de programa. El archivo contiene MSI un archivo de base de datos y un archivo de registro comprimidos.  
  
3.  Mueva el archivo de base de datos y el archivo de registro extraídos a una ubicación adecuada del sistema de archivos.  
  
     Si deja los archivos en su ubicación predeterminada, no será posible extraer otra copia de la base de datos para otra instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    > [!IMPORTANT]  
    >  Cuando se extrae la base de datos de estadísticas semánticas de lenguaje, se asignan permisos restringidos al archivo de base de datos y al archivo de registro en la ubicación predeterminada del sistema de archivos. Como resultado, es posible que no tenga permiso para adjuntar la base de datos si la deja en la ubicación predeterminada. Si se produce un error al intentar adjuntar la base de datos, mueva los archivos o compruebe y corrija los permisos del sistema de archivos según corresponda.  
  
 **2. Adjunte la base de datos de estadísticas semánticas de lenguaje.**
   
 Adjunte la base de datos a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] o puede llamar a [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md) con la sintaxis **FOR ATTACH**. Para obtener más información, vea [Adjuntar y separar bases de datos &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md).  
  
 De forma predeterminada, el nombre de la base de datos es **semanticsdb**. También puede asignar a la base de datos un nombre distinto al adjuntarla. Tiene que proporcionar este nombre al registrar la base de datos en el paso posterior.  
  
```tsql  
CREATE DATABASE semanticsdb  
            ON ( FILENAME = 'C:\Microsoft Semantic Language Database\semanticsdb.mdf' )  
            LOG ON ( FILENAME = 'C:\Microsoft Semantic Language Database\semanticsdb_log.ldf' )  
            FOR ATTACH;  
GO  
```  
  
 En esta muestra de código se supone que la base de datos se ha movido desde su ubicación predeterminada a una nueva.  
  
 **3. Registre la base de datos de estadísticas semánticas de lenguaje.** 
  
 Llame al procedimiento almacenado [sp_fulltext_semantic_register_language_statistics_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-semantic-register-language-statistics-db-transact-sql.md) y proporcione el nombre que asignó a la base de datos cuando la adjuntó.  
  
```tsql  
EXEC sp_fulltext_semantic_register_language_statistics_db @dbname = N'semanticsdb';  
GO  
```  

##  <a name="reqinstall"></a> Requisitos y restricciones para la base de datos de estadísticas de lenguaje semántico  
  
-   Solo puede adjuntar y registrar una base de datos de estadísticas de lenguaje semántico en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Cada instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un solo equipo requiere una copia física independiente de la base de datos de estadísticas semánticas de lenguaje. Adjunte una copia en cada instancia.  
  
-   No puede separar una base de datos de estadísticas semánticas de lenguaje válida y registrada, y reemplazarla por una base de datos arbitraria que tenga el mismo nombre. Si lo hace, se producirá un error de rellenado de índice activo o futuro.  
  
-   La base de datos de estadísticas semánticas de lenguaje es de solo lectura. No puede personalizar esta base de datos. Si modifica el contenido de la base de datos de la manera que fuere, los resultados de las futuras indizaciones semánticas son indeterministas. Para restaurar estos datos a su estado original, puede quitar la base de datos modificada. Después puede descargar y adjuntar una nueva copia sin modificar de la base de datos.  
  
-   Es posible desasociar o quitar la base de datos de estadísticas semánticas de lenguaje. Si hay operaciones de indización activas que tengan bloqueos de lectura en la base de datos, se producirá un error en la operación de separación o eliminación o se agotará el tiempo de espera. Esto es coherente con el comportamiento existente. Después de quitar la base de datos, se producirá un error en cualquier operación de indización semántica.  
 
##  <a name="HowToUnregister"></a> Quitar la base de datos de estadísticas semánticas de lenguaje  

###  <a name="unregister-detach-and-remove-the-semantic-language-statistics-database"></a>Eliminar del Registro, separar y quitar la base de datos de estadísticas de lenguaje semántico 

 **1. Elimine del Registro la base de datos de estadísticas semánticas de lenguaje.**
   
 Llame al procedimiento almacenado [sp_fulltext_semantic_unregister_language_statistics_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-semantic-unregister-language-statistics-db-transact-sql.md). No tiene que proporcionar el nombre de la base de datos ya que una instancia solo puede tener una base de datos de estadísticas semánticas de lenguaje.  
  
```tsql  
EXEC sp_fulltext_semantic_unregister_language_statistics_db;  
GO  
```  
  
 **2. Separe la base de datos de estadísticas semánticas de lenguaje.**  
 
 Llame al procedimiento almacenado [sp_detach_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md) y proporcione el nombre de la base de datos.  
  
```tsql  
USE master;  
GO  
  
EXEC sp_detach_db @dbname = N'semanticsdb';  
GO  
```  
  
 **3. Quite la base de datos de estadísticas semánticas de lenguaje.**  
 
 Después de cancelar el registro y de separar la base de datos, puede eliminar el archivo de base de datos. No existe ningún programa de desinstalación ni hay ninguna entrada en la opción **Programas y características** en el Panel de control.  
  
## <a name="install-optional-support-for-newer-document-types"></a>Instalar compatibilidad opcional para nuevos tipos de documento  
  
###  <a name="office"></a> Instalar los filtros más recientes para Microsoft Office y otros tipos de documento de Microsoft  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instala los separadores de palabras y analizadores lingüísticos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] más recientes, pero no instala los últimos filtros para los documentos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office ni otros tipos de documento de [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Estos filtros son necesarios para indizar documentos creados con versiones recientes de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office y otras aplicaciones de [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Para descargar los filtros más recientes, vea [Paquetes de filtros de Microsoft Office 2010](http://go.microsoft.com/fwlink/?LinkId=218293). (Parece que no hay una versión de Filter Pack para Office 2013 ni Office 2016).
  
  
